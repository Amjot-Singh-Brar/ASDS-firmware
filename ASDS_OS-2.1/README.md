# ASDS_OS-2.1

Firmware and documentation for **ASDS OS 2.1**, the control software for the  
**Automated Substrate Dipping System (ASDS)** based on an Arduino Nano.

This directory contains everything a lab user needs to:

- Identify the correct firmware version for their controller.
- Download the compiled firmware image (`.hex`).
- Update the ASDS controller.
- Access the user manual and release notes.

---

## 1. Overview

**ASDS_OS-2.1** is a time-based motion control firmware that:

- Drives a continuous-rotation servo to move the substrate carrier:
  - **Down** into the process bath,
  - **Hold** at the dipping position for a user-defined dwell time,
  - **Up** to the Home (upper) position.
- Provides a simple **4-button** front panel interface:
  - `START`, `STOP`, `+1 MIN`, `+1 SEC`.
- Uses a **16×2 I²C LCD** to display:
  - Idle screen (`Hold: MM:SS` / `Press START`)
  - Status (`Running: Down`, `Hold...`, `Running: Up`, `Returning...`).

Key behavior:

- Fixed travel time each direction: **≈ 2 s down**, **≈ 2 s up**.
- Adjustable dwell time: **0–120 min** in **1 s** and **1 min** increments.
- STOP button logic:
  - Idle → resets the hold time.
  - At full down (Hold, not moving) → returns to Home in a controlled way.
  - During motion → emergency-only abort; may cause mechanical stress (see manual).

---

## 2. Repository Contents (OS 2.1 Folder)

Typical content of this folder:

- `firmware/`
  - `ASDS_OS-2.1_nano.hex`  
    → Compiled firmware image for Arduino Nano (recommended file to flash).
  - *(optional)* `ASDS_OS-2.1_nano_with_bootloader.hex`  
    → Image including bootloader, for factory/ISP programming only.

- `docs/`
  - `ASDS_Manual_Rev2.1C.pdf`  
    → Full instruction manual for the Automated Substrate Dipping System.
  - `CHANGELOG_OS-2.1.md`  
    → Version-specific changes, bug fixes, and notes.

- `FLASHING_INSTRUCTIONS_OS-2.1.md`  
  → Step-by-step guide for updating the firmware on the Arduino Nano.

File names may differ slightly depending on how releases are packaged, but the structure will be similar.

---

## 3. Which Firmware File Should I Use?

For **normal firmware updates over USB** with an existing Arduino Nano:

-  Use:  
  **`ASDS_OS2_1.hex`**  
  (or the equivalently named `.hex` file)


---

## 4. How to Update the Firmware

For detailed, OS-specific steps (including screenshots and OS-specific tools),  
please see:

> **`FLASHING_INSTRUCTIONS.md`**


---

## 5. Compatibility

**Controller hardware:**  
- Arduino Nano (ATmega328P-based)

**Designed for:**  
- Automated Substrate Dipping System (ASDS) using:
  - Continuous-rotation servo on pin 9
  - Four active-LOW pushbuttons on pins 2, 3, 4, 5
  - I²C 16×2 LCD (address `0x27`)

If your hardware wiring differs from the reference design described in the  
manual, this firmware may not behave correctly.

---

## 6. Safety Notes

- Always power down the ASDS before changing wiring, mechanical components, or load configuration.
- Follow all chemical safety, PPE, and lab procedures described in the manual.
- The **STOP** button is safe to use:
  - On the **idle** screen (resets hold time).
  - At the **dipping/hold** position when the arm is fully down and not moving.
- **Do not** routinely press STOP during motion (`Running: Down` / `Running: Up`).  
  It is intended as an **emergency-only** action and may cause mechanical shock or gear derailment.

---

## 7. Versioning and Support

- **Firmware version:** `ASDS_OS-2.1`
- **Device hardware revision:** `Rev 2.1C` (printed on the ASDS nameplate)
- **User manual:** see the version/date printed on the PDF front page

