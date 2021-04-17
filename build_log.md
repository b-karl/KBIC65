# KBIC65 Build Log
Overview of build steps
- Prepare nice!nano
    - Set up ZMK and generate uf2 file
    - Load firmware with keymap
- Prepare foam/rubber layers (optional)
    - Attach plate foam
    - Cut out neoprene sheet
- Prepare bottom plate
    - Attach rubbet feet
    - Attach spacers to align components
- Prepare PCB
    - Solder on diodes
    - Socket nice!nano
    - Test PCB
- Prepare and attach stabilizers
    - Stabilizer foam / band-aid mod
    - Clipping (not necessary)
    - Crimp tube mod (reverted after testing)
    - Lube
    - Attach stabilizers
- Assemble plate-PCB package
    - Attach and solder on switches
    - Test assembled module
- Assemble keyboard without battery
- Test keyboard
- Add battery
- Test again (now with Bluetooth!)
- Put on keycaps
- Enjoy!
- Remember you were supposed to put on am acrylic window, order it and wait

# Prepare nice!nano
I had been looking at how to create a custom wireless keyboard for a while. My initial research suggested using an Adafruit Feather BLE with QMK, such as the [Dissatisfaction65 by Nicell](https://github.com/Nicell/Dissatisfaction-65), but luckily just a few months earlier Nicell himself had created the nice!nano controller, which is a ProMicro footprint Arduino close with bluetooth. Even better, I found there was a relatively new keyboard firmware project called [ZMK](https://zmkfirmware.dev/), that addressed a bunch of the issues that QMK has with wireless. The two primary issues resolved by ZMK is (1) more battery-efficient scanning algorithms to improve battery life and (2) a license that is compatible with the Bluetooth libraries since QMK is not legally compatible with the libraries required to run Bluetooth chips.

In additio, however, ZMK has learned a lot from how QMK is used and also improved other aspects of the project, such as minimal user repositories that hosts your personal keymaps and keyboard configurations and that then builds the ZMK firmware using GitHub Actions. A really neat setup in my opinion. Of course, they still don't have VIA or something like the QMK web tool, but in my case I was building my own PCB and matrix and therefore would need to dig into some code either way.

ZMK has pretty good documentation, but it also helped looking at other ZMK user repos. My recommended reading guide order someone new to ZMK and that would like to replicate my work would be
1. [Read the introduction](https://zmkfirmware.dev/docs/)
2. [Read the FAQ and understand the difference between board and shield](https://zmkfirmware.dev/docs/faq)
3. [Set up a ZMK user repo](https://zmkfirmware.dev/docs/user-setup)
4. [Create a new shield](https://zmkfirmware.dev/docs/development/new-shield/)

I then used the [Nibble ZMK shield](https://github.com/zmkfirmware/zmk/tree/main/app/boards/shields/nibble) as a reference, there are probably better options though since the Nibble has an extra column to the left, a multiplexer for the matrix and support for rotary encoders, all of which I didn't need for my build.

I then created a first keymap, pushed to my [personal config repo](https://github.com/b-karl/zmk-config) and with some [ZMK GitHub Actions magic](https://github.com/b-karl/zmk-config/actions) I could download a uf2 file to flash my nice!nano with.

The nice!nano was super-easy to flash with a new firmware since it uses a bootloader that makes it show up as a mass-storage device. Then it is simple copy-paste or drag-and-drop of the new .uf2 file to the device and once the transfer is complete it automically flashes itself and voilá, a new keyboard is detected.

# Prepare foam and rubber
## Plate foam
This is my second keyboard build, my first was a KBD75v2 kit from KBDfans. For that build I got [plate foam](https://kbdfans.com/collections/keyboard-foam/products/kbdfans-module-foam) and I had enough leftover to also cover this build. The modular plate foam is most easily placed using a tweezer to avoid deforming the pieces to much before the glue touches the plate. I also tried to keep the surrouding edges clean since they will be visible from the sides. 

<img src="img\build_log\20210405_201929.jpg">

Unfortunately, I was a little too eager with covering everything. It turned out when I was assembpling the plate and PCB  that some of the foam I had put in around the stabilizers was pressing on them, so I had to disassemble my work so far and clean up all the foam above and below the stabilizer mounts and along the stabilizer wire.

## Case foam/rubber
To add some weight and sound dampening without impeding the wireless signal too much, I decided to add a [3 mm thick neoprene rubber](https://www.swedol.se/neoprengummipg-1001022.html) cutout between the PCB and the bottom plate. I took one of my spare PCBs and used it to draw the outline on my neoprene sheet and then I used a carpet knife and a hole puncher to create the shape.

<img src="img\build_log\20210405_201821.jpg">

# Prepare bottom plate
As they always say in keyboard build videos, start with putting rubbet feet on your case to protect it from scratches. In addition, it will also be nice to occasionally use the bottom and neoprene sheet as a base when working with the PCB and plate.

For screws and spacers I wanted them to be in brass, or look like golden brass at least. This was a bit tricky to find in Sweden, but I eventually learned that Amazon is a pretty good source for random screws and I picked up [this kit](https://www.amazon.se/gp/product/B087N3Z4RY/ref=ppx_od_dt_b_asin_title_s00?ie=UTF8&psc=1), giving me some flexibility if I want to play with the mounting. I attached 10 mm spacers to the bottom and then put the neoprene on in for the moment.

<img src="img\build_log\20210405_201831.jpg">
<img src="img\build_log\20210405_202032.jpg">

# Prepare PCB

# Prepare and attach stabilizers

# Assemble plate-PCB package

# Assemble complete keyboard

# Put on keycaps

# Final testing
