# Train Ticket Vending Machine (FPGA / VHDL)

## General Description

This project implements a digital vending machine for selling train tickets, developed on a **Basys 3** FPGA development board. The system allows the user to input the distance, calculates the price, processes the payment, and dispenses the ticket and any necessary change, while also signaling various error conditions.

The project was developed as part of the **Digital Systems Design** (Proiectarea Sistemelor Numerice - PSN) course.

## Implementation Details

| Detail | Value |
| :--- | :--- |
| **Student** | Avram Oana-Teodora |
| **Development Board** | Digilent Basys 3 (Xilinx Artix-7, **xc7a35tcpg236-1**) |
| **Hardware Description Language**| VHDL |
| **Software** | Xilinx Vivado (v2024.2) |

## Key Functionalities

The system is designed as a Finite State Machine (FSM) clearly partitioned into a **Control Unit (UC)** and an **Execution Unit (UE)**, which manages the following steps:

1.  **Distance Input:** The user inputs the desired distance (in tens of kilometers) using a set of switches.
2.  **Price Generation:** The ticket price is automatically calculated based on a fixed rate of **5 Euro per kilometer**.
3.  **Payment and Display:** The price, the amount introduced, and the change (restul) are displayed on the 7-segment display, controlled via multiplexing. The currency used is EURO.
4.  **Change Management:** The machine dispenses change, if available. It starts pre-loaded with various denominations between 1 Euro and 50 Euro.
5.  **Ticket Dispensing:** After the process is confirmed, the ticket is dispensed, signaled by a dedicated LED (**`bilet_eliberat`**).
6.  **Cancellation:** The operation can be canceled at any time, resulting in the reimbursement of the amount introduced.

### Error Signals

The system uses an LED (**`eroare`**) to signal the following critical error conditions:

* The amount introduced is less than the price.
* The machine is out of tickets.
* It is impossible to provide the correct change.

### Key Logical Components

* **Binary to BCD Converter (`convertor_binar_bcd`):** This component translates the binary value into BCD (Binary-Coded Decimal) to enable the independent display of each digit (hundreds, tens, and units) on the 7-segment display.
* **Method Used:** **Double Dabble** algorithm.
* **Display Component (`Afisor`):** Uses the `convertor_binar_bcd` and multiplexing, synchronized with the clock, to cycle through and display the Hundreds, Tens, and Units digits.

## Usage Instructions (Basys 3 Hardware Mapping)

To run the project on the Basys 3 board, refer to the image below for the allocation of the input/output pins:

| Signal | Type | Basys 3 Location | Description |
| :--- | :--- | :--- | :--- |
| **`distanța`** | Input | Switches (SW) | Input for the desired distance (in tens of kilometers). |
| **`suma_plătită`** | Input | Switches (SW) | Input for the money paid by the traveler. |
| **`btn_confirm1`** | Input | Button (BTN) | Confirms continuation of the process. |
| **`cancel`** | Input | Switch (SW) | Action to cancel the transaction[cite: 89]. |
| **`reset`** | Input | Button (BTN) | Resets the machine to the initial state. |
| **Display** | Output | 7-Segment Display | Shows the ticket price, amount paid, and change. |
| **`bilet_eliberat`** | Output | LED (LD) | Lights up upon successful ticket dispensing. |
| **`eroare`** | Output | LED (LD) | Signals the impossibility of finalizing the transaction.

## Future Development Possibilities

The project can be expanded with the following enhancements:

* **Travel Class Selection:** Introduce options for different classes (e.g., 1st class, 2nd class), each with its own per-kilometer rate.
* **Multi-Currency Support:** Adapt the system to accept payments in multiple currency types.
* **Graphical Interface:** Connect the system to a VGA screen to simulate a more advanced graphical display panel.
