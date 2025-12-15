# Microcontroller Theory - Concise Notes

---

## 1. Microcontroller Architecture

### Flow Diagram

```
┌─────────────────────────────────────────────────────────┐
│           MICROCONTROLLER ARCHITECTURE                   │
└─────────────────────────────────────────────────────────┘

Classification Based On:
═══════════════════════

┌─────────────┐
│   BY BITS   │
└──────┬──────┘
       │
       ├─→ 8-bit  → Intel 8051, MC68HC11
       ├─→ 16-bit → Intel 8096, MC68HC12
       └─→ 32-bit → Intel 80960, M683xx

┌──────────────┐
│  BY MEMORY   │
└──────┬───────┘
       │
       ├─→ Embedded: All on chip (8051)
       └─→ External: Memory outside (8031)

┌─────────────────┐
│ BY INSTRUCTION  │
└──────┬──────────┘
       │
       ├─→ CISC: Complex instructions
       └─→ RISC: Simple, faster

┌────────────────────┐
│ BY ARCHITECTURE    │
└──────┬─────────────┘
       │
       ├─→ Von Neumann: 1 bus (slower)
       └─→ Harvard: 2 buses (faster)
```

### Summary Table

| Classification | Types | Key Difference | Example |
|----------------|-------|----------------|---------|
| **By Bits** | 8-bit, 16-bit, 32-bit | Processing width | 8-bit: 8051, 32-bit: ARM |
| **By Memory** | Embedded, External | Memory location | Embedded: All on chip |
| **By Instruction** | CISC, RISC | Instruction complexity | RISC: Faster, simpler |
| **By Architecture** | Von Neumann, Harvard | Bus structure | Harvard: Parallel, faster |

---

## 2. Core Microcontroller Components

### Flow Diagram

```
        OSCILLATOR (Clock)
              ↓
            CPU
         ↙       ↘
       ALU    REGISTERS
              ↓
      SPECIAL REGISTERS
      • Program Counter
      • Stack Pointer
      • Status Register
              ↓
      MEMORY (ROM + RAM)
              ↓
      WATCHDOG TIMER
```

### Summary Table

| Component | Function | Key Point |
|-----------|----------|-----------|
| **CPU** | Execute instructions | Brain of MCU |
| **ALU** | Math & logic operations | Add, subtract, AND, OR |
| **Oscillator** | Generate clock | Timing for all operations |
| **ROM/Flash** | Store program | Non-volatile (4K-64K) |
| **RAM** | Temporary data | Volatile (few hundred bytes) |
| **Registers** | Fast data storage | General + Special purpose |
| **Program Counter** | Point to next instruction | Auto-increments |
| **Stack Pointer** | Track stack location | For function calls |
| **Watchdog Timer** | Prevent system hang | Auto-reset if stuck |

---

## 3. Peripheral Microcontroller Components

### Flow Diagram

```
EXTERNAL WORLD ←→ PERIPHERALS ←→ CPU

Digital:                Analog:
• I/O Ports            • ADC (Analog → Digital)
• Timers/Counters      • DAC (Digital → Analog)
• PWM

Communication:
• UART (PC, Bluetooth)
• SPI (Sensors, SD card)
• I²C (LCD, EEPROM)
```

### Summary Table

| Peripheral | Function | Use Case |
|------------|----------|----------|
| **ADC** | Analog → Digital | Read sensors (temperature, light) |
| **DAC** | Digital → Analog | Control motor speed, audio |
| **I/O Ports** | Digital input/output | LED, button, relay |
| **Timers** | Delays, counting | Blink LED, measure time |
| **PWM** | Pulse width modulation | Motor speed, LED brightness |
| **UART** | Serial communication | PC connection |
| **SPI** | Fast serial (4 wires) | Sensors, memory cards |
| **I²C** | Multi-device (2 wires) | LCD, multiple sensors |

---

## 4. Advantages of Microcontrollers

### Flow Diagram

```
┌─────────────────────────────────────────┐
│      WHY USE MICROCONTROLLERS?          │
├─────────────────────────────────────────┤
│  All-in-One  →  Cost Effective          │
│  Small Size  →  Portable                │
│  Low Power   →  Battery Friendly        │
│  Integrated  →  Reliable                │
│  Real-Time   →  Fast Response           │
│  Easy Tools  →  Quick Development       │
└─────────────────────────────────────────┘
```

### Summary Table

| Advantage | Benefit | Comparison |
|-----------|---------|------------|
| **Cost-Effective** | $1-$10 vs $50+ | Single chip vs multiple |
| **Low Power** | µW to mW | Battery lasts months/years |
| **Compact Size** | 5mm × 5mm | Fits in wearables |
| **Real-Time** | <1ms response | Critical control systems |
| **Easy Programming** | Arduino, free tools | Days vs months to learn |
| **Integrated Peripherals** | No external chips | Simpler design |
| **Single Chip** | All in one | Fewer failures |
| **Reliable** | 10+ years | Industrial grade |
| **Flexible Development** | Many tools available | Fast prototyping |
| **Long-Term Support** | 10-20 years production | No redesign needed |

---

## Quick Reference Card

| Topic | Key Takeaway |
|-------|--------------|
| **Architecture** | 4 ways to classify: Bits, Memory, Instruction, Bus |
| **Core Components** | CPU, Memory, Timers - essential for operation |
| **Peripherals** | ADC/DAC for analog, I/O for digital, Comm for data transfer |
| **Advantages** | Cheap, small, low power, reliable, easy |
