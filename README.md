# L476-PJ11-ExtrenalInterrupToControlAnLED

## 📌 Project Overview

This project demonstrates how to use **external interrupts (EXTI)** on an STM32 microcontroller to control an LED.

👉 Each time the user presses a button, an interrupt is triggered, and the LED toggles its state (ON ↔ OFF).

---

## 🎯 Features

* ✅ GPIO External Interrupt (EXTI)
* ✅ NVIC interrupt handling
* ✅ LED toggle using `HAL_GPIO_TogglePin`
* ✅ Interrupt-based design (no polling)
* ✅ Clean and efficient embedded architecture

---

## 🧠 How It Works

1. Button is connected to a GPIO pin (e.g., PC13)
2. GPIO is configured as **EXTI (Interrupt Mode)**
3. When button is pressed:

   * EXTI interrupt is triggered
   * NVIC handles interrupt priority
   * Callback function is executed
4. LED state is toggled

---

## 🔁 System Flow

```
Button Press
     ↓
GPIO EXTI Trigger
     ↓
NVIC Interrupt Controller
     ↓
EXTI IRQ Handler
     ↓
HAL_GPIO_EXTI_Callback()
     ↓
HAL_GPIO_TogglePin()
     ↓
LED ON / OFF
```

---

## 🛠️ Hardware Setup

| Component   | Description         |
| ----------- | ------------------- |
| STM32 Board | (e.g., STM32L476RG) |
| Button      | Connected to PC13   |
| LED         | Connected to PA5    |

---

## ⚙️ Software Configuration

Using **STM32CubeIDE**:

### GPIO Settings

* **PC13** → External Interrupt Mode (Falling Edge)
* **PA5** → Output No Push-up and No Pull-down

### NVIC Settings

* Enable: `EXTI15_10_IRQn`
* Set appropriate priority

---

## 💻 Code Example

### Interrupt Callback

```c
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{
    if(GPIO_Pin == GPIO_PIN_13)
    {
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    }
}
```

---

## ⚠️ Notes

### 🔸 Debounce Issue

Mechanical buttons may trigger multiple interrupts due to noise.

👉 Simple solution:

* Add delay or software filtering

---

### 🔸 Avoid Heavy Code in Interrupt

Do NOT use:

* `HAL_Delay()`
* `printf()`
* Long loops


---

## 📚 Key Concepts Learned

* Interrupt vs Polling
* NVIC (Nested Vector Interrupt Controller)
* ISR (Interrupt Service Routine)
* Callback mechanism in HAL


