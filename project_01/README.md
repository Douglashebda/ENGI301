An implementation of BeagleG using a PocketBeagle and a GRBL Arduino CNC Shield.

**Building Instructions:**
Follow the install directions for BeagleG outlined here:
https://github.com/hzeller/beagleg/blob/master/INSTALL.md

Once installed you need to clone the PocketBeagle/GRBL shield hardware setup into the hardware directory. 
```
git clone --recursive https://github.com/Douglashebda/ENGI301/project_01.git
```
These files contain valid pin mapping for a 3-axis CNC on the PocketBeagle.

Then run this line from your hardware directory to update generate an updated .dtbo from the Devicetree Source file
```
sudo /start-devicetree-overlay.sh /GRBL/BeagleG-GRBL.dts
```
This returns an error, but should generate the file. 
The following code achieves the same end result as the failed function of the above line:
```
cd /boot
sudo nano uEnv.txt
```
under "Additional Custom Capes" add
```
uboot_overlay_addr4=/<full address>/beagleg/hardware/GRBL/BeagleG-GRBL-00A0.dtbo
```
then reboot.
 
Finally you have to remake the file with your hardware configuration:
```
make clean
make BEAGLEG_HARDWARE_TARGET=GRBL
```

Then a configuration file should be compiled, using mine or the sample config in the BeagleG repository.

**Other Additions:**
I also changed the homing speed for use with my limit switches. 
Open Gcode-machine-control.cc in src directory, and change line #967
```
const float kHomingSpeed = 30;  // mm/sec  (make configurable ?)
```
I found 30 to be decent but can set and test to your own liking.

**References**

Henner Zeller- https://github.com/hzeller/beagleg
