# Grit and Wounds in 5E (WIP)


<!--more-->

## 1: The Problem

The 5E rules describe hit points as 'a combination of physical and mental
durability, the will to live, and luck.' The problem with this is that the rules
don't really back this up. When you get hit with an attack, you lose hit points,
but does this represent you actually getting hit? Or does it represent you
dodging out of the way, or getting lucky somehow? And if it does mean you dodged
or get lucky, how does *cure wounds* heal you?

I don't think I need to go into the shitshow that is the death save system. It
doesn't make any sense, and furthermore it incentivizes playing like you're a
piece in a board game, instead of as if you were a person. This is apparent when
you consider a cleric with *healing word* ready and an ally at 1 hp. In
'reality' you'd use this sort of healing ability as soon as you could in that
situation, because your friend might die at any moment. In 5E it's optimal to
wait for the ally to get hit and go unconscious, because any amount of healing
will bring them back to consciousness no matter how hard they got hit.

Lastly, consider rest and recovery. In older versions of the game you would heal
very slowly, in the low single digits per day with bed rest. Under this type of
system you could get hit and require days (or even weeks) of rest to recover.
Contrast this with 5E, where you can be taken to the brink of death and recover
fully with a night's rest.

So let's talk about fixing it, shall we?[^inspiration]

  [^inspiration]: The system I describe here is adapted from other games. The
  first time I saw such a system used was in Star Wars D20, which called the two
  stats *Wound Points* and *Vitality Points*. I think the idea of using your
  vitality to power your abilities is pretty interesting but the way it was
  implemented in this game had some problems. That game didn't have critical
  injuries, of course - for that I draw inspiration from Warhammer Fantasy
  Roleplay and the excellent B/X-based games written by [Emmy Allen aka
  cavegirl](https://www.drivethrurpg.com/browse.php?author=Emmy%20Allen) such as
  Esoteric Enterprises and Wolf-Packs and Winter Snow. And of course separating
  HP from your health is one of the core features of Into the Odd by [Chris
  McDowall](https://www.bastionland.com/).

## 2: Grit

The first thing to do is to make it explicit - hit points don't represent your
health, they represent your ability to avoid bodily damage. To make this a bit
clearer and avoid confusion, we're going to change the name to *Grit*. Grit can
manifest in several different forms:

* The nimble duelist who swiftly ducks out of the way of a blow.
* The brawler with a chin like a block of concrete, who takes punches without flinching.
* The mystic with the strength of will to continue on despite the pain.

The desired gameplay effects are that, most of the time, the mechanics are
essentially unchanged from regular 5E. When you get hit in combat you still lose
the same amount. This lets us continue to represent the (usually quite
far-fetched) mechanics in the fiction with a higher degree of verisimilitude.

### 2.1: Maximum Grit

A character's maximum grit is calculated in basically the same way as HP is
normally:

> **Maximum Grit = hit dice roll + (Grit Modifier x level)**

Your **Grit Modifier** is the combination of class abilities, magic items,
ability scores, and other effects. All characters start with a grit modifier
equal to the Dexterity bonus (minimum 0).

> *Example: Sarah casts a spell which allows her to add her Intelligence
> modifier to her grit modifier in addition to any others she could
> already use. With an 18 Intelligence, this increases her Grit Modifier by +4,
> and immediately raises her current and maximum grit by 4 x HD.*

Any time you gain a level, you roll your maximum grit again. You gain either 1hp
or your the results of your new roll, whichever is higher.[^crawford]

  [^crawford]: This comes from the excellent Stars Without Number, Worlds
  Without Number, and so on, by Kevin Crawford over at [Sine Nomine
  Publishing](http://www.sinenomine-pub.com/).

> *Example: Sarah is a Wizard 2/Fighter 3 with 16 Constitution. Her maximum HP
> was rolled 2d6 + 3d10 + 15 = 41. When she gains another level of Wizard, she
> will roll 3d6 + 3d10 + 18, with a minimum new value of 42.*

## 3: Losing Grit

When a character takes damage (in combat or otherwise) it is subtracted from
their Grit. If all damage is absorbed by your Grit, this means that the
character wasn't wounded. From a narrative perspective, perhaps they dodged
aside at the last second, or they took a punch on the chin without flinching.
Mechanically speaking, as long as you still have Grit remaining, there aren't
any ill effects from taking damage as long as you still have some Grit
remaining.

> *Example: Sarah has 18 Grit when she is attacked by a bear, which swipes at
> her with its claws. It hits her AC, and rolls 7 damage. Sarah's player
> subtracts 7 from her current Grit. Since she still has 11 Grit remaining there
> are no other effects.*

### 3.1: Critical Hits

Critical hits bypass Grit. No matter how skilled you are, there is always a
chance of a lucky blow connecting. However, they do not deal increased damage.
(Abilities that deal additional damage on a critical hit, such as *flaming
burst*, function as written)

> *Example: The bear swipes at Sarah with its other claw, and the attack roll is
> a 20 with a damage roll of 5. Since this is a critical hit, this 5 damage
> bypasses Sarah's Grit.*

### 3.2: Wounds

Any time you take damage which is not absorbed by your Grit, you suffer one or
more Wounds. This represents that your PC has hit hard enough, or in a
vulnerable enough spot, that they will begin suffering ill effects. A character
can suffer as many wounds as they have Constitution - if their current wounds is
higher than their current Constitution, they die.

Some wounds cause lasting effects to a character, taking the form of ability
score penalties, conditions, or ongoing damage. To determine the effects of a
wound, you must make a **Critical Wound Save**. This is a Constitution saving
throw with a DC equal to the number of wounds the character has suffered so far
plus the amount of damage being suffered.

> **Critical Wound Save DC:** Current Wounds + Incoming Damage

*Current Wounds* means the number of wounds the character has already suffered,
before determining the effects of this new injury. *Incoming Damage* means the
amount of damage remaining after absorption from grit, magical effects, etc.

> *Example: Sarah has 5 grit remaining, and is shot with an arrow for 7 damage.
> Since this causes her to drop to 0 grit, she will need to make a critical
> wound save. Since this is her second wound, she calculates her save DC as 1
> current wound + 2 incoming damage = DC 3.*

Failing this saving throw means receiving a killing blow of some kind. Beating
the saving throw means receiving a wound which does not outright kill you, but
may have other effects. The severity of these effects are based on the margin of
success on the throw, as indicated below:

| Beat DC by: | Severity: | Description: |
| ------| --- |--- |
| 20+   | ***Dramatic Injury*** | Not only does this injury not impact your abilities, it'll even make you look cool and leave an impressive scar. |
| 14-19 | ***Flesh Wound*** | This type of injury certainly hurts, and takes a while to heal, but ultimately it's unlikely to be the end of you. Most PC's will be able to handle taking a flesh wound or two without any difficulty - so long as the fight ends soon after.                         |
| 6-13 | ***Minor Injury*** | This type of wound will have moderately debilitating effects, but they won't be permanent. A pulled muscle, bad contusion, or mild concussion.                                                                                                                       |
| 0-5  | ***Critical Injury*** | This type of wound not only hurts but has a very real impact on your ability to continue on and may even be permanent. Broken limbs, amputations, and gut wounds are all examples of this sort of thing. Few adventurers will be able to withstand more than one. |
| failure | ***Death Blow*** | If this type of injury doesn't kill you immediately, it's only because it wants you to suffer for a while before you die.                                                                                                                                              |

Regardless of other effects, on a Critical Wound Save a natural 20 always
results in a Dramatic Injury, and a natural 1 always results in a Death
Blow.[^percentages]

  [^percentages]: The intent of the distribution of wound effects, and the
  natural 20/natural 1 rules, is to create an environment where being wounded is
  *always* something to be avoided if possible, because there is a decent chance
  that it will have lasting effects on your character. While the chance of death
  might be quite small, it never drops below 5%. Even if your PC won't die
  outright, the chance of critical injury is still fairly significant (depending
  on equipment and effects).

### 3.3: Armor

The major advantage of heavier armor is its increased protection against
critical wounds. If your character is wearing armor they are proficient in, they
add the corresponding bonus to their saving throw modifier when rolling a wound save.

| Armor           | Save Bonus | Maximum Dexterity Bonus |
| --------------- | ---------- | ----------------------- |
| Padded          | +1         | Any                     |
| Leather         | +1         | Any                     |
| Studded Leather | +2         | Any                     |
| Hide            | +2         | +2                      |
| Chain Shirt     | +3         | +2                      |
| Scale Mail      | +4         | +2                      |
| Breastplate     | +4         | +2                      |
| Half Plate      | +5         | +2                      |
| Ring Mail       | +4         | None                    |
| Chain Mail      | +6         | None                    |
| Splint Mail     | +7         | None                    |
| Plate           | +8         | None                    |

If a character would add their Dexterity modifier to their Grit, they may not
add more than the amount listed for the corresponding armor.

## 4: Regaining Grit

Grit recovers relatively quickly, while wounds take much longer to heal.

### 4.1: Rest and Recovery

A character recovers Grit just like in regular 5e, rolling hit dice during short
rests using their Grit modifier and recovering all such hit dice after a long
rest. However, if the character is wounded, their recovery is limited. Any
unhealed wounds are subtracted from the grit modifier when rolling hit dice to
recover, and limit the maximum grit after a long rest.

### 4.2: Healing Wounds

At the end of a Long Rest, you may make a Constitution saving throw, and if you
succeed you heal one wound. The DC of the check has a base of 10 + the number of
wounds you have suffered, with modifiers based on the circumstances of your
healing:

| Status: | Required Conditions: | DC Modifier: |
| --------| -------------------- | ------------ |
| Nursed | Attendant needs to expend a use of a healer's kit and make a Wisdom (Medicine) check, DC 5 + number of wounds, at disadvantage if on self | -5 |
| Received surgery | Surgeon requires expert tools and must make Wisdom (Medicine) check, DC 15 + number of wounds, at disadvantage if on self | -10 |
| Complete bed rest | This means you may as well be sleeping for 24 hours straight | -5 |
| Difficult conditions | aboard ship, in a tent during a storm, rough travel in a wagon, etc | +5 |
| Significant physical activity | most things undertaken by typical adventurers, such as exploring a dungeon, movement requiring a Strength- of Dexterity-based skill check, carrying more than a Light load of equipment, etc | +5 |

Some injuries have lasting effects. To recover from these effects you must heal
wounds equal to the original damage suffered. If there are multiple such wounds
determine which one is healed randomly. Some of these wounds cannot be healed
without medical attention, surgery, or magical healing.

Regardless of other effects to the DC, a natural roll of 20 always succeeds and
a natural roll of 1 always fails.

## 5: Magic

The basic idea is that anything from vanilla 5E which restores HP instead
restores an equivalent amount of grit. This is the rule you should follow for
any sort of healing effect unless the item is mentioned later in this section.

### 5.1: Spell Conversions

Here's an incomplete list of spells converted from vanilla 5E:

| Spell: | Notes: |
| --- | --- |
| *(Mass) Cure Wounds* | This spell doesn't exist in this form and is replaced with *Invigorate* (see below). |
| *Enervation* | On a failed save, the target takes 1d8 damage, bypassing grit. |
| *Goodberry* | Setting aside the nourishment question[^goodberry], someone who eats a *goodberry* acts as if they are being nursed with a healer's kit. |
| *(Mass) Heal* | Instead of regaining 70 hit points, the target recovers 7 wounds (+ 1 wound/level for spell level above 6th). The mass version restores 70 wounds. |
| *Greater/lesser restoration* | These spells work as written, and are used to heal critical injuries with lasting effects. |
| *Life Transference* | You suffer 1d4 wounds, and the target recovers twice that amount. If this removes the wounds associated with a critical injury then the effect of that injury is also removed. |
| *Power Word Heal* | The target regains any lost wounds, ending any critical injury effects, as well as any lost grit. |
| *Raise Dead* | The creature returns with 0 grit. The spell heals all wounds which do not cause missing body parts, meaning any critical injury effects unrelated to severed limbs/appendages/etc are healed and the associated wounds are recovered. |
| *Regenerate* | The target regains 2d4+3 wounds immediately, + 1 wound per minute. |
| *Resurrection* | This spell heals all wounds and grit. |
| *Revivify* | This spell causes the target to heal the wound which killed them. If this was a critical injury, any associated effects are also healed. |
| *Spare the Dying* | Being at 0 grit is not the same thing in this new system so this spell is removed.[^sparethedying] |
| *Vampiric Touch* | On a hit, the target suffers 1d6 necrotic damage, bypassing grit, and you recover wounds equal to half the amount suffered (minimum 1). |

  [^sparethedying]: Optionally, this could work to halt the effects of a death
  blow, however I think this will trivialize these injury types so it won't be a
  thing at my table.

  [^goodberry]: At my table it converts one 'supply' of suitable herbs into one
  'supply' of rations, which feeds one person for a day.

### 5.2: New Spells

Some new spells to work around the new system:

* **Cure Wounds**
  * *Level:* 1st
  * *Casting Time:* 1 action
  * *Range/Area:* touch
  * *Components:* verbal, somatic
  * *Duration:* instantaneous
  * *School:* evocation
  * *Attack/Save:* none
  * *Damage/Effect:* healing
  * *Description:* A creature you touch regains 1 wound. (When you cast this
      spell using a spell slot of 2nd level or higher, the healing increases by
      1 wound per slot level above 1st.) This spell does not heal critical
      injury effects.

* **Lesser Restoration**
  * *Level:* 2nd
  * *Casting Time:* 1 action
  * *Range/Area:* touch
  * *Components:* V, S
  * *Duration:* instantaneous
  * *School:* abjuration
  * *Attack/Save:* none
  * *Damage/Effect:* healing
  * *Description:* You touch a creature and choose one of the following:
    * Cure a disease.
    * Cure the conditions (but not wounds) associated with one Minor Injury or
        Flesh Wound.

* **Greater Restoration**
  * *Level:* 5th
  * *Casting Time:* 1 action
  * *Range/Area:* touch
  * *Components:* V, S, M (diamond dust worth at least 100 gp, which the spell
      consumes)
  * *Duration:* instantaneous
  * *School:* abjuration
  * *Attack/Save:* none
  * *Damage/Effect:* healing
  * *Description:* You touch a creature and choose one of the following:
    * Reduce the target's exhaustion by one
    * End one charm or petrify effect
    * Remove a curse
    * Cure one critical injury (other than a death blow)

### 5.3: Abilities

Some important class and other special abilities also need conversion.

* *Unarmored Defense:* A Barbarian adds their Constitution modifier to the Grit
    modifier. A Monk adds their Wisdom modifier.
* *Relentless Rage*:* If you suffer wounds equal to your Constitution without
    suffering a death blow, you can make a DC 10 Constitution saving throw. If
    you succeed, you have 1 wound remaining instead.
* *Rage beyond Death:* You don't die from losing wounds or the effects of
    critical injuries so long as your rage continues.

## 6: Injury Effects

Wounds inflict a variety of different effects, sometimes more than one. New
conditions are listed here:

* **Dying:** Sometimes death is basically inevitable, but not immediate.
  While in this state, you get one more turn before you die. (You must take your
  action as soon as it's available.) Nothing can be done to stop this. A dying
  character’s death sentence is merely slightly delayed, but still irrevocable.

* **Bleeding Out:** A character who is bleeding out gains 1d4 wounds at the
  start of every round. As an action, a character can attempt a Wisdom
  (Medicine) roll to staunch the bleeding, with DC 5 + the number of wounds the
  character has suffered. It is particularly difficult to do this to yourself,
  raising the DC by 5. If the check is successful, the bleeding is slowed to a
  rate of turns instead of rounds.

  A character can also attempt to properly treat the bleeding of a character
  bleeding at a rate of turns. Doing so is more involved, so takes a full turn.
  If successful, the patient stops bleeding entirely.

* **Broken Leg:** You are **Restrained** and knocked **Prone**.

  * A broken leg can be temporarily treated with a splint. As an action, make a
    Wisdom (Medicine) check with DC 5 + the number of wounds the character has
    suffered. It is difficult to do this to your own leg, raising the DC by 5.

  * As an action, you can crawl despite being **Restrained**. Make a
    Constitution saving throw, DC 10 + the number of wounds you have suffered.
    If successful, you may move up to 5ft. If your leg is splinted (see above),
    or if you have something to use as a crutch, this can be done without a
    saving throw.

* **Broken Arm:** Anything you were carrying in that hand is dropped. One-handed
  actions with that limb are essentially impossible. Two-handed actions may be
  possible at disadvantage. A broken arm can be splinted just like a leg,
  allowing some use of the limb.

* **Amputated Limb:** As above, but cannot be splinted, and will be permanent
  except for high-level healing spells.

* **Head Trauma:** Depending on severity, the following effects are possible:
  * Fall **Unconscious** for a number of rounds
  * Short-term **Stunned**
  * Short-term **Blindness**
  * Short-term **Deafened**
  * Short- or long-term **Exhaustion**

* **Eye Wound:** Disadvantage on Wisdom (Perception) checks based on sight, with
  duration depending on severity. If it happens to both eyes, this is
  **Blindness** instead.

* **Ear Wound:** As eye wound, but based on sound, and **Deafened**.

* **Hand Wound:** Depending on severity, this can range from a smashed hand to
  severed fingers. This impedes some Dexterity-based ability checks as well as
  somatic spellcasting.

* **Gut Wound:** Gain the **Poisoned** condition until treated (as if Bleeding
  Out, see above).


