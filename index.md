---
layout: default
title: 2048 Game on CC3200
description: A standalone version of 2048 implemented in embedded C on a CC3200 with IR input, OLED display, temperature visualization, and AWS IoT score uploads.
---

# 2048 Game – EEC 172 Final Project

This is a standalone, embedded implementation of the classic 2048 puzzle game, created on the **TI CC3200 microcontroller**. It uses an **OLED screen** for display, an **IR remote** or **tilt sensor** for input, a **temperature sensor** to adapt visuals, and **AWS IoT** integration to post high scores to the cloud.

---

## 📝 Description (0.5 pt)

The player slides tiles on a 4×4 grid. Identical tiles that collide merge into one with double the value. A new tile (2 or 4) appears each move. The goal is to reach 2048, though players can continue afterward. The game ends when no moves are left.

---

## 🧠 Functional Specification (2.5 pts)

The software is built around a finite state machine:

- **INIT** – Initializes Wi-Fi, OLED, and sensors
- **IDLE** – Waits for valid gesture or IR input
- **PROCESS_INPUT** – Updates grid and game logic
- **UPDATE_DISPLAY** – Redraws screen and score
- **GAME_OVER** – Displays result, posts to AWS
- **RESET** – Waits for reset or timeout to restart

![State Diagram](media/fsm.png)

---

## 🧩 System Architecture (2.5 pts)

Our hardware-software architecture includes:

- **CC3200 LaunchPad**: Core processor
- **IR Receiver / Accelerometer**: User input
- **Adafruit OLED**: Game display
- **TMP006 Temp Sensor**: Controls color scheme
- **AWS IoT**: Uploads score for leaderboard tracking

![System Block Diagram](media/system-architecture.png)

---

## 🔧 Implementation (5 pts)

### Game Logic
- 2048 mechanics (sliding, merging, spawning new tiles)
- C array-based grid system with movement vectors
- State transition logic driven by GPIO/IR interrupts

### Input Handling
- IR signals decoded via timer-based GPIO interrupt
- Accelerometer polled periodically as optional fallback

### Display
- SSD1351 OLED driven over SPI
- Game board redrawn on every state update
- Font rendering via `glcdfont.h` and GFX primitives

### Temperature Integration
- TMP006 I2C sensor reads ambient temperature
- Visual style changes (e.g., blue/cool, red/hot themes)

### Cloud Integration
- High score sent to AWS IoT using MQTT via CC3200 Wi-Fi
- Server receives, logs, and returns leaderboard data

---

## 🧪 Challenges (2 pts)

- **IR decoding**: Needed precise edge detection and timing to decode NEC protocol correctly
- **Display flicker**: Fixed by optimizing redraw logic and partial screen refresh
- **Tile movement bugs**: Required multiple code rewrites to preserve merge rules
- **AWS/MQTT latency**: Solved with async retry logic and manual payload optimization

---

## 🚀 Future Work (0.5 pt)

- Add sound using PWM and speaker
- Expand leaderboard with persistent storage
- Enhance UI with animation effects
- Switch to capacitive touch input

---

## 🧾 Bill of Materials (2 pts)

| Item                       | Qty | Price | Source        |
|----------------------------|-----|-------|---------------|
| TI CC3200 LaunchPad        | 1   | $30   | TI            |
| Adafruit OLED (SSD1351)    | 1   | $20   | Adafruit      |
| IR Receiver                | 1   | $2    | Amazon        |
| TMP006 Temp Sensor         | 1   | $1    | Amazon        |
| Micro USB Cable            | 1   | $0    | Included      |
| Breadboard + wires         | 1   | $10   | Amazon        |
| AWS Free Tier              | 1   | $0    | aws.amazon.com |

---

## 📹 Video Demo (2.5 pts)

<iframe width="100%" height="315" src="https://www.youtube.com/embed/YOUR_VIDEO_ID" frameborder="0" allowfullscreen></iframe>

---

## 🎨 Aesthetics (2.5 pts)

This project site is designed using GitHub Pages with the **Cayman theme**, featuring organized sections, embedded media, and reproducibility-focused documentation.

---

> 📌 For source code and schematics, visit the [GitHub Repository](https://github.com/frisky-opps/EEC-172-Final-Project)
