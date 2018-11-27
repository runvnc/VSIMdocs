## emulate
Run in emulator (set with emucore) in a new screen to emulate a given system with an optional command/rom/binary.
See also emucore() for changing cores.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
 mulate(-1, 'topgear.sfc') 
```
## parent

## dirlight

## setmem
change emulator memory data

```lua
emuN = 0
bank = 2
offset = 1024 -- C64 screen mem start
str = "123456789"
-- (this was tested on vice-libretro)
setmem(emuN, bank, offset, str)
```
## insert

## memsize
get size of memory from emulator

## line3d

## sel

## emucore
specify the emulator core to use with emulate() commmands

```lua
emucore("mame")
```
## force

## sky

## screeninp

## getmem
get memory data from emulator

## put

## lookAt

## get

## emufull

## releasekey

## showscreen

## line3dex

## on

## screenon

## dirtable

## sendtext

## palette

## rez
          Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply)
          NOTE: Not all models are compatible. YMMV. 

```lua
 rez('mymodel.3ds') 
```
```lua
 local mynodeid = rez('myhouse.obj') 
```
## eject

## texture

## pointlight

## saveurl

## geturl

## scale

## impulse

## screen

## node

## wait

## rot

## waitui
wait for UI to process all lua commands

## save

## sendkeys

## pos

## holdkey

## load

## print

## cls

## mesh

## emuopt

