# Physics
## impulse

## force

# Models and Positioning
## dirlight

## scale

## line3dex

## parent

## lookat

## pos

## get

## line3d

## pointlight

## texture

## rez
          Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply)
          NOTE: Not all models are compatible. YMMV. 

```lua
 rez('mymodel.3ds') 
```
```lua
 local mynodeid = rez('myhouse.obj') 
```
## sel

## rot

## put

## sky

## node

## mesh

# Emulation
## emucore
specify the emulator core to use with emulate() commmands

```lua
emucore("mame")
```
## sendtext

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
## emuopt

## insert

## holdkey

## getmem
get memory data from emulator

## emulate
Run in emulator (set with emucore) in a new screen to emulate a given system with an optional command/rom/binary.
See also emucore() for changing cores.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
emulate(-1, 'topgear.sfc') 
```
## memsize
get size of memory from emulator

## eject

## releasekey

## sendkeys

# Flow Control
## on

## wait

# User Interface
## palette

## print

## screeninp

## screen

## showscreen

## screenon

## cls

