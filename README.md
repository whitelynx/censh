censh
=====

_Design for an integrated car entertainment/navigation system and HUD._

This design is based on my 2010 Subaru Outback 2.5i Limited.


Hardware
--------

**In-dash navigation / entertainment:**
- [Raspberry Pi 3 Model B+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/)
- [Raspberry Pi 7" Touch Display](https://www.raspberrypi.org/products/raspberry-pi-touch-display/)

**Heads-Up Display:**
- Used [OnePlus 3T](https://oneplus.net/3t)

**Steering Wheel Controls:**
- [Nano DCCduino](http://arduinolearning.com/hardware/dccduino-arduino-nano-clone.php) or [Teensy-LC](https://www.pjrc.com/store/teensylc.html)

_(Since the steering wheel controls no longer work correctly, the plan is to replace the original resistance-based circuit with a USB HID board)_

**Audio:**
- [Vantec NBA-200U USB External 7.1 Channel Audio Amplifier](https://smile.amazon.com/Vantec-NBA-200U-External-Channel-Adapter/dp/B004HXGJ3S/ref=pd_sim_147_25?_encoding=UTF8&pd_rd_i=B004HXGJ3S&pd_rd_r=FZG4H7Z0KSB70M6TDVZA&pd_rd_w=hMcMF&pd_rd_wg=r5uUV&psc=1&refRID=FZG4H7Z0KSB70M6TDVZA) or [HDE USB 2.0 External 5.1 Channel Sound Card](https://smile.amazon.com/HDE-External-Channel-Surround-Optical/dp/B009NVS6KS/ref=sr_1_39?ie=UTF8&qid=1522769910&sr=8-39&keywords=usb+surround+sound+adapter)


Software
--------

- [Arch Linux ARM](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3)
- [karvy](https://github.com/whitelynx/karvy) - a Kivy-based car entertainment and navigation system interface
