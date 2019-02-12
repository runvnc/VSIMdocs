# Intro
## About VSIM
Vintage Simulator is a (currently 100% FREE) custom libretro front-end (sharing zero code with RetroArch) with the following features:
* Implements most of the libretro API
* Run several emulators at the same time
* Full Lua scripting API
* 3D graphics and sound
* Easily load most 3D models such as 3DS or OBJ
* Bullet Physics engine
* Plugins
* includes LOVE plugin (for UI screens in separate windows or generating textures etc.)

## Developers
VSIM is a work in progress.  VSIM is currently primarily aimed at programmers who are interested in things like emulation, Lua, 3D models, or physics simulation.  For example, it can provide a good starting point for creating your own custom front-end for libretro.  The hope is that some developers will be interested and will create plugins that add functionality or content that non-programmers can easily access.

## Keybindings
|Key|What It Does|
|----|------------|
|`F5`  |Install plugin|
|`Ctrl-F1`|Open help in browser              |
|`` ` ``   |Toggle Lua console|
|`1-9` | Zoom and interact with emulator #N|
|`F7`  | Put zoomed emulator in full screen mode|
|`Ctrl-F10`|Exit|

## Finding Plugins
Currently https://reddit.com/r/vsim is the best place to find plugins or post any you create.

# top
## Installing Plugins
To install a plugin press F5, paste in the plugin URL with Control-V, then hit ENTER.  You will need to restart the program before the plugin will be active.

## Creating Plugins
To create a plugin, first make a directory in [VSIM root]/lua/.  Plugins can contain files and/or lua code in init.lua.  You can test your plugin by adding it to the list in the [VSIM root]/plugins file and restarting VSIM.  When it is ready open the console and type plugin_makezip("mydir")[ENTER] where mydir is the subdirectory of [VSIM root]/lua/ (just the folder name, not a full path).  It will create a .7z file in [VSIM root]/lua/plugins/forupload which you can upload to your host.  Then just share the URL for your plugin. 

# Emulation
## emu.emulate(emulatorid,filetoload,tableopts)
Run selected emulator (set with emu.core()) with an optional command/rom/binary and options table with emulator variable settings. Note: if there is a cores.cfg file it is parsed by the utils plugin at program start and placed in vsimcorecfg.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.  You may run the same core multiple times simultaneously or several different cores depending on system resources.

### run Top Gear SNES game
```lua
emu.core('snes9x')
emulatorid = emu.emulate(-1, 'topgear.sfc', vsimcorecfg.snes9x) 
```
## emu.core(fnameNoExt)
specify the emulator core to use with emulate() commmands

### next emulate() with MAME core
```lua
emu.core("mame") -- needs mame.dll
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
set this emu option to string "true" to pause emulation

## vsim_3daudio
set this emu option to string "true" to turn on positional audio from emulator

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

## VSIM_CAST_SHADOW
(model.put "true"): selected node casts a shadow (does not work on high-poly meshes)

## model.sky(skydomeTextureFname,texturePerc, spherePerc, radius)
create a sky dome; texturePerc=0..1, spherePerc=0..2

## VSIM_AMBIENT
set this variable on any node to change ambient light color of entire scene

```lua
put('VSIM_AMBIENT', 255,95, 95, 95)
```
## model.put(property, value1, value2..)
set an attribute on a node or the system

## VSIM_DBG_MSGS
set this attribute on any node to string "true" to show VSIM internal messages in STDOUT

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
add a scene node based on a mesh

## model.pointlight(r, g, b, radius)
add a point light; rgb 0..1

## model.texture(imgfname, [n]
apply an image as a texture to a node; optional texture num n

## model.line3dex(x1,y1,z1,x2,y2,z2,clr)
add a 3d line with thickness

## model.line3d(x1,y1,z1,x2,y2,z2,clr)
add a 3d line

## model.get(property)
get attribute value of selected node

## model.lookat(x,y,z)
aim the camera at a position

## model.siton(nodeid)
position and look direction of selected node becomes relative to nodeid

## model.fly(x1,y1,z1,x2,y2,z2,ms,loop,repeat)
animate selected node; loop/repeat string "true" or "false"

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
### Menu example
```lua
require 'utils'
function menukey(code, char) 
  if handler ~= nil then handler(char) end
end
function firstMenu()
  ui.cls()
  ui.palette(2,255,255,255,255)
  ui.showscreen(1)
  print("Press key to select an option:")
  print('1) Option The First')
  print('2) Option The Second')
  print('3) Cancel')
  handler = secondMenu
end
function secondMenu(opt)
 if (opt == "3") then
    print("Cancel")
    handler = nil
    return
  end
  print("You selected "..opt)
 
  print("Press key to select a suboption")
  print("1) Option A")
  print("2) Option B")
  handler = thirdMenu
end
function thirdMenu(opt)
  print("You selected suboption "..opt)
  print("Thank you for your input.")
  handler = nil
end
function menutest()
 firstMenu()
end
flow.on('keydown', 'menukey')
 
menutest()
```
# Physics
## physics.force(fx,fy,fz,px,py,pz)
add a force w/dir (fx,fy,fz) and rel. pos (px,py,pz); returns forceid

## physics.delforce(forceid)
remove force

## physics.deltorque(torqueid)
remove torque

## physics.torque(tx,ty,tz)
add a torque around axis tx,ty,tz ; longer vector = greater torque; returns torqueid

## physics.impulse(fx,fx,yz,px,py,pz)
apply an impulse given direction and relative position

## collision
Enable collisions by setting this attribute

### enable collision and set mass to 5
```lua
model.put("collision", "gimpact", 5)
```
# User Interface
## ui.screeninp(which)
keys used for movement (0), console (1) or emulator(2+)

## flow.waitui()
wait for UI to process all lua commands

## print(arg1,arg2..)

## ui.cls()

## VSIM_OVERLAY
set w/model.put on any node to png filename to change the overlay image

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
### write some text on a mesh/node
```lua
geom = require 'geom'
i,v = geom.face2(5,5,0,0,0)
labelMesh = model.mesh(i,v)
lblnode = model.node(labelMesh)
ui.screen()
print("Text on node")
flow.waitui()
ui.screenon()
ui.screen(0)
```
## ui.palette(index,r,g,b,a)
change color values at index

## ui.showscreen(num)
show console (1) or hide (0)

## ui.filedialog(title, filetypes)
Open a file dialog and return the selected filename

```lua
f=ui.filedialog('Choose file', "Any file\0*.*\0"
```
## ui.draw(id, commands)
add, update or delete draw commands based on Cairo.
Commands and arguments separated by spaces. id -1 to append, blank command string to delete. Available commands: font, size, path (start new path), move x y, line x y, sub (new subpath), end (end sub-path), scale x y, trans x y, save (save state), rest (restore state), arc x y radius degreestart degreeend, curve (cubic Bezier) dx1 dy1 dx2 dy2 dx3 dy3, rot deg, rect x y w h, color r g b a (0..1), fill, stroke (fill/stroke required to actually output shapes). See Cairo documentation and the following examples.

### load and select font; then change the command list at that index to use a different font
```lua
f=ui.draw(-1, "font fonts\\Open_Sans.ttf size 20"
ui.draw(f, "font MyFont.ttf size 22")
```
### creates a rotating plus with label indicating degrees rotated
```lua
ui.palette(1,0,0,0,0) -- transparent screen (console) background
ui.cls()
ui.draw(-1, "trans 200 200")
ui.draw(-1, "rot 0")
ui.draw(-1, "trans -25 -25")
ui.draw(-1, "move 60 0")
ui.text(-1, "0")
-- note that stroke and/or fill are required to actually show anything
ui.draw(-1, "move -50 0 line 50 0 move 0 -50 line 0 50 stroke")
function dorot()
  -- use clock for smoother animation
  r = os.clock() * 50
  -- modifies the draw command at position 1 (0 is first)
  -- note use of substitution with globals table can be useful for constructing
  -- dynamic command strings
  ui.draw(1, "rot ${r}" % _G)
  -- update text which is index 4 in draw command line
  ui.text(4, r)
end
-- animate by updating draw command list every 16 ms
flow.wait(16, 'dorot', 'repeat')
```
## ui.text(id, string)
add,update, or delete a text element at the current x, y coordinate

# Networking
## net.geturl(url, callback)
HTTP GET and return response body to callback function

## net.saveurl(url, fname, callback)
HTTP GET and save response to fname

# Utilities
## emucmd(core, argswspaces)
run a .cmd that simulates cmd-line for emulator

## dir(glob)
List files in directory

# 7-zip compression and decompression
## unzip(fname)
unzip a file (uses 7-Zip, LGPL, www.7-zip.org)

# love 2D engine
## lovewait(plugindir)
run a love program from vsimroot/lua/plugindir/main.lua and return the stdout as a string

## love(plugindir)
run a love program from vsimroot/lua/plugindir/main.lua in the background i.e. dont wait for it to finish

