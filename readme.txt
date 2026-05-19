# Tiva C FreeRTOS RGB Controller

This project is a demonstration of **FreeRTOS** on the TM4C123GXL LaunchPad. It utilizes the standard TivaWare `third_party` FreeRTOS integration to manage concurrent tasks for user input and hardware output.

## 🚀 Features
- **Multi-tasking:** Separate tasks for button debouncing and LED PWM/Blinking.
- **Inter-task Communication:** Uses FreeRTOS **Queues** to send button events.
- **Dynamic Control:** 
  - **Left Button (SW1):** Cycles through RGB colors (Red -> Green -> Blue ).
  - **Right Button (SW2):** Decrease the blinking frequency .

## 🛠 Hardware Mapping
The project uses the onboard peripherals of the Tiva C LaunchPad:
| Peripheral | Pin | Function |
| :--- | :--- | :--- |
| **RGB LED (Red)** | PF1 | PWM/GPIO Output |
| **RGB LED (Blue)** | PF2 | PWM/GPIO Output |
| **RGB LED (Green)** | PF3 | PWM/GPIO Output |
| **Left Button (SW1)** | PF4 | Input (Active Low) |
| **Right Button (SW2)** | PF0 | Input (Active Low/Locked) |

## 🏗 Software Logic
1.  **SwitchTask:** Polls the buttons every 10ms. When a press is detected, it sends a message (`LEFT_PRESS` or `RIGHT_PRESS`) to the `g_pLEDQueue`.
2.  **LEDTask:** Blocks on the queue. 
    - If it receives a `LEFT_PRESS`, it increments a color index.
    - If it receives a `RIGHT_PRESS`, it reduces the `vTaskDelay` time, making the LED blink faster.

## ⚙️ Setup
1.  Ensure **TivaWare** is installed in `C:/ti/TivaWare_C_Series-2.x`.
2.  The FreeRTOS source must be linked from the `third_party/FreeRTOS` folder.
3.  Set the CPU clock to **50MHz** (standard for this demo).

## 📺 Demo
<!-- Drag and drop your video here to render the player -->
<video src="https://github.com/user-attachments/assets/a14e40c7-09d9-4e5b-819a-b311cdd9efb3" controls="controls" style="max-width: 100%;">
</video>
