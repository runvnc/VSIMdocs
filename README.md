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
## emu.opt(emulatorid,property,value)
specify emulator option

## emu.insert(emulatorid,drivenum,dskfile)
insert virtual disk into emulator drive

## emu.eject(emulatorid,drivenum)
eject disk from virtual emulator drive

## emu.sendtext(emulatorid,text)

## emu.sendkeys(emulatorid,keys)

## emu.holdkey(emulatorid, key, duration)

## emu.releasekey(emulatorid, key)

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

## model.pointlight

## model.texture(fname)

## model.line3dex(x1,y1,z1,x2,y2,z2,clr)

## model.line3d(x1,y1,z1,x2,y2,z2,clr)

## model.get(property)

## model.lookat(x,y,z)

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
on("keydown", "mykeyhandler"
```
```lua
on("mousedownobj", "mynodeclickhandler")
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
apply the screen as a texture to a node

## ui.palette(index,r,g,b,a)
change color values at index

## ui.screeninp(noneOrConsOrEmu)

## ui.showscreen(num)

# Networking
## net.geturl(url)

## net.saveurl(url, fname)

