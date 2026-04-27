# Jett-Stream
<img width="480" height="393" alt="Image" src="https://github.com/user-attachments/assets/7eaa618c-8a15-45e8-bb2d-cb59a16c0cfc" />
A tool to help connect your Hot Octopuss Jett to the OSR/TCode ecosphere.

> [!WARNING]
> **Warning: This modification takes away any safety/ fail safes the original device has. I am not responsible for any damaged devices and other harm that comes with homebrewed electronics(Overheating, Fires, etc.).**

This device utilizes T- Code…
Created by [Tempest For the OSR-2, SR-6, and other DIY toys](https://patreon.com/tempestvr)

The specific Firmware I will be using in this guide is [Khrull’s TCodeESP32 Firmware](https://www.patreon.com/Khrull)

Heavy inspiration (Pretty much a complete copy lol) of TidyPrints’ PD Tigger created for his SR6 Tray + Holder is used. [Find them here (TidyPrints Patreon)](https://www.patreon.com/TidyPrints)

# <ins>What you will need…</ins>

**Tools**
* Multimeter
* Soldering Iron
* 3D printer

**Printed Parts**
[Find the STLs here](https://github.com/CactusJuice9/Jett-Stream/tree/main/STL%20Print%20Files)
* 1x $\color{#0000FF}{Jett\ Stream\ Body}$
* 1x $\color{#FFFF00}{Jett\ Stream\ Lid}$
* 1x $\color{#00FF00}{Jett\ Stream\ Buck\ Mount}$
* 1x $\color{#FF0000}{Jett\ Stream\ PD\ Clamp}$

<img width="525" height="331" alt="Image" src="https://github.com/user-attachments/assets/13e4e58d-4b14-4b68-9ecf-79499b837de8" />

**Other Items**
| Item (#)                                                        | Example Purchase Link                                                                          |
|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| Heat Shrink (x4)                                                |                                                                                                |
| 18-22 AWG Wire                                                  |                                                                                                |
| Female Dupont wires  (x4)                                       |                                                                                                |
| M3x5x4 Heat Set Inserts (x4)                                    |                                                                                                |
| M2 x 4mm bolt (x2)                                              |                                                                                                |
| M2 x 8mm bolt (x4)                                              |                                                                                                |
| M3 x 8mm bolt (x4)                                              |                                                                                                |
| USB-C Power Delivery (9v compatible) (x1)                       | https://www.amazon.com/Charger-Anker-Compact-Foldable-Included/dp/B0C1FZWT8M                   |
| 3M VHB double sided tape (or other strong adhesive)             |                                                                                                |
| 2.5mm Mono Audio Panel Mount Snap-In (x2)                       |                                                                                                |
| Type-C PD3.0 QC 9V Trigger Board (x1)<br><br>(11.5mm x 21.5 mm) | https://www.amazon.com/Trigger-Voltage-Housing-Household-Electronics/dp/B0F23KSYQ5             |
| MX1616H Dual H-Bridge DC Stepper (x1)(21mm x 24.7mm)            | https://www.amazon.com/Aideepen-Driver-H-Bridge-Replace-Stepper/dp/B075S368Y2                  |
| Mini MP1584EN DC-DC Buck Converter (x1)                         | https://www.amazon.com/MP1584EN-DC-DC-Converter-Adjustable-Module/dp/B01MQGMOKI                |
| ESP32 DevKit Clone (x1)<br>(29mm x  51.75mm)                    | https://www.amazon.com/ELEGOO-ESP-WROOM-32-Development-Bluetooth-Microcontroller/dp/B0D8T53CQ5 |

# Build Guide

<img width="493" height="310" alt="Image" src="https://github.com/user-attachments/assets/61d70d15-3eb1-4418-9aa5-d39565997794" />

In most audio applications when dealing with a mono TS(Tip Sleeve) cable the Sleeve is ground and the Tip is audio/power (See IMG below)

<img width="145" height="165" alt="Image" src="https://github.com/user-attachments/assets/929c5729-ed07-4d64-a940-e0d0224addd5" />

The Original Hot Octopuss Jett is wired in reverse to what you would typically see in audio (Tip - / Sleeve +). This leaves you with two options, Wire the Snap-in Mount like audio with TS polarized correctly or wire it flipped. 

In the wire diagram above I wired polarity to traditional audio rather than what the Jett uses. Because of this I wired the Dual H-Bridge DC Stepper on PWM IN2 & IN4. These pins drive the motors in reverse giving us our desired polarity. 

Alternatively you can wire the Dual H-Bridge DC Stepper output forward with IN1 & IN3 and just wire the 2.5mm Mono Audio Panel Mount Snap-In with a flipped polarity (Sort leg negative/Long leg positive)


> [!CAUTION]
> VOLTAGE TO/FROM THE BUCK CONVERTER & INTO ESP32/H-BRIDGE SHOULD ALWAYS BE WIRED IN CORRECT POLARITY

> [!NOTE]
> If you are unfamiliar with the ESP32 you may want to start with step 12 first to ensure the firmware is uploaded correctly before continuing.


1. Start by taking your PD trigger and bridge the 9V pin. Power the PD trigger and confirm the 9V voltage with a multimeter.

<img width="99" height="175" alt="Image" src="https://github.com/user-attachments/assets/72fd6164-895e-4553-bffe-e35edfc9c486" />

2. Wire the PD trigger to your buck converter ensuring the USB-C PD trigger is wired to the input side of the buck converter (Usually an arrow showing direction on the bottom). Wire your 2 dupont connectors (for ESP32) and 2 extra wires (for H-bridge).

<img width="373" height="185" alt="Image" src="https://github.com/user-attachments/assets/e00ce80e-c05d-406c-a828-f04fdf9257f2" />

3. Adjust your voltage out of your buck converter using the adjustment screw until you get to your desired voltage using a multimeter. I set mine to ≈ 5.7 V; however, I recommend you take your own readings out of the original Hot Octopuss Jett and use those values as over-voltage can damage the motors.
4. Apply tape to the Jett Stream Buck Mount

<img width="318" height="212" alt="Image" src="https://github.com/user-attachments/assets/0e7f21cf-08ba-47bf-b27e-39d1fb5d4c82" />

5. Mount the PD Tigger onto the Buck Mount and place the PD Trigger Clamp on top to secure it in place. Use a M2 x 4mm bolt to secure the clamp in place. Mount the buck converter onto the Buck Mount using the tape to fix it in place.

<img width="334" height="175" alt="Image" src="https://github.com/user-attachments/assets/60371b59-bcb1-4616-91dc-d0781429a1b4" />

6. Wire the 2 extra H-Bridge wires from the buck to your H-Bridge. Also attach 2 female dupont cables to IN2 & IN4 (assuming using the same polarity/wire diagram I did) and wire a red & black wire pair to the motor-A and motor-B output. This image is a mess so be sure to consult the wire diagram.

<img width="310" height="327" alt="Image" src="https://github.com/user-attachments/assets/a8ccdd99-d27c-4c4d-b226-9a090e5d0544" />

7. Solder/secure your M3x5x4 Heat Set Inserts into the 3D printed Jett Body. then place the ESP32 in place upside down.

<img width="295" height="327" alt="Image" src="https://github.com/user-attachments/assets/f5261190-aff7-4e0e-8f2c-6506799bfbf0" />

8. Place the Buck Mount on top of the ESP32 and secure both in place with x4  M2 x 8mm bolts. Secure the Dual H-Bridge DC Stepper with a M2 x 4mm bolt.

<img width="302" height="365" alt="Image" src="https://github.com/user-attachments/assets/47bf9772-f1eb-4233-8527-ce644e43f11e" />

9. Place heat shrink over the motor-A and motor-B wire pairs and solder them to the 2.5mm snap-in female audio jacks. Then secure the heat shrinks with heat.

<img width="387" height="322" alt="Image" src="https://github.com/user-attachments/assets/b3530051-bfc1-4281-bc23-e3f9ff369b1a" />

10. Attach your power dupont wire pair to GND and VIN. Then connect your H-bridge IN2 & IN4 to GPIO pin 18 & 19

<img src="https://github.com/user-attachments/assets/bb1b985e-7cd3-4bf4-abe3-b885ab5cd176" width="25%"><img src="https://github.com/user-attachments/assets/75f09030-19d5-4bf4-a6d3-af89e8816f19" width="49%"> 
> [!NOTE]
> Remember the ESP32 is mounted upside down
11. Wire manage the print making sure everything is inside the case except for the 2.5mm snap in jacks which can hand out the holes. Place the printed Lid on top of the Jett Stream Body and secure it with 4 M3 x 8mm bolts. Finally snap the 2.5mm jacks into their mounting holes.

<img width="350" height="286" alt="Image" src="https://github.com/user-attachments/assets/7eaa618c-8a15-45e8-bb2d-cb59a16c0cfc" />

12. The Instruction guide and firmware for TCodeESP32 can be found at https://github.com/jcfain/TCodeESP32/releases. 

Flash the firmware onto the esp32 using the bottom usb c. The bottom usb c powers just the ESP32; use this one to upload firmware and connect the device via serial. The top device will power the motors and the ESP32 however doesn't have data pins connected to the ESP32. Once you have Khrull’s firmware this isn’t an issue as you can access the esp32 without it being connected to the computer.Follow the install guide and set the device type to a T-Vibe. V0 (Vib 1) and V1 (Vib 2) should already be set as 18 & 19 in the T-Vibe device profile; if not set them.

 <img width="352" height="229" alt="Image" src="https://github.com/user-attachments/assets/c22ace12-b133-4404-817a-58a932060eba" />


13. Connect the Jett and test the device via the ESP32 IP or at tcode.local ensuring V0 & V1 controls both motors.

---
Then you're all done! I would highly recommend checking out [MultiFunPlayer by Yoooi0](https://github.com/Yoooi0/MultiFunPlayer) if you haven't before. It's a great tool for hooking into applications and streaming platforms with TCode controlled devices.

Also check out Vibhub for a similar open source tool in a much cleaner form factor then what I could ever make. [Find it here](https://vibhub.io/)


## What else can I do with this?

This really is just a Buck converter and DC motor controller stuffed into a pretty box; Other than that it's the exact same as Tempest's T-Vibe. Thus, you can attach whatever Vibration Toy you want to it. You can remove the 2.5mm jacks all together if you want to use a different vibe bullet. You can make it into a Pogo pin connector, another random Molex Connector, or even just direct wire a different device right to the motor controller. All you have to do is adjust your voltage to whatever your new you needs and ensure the H-Bridge stepper you choose isnt going to current limit it. Also remeber to drive your toy in the same polarity to whatever original deivce you are modding. This shouldnt matter as most DC motors can be driven forward and in reverse but its not worth finding out by frying your new toy. H-Bridge input IN1 & IN3 drive motors forward and IN2 & IN4 drive in reverse.
