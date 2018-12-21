# Emulation
## emu.emulate(emulatorid,filetoload)
Run selected emulator (set with emucore()) with an optional command/rom/binary.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.  You may run the same core multiple times simultaneously or several different cores depending on system resources.

### run Top Gear SNES game
```lua
emu.emucore('snes9x')
emulatorid = emu.emulate(-1, 'topgear.sfc') 
```
## emu.core(fnameNoExt)
specify the emulator core to use with emulate() commmands

### next emulate() with MAME core
```lua
emu.emucore("mame") -- needs mame.dll
```
## emu.getmem(emulatorid,bank,offset,numbytes)
get memory data from emulator; returns a lua string

## emu.memsize(emulatorid,bank)
get size of memory from emulator

## emu.setmem(emulatorid,bank,offset,binStr)
change emulator memory data

### show some numbers at top of C64 screen
```lua
emuN = 0
bank = 2
offset = 1024 -- C64 screen mem start
str = "123456789"
-- (this was tested on vice-libretro)
emu.setmem(emuN, bank, offset, str)
```
## emu.reset(emulatorid)
reset emulator machine

## emu.opt(emulatorid,property,value)
specify emulator option

## vsim_pause
set this emu option to true to pause emulation

## vsim_3daudio
set this emu option to true to turn on positional audio from emulator

## emu.insert(emulatorid,drivenum,dskfile)
insert virtual disk into emulator drive

## emu.eject(emulatorid,drivenum)
eject disk from virtual emulator drive

## emu.delete(emulatorid)
delete emulator and node

## emu.full(emulatorid)
run emulator in the full window

# Models and Positioning
## model.rez
Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply) NOTE: Not all models are compatible. YMMV.

```lua
model.rez('mymodel.3ds')
```
```lua
local mynodeid = model.rez('myhouse.obj')
```
## model.sel(nodeid)
change selected node which subsequent commands like pos() and rot() affect

## model.sky(skydomeTextureFname,texturePerc, spherePerc, radius)
create a sky dome; texturePerc=0..1, spherePerc=0..2

## VSIM_AMBIENT
set this variable on any node to change ambient light color of entire scene

```lua
put('VSIM_AMBIENT', 255,95, 95, 95)
```
## model.put(property, value1, value2..)

## model.parent(nodeid)
make the selected node a child of nodeid

## model.pos(x, y, z)
move the currently selected node

## model.scale(xscl, yscl, zscl)
scale the currently selected node

## model.rot(x, y, z)
rotate the currently selected node

## model.mesh(indices, vertices)
create a mesh from the specified tables

### create a simple triangle mesh and a node from it
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
  meshid=model.mesh(i,v)
  id=model.node(meshid)
```
## model.node(meshid)

## model.pointlight(r, g, b, radius)
add a point light; rgb 0..1

## model.texture(imgfname)
apply an image as a texture to a node

## model.line3dex(x1,y1,z1,x2,y2,z2,clr)

## model.line3d(x1,y1,z1,x2,y2,z2,clr)

## model.get(property)
get attribute value of selected node

## model.lookat(x,y,z)
aim the camera at a position

## model.siton(nodeid)
position and look direction of selected node becomes relative to nodeid

# Flow Control
## flow.wait(ms, funcname, repeat)
wait X milliseconds and then run a function by name

```lua
flow.wait(1000, "myFunction")
```
### calls funcRepeats() approx. every 20 ms
```lua
flow.wait(20, "funcRepeats", "repeat")
```
## flow.on(event, funcname)
call a handler on event trigger

```lua
flow.on("keydown", "mykeyhandler")
```
```lua
flow.on("mousedownobj", "mynodeclickhandler")
```
# Physics
## physics.force()

## physics.impulse()

# User Interface
## ui.screeninp(noneOrConsOrEmu)

## print(arg1,arg2..)

## ui.cls()

## ui.screen(num)
create a new screen or switch to an existing; print() and palette() affect this screen

## ui.screenon(nodeid)
apply emu or ui screen as a texture to a node

### texture a node with an emulator screen
```lua
geom = require 'geom'
require 'utils'
i,v = geom.face2(0.5,0.5,1,0,0,0)
screenMesh = model.mesh(i,v)
screen = model.node(screenMesh)
model.pos(0,-5,0)
model.rot(0,0,90)
model.scale(10,10,10)
rtype = emucmd('cores/mamenew', 'rtype2')
model.scale(0.0001, 0.0001, 0.0001)
function emustarted(which)
  model.sel(screen)
  ui.screenon(rtype)
end
flow.wait(2000, 'emustarted')
```
## ui.palette(index,r,g,b,a)
change color values at index

## ui.screeninp(noneOrConsOrEmu)

## ui.showscreen(num)

# Networking
## net.geturl(url)

## net.saveurl(url, fname)

# Utilities
## dir(glob)
List files in directory

## emucmd(core, argswspaces)
run a .cmd that simulates cmd-line for emulator

