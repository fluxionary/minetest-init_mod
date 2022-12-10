# init_mod

an opinionated tool for creating new minetest mods from a template

usage:

from a shell, execute

```shell
/path/to/init_mod/init_mod name_of_mod_to_make 
```

# on writing minetest mods

NOTE: this section is *VERY UNFINISHED* but i want to back it up cuz i've paused finishing it for a while.

## style

for reference: http://lua-users.org/wiki/LuaStyleGuide

but i haven't read through all of that.

mostly, adopt the style of an existing project as it is, unless you are taking it over entirely. just because you 
prefer spaces over tabs, does not mean you should use your preference if the project uses one or the other 
consistently. 

otherwise, keep in mind the maxim that code is written in order to be readable by other humans more than it is 
to be read by a computer. lua has a number of "weird" features that i discourage you from using in order not to 
confuse neophytes. this includes things like calling a function w/out parentheses, and at the extreme end, writing
your own dialect of lua that needs a custom preprocessor before minetest can use it (you know who you are).

## semantics 

mods should generally do a single thing. if it does more than one thing, consider turning your mod into a modpack.
however, i'm of the opinion that e.g. mesecons doesn't need to be *quite* so many individual mods.  

imo there's 3 major kinds of minetest mods:

### API mods

these mods just provide code for other mods to make use of. examples include mobs_redo and tubelib. 

### content mods

these create nodes/items/tools/commands etc.. 

some content mods may very well have an API, particularly machine mods, for e.g. allowing others to register
machine crafting recipes.

### integration mods

these are mods that fix incompatibilities between various mods. sometimes it's preferable to create an API to
avoid the incompatibility (player_monoids are a great example of such), but sometimes it's not tenable to fix 
everything that way. some examples of this are in dealing w/ right-click behavior. some tools (or other items)
have special right-click behavior, and some nodes (and entities) have their own behavior when right-clicked.
there is often no way to tell a priori which is the correct behavior to trigger in every circumstance. 
for example, tools with right-click behavior may not place on an anvil, preventing them from being repaired.

however, integration mods are often very server-specific and thus are often not fully public, in part because they
aren't incredibly useful to the public. 

## how to use these semantics

* API mods can depend on other API mods, but most not depend on content or integration mods.
* content mods can depend on API mods or other content mods, but must not depend on integration mods.
* integration mods can depend on everything. nothing other than another integration mod should depend on an 
    integration mod.

## some case studies

i will analyze some current issues

### i3

i must disclose that i have inadvertently started a "beef" w/ the creator of i3, and i regret having done so w/out
having documented my views beforehand. i3 has at least one great feature over unified_inventory (compressed groups),
but it does a huge number of things that break other mods, and there's no way to uninstall it and not suffer from 
permanent side effects more serious than an "unknown node".

TODO: explain

### ethereal

TODO: 

## license

agpl if you want to help the modding and server-running community.
