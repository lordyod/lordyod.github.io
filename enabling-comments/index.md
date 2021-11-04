# Enabling Comments in Hugo with Isso


There are a lot of great reasons to use a static site. One of the challenges
for a blog based on a static site generator like Hugo is incorporating a
comment system. In this post, we'll walk through adding a comment system using
Isso, a self-hosted and open-source comment library.

<!--more-->

## Isso?

[Isso](https://posativ.org/isso/) is an open-source comment server which you
host on your own infrastructure. Comments are written in Markdown and stored
internally in a SQLite database. All you need to do is run the server and embed
the script in your template. It has several big advantages:

* Because it is hosted on your own infrastructure, nobody else has control of
    your data, and in particular nobody can make money off your users
* There isn't a lot of complicated web programming needed
* It's _very_ simple

Of course, it does have drawbacks:

* You have to be able to host a comment server
* You need to be proficient with some basic terminal skills and willing to debug
    things when they break
* It's not one of the built-in comment systems supported by Hugo
* Hosting a server on your own infrastructure is not without security risks

Following in the footsteps of several other authors on the subject[^footsteps],
let's walk through what's needed in order to add comments to our blog.

## Server hosting

The first thing we'll need is an Isso server up and running. To obtain this you
will need to have a server accessible to the public internet, such as one of the
following:

* A Raspberry Pi, spare laptop or similar
* A headless VM on a server you already have
* A cloud server

There are lots of resources for hosting things in the cloud, and this is a
viable option. Similarly, hosting something on a small box like a Pi is a great
project. Since I already have a dedicated VM host running
[Proxmox](https://www.proxmox.com), I decided to deploy Isso as a Docker
container. It's possible to run Isso directly but the ability to redeploy
resources more easily makes Docker a win in my book.

## Mail

We want users to be able to subscribe to replies to their comments. Other
comment services like Disqus handle this for us but for any self-hosted solution
we'll need to work it out. It's completely possible to host our own mail server,
but it's a mountain of work to manage it. A much simpler solution is to use a
third-party solution like [Mailgun](https://www.mailgun.com). Sign up for a free
account (you'll need to enter a credit card but won't need to pay anything).

## Prerequisites

Before we continue, let's make sure we have our infrastructure setup. Our host
machine looks like this:

* Running [Ubuntu](https://www.ubuntu.com)[^ubuntu], though basically any Linux
    distribution will look substantially similar to this.
* [Docker](https://www.docker.com) and
    [Docker-Compose](https://docs.docker.com/compose/) are installed.[^docker]
* Our gateway is setup for port forwarding HTTPS traffic[^portforwarding].
* We have a web server/reverse proxy set up and configured.[^proxy]
* We have a [Mailgun](https://www.mailgun.com) account setup with a key.

Once our host is ready we can proceed.

## Docker-compose

We'll add the following to our `docker-compose.yml`:

```yml
  isso:
    image: isso:latest
    container_name: isso
    hostname: isso
    restart: unless-stopped
    volumes:
      - ${DIR}/config:/config
      - ${DIR}/db:/db
    ports:
      - ${PORT}:8080
    environment:
      - UID=${UID}
      - GID=${GID}
```

In this code, we'll replace the following:

| Variable | Meaning |
|---|---|
| `DIR`  | Directory on the host, which contains the Isso config and database. Make sure it is owned by the user which runs `docker-compose`. |
| `PORT` | The port on the host which maps to the Isso container. You can leave this entry out if you aren't using `8080` for anything. |
| `UID`  | The user ID of the user which owns `DIR`. |
| `GID`  | The group ID of the user which owns `DIR`. |

## Reverse proxy with nginx

Next we'll add a config file so that our web server will point requests to the
container as a reverse proxy. If you are using the Swag container from
Linuxserver.io (and I recommend that you do) you can add this to your
`swag/nginx/site-confs` directory as `isso.conf`:

```nginx
server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name isso.*;

    include /config/nginx/ssl.conf;

    client_max_body_size 0;

    location / {
        include /config/nginx/proxy.conf;
        resolver 127.0.0.11 valid=30s;
        set $upstream_app localhost;
        set $upstream_port ${PORT};
        set $upstream_proto http;
        proxy_pass $upstream_proto://$upstream_app:$upstream_port;

    }
}
```

Note here we need to set `${PORT}` to match what was used in the
`docker-compose.yml` file. (If you removed the entry just use `8080`)

## Isso config

Now we'll setup our Isso config file at `${DIR}/config/isso.cfg`:

```config
[general]
; database location, check permissions, automatically created if not exists
dbpath = /db/comments.db
; your website or blog (not the location of Isso!)
host = https://${BLOG_URL}
; you can add multiple hosts for local development
; or SSL connections. There is no wildcard to allow
; any domain.
notify = smtp
reply-notifications = true
gravatar = true

[smtp]
; your mailgun username
username = ${MAILGUN_USERNAME}
; your mailgun password
password = ${MAILGUN_PASSWORD}
host = smtp.mailgun.org
port = 587
security = starttls
; this address will receive messages when there are new comments for moderation
to = ${TO_ADDRESS}
; mail to users comes from this address
from = ${FROM_ADDRESS}
timeout = 10s

[server]
listen = http://localhost:8080
reload = off
profile = off
; the public URL for the Isso server
public-endpoint = https://${ISSO_URL}

[moderation]
enabled = true
purge-after = 30d

[guard]
enabled = true
ratelimit = 10
direct-reply = 3
reply-to-self = false
require-author = true
require-email = true

[hash]
salt = ${SALT}
algorithm = pbkdf2

[admin]
enabled = true
; the admin password for Isso
password = ${PASSWORD}
```

You'll need to edit a number of the entries in this config file to match your
setup, using info from your Mailgun and server config.

## Edit Hugo template

Next up we'll need to edit our blog template to add the comment form. This part
is pretty easy but will have one wrinkle to deal with. The specific file you
need to edit will depend on your template, for mine I edit
`layouts/partials/comment.html` and add the following:

```html
    <div id="comments">
        {{- /* Isso Comment System */ -}}
        {{"<!-- begin comments //-->" | safeHTML}}
        <div class="post-footer">
            <section id="isso-thread"></section>
            <script data-isso="https://isso.lordyod.com/" 
                    data-isso-id="thread-id"
                    data-isso-css="true"
                    data-isso-lang="en"
                    data-isso-reply-to-self="true"
                    data-isso-reply-notifications="true"
                    data-isso-require-author="true"
                    data-isso-require-email="true"
                    data-isso-max-comments-top="10"
                    data-isso-max-comments-nested="5"
                    data-isso-reveal-on-click="5"
                    data-isso-avatar="false"
                    data-isso-gravatar="true"
                    data-isso-feed="true"
                    data-isso-vote="false"
                    src="https://${ISSO_URL}/js/embed.min.js"></script>
        </div>
        {{"<!-- end comments //-->" | safeHTML}}
    </div>
```

Make sure to edit `${ISSO_URL}` to match your hosted Isso instance.

## Start Isso

This part is simple, just run `docker-compose up -d` to start the container.
Once it's up and running, we should be able to load any of our posts and see a
comment form at the bottom.

## Final thoughts

This setup is pretty basic. You can customize it further by using some CSS or
further customizing the template. That said, it fulfills the basic needs pretty
well, and does so without selling our users' data.

[^footsteps]: See
  [Stíobhart Matulevicz](https://stiobhart.net/2017-02-24-isso-comments/) and
  [Kevin Masson](https://oktomus.com/posts/2020/add-comments-to-a-static-blog-with-isso/).
[^ubuntu]: I prefer to use LTS distributions when possible. As I am writing this
  that means Ubuntu 20.04.
[^docker]: For more on installing Docker (or any other Linux tools, really) I
  recommend the extremely well-written [Digital Ocean
  tutorials](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04).
[^portforwarding]: This is a complicated topic with a lot of system-dependent
  details, probably [Port Forward](https://portforward.com/) is the best place
  to get started learning about it.
[^proxy]: Another big topic. For brevity, I'll suggest just going with a
  [Swag](https://docs.linuxserver.io/general/swag) container, that's what I use.

