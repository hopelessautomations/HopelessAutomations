---
layout: page
title: "3D Printers"
---

1. 2x Ender-3
2. Geeetech A10
3. Biqu Legend
4. Prusa Mini
5. AM8
5. Prusa Bear MK2
6. 3x Prusa Bear MK3
7. Hypercube300
8. Hypercube800

---

All printers are modded, most of them have 32bits boards, Trinamic stepper drivers and auto bed leveling sensor. The Hypercube300 has Duet Maestro board and the Hypercube800 has Duet 2 WiFi + Duex5 all the other ones run self-compiled version of Marlin.

Every printer besides the Hypercubes are connected to my Octoprint-farm server with a Octoprint setup for each and the folders are shared between Octoprint's and all of them as a smart switches that I can turn on/off on Home Assistant.

On Home Assistant I also use the Octoprint integration and have a couple of automations for the printers.
Whenever a printer finish printing and is idling for more than 5 minutes Home Assistant will turn off the printer
Otherwise if the printer is just idling for more than 30 minutes it will also turn it off (sometimes I forget it's on or to start printing).
When any of the Marlin printers finishes printing me or my wife (depending on who is home) will receive a WhatsApp message alerting we should remove the print and start new print if wanted.

---

### Ender-3 #1
Generally this is the printer I use for any of my personal projects.

| Hardware        |                        |
| :-------------- | :--------------------- |
| Board           | SKR E3 v1.2 DIP        |
| PSU             | Stock                  |
| Stepper Drivers | TMC2208                |
| Display         | Biqu TFT70             |
| Extra 1         | BLTouch                |
| Extra 2         | Metal Extruder         |
| Extra 3         | Glass Sheet            |
| Extra 4         | X-Axis Metal Tensioner |

---

### Ender-3 #2
This one is taking the old hardware from the other one.

| Hardware        |                 |
| :-------------- | :-------------- |
| Board           | SKR E3 DIP      |
| PSU             | Stock           |
| Stepper Drivers | TMC2208         |
| Display         | Biqu TFT35 E3   |
| Extra 1         | BLTouch         |
| Extra 2         | Metal Extruder  |
| Extra 3         | Glass Sheet     |

---

### Geeetech A10
Extremely modded! Converted to direct drive extruder with a smaller nema17 and removed the endstops using TMC2209 function and removed all the blue covers. 

| Hardware            |                         |
| :------------------ | :---------------------- |
| Board               | SKR v1.3                |
| PSU                 | Stock                   |
| Stepper Drivers     | TMC2208                 |
| Stepper Drivers X&Y | TMC2209                 |
| Display             | Biqu TFT35 v3           |
| Extra 2             | BMG Direct Extruder     |

---

### Biqu Legend
This is in the operation table, I have removed the endstop switches and upgraded the board to SKR v1.4 with TMC2209 added a Ender-3 X carriage and a dual extruder because I didn't like at all the stock carriage and hotend but that made me lose about 1cm on X and Y axis.
To fix that the X axis has to be enlarged, easy way I clone more the frame of the Ender-3 otherwise some adapters have to be made to adjust the enlargement. 

| Hardware        |          |
| :-------------- | :------- |
| Board           | SKR v1.4 |
| PSU             | Stock    |
| Stepper Drivers | TMC2209  |

---

### Prusa Mini
This is all stock I pretend to clone it once more hardware is available on AliExpress.

---

### AM8
Originally Anet A8 my first 3D Printer, but there's nothing left of it! 
Stepper motors were all changed.
PSU was upgraded to 24V.
Motherboard is SKR v1.3
Stepper Drivers X & Y are TMC2209
Stepper Drivers Z & E0 are TMC2208
Metal Extruder
MK52 Heated Bed 24V with magnetic plate
E3D v6 Bowden 24V
