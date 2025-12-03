# 🧊 STM32 Thermostat Controller  
**Author:** Hà Gia An – *2352004*  
**Lecturer:** Bùi Quốc Bảo  
**MCU:** STM32F411CEU6  
**Display:** 16×2 LCD (I2C backpack)  
**Input:** 4 physical buttons (POWER, SET, UP, DOWN)

---

## 📌 Overview  
This project implements a simple **thermostat controller** using the STM32F411CEU6 microcontroller.  
It monitors room temperature (0–60 °C), allows the user to set a target temperature, and controls the cooling fan using a classic **ON/OFF control algorithm**.

---

## ✨ Features  
- **1°C resolution** from 0°C → 60°C  
- **16×2 I2C LCD** user interface  
- **User-configurable temperature threshold**  
- **ON/OFF cooling control**  
- **Four-button control system**  
- **Fan status displayed on LCD**
- **EEPROM storage** for the last temperature set point
- Add **hysteresis** (±1°C) to reduce relay switching  

---

## 📟 Hardware Used  
| Component | Description |
|----------|-------------|
| **STM32F411CEU6 (“Blackpill”)** | Main microcontroller |
| **16×2 I2C LCD** | For UI and temperature display |
| **4× Push Buttons** | Power, Set, Up, Down |
| **Temperature Sensor** | LM35 |

---

## 🎮 Button Functions  
All buttons support **short press**.

### 📘 Button Behavior  
| Button | Short Press | Long Press |
|--------|-------------|------------|
| **POWER** | Toggle system ON/OFF | — |
| **SET** | Enter/Exit temperature setting mode | — |
| **UP** | Increase temperature by +1°C |
| **DOWN** | Decrease temperature by −1°C |

---

## 🧠 Control Algorithm — ON/OFF Logic  
The thermostat uses classic **hysteresis ON/OFF control**:

---

## 📺 LCD Display Format  
**Normal Mode:**
```
Temp: 26°C
Fan: OFF
```

**Setting Mode:**
```
Set Temp: 24°C
<UP/DOWN to adjust>
```

---

## 🔧 Firmware Behavior  
- Button debouncing included
- State machine handles:
  - **POWER_STATE**
  - **SET_TEMP_STATE**
  - **RUN_STATE**

---

## 📁 Project Structure  
```
/ProjectRoot
│
├── Core/
│   ├── Inc/
│   │   ├── main.h
│   │   ├── lcd_i2c.h
│   │   ├── buttons.h
│   │   ├── thermostat.h
│   │   └── eeprom_emulation.h
│   │
│   └── Src/
│       ├── main.c
│       ├── lcd_i2c.c
│       ├── buttons.c
│       ├── thermostat.c
│       └── eeprom_emulation.c
│
│
├── BSP/                      ← Board Support Package
│   ├── Inc/
│   │   ├── bsp_lcd.h
│   │   ├── bsp_buttons.h
│   │   └── bsp_temp_sensor.h
│   │
│   └── Src/
│       ├── bsp_lcd.c
│       ├── bsp_buttons.c
│       └── bsp_temp_sensor.c
│
│
├── App/                      ← Application logic (UI + State Machine)
│   ├── Inc/
│   │   ├── app_display.h
│   │   ├── app_buttons.h
│   │   └── app_controller.h
│   │
│   └── Src/
│       ├── app_display.c     ← builds LCD text ("Fan: ON/OFF")
│       ├── app_buttons.c
│       ├── app_controller.c  ← thermostat control state machine
│       └── (any other .c files you add)
│
│
├── Docs/
│   ├── wiring_diagram.png
│   └── state_machine_diagram.png
│
└── .gitignore


```

---

## 🚀 How to Use  
1. Power the system using USB or 5V input.  
2. Press **POWER** to start the thermostat.  
3. View current temperature on LCD.  
4. Press **SET** to enter temperature configuration.  
5. Use **UP/DOWN** to adjust temperature.  
6. Fan automatically turns ON/OFF depending on room temperature.

---

## 🛠️ Future Improvements  
- Add **PID control** for smoother response  
- Add **Buzzer** notification

---

## 📜 License  
MIT License — feel free to use and modify.
