# 8086 Pins & Interrupts — Ultra‑Simple Cheat Sheet (with Emojis)

Make the 8086 feel like real life: think classroom, office, and roads. Short, simple, and visual.

---

## 🗺️ Quick Map

* ⚡ **Power**: `VCC / GND`
* 🧭 **Mode**: `MN / MX̄` (Minimum / Maximum)
* 🛣️ **Data Lanes**: `BHĒ` (Upper byte D15–D8)
* ⏳ **Pausing**: `READY`, `TEST` + `WAIT`
* 🚨 **Interrupts**: `INTR`, `INTĀ`, `NMI`
* 🔒 **Atomic Lock**: `LOCK`
* 🔁 **Bus Sharing**: `HOLD / HLDA`, `RQ/GT0, RQ/GT1`

---

## ⚡ Power

**VCC / GND** — 5V power and ground.

* **Analogy**: 📱 Plugging in your phone. No power → nothing works.

---

## 🧭 System Mode

**MN / MX̄** — Choose how the system is organized.

* **MN (Minimum = 1)**: Solo mode; CPU manages the bus itself.

  * Analogy: 🚗 You drive on an empty road—no traffic police.
* **MX̄ (Maximum = 0)**: Team mode; helper chips manage sharing.

  * Analogy: 👮 Traffic cop coordinates many cars (CPUs/DMA).

---

## 🛣️ Data Lanes (Upper Byte)

**BHĒ (Bus High Enable)** — Turn on the **upper 8-bit lane** (D15–D8).

* **Why**: Access odd-address bytes or upper half of a word.
* **Analogy**: 🛤️ Two-level flyover; sometimes you open **only the upper lane**.

---

## ⏳ Waiting & Sync

**READY** — Let slow parts say “please wait”.

* `READY = 0` → CPU inserts wait states (pauses);
* `READY = 1` → run normally.
* **Analogy**: 🛍️ Shopkeeper says “one minute”; you wait politely.

**TEST + WAIT** — Pause until external “done” signal.

* `TEST = 1` → `WAIT` keeps idling;
* `TEST = 0` → continue.
* **Analogy**: 🚦 “Busy/Free” sign outside a lab; go only when it flips to **Free**.

---

## 🚨 Interrupts (Getting Attention)

**INTR (input)** — Normal (maskable) interrupt request.

* Works only if **IF = 1** (interrupts allowed).
* **Analogy**: ✋ Student raises hand; teacher takes questions only on “Q&A day”.

**INTĀ (output)** — Interrupt Acknowledge.

* CPU says “I’m listening—tell me the **issue number** (vector).”
* **Analogy**: 🧑‍🏫 Teacher says “yes?” and you say the topic code.

**NMI (input)** — Non‑maskable interrupt (can’t be ignored).

* For emergencies (power/memory errors).
* **Analogy**: 🔔 Fire alarm—class stops **immediately**.

---

## 🔒 Atomic Operations

**LOCK (output)** — Block others during a critical read‑modify‑write.

* **Analogy**: 🚧 “Do Not Disturb” sign while counting cash.

---

## 🔁 Bus Sharing / DMA

**HOLD (in) / HLDA (out)** — Hand over the bus for Direct Memory Access.

* Flow: Device asks **HOLD** → CPU finishes a beat → tri‑states bus → asserts **HLDA** → device uses bus → returns control.
* **Analogy**: 🪑 Classmate asks for your desk; you step aside and let them work, then you sit back.

**RQ/GT0, RQ/GT1 (max mode)** — Formal request/grant handshake.

* **Analogy**: 🚧 Gate guard: request to enter; guard later waves you in.

---

## 🧩 Mini Scenarios (Story Mode)

1. **Slow Memory**: `READY=0` → ⏳ CPU waits; `READY=1` → ✅ continue.
2. **Odd Byte Access**: Need upper lane only → 🛣️ enable **BHĒ**.
3. **Maskable Interrupt**: ✋ `INTR` + **IF=1** → CPU finishes current step → 🤝 `INTĀ` → gets vector → jumps to service.
4. **Emergency**: 🔔 `NMI` → immediate service—no permission check.
5. **DMA Transfer**: 🙋 `HOLD` → 🤝 `HLDA` → device moves data memory↔device → control returns.
6. **Atomic Update**: 🔒 `LOCK` during `XCHG`/RMW → no one else touches the bus.
7. **Coprocessor Wait**: `WAIT` watches **TEST** (8087 busy light) → continue when free.

---

## 🧠 TL;DR (One Line)

**Power on, pick control style, choose lane width, wait if needed, handle attention (INTR/NMI), lock for critical work, and share the bus politely (HOLD/HLDA or RQ/GT).**

---

## 📝 Quick Self‑Check (2 Qs)

1. You need a byte at an **odd** address—what helps? → **BHĒ** 🛣️
2. An emergency occurs—what signal is used? → **NMI** 🔔

---

## ✅ Coverage Map (What’s explained)

* ⚡ **VCC / GND** — what they are and why needed (power).
* 🧭 **MN / MX̄** — minimum vs maximum mode (who manages the bus).
* 🛣️ **BHĒ** — upper byte lane D15–D8 and odd/word access.
* ⏳ **READY** — adding wait states for slow memory.
* 🚦 **TEST + WAIT** — pause until external “done” signal (8087 use-case).
* ✋ **INTR** — normal (maskable) interrupt request.
* 🤝 **INTĀ** — CPU’s acknowledge + vector handoff (via PIC).
* 🔔 **NMI** — non-maskable emergency interrupt.
* 🔒 **LOCK** — atomic read‑modify‑write (blocks other bus masters).
* 🔁 **HOLD / HLDA** — DMA bus handover sequence.
* 🚧 **RQ/GT0, RQ/GT1** — request/grant handshake in maximum mode.
* 🧩 **External Interrupt Connections** — covered via the INTR/INTĀ section with the role of a **PIC (e.g., 8259A)**.

*End of sheet — keep for exams and quick revision!*
