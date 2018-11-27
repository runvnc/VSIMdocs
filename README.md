# Emulation
## emulate
Run selected emulator (set with emucore()) with an optional command/rom/binary.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
emulate(-1, 'topgear.sfc') 
```
## emucore
specify the emulator core to use with emulate() commmands

```lua
emucore("mame") -- needs mame.dll
```
## getmem
get memory data from emulator

## memsize
get size of memory from emulator

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

## eject

## sendtext

## sendkeys

## holdkey

## releasekey

# Models and Positioning
## rez
Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply) NOTE: Not all models are compatible. YMMV.

```lua
rez('mymodel.3ds')
```
```lua
local mynodeid = rez('myhouse.obj')
```
## sel

## sky

## put

## parent

## pos

## scale

## rot

## mesh

## node

## pointlight

## dirlight

## texture

## line3dex

## line3d

## get

## lookat

# Flow Control
## wait

## on

## wait

# Physics
## force

## impulse

# User Interface
## screeninp

## print

## cls

## screen

## screenon

## palette

## screeninp

## showscreen

