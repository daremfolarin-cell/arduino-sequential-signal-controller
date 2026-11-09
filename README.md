# Arduino Button-Controlled Sequential Signal Controller

An interactive, button-triggered sequential signal controller based on the classic Arduino "Spaceship Interface" concept. The system monitors the state of a physical push-button to switch between a stable standby state and an alternating LED sequence.

## 🔗 Live Simulation

You can test and interact with this project virtually without any hardware:

https://wokwi.com/projects/480158477404976129

## ⚙️ How It Works

The controller operates in two distinct modes depending on the button input connected to **Pin 2**. The program continuously reads the button's state using `digitalRead(2)` and stores the result in the `switchState` variable.

### 1. Standby Mode (Button NOT Pressed / `LOW`)

When the button is not pressed:

- Pin 3 turns **HIGH**, illuminating the standby LED.
- Pins 4 and 5 remain **LOW**, keeping the other two LEDs switched off.

This provides a stable visual indication that the system is in standby mode.

### 2. Sequential Alert Mode (Button Pressed / `HIGH`)

When the button is pressed:

- Pin 3 switches **LOW**, turning off the standby LED.
- Pin 5 turns **HIGH**, illuminating the first sequence LED.
- After 250 milliseconds, Pin 5 switches **LOW**, while Pin 4 turns **HIGH**.
- After another 250 milliseconds, the loop repeats, alternating between the LEDs connected to Pins 4 and 5.

The alternating sequence continues for as long as the button remains pressed.

When the button is released, the program detects the LOW input during the next loop iteration and returns to standby mode.

## 🔄 Timing and State Transitions

The program uses an `if-else if` conditional structure to determine which operating mode should be active.

- `if (switchState == LOW)`: Activates standby mode by illuminating the LED connected to Pin 3.
- `else if (switchState == HIGH)`: Activates the sequential LED pattern using Pins 4 and 5.

A **250-millisecond delay** (`delay(250)`) is used between LED transitions. This timing was selected to make the alternating pattern clearly visible while maintaining a consistent sequence.

The button's state is read again at the beginning of every `loop()` iteration. This allows the controller to switch between standby and sequential alert modes depending on the current input.

**Design consideration:** The use of `delay()` temporarily pauses program execution. Consequently, the button is not checked during each 250-millisecond delay. This means there may be a slight delay before the controller responds when the button is released.

## 🛠️ Hardware Requirements

- 1x Arduino (Uno, Nano, or compatible board)
- 1x Push-button
- 3x LEDs (e.g., 1 Green, 2 Red)
- 3x 220Ω Current-limiting resistors (for the LEDs)
- 1x 10kΩ Pull-down resistor (for the push-button input)
- Breadboard and jumper wires

## 🔌 Pin Mapping Reference

| Component | Arduino Pin | Type | Active State |
| :--- | :--- | :--- | :--- |
| **Push-Button** | Pin 2 | INPUT | HIGH when pressed |
| **LED 1 (Standby)** | Pin 3 | OUTPUT | HIGH on standby |
| **LED 2 (Sequence A)** | Pin 4 | OUTPUT | HIGH during sequence |
| **LED 3 (Sequence B)** | Pin 5 | OUTPUT | HIGH during sequence |

## 💻 Installation & Upload

1. Open the [Arduino IDE](https://arduino.cc).
2. Create a new sketch.
3. Paste the project code into the editor window.
4. Select your correct board type and COM port via `Tools`.
5. Click **Upload** to upload the sketch to your Arduino board.
