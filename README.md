# Arduino Button-Controlled Sequential Signal Controller

An interactive, button-triggered sequential signal controller based on the classic Arduino "Spaceship Interface" concept. The system monitors the state of a physical push-button to alternate between a stable standby state and an animated alert/action sequence.

## 🔗 Live Simulation
You can test and interact with this project virtually without any hardware:
https://wokwi.com/projects/480158477404976129

## ⚙️ How It Works
The controller operates in two distinct modes depending on the button input on **Pin 2**:

1. **Standby Mode (Button NOT Pressed / `LOW`):** 
   * Pin 3 turns **HIGH** (e.g., Green "Ready" LED).
   * Pins 4 and 5 remain **LOW** (e.g., Red "Alert" LEDs off).

2. **Sequential Alert Mode (Button Pressed / `HIGH`):** 
   * Pin 3 shuts off immediately.
   * Pin 5 triggers **HIGH** for 250 milliseconds.
   * Control shifts to Pin 4, which triggers **HIGH** for another 250 milliseconds while Pin 5 shuts off.
   * The animation continuously loops back and forth as long as the button remains pressed.

## 🛠️ Hardware Requirements
* 1x Arduino (Uno, Nano, or compatible board)
* 1x Push-button
* 3x LEDs (e.g., 1 Green, 2 Red)
* 3x 220Ω Current-limiting resistors (for the LEDs)
* 1x 10kΩ Pull-down resistor (for the push-button input)
* Breadboard and jumper wires

## 🔌 Pin Mapping Reference

| Component | Arduino Pin | Type | Active State |
| :--- | :--- | :--- | :--- |
| **Push-Button** | Pin 2 | INPUT | HIGH when pressed |
| **LED 1 (Standby)** | Pin 3 | OUTPUT | HIGH on standby |
| **LED 2 (Sequence Sequence A)** | Pin 4 | OUTPUT | Flashes during sequence |
| **LED 3 (Sequence Sequence B)** | Pin 5 | OUTPUT | Flashes during sequence |

## 💻 Installation & Upload
1. Open the [Arduino IDE](https://arduino.cc).
2. Create a new sketch.
3. Paste the project code into the editor window.
4. Select your correct board type and COM port via `Tools`.
5. Click **Upload** to push the sketch to your board.
