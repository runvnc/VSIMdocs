# Emulation
## emulate(emulatorid,filetoload)
Run selected emulator (set with emucore()) with an optional command/rom/binary.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
emulate(-1, 'topgear.sfc') 
```
## emucore(fnameNoExt)
specify the emulator core to use with emulate() commmands

```lua
emucore("mame") -- needs mame.dll
```
## getmem(emulatorid,bank,offset,numbytes)
get memory data from emulator

## memsize(emulatorid,bank)
get size of memory from emulator

## setmem(emulatorid,bank,offset,binStr)
change emulator memory data

```lua
emuN = 0
bank = 2
offset = 1024 -- C64 screen mem start
str = "123456789"
-- (this was tested on vice-libretro)
setmem(emuN, bank, offset, str)
```
## emuopt(emulatorid,property,value)

## insert(emulatorid,drivenum,dskfile)

## eject(emulatorid,drivenum)

## sendtext(emulatorid,text)

## sendkeys(emulatorid,keys)

## holdkey(emulatorid, key, duration)

## releasekey(emulatorid, key)

# Models and Positioning
## rez
Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply) NOTE: Not all models are compatible. YMMV.

```lua
rez('mymodel.3ds')
```
```lua
local mynodeid = rez('myhouse.obj')
```
## sel(nodeid)

## sky(skyboxTexture,)

## put(property, value1, value2..)

## parent(nodeid)

## pos(x, y, z)

## scale(xscl, yscl, zscl)

## rot(x, y, z)

## mesh

## node(meshid)

## pointlight

## dirlight

## texture(fname)

## line3dex(x1,y1,z1,x2,y2,z2,clr)

## line3d(x1,y1,z1,x2,y2,z2,clr)

## get(property)

## lookat(x,y,z)

# Flow Control
## wait(ms, funcname)
wait X milliseconds and then run a function by name

```lua
wait(1000, "myFunction")
```
## on(event, funcname)

# Physics
## force()

## impulse()

# User Interface
## screeninp(noneOrConsOrEmu)

## print(arg1,arg2..)

## cls()

## screen()

## screenon(selsecreen)

## palette(color,r,g,b,a)

## screeninp(noneOrConsOrEmu)

## showscreen(num)

