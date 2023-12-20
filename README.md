censh
=====

_Design for an integrated car entertainment/navigation system and HUD._

This design is based on my 2010 Subaru Outback 2.5i Limited.


Hardware
--------

**In-dash navigation / entertainment:**
- ~[Raspberry Pi 3 Model B+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/)~ [Raspberry Pi 4 Model B 2GB](https://www.raspberrypi.org/products/raspberry-pi-4-model-b)
- [Raspberry Pi 7" Touch Display](https://www.raspberrypi.org/products/raspberry-pi-touch-display/)

**Heads-Up Display:**
- Used [OnePlus 3T](https://oneplus.net/3t)

**Steering Wheel Controls:**
- [Nano DCCduino](http://arduinolearning.com/hardware/dccduino-arduino-nano-clone.php) or [Teensy-LC](https://www.pjrc.com/store/teensylc.html)

_(Since the steering wheel controls no longer work correctly, the plan is to replace the original resistance-based circuit with a USB HID board)_

**Audio:**
- [Vantec NBA-200U USB External 7.1 Channel Audio Amplifier](https://smile.amazon.com/Vantec-NBA-200U-External-Channel-Adapter/dp/B004HXGJ3S/ref=pd_sim_147_25?_encoding=UTF8&pd_rd_i=B004HXGJ3S&pd_rd_r=FZG4H7Z0KSB70M6TDVZA&pd_rd_w=hMcMF&pd_rd_wg=r5uUV&psc=1&refRID=FZG4H7Z0KSB70M6TDVZA) or [HDE USB 2.0 External 5.1 Channel Sound Card](https://smile.amazon.com/HDE-External-Channel-Surround-Optical/dp/B009NVS6KS/ref=sr_1_39?ie=UTF8&qid=1522769910&sr=8-39&keywords=usb+surround+sound+adapter)

_(Any USB sound card with enough output channels should do fine)_


Software
--------

- [Arch Linux ARM](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3) (also evaluating [Alpine Linux](https://wiki.alpinelinux.org/wiki/Raspberry_Pi))
- [karvy](https://github.com/whitelynx/karvy) - a Kivy-based car entertainment and navigation system interface


Setup
-----

### Get Bluetooth working

On some distros, it just works. For ArchLinux ARM, you need to do a bit more legwork: https://archlinuxarm.org/forum/viewtopic.php?p=63076#p63076


### Edit `/etc/bluetooth/main.conf`

- Set `Name` to a name you can recognize (I used `Censh`)
- Set `Class` to `0x200420`
- Set `AutoEnable=true`


### Edit `/etc/pulse/client.conf`

Add the following line:
```
extra-arguments = --exit-idle-time=-1 --log-target=syslog
```


### Add Bluetooth service class UUIDs

```sh
sudo btmgmt --index 1 clr-uuids
sudo btmgmt --index 1 add-uuid 0000110b-0000-1000-8000-00805f9b34fb 32  # A2DP AudioSink
sudo btmgmt --index 1 add-uuid 0000110e-0000-1000-8000-00805f9b34fb 0   # AVRCP A/V_RemoteControl
sudo btmgmt --index 1 add-uuid 0000110f-0000-1000-8000-00805f9b34fb 0   # AVRCP A/V_RemoteControlController
```

Then, in `bluetoothctl`:
```sh
menu gatt
register-service 0000110b-0000-1000-8000-00805f9b34fb
```
and answer `yes` when it asks whether it should be the primary service.
