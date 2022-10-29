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

integration mods are often very server-specific and thus are often not fully public.

## license

agpl if you want to help the modding and server-running community.
