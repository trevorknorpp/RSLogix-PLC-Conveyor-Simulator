# PLC Conveyor Control Simulation (RSLogix Micro + Emulate)

This project simulates a basic industrial conveyor system using **RSLogix Micro Starter Lite** and **ladder logic**.

[![Watch the demo](https://img.youtube.com/vi/WWMfdzyY2Ms/0.jpg)](https://youtu.be/WWMfdzyY2Ms?si=W0cI22AhVHwEcnpK)

---

## Overview

**Goal**: Demonstrate start/stop motor control, diverter activation via a photoeye sensor, jam detection with a delay timer, and latched alarm behavior.

### Real-world Use Cases
- Parcel/conveyor lines
- Baggage handling systems
- Manufacturing automation cells

---

## Files
- `Video_Explanation.mp4` – Video explanation of the project
- `Ladder_Logic_Screenshot.png` – Visual of each rung
- `README.md` – This document
- `CONVEYORSIMULATOR.RSS` – RSLogix project
  
---

## Ladder Logic Summary

### Rung 0 – Start/Stop Conveyor Motor
- `I:0/0` → Start button
- `I:0/1` → Stop button
- `B3:0/1` → Seal-in memory bit
- `O:0/0` → Motor output

### Rung 1 – Motor Memory Bit Latch
- Latches `B3:0/1` if motor is on

### Rung 2 – Photoeye → Diverter Gate
- `I:0/2` → Photoeye sensor
- `O:0/1` → Diverter solenoid output

### Rung 3 – Jam Timer
- `I:0/3` → Jam sensor
- `T4:0` → 3-second TON delay timer

### Rung 4 – Alarm Latch Logic
- `T4:0/DN` → Triggers latch
- `B3:0/0` → Alarm memory bit (latched)

### Rung 5 – Alarm Output
- `O:0/2` → Buzzer/light output based on `B3:0/0`

### Rung 6 – Manual Reset
- `I:0/4` → Reset button
- Resets `T4:0` and unlatches `B3:0/0`

---

## Address Reference

| Address     | Description                        |
|-------------|------------------------------------|
| `I:0/0`     | Start Button                        |
| `I:0/1`     | Stop Button                         |
| `I:0/2`     | Photoeye Sensor                     |
| `I:0/3`     | Jam Sensor                          |
| `I:0/4`     | Reset Button                        |
| `O:0/0`     | Conveyor Motor                      |
| `O:0/1`     | Diverter Gate Solenoid              |
| `O:0/2`     | Alarm Buzzer/Light                  |
| `B3:0/0`    | Alarm Memory Bit (latched)          |
| `T4:0`      | TON Timer for Jam Detection         |

---

## Video Walkthrough
Open "Video_Explanation.mp4"

---

## Testing Tips (if using RSEmulate 500)

1. Open RSEmulate → Load `.RSS` file into Slot 1
2. Open RSLogix Micro → Comms > System Comms → Download to Emulator
3. Toggle bits in `I:0` data file to simulate:
   - Start, Stop, Photoeye, Jam, and Reset
4. Watch outputs `O:0` for correct response

---

## 📜 License
MIT License — open source and free to build upon.

