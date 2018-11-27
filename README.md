# Models and Positioning
## rez
          Rez (instantiate) a 3d model (3ds dae xml x mdl lwo obj mesh bsp md2 md3 stl ply)
          NOTE: Not all models are compatible. YMMV. 

```lua
 rez('mymodel.3ds') 
```
```lua
 local mynodeid = rez('myhouse.obj') 
```
# Emulation
## emulate
Run in emulator (set with emucore) in a new screen to emulate a given system with an optional command/rom/binary.
See also emucore() for changing cores.
NOTE: YOU MUST HAVE THE REQUIRED ROM OR OTHER FILES INSTALLED IN THE EXPECTED LOCATIONS.

```lua
emucore('snes9x')
emulate(-1, 'topgear.sfc') 
```
