---
layout: default
title: CC3200 Game Project
---

# CC3200 Game Project – EEC 172 Final Report

This site documents our final project for EEC 172: a real-time embedded game built on the **TI CC3200 LaunchPad** using GPIO interrupts, LEDs, and buttons. The project is designed for reproducibility and serves as a complete technical portfolio piece.

---

## 📝 Description (0.5 pt)

Our prototype is a reaction-based game built using the CC3200. The player must press a button in response to a randomly-timed LED signal. The game uses timers, GPIO, and interrupts to control game flow and logic, and runs entirely on embedded C code using TI’s DriverLib.

---

## 🧠 Functional Specification (2.5 pts)

The game is implemented as a finite state machine (FSM) with the following states:

- `INIT`: Initialize peripherals
- `WAIT_START`: Wait for the player to press the start button
- `READY`: Display LED countdown, wait random delay
- `PLAY`: Turn on LED, wait for reaction
- `RESULT`: Show whether player was too early, on time, or too slow

![State Diagram](media/fsm.png)

---

## 🧩 System Architecture (2.5 pts)

The architecture consists of the following components:

- **CC3200 MCU**: Runs the game logic
- **SW2 / SW3**: Used for game input
- **LEDs**: Indicate countdown and result
- **Timer / SysTick**: Used for reaction timing
- **UART (optional)**: Debug messages

![System Architecture](media/system-architecture.png)

---

## 🔧 Implementation (5 pts)

### Hardware
- GPIO pins configured using `MAP_GPIOPinTypeGPIOOutput`
- Interrupts set up with `GPIOIntRegister`, `GPIOIntEnable`
- SysTick used to time the reaction phase (`SysTickIntHandler`)

### Software
- FSM implemented in C with clear state transitions
- Debouncing handled in software using a lockout timer
- UART output used for debug mode
- The code uses TI’s DriverLib APIs throughout (e.g. `MAP_GPIOPinRead`, `MAP_PRCMPeripheralClkEnable`)

**Note**: All logic and timing are handled without an RTOS.

---

## 🧪 Challenges (2 pts)

- **Debouncing**: False button presses were common initially. We solved this using a cooldown counter in SysTick.
- **Interrupt Priority**
