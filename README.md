# STM32L496 OBC Test Board
 
[![Board Render](Images/PCB_3D_Render.png)](Images/PCB_3D_Render.png)
 
A breakout board built around the **STM32L496RG** microcontroller. The board breaks out an **I²C** bus (through a level-translating buffer) and a **CAN** bus 
(through a fault-protected transceiver), along with a **timer/PWM** channel, **SPI**, and a debug/serial header. Designed in Altium, fabricated through JLCPCB, 
and brought up on the bench with STM32CubeIDE and an ST-LINK.
  
---
 
## Overview
 
| | |
|---|---|
| **MCU** | STM32L496RGT3 — Arm Cortex-M4, LQFP64 |
| **Key peripherals** | I²C, CAN, timer/PWM, SPI |
| **Debug / programming** | SWD (ST-LINK) + SWO trace; USART1 broken out on the same header |
| **Tools** | Altium Designer · JLCPCB · STM32CubeIDE · ST-LINK |
  
---
 
## Key Images
 
### Schematic
 
[![Schematic](Images/PCB_Schematic.png)](Images/PCB_Schematic.png)
 
### PCB Layout
 
[![PCB Layout1](Images/STM32L496RG_Breakout_PcbDoc_Small_2D.png)](Images/STM32L496RG_Breakout_PcbDoc_Small_2D.png)

[![PCB Layout2](Images/Sources__STM32L496RG_Breakout_Soldermask_Top_Gerber274XDocument_cam_Small.png)](Images/Sources__STM32L496RG_Breakout_Soldermask_Top_Gerber274XDocument_cam_Small.png)

---
 
## Bring-Up & Testing
  
### Timer / PWM ✅
 
`TIM3_CH3` configured for PWM generation on **PB0** and broken out to the header. With `PSC = 1`, `ARR = 999` off the 4 MHz timer clock the output lands at **2 kHz at 50 % duty**, confirmed on the scope.
 
[![PWM Capture](Images/Timer_waveform.png)](Images/Timer_waveform.png)
 
### I²C ✅
 
The I²C waveform path was verified by issuing a master transmit to an unpopulated address. The capture shows a clean **START → 7-bit address → NACK** on the 9th bit (no slave present to acknowledge).
 
[![I²C Capture1](Images/I2C_waveform1.png)](Images/I2C_waveform1.png)

[![I²C Capture2](Images/I2C_waveform2.png)](Images/I2C_waveform2.png)
 
### CAN Bus ✅
 
CAN2 was exercised in **loopback** with auto-retransmission, transmitting an 8-byte standard frame (ID `0x123`). On the scope, the pre-transceiver TX/RX test points show idle-high / dominant-low signalling with **RX mirroring TX**, verifying the TCAN337 is actively driving and echoing the bus rather than the MCU just talking to itself.
 
[![CAN Capture](Images/CANBus_Waveform.png)](Images/CANBus_Waveform.png)

---
 
## Repository Contents
 
- Altium project files (schematic, PCB, project)
- `Images/` — renders, layout, assembled board, and oscilloscope captures
- This README
---
 
*Built and tested by [Laaaarry](https://github.com/Laaaarry).*
