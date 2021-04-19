# KBIC65 Build Log
Overview of build steps
- Prepare nice!nano
    - Set up ZMK and generate uf2 file
    - Load firmware with keymap
- Prepare foam/rubber layers (optional)
    - Attach plate foam
    - Cut out neoprene sheet
- Prepare bottom plate
    - Attach rubber feet
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
I had been looking at how to create a custom wireless keyboard for a while. My initial research suggested using an Adafruit Feather BLE with QMK, such as the [Dissatisfaction65 by Nicell](https://github.com/Nicell/Dissatisfaction-65), but luckily just a few months earlier Nicell himself had created the nice!nano controller, which is a ProMicro footprint Arduino close with Bluetooth. Even better, I found there was a relatively new keyboard firmware project called [ZMK](https://zmkfirmware.dev/), that addressed a bunch of the issues that QMK has with wireless. The two primary issues resolved by ZMK is (1) more battery-efficient scanning algorithms to improve battery life and (2) a license that is compatible with the Bluetooth libraries since QMK is not legally compatible with the libraries required to run Bluetooth chips.

In addition, however, ZMK has learned a lot from how QMK is used and also improved other aspects of the project, such as minimal user repositories that hosts your personal keymap and keyboard configurations and that then builds the ZMK firmware using GitHub Actions. A really neat setup in my opinion. Of course, they still don't have VIA or something like the QMK web tool, but in my case I was building my own PCB and matrix and therefore would need to dig into some code either way.

ZMK has pretty good documentation, but it also helped looking at other ZMK user repositories. My recommended reading guide order someone new to ZMK and that would like to replicate my work would be
1. [Read the introduction](https://zmkfirmware.dev/docs/)
2. [Read the FAQ and understand the difference between board and shield](https://zmkfirmware.dev/docs/faq)
3. [Set up a ZMK user repo](https://zmkfirmware.dev/docs/user-setup)
4. [Create a new shield](https://zmkfirmware.dev/docs/development/new-shield/)

I then used the [Nibble ZMK shield](https://github.com/zmkfirmware/zmk/tree/main/app/boards/shields/nibble) as a reference, there are probably better options though since the Nibble has an extra column to the left, a multiplexer for the matrix and support for rotary encoders, all of which I didn't need for my build.

I then created a first keymap, pushed to my [personal config repo](https://github.com/b-karl/zmk-config) and with some [ZMK GitHub Actions magic](https://github.com/b-karl/zmk-config/actions) I could download a uf2 file to flash my nice!nano with.

The nice!nano was super-easy to flash with a new firmware since it uses a bootloader that makes it show up as a mass-storage device. Then it is simple copy-paste or drag-and-drop of the new .uf2 file to the device and once the transfer is complete it automatically flashes itself and voilà, a new keyboard is detected.

# Prepare foam and rubber
## Plate foam
This is my second keyboard build, my first was a KBD75v2 kit from KBDfans. For that build I got [plate foam](https://kbdfans.com/collections/keyboard-foam/products/kbdfans-module-foam) and I had enough leftover to also cover this build. The modular plate foam is most easily placed using a tweezer to avoid deforming the pieces to much before the glue touches the plate. I also tried to keep the surrounding edges clean since they will be visible from the sides. 

<img src="img\build_log\20210405_201929.jpg">

Unfortunately, I was a little too eager with covering everything. It turned out when I was assembling the plate and PCB  that some of the foam I had put in around the stabilizers was pressing on them, so I had to disassemble my work so far and clean up all the foam above and below the stabilizer mounts and along the stabilizer wire.

## Case foam/rubber
To add some weight and sound dampening without impeding the wireless signal too much, I decided to add a [3 mm thick neoprene rubber](https://www.swedol.se/neoprengummipg-1001022.html) cutout between the PCB and the bottom plate. I took one of my spare PCBs and used it to draw the outline on my neoprene sheet and then I used a carpet knife and a hole puncher to create the shape.

<img src="img\build_log\20210405_201821.jpg">

### Some notes on silencing a mechanical keyboard (or controlling sound profile)

Doing some research on how to dampen the sound of the keyboard (since I want to use it at my office in the future without pissing off my colleagues) the factors that I have understood to be most important, and think makes sense from my limited experience with two keyboards are the following

- Use a silent linear, silent tactile, linear or tactile switch (on order of most to least silent), a clicky switch is by definition not silent.
- Weight is one of the most important factors, the heavier the better so metal cases are better than plastic ones. This goes in conflict with a wireless build so I opted to aim to make the keyboard as heavy as possible without using metals that might shield the Bluetooth signal.
- Put the keyboard on a soft desk mat.
- Fill up hollow spaces in the keyboard with foam, rubber or some other material. Foam makes most sense usually since it probably has the least impact on the flexibility and motion of the plate and thus the give with each keystroke.
- Use a softer plate material, aluminum is usually considered OK among metal but brass and steel might cause ping sounds.
- Band-aid mod stabilizers and possibly crimp tube mod them.
- Lube stabilizers
- Lube switches

If you have done all of the above and want to try something else, you can try - Putting O-rings on the key cap stems. The idea with this is that it will dampen the sound when bottoming out, but it might also make the keys feel more mushy and reduces key travel somewhat. If and how well it works also depends on your key cap profile and materials. This mod is a very loaded subject on r/mk and I think it has very little impact compared to the points above.
- Fill larger keycaps, or if you're extreme all keycaps, with foam to remove and reverb inside the keycap. This mod is most commonly done for the space bar.

### Choice of case foam
Since I wanted my case foam to both be a good sound absorber and provide as much weight as possible the options I found most suitable were:
- Sorbothane: Expensive and hard to get in a good size if you have an open case design as my first iteration will be
- Butyl rubber or similar: Used for sound deadening in cars and the best alternative I found was something like [Dynamat Dynaliner](https://www.amazon.com/Dynamat-11101-Dynaliner-Self-Adhesive-Deadener/dp/B001KM9C4C). Issues with this was once again price but I also read that it can smell quite a bit and it takes a while before the smell goes away, which again is maybe not the best choice with an open case design. The benefit would, however, be that it is probably the heaviest of the options around.
- High-density EVA foam: Relatively cheap but dense foam commonly used for cosplay and role playing.
- Neoprene rubber: Also relatively cheap and available.

Comparing these I ruled out sorbothane and butyl rubber, leaving HD-EVA and neoprene. Out of these I then looked up the common densities of these materials and neoprene won by a small margin so I settled on neoprene.

# Prepare bottom plate
As they always say in keyboard build videos, start with putting rubber feet on your case to protect it from scratches. In addition, it will also be nice to occasionally use the bottom and neoprene sheet as a base when working with the PCB and plate.

For screws and spacers I wanted them to be in brass, or look like golden brass at least. This was a bit tricky to find in Sweden, but I eventually learned that Amazon is a pretty good source for random screws and I picked up [this kit](https://www.amazon.se/gp/product/B087N3Z4RY/ref=ppx_od_dt_b_asin_title_s00?ie=UTF8&psc=1), giving me some flexibility if I want to play with the mounting. I attached 10 mm spacers to the bottom and then put the neoprene on for the moment. The neoprene feels like a good soft surface to rest the PCB once diodes, controller and switches are soldered in.

<img src="img\build_log\20210405_201831.jpg">
<img src="img\build_log\20210405_202032.jpg">

# Prepare PCB
There is no real test like getting something to run in real life. I ran checks in KiCad when developing my PCB and in addition, JLCPCB do probe testing to check the PCB. I could, of course, have messed up something more fundamental in my design that wouldn't be caught in any of these checks.

To get the PCB up and running required two general steps
- Attach the nice!nano (which I did by socketing it so I can remove it easily if I want).
- Solder in diodes for all switches.


# Prepare and attach stabilizers

# Assemble plate-PCB package

# Assemble complete keyboard

# Put on key caps

# Final testing
