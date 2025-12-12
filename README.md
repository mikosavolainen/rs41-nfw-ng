# RS41-NFW - Versatile, custom firmware for ALL revisions of Vaisala RS41 radiosondes
## **Vaisala RS41 New Firmware** (*RS41 Nevvman's Firmware*) <br>
**NOTE:** This firmware works with the **ALL** variants of RS41 radiosondes, with the new (2023 and 2025) ones too, bringing full hardware and software support with lots of features for everyone. More below.<br><br>
Vaisala some time ago began launching new RS41 sonde revisions, with new internal design. They can be recognized by a last digit of 4 or 5 of the PCB model (eg. `RSM414`, `RSM424`, `RSM425`). This firmware is an approach for reusing them as amateur devices for many different purposes. It brings full and thorough support for [all revisions](../hw/README.md#older-vs-newer---how-do-i-know-which-one-im-holding-now).<br>

* [RS41-NFW Firmware features](#rs41-nfw-firmware-features)
* [Terms of Use](#terms-of-use)
* [Radiosondes?](#radiosondes)
* [Installation guide](#installation-guide)
* [Firmware flashing](#firmware-flashing)
* [Firmware compilation](#firmware-compilation)
* [Firmware and device operation](#firmware-and-device-operation)
* [RSM414 hardware](#rsm414-hardware)
* [Firmware changelog](#firmware-changelog)
* [Authors and contributors to this branch](#authors-and-contributors-to-this-branch)
* [References](#references)
* [Final notes](#final-notes)

## RS41-NFW Firmware features
* **Full support for ALL** RS41 versions (eg. `RSM421`, `RSM412`, `RSM414`, `RSM424`, `RSM425`), including the old and new ones with the '4' at the end of the PCB model
* Multiple, customizable transmission modes
    * [**Horus Binary 4FSK v2**](https://github.com/projecthorus/horusdemodlib/wiki)
        * One of the most efficient radio modes for HAB and other simple telemetry designs, allows for decoding of very weak signals
        * Multi-QRG operation (ability to specify second Horus one, user can modify the code easily to get as much QRGs as wanted on every mode)
    * APRS
      * 1200 baud, with 1200Hz and 2200Hz tones, achieved by FSK switching in a precisely tuned loop (very good performance)
      * Many config options, including HAB (PSTVC structure compliant with RS41ng) and WX station reporting formats, overlay symbol modifier, SSID, destination (`APZNFW` supported and decoded by SondeHub), digi, etc.
    * RTTY
        * Customizable 45, 75 and 100 baud rates, also other available
        * Customizable tone spacing as a multiplication of 270Hz, default 570Hz
        * Data bits and stop bits customizable (default 7N2)
        * Compliant with UKHAS format. Provided by OM3BC
    * Morse code (CW)
        * Customizable wpm speed and dot length
        * Compliant with UKHAS format
    * PIP
        * Beacon operation, transmitting short beep with a specified interval, which could be used as a foxhunting TX device
* Thorough support of RS41 hardware, including GPS, radio, power circuitry, reference heating etc. ...and:
* Support for **onboard boom sensors**, including **temperature and humidity** sensors. Pressure *estimation* (like SG models)
* Detailed in-built **debugging** features via LED status and serial messages
* Onboard **button** allowing user to change different operation modes and parameters 'in-flight'
* **Safety features**, including GPS watchdog and position improvement (these two improve flights in environments with interference/noise), battery voltage protection, sensors defrosting and condensation prevention, system reset watchdog
* Support for extending hardware capabilities, including **OIF411**
* **Power saving** features, including GPS power management (together with powersaving modes and OFF mode for stationary use cases) and automatic radio adjusting
* **User-friendly** firmware and IDE allows users to easily customimze the device operation
* Weather station mode, supporting APRS WX report, constant coordinates
* Fox hunting mode, with CW and FM audio beacons
* Flight controling algorithms. Ability to rapidly send packets when below set altitude. Data analysis and debug sent via APRS extended packets every set interval
* Automatic calibration modes for temperature and humidity sensors on the silver boom, ground-check procedures, humidity module reconditioning. Ability to further improve accuracy by manually calibrating the readings
* And many more - mentioned in [changelog](#firmware-changelog) and [manual](./fw/OPERATION_MANUAL.md)


## Terms of Use
**RS41-NFW** project (author - Franek *nevvman SP5FRA*) is released under **GNU GPL-3.0 license**. This software is **open source** and **free to use for amateur projects**, **which cannot lead to profit** in any kind. This excludes usage of this firmware as a commercial product. **For commercial use, please contact me**. 
The creator of this project isn't at all responsible for any kind of harm made by devices operated with these instructions. Follow your local law about radio transmissions and balloon flights. Altough the firmware **tested successfully** on several dozen of flights, keep in mind that it is still a *hobbyst project*.


## Radiosondes?
These small electronic devices are used by weather instututes to perform atmospheric sounding and high altitude measurements, up to the stratosphere (HAB - high altitude ballooning). After the flight, usually they are *meaningless* for the launch company, so they can be collected by people (verify this according to the certain launch site). This acvitivty is called *radiosonde hunting*<br><br>
The most simple and costless way of collecting radiosondes is to track them on sites like [radiosondy.info](https://radiosondy.info/) or [SondeHub](https://sondehub.org/) (previously HabHub). <br>
Another, more advanced way is to hunt them with radio receivers. Most of them transmit on the EU 400-406 MHz radiosonde band, near an amateur 70cm band. You can do that by a simple direction finding with a directional (for example Yagi) antenna and a handheld receiver. <br><br>
But, currently the best way is to utilize a Software-Defined Radio (SDR, for example an RTL-SDR v3 / v4, Nooelec SDR, RSP1 or HackRF) together with a 70cm band antenna (dipole should work for sondes in air as far as 100km, the best is a high gain Yagi, with this setup you could easily hear a radiosonde hundreds kilometers away) and a specialized software for a computer, laptop or a Raspberry Pi. On the internet you will find lots of tutorials for receiver setup, tracking and hunting of them. Also, mobile tracking devices gain popularity, such as Lilygo TTGO boards flashed with RDZsonde (suggested) or MySondy (alternative to rdz) firmwares. <br><br>
**Kind note:** After each hunt, either successful or not, please change the radiosonde status on the previously mentioned trakcing sites. This will not only let many people save on fuel and patience, but also allow everyone to take a look on sounding statistics and other things. On the most simple site for tracking (SondeHub) you don't even need to create an account to change the sonde status, which only takes a minute. <br>
*It's an unpleasant feeling, when after driving dozens of kilometers in search for radiosonde you come across an empty field without any balloon traces.*<br><br>
For more details about HAB and sonde hunting, please look on google and social media, there is a ton of valuable content.

## Installation guide
A thorough, detailed project guide is available at the links below.<br>
**If you want to fully utilize all capabilities of this firmware**, please, read the documentation in the following header order:


## Firmware flashing
See: [fw/FLASHING.md](./fw/FLASHING.md)


## Firmware compilation
See: [fw/COMPILE.md](./fw/COMPILE.md)


## Firmware and device operation
See: [fw/OPERATION_MANUAL.md](./fw/OPERATION_MANUAL.md) <br>
The options in the firmware file should be self explanatory (alongside with the comments near them). This manual should be up-to-date, but there may be some issues with it (it's hard to manage that long markdown file, sorry :) ). If you have **any** problems, questions and suggestions, feel free to open issues here!


## RSM414 hardware
See: [hw/README.md](./hw/README.md)


<br>

Incoming features:
* Document the hardware of `RSM425` revision - it works flawlessly with the RS41-NFW, however, I don't have one yet that I can study on. If you have one, please contact me.
* Somehow get the RPM411 to work


## People responsible for this project
* Authors
  * **Franek SP5FRA 'nevvman'**
* Contributors - speical thanks to:
  * My dad, for his help in catching the radiosondes and suggestions
  * Erik PA0ESH - helped with lots of issues
  * Mark VK5QI - for help with GPS settings, Horus and sensors
  * zanco PE2BZ - for a test flight and other notes
  * Ludwik SP6MPL - for a few flights and big help in development
  * Mateusz SP3WRO - for test flights, kind words and help in development, and also his team
  * [radioszynka blog](https://radioszynka.pl/) team - for article about this project
  * Mark PC9DB - TX formats etc.
  * KB8RCO - big thread about APRS (also code to fix coordinate issue), WX use and others
  * whallman DF7PN - much help in discussions
  * Damian SQ2DEF and his team - SQ6KXY, Paweł, Lechu, McXander, wprzyb, Michał, Hubert...
  * obi7zik - thread about GPS power mode issue
  * OM3BC - big help in getting the RTTY to finally have a proper format and timings
  * maxkup14 - suggested accuracy of sensor measurements is affected by GPS (to be investigated) and successfully tested the RS41-NFW with 2025 `RSM425` revision!
  * People from *Radiosondy Polska* group - Jarosław, Wojtek... - kind words in a local group argument


## References
* [*RS41ng* - inspiration for this project (NFW is not a fork of any kind (too much differing to be called so), just a few pieces of it's code structure is used here)](https://github.com/mikaelnousiainen/RS41ng)<br>
* [**RS41ng - issues discussion about new models and supporting them**](https://github.com/mikaelnousiainen/RS41ng/issues/92)
* [*RS41HUP* - also inspiration](https://github.com/darksidelemm/RS41HUP)<br>
* [*radiosonde_hardware* - made reversing the new version easier](https://github.com/bazjo/radiosonde_hardware)<br>
* [*Horus Binary* - awesome HAB radio protocol](https://github.com/projecthorus/horusdemodlib)<br>
* [*Arduino APRS*](https://handiko.github.io/Arduino-APRS/) library, partially utilized here to create APRS messages
