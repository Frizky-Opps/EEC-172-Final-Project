from pathlib import Path

# Define the markdown content based on the final report
final_report_md = """
---
layout: default
title: 2048 Game on CC3200
description: A standalone 2048 game implemented using the CC3200 microcontroller with tilt input, OLED display, and AWS IoT integration.
---

# 2048 Game – EEC 172 Final Project Report

By Arun Khanijau and Jesse Gomez

---

## 📝 Project Description

This project implements the 2048 puzzle game on a standalone embedded system using the TI CC3200 microcontroller. All game logic, input handling, and display rendering are performed directly on the MCU. Players interact using the onboard **accelerometer**, and the game is displayed on an **Adafruit SSD1351 OLED screen**. Upon completion, game results are posted to **AWS IoT** for leaderboard tracking.

---

## 🎮 Game Overview

**2048** is a sliding tile puzzle played on a 4×4 grid. The player merges tiles by sliding them in one of four directions—up, down, left, or right—with the goal of forming a tile with the number **2048**.

- **Initial Setup**: Two random tiles (2 or 4) appear on the grid.
- **Movement**: Tiles move as far as possible in the selected direction.
- **Merging**: Identical adjacent tiles combine (e.g., 2 + 2 → 4).
- **Tile Spawn**: A new tile spawns after each move in an empty space.
- **End Condition**: The game ends when no moves remain.

---

## 🧠 Functional Specification

The game operates as a finite state machine (FSM) with the following states:

- **INIT** – Initializes SPI, I2C, and peripherals; draws the game board.
- **WAIT_INPUT** – Waits for tilt or UART input.
- **PROCESS_MOVE** – Executes move logic, spawns new tile, and updates screen.
- **CHECK_GAME_OVER** – Checks for available moves.
- **END_GAME** – Displays final score and posts to AWS IoT.

![FSM Diagram](media/fsm.png)

---

## 🧩 System Architecture

**Hardware Components**:
- **TI CC3200 MCU**: Central processor.
- **Adafruit SSD1351 OLED Display**: SPI-based graphical output.
- **BMA222 Accelerometer**: I2C input via tilt gesture.
- **UART**: Debugging and optional keyboard control.
- **AWS IoT**: Cloud posting of game results.

**Software Modules**:
- `test.c`: Handles board drawing.
- `main.c`: Contains logic and system initialization.
- `http_post()`: Sends final score and tile data to AWS over TLS.

![System Architecture](media/system-architecture.png)

---

## 🔧 Implementation

### Hardware Interface
- **SPI**: Drives OLED at 20 MHz using Adafruit SSD1351 driver.
- **I2C**: Communicates with BMA222 (0x18) for X/Y axis readings.
- **UART**: Optional for debug input/output using W/A/S/D keys.

### Display Rendering
- `draw2048Board()`: Draws grid and margins.
- `display2048Numbers()`: Writes tile numbers with scaling.

### Game Logic
- Grid stored as a `4x4 int` array.
- Movement via `moveLeft()`, `moveRight()`, etc.
- `spawnTile()` adds new tile post-move.
- `movesAvailable()` detects if the game is over.

### Input Handling
- **Tilt Input**: Thresholded accelerometer readings with cooldown.
- **UART Input**: 'W', 'A', 'S', 'D' for movement.
- Neutral orientation required between moves to debounce.

### Cloud Integration
- TLS-secured HTTP POST to AWS IoT
- Sends JSON payload with largest tile and score
- Uses `construct_data1()` and `http_post()` to format and send data

---

## 🧪 Challenges

- **OLED Flickering**: Solved by increasing SPI speed to 20 MHz.
- **Tilt Stability**: Solved with cooldown + neutral reset logic.
- **AWS Integration**: Required troubleshooting of TLS sockets, JSON formatting, and payload delivery.

---

## 🚀 Future Work

- Implement temperature-based tile coloring.
- Store high scores in flash memory.
- Add animated tile transitions.
- Explore gesture or touch-based input.
- Power optimization via low-power modes.

---

## 🧾 Bill of Materials

| Component                  | Description                | Vendor              | Cost  |
|----------------------------|----------------------------|----------------------|-------|
| CC3200 MCU                 | Development board          | Texas Instruments    | $65   |
| SSD1351 OLED Display       | 1.5\" SPI OLED             | Adafruit             | $40   |
| BMA222 Accelerometer       | Tilt sensor (I2C)          | Included             | $0    |
| Breadboard + Jumper Wires | Prototyping materials      | Amazon               | $10   |

---

## 📹 Video Demo

<iframe width="100%" height="315" src="https://www.youtube.com/embed/YOUR_VIDEO_ID" frameborder="0" allowfullscreen></iframe>

---

## 🌐 Site Aesthetics

This page is styled using the **Cayman theme** via GitHub Pages, designed to match grading requirements for clarity, documentation quality, and reproducibility.
"""

# Save the report to a file named index.md
output_path = Path("/mnt/data/index.md")
output_path.write_text(final_report_md)

# Provide download link
output_path.name
