# EmberyLine: Automated Sorting & Assembly Simulation 

A sophisticated **ABB RobotStudio** simulation of an automated assembly line. The project features a synchronized conveyor system and three **IRB 1300** robots that perform sorting, painting, and pick-and-place operations based on variable product inputs.

## Project Overview
The "EmberyLine" simulates a T-shirt processing plant. A conveyor generates products ("Cosmic T-Shirts") at random intervals (every 3 seconds). The system sorts these products by **size**, directing them to specific workstations where robots perform value-added tasks before palletizing them into baskets.

## Tech Stack & Hardware
* **Software:** ABB RobotStudio & RAPID Programming.
* **Robots:** 3x **IRB 1300-7/1.4** (Selected for 1.4m reach and 6-DOF flexibility).
* **End-Effectors:** Custom-built **Vacuum PenTool** (Smart Component).

## Key Technical Features

### 1. Smart Components & Logic
The simulation relies heavily on **Smart Components** to handle physics and logic signals without external PLC code:
* **Custom Tools:** Created `VacuumPenToolSC.rslib` to handle dynamic attaching/detaching of objects using signals like `diAttacher`.
* **Conveyor Logic:** Utilizes sensors and logic gates to detect T-shirt size and stop the belt at the precise coordinate for the assigned robot.

### 2. RAPID Programming (I/O & Interrupts)
The robots communicate with the station via digital I/O signals. The logic follows a structured flowchart:
1.  **Wait:** Robot waits for `TShirt-Ready` signal.
2.  **Process:** Activates `doPaint` to simulate the painting process.
3.  **Actuation:** triggers `doVacuum` to pick the item.
4.  **Transport:** Moves via specific paths to the basket.

**Signal Mapping Example:**
| Signal Name | Type | Function |
| :--- | :--- | :--- |
| `doPaint` | Digital Output | Activates painting animation/logic |
| `doVacuum` | Digital Output | Activates the vacuum gripper |
| `diTshirt` | Digital Input | Confirms product presence at station |

## How to Run the Simulation

1.  **Clone the repository.**
2.  Open **ABB RobotStudio**.
3.  Go to **File > Open > Unpack & Work**.
4.  Select the file `project_files/EmberyLine.rspag`.
5.  Follow the wizard to unpack the controller data.
6.  Once loaded, go to the **Simulation** tab and press **Play**.

## File Description
* **`EmberyLine.rspag`:** The complete Pack-and-Go file (includes Station + RAPID code).
* **`VacuumPenToolSC.rslib`:** Standalone custom smart component library.
* **`Report.pdf`:** Full project documentation, flowcharts, and component breakdown.

---
*Developed by Raphael García Zapata - Robotics Engineering Student at UC3M.*
