##node

##print

##sendtext

##sky

##insert

##on

##palette

##emucore
specify the emulator core to use with emulate() commmands

```lua
emucore("mame")
```
##geturl

##emuopt

##rez
          Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply)
          NOTE: Not all models are compatible. YMMV. 

```lua
 rez('mymodel.3ds') 
```
```lua
 local mynodeid = rez('myhouse.obj') 
```
##releasekey

##wait

##line3dex

##cls

##get

##parent

##emufull

##getmem
get memory data from emulator

##showscreen

##line3d

##lookAt

##waitui
wait for UI to process all lua commands

##dirtable

##force

##pos

##texture

##save

##dirlight

##screenon

##load

##pointlight

##saveurl

##sendkeys

##screen

##mesh

##emulate
Run in emulator (set with emucore) in a new screen to emulate a given system with an optional command/rom/binary.
See also emucore() for changing cores.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
 mulate(-1, 'topgear.sfc') 
```
##screeninp

##rot

##holdkey

##memsize
get size of memory from emulator

##put

##impulse

##sel

##scale

##eject

##setmem
change emulator memory data

```lua
emuN = 0
bank = 2
offset = 1024 -- C64 screen mem start
str = "123456789"
-- (this was tested on vice-libretro)
setmem(emuN, bank, offset, str)
```
