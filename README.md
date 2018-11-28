# Emulation
## emulate(emulatorid,filetoload)
Run selected emulator (set with emucore()) with an optional command/rom/binary.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.  You may run the same core multiple times simultaneously or several different cores depending on system resources.

run Top Gear SNES game
```lua
emucore('snes9x')
emulatorid = emulate(-1, 'topgear.sfc') 
```
## emucore(fnameNoExt)
specify the emulator core to use with emulate() commmands

next emulate() with MAME core
```lua
emucore("mame") -- needs mame.dll
```
## getmem(emulatorid,bank,offset,numbytes)
get memory data from emulator; returns a lua string

## memsize(emulatorid,bank)
get size of memory from emulator

## setmem(emulatorid,bank,offset,binStr)
change emulator memory data

show some numbers at top of C64 screen
```lua
emuN = 0
bank = 2
offset = 1024 -- C64 screen mem start
str = "123456789"
-- (this was tested on vice-libretro)
setmem(emuN, bank, offset, str)
```
## emuopt(emulatorid,property,value)
specify emulator option

## insert(emulatorid,drivenum,dskfile)
insert virtual disk into emulator drive

## eject(emulatorid,drivenum)
eject disk from virtual emulator drive

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
change selected node which subsequent commands like pos() and rot() affect

## sky(skydomeTextureFname,texturePerc, spherePerc, radius)
create a sky dome; texturePerc=0..1, spherePerc=0..2

## put(property, value1, value2..)

## parent(nodeid)
make the selected node a child of nodeid

## pos(x, y, z)
move the currently selected node

## scale(xscl, yscl, zscl)
scale the currently selected node

## rot(x, y, z)
rotate the currently selected node

## mesh(indices, vertices)
create a mesh from the specified tables

create a simple triangle mesh and a node from it
```lua
  c = { r=255, g=255, b=255, a=255 }
  v = { { pos = {x=0,y=0,z=0}, color=c, 
         texturecoords = {u=0, v=0},
         normal = {x=0,y=1,z=0} },
       { pos = {x=10,y=0,z=0}, color=c, 
         texturecoords = {u=0, v=1},
         normal = {x=0,y=1,z=0} },
       { pos = {x=0,y=0,z=10}, color=c,  
         texturecoords = {u=0, v=0},
         normal = {x=0,y=1,z=0} } }
  i = {1,2,3}
  meshid=mesh(i,v)
  id=node(meshid)
```
## node(meshid)

## pointlight

## dirlight

## texture(fname)

## line3dex(x1,y1,z1,x2,y2,z2,clr)

## line3d(x1,y1,z1,x2,y2,z2,clr)

## get(property)

## lookat(x,y,z)

# Flow Control
## wait(ms, funcname, repeat)
wait X milliseconds and then run a function by name

```lua
wait(1000, "myFunction")
```
calls funcRepeats() approx. every 20 ms
```lua
wait(20, "funcRepeats", "repeat")
```
## on(event, funcname)
call a handler on event trigger

```lua
on("keydown", "mykeyhandler"
```
```lua
on("mousedownobj", "mynodeclickhandler")
```
# Physics
## force()

## impulse()

# User Interface
## screeninp(noneOrConsOrEmu)

## print(arg1,arg2..)

## cls()

## screen(num)
create a new screen or switch to an existing; print() and palette() affect this screen

## screenon(nodeid)
apply the screen as a texture to a node

## palette(index,r,g,b,a)
change color values at index

## screeninp(noneOrConsOrEmu)

## showscreen(num)

# Networking
## geturl(url)

## saveurl(url, fname)

