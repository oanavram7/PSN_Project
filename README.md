# Train Ticket Vending Machine (FPGA / VHDL)

## General Description

This project implements a digital vending machine for selling train tickets, developed on a **Basys 3** FPGA development board. The system allows the user to input the distance, calculates the price, processes the payment, and dispenses the ticket and any necessary change, while also signaling various error conditions.

The project was developed as part of the **Digital Systems Design** (Proiectarea Sistemelor Numerice - PSN) course.

## Implementation Details

| Detail | Value 
| :--- | :--- |
| **Student** | Avram Oana-Teodora |
| **Development Board** | Digilent Basys 3 (Xilinx Artix-7, **xc7a35tcpg236-1**) |
| **Hardware Description Language**| VHDL |
| **Software** | Xilinx Vivado (v2024.2) |

## Key Functionalities

[cite_start]The system is designed as a Finite State Machine (FSM) clearly partitioned into a **Control Unit (UC)** and an **Execution Unit (UE)**[cite: 169], which manages the following steps:

1.  [cite_start]**Distance Input:** The user inputs the desired distance (in tens of kilometers) using a set of switches[cite: 63, 69].
2.  [cite_start]**Price Generation:** The ticket price is automatically calculated based on a fixed rate of **5 Euro per kilometer**[cite: 64, 136].
3.  [cite_start]**Payment and Display:** The price, the amount introduced, and the change (restul) are displayed on the 7-segment display, controlled via multiplexing[cite: 65, 70, 74, 171]. [cite_start]The currency used is EURO[cite: 56].
4.  [cite_start]**Change Management:** The machine dispenses change, if available[cite: 73]. [cite_start]It starts pre-loaded with various denominations between 1 Euro and 50 Euro[cite: 58].
5.  [cite_start]**Ticket Dispensing:** After the process is confirmed, the ticket is dispensed, signaled by a dedicated LED (**`bilet_eliberat`**)[cite: 76, 97].
6.  [cite_start]**Cancellation:** The operation can be canceled at any time, resulting in the reimbursement of the amount introduced[cite: 60, 89].

### Error Signals

[cite_start]The system uses an LED (**`eroare`**) to signal the following critical error conditions[cite: 77, 98, 99, 173]:

* [cite_start]The amount introduced is less than the price[cite: 78].
* [cite_start]The machine is out of tickets[cite: 79].
* [cite_start]It is impossible to provide the correct change[cite: 80].

### Key Logical Components

* [cite_start]**Binary to BCD Converter (`convertor_binar_bcd`):** This component translates the binary value into BCD (Binary-Coded Decimal) to enable the independent display of each digit (hundreds, tens, and units) on the 7-segment display[cite: 104, 111].
* [cite_start]**Method Used:** **Double Dabble** algorithm[cite: 117].
* [cite_start]**Display Component (`Afisor`):** Uses the `convertor_binar_bcd` and multiplexing, synchronized with the clock, to cycle through and display the Hundreds, Tens, and Units digits [cite: 124, 127-131].

## Usage Instructions (Basys 3 Hardware Mapping)

[cite_start]To run the project on the Basys 3 board, refer to the image below for the allocation of the input/output pins[cite: 164]:

| Signal | Type | Basys 3 Location | Description |
| :--- | :--- | :--- | :--- |
| **`distanța`** | Input | Switches (SW) | [cite_start]Input for the desired distance (in tens of kilometers)[cite: 85]. |
| **`suma_plătită`** | Input | Switches (SW) | [cite_start]Input for the money paid by the traveler[cite: 87]. |
| **`btn_confirm1`** | Input | Button (BTN) | [cite_start]Confirms continuation of the process[cite: 92]. |
| **`cancel`** | Input | Switch (SW) | [cite_start]Action to cancel the transaction[cite: 89]. |
| **`reset`** | Input | Button (BTN) | [cite_start]Resets the machine to the initial state[cite: 90]. |
| **Display** | Output | 7-Segment Display | [cite_start]Shows the ticket price, amount paid, and change[cite: 95]. |
| **`bilet_eliberat`** | Output | LED (LD) | [cite_start]Lights up upon successful ticket dispensing[cite: 97]. |
| **`eroare`** | Output | LED (LD) | [cite_start]Signals the impossibility of finalizing the transaction[cite: 98].

## Future Development Possibilities

[cite_start]The project can be expanded with the following enhancements[cite: 176, 177]:

* [cite_start]**Travel Class Selection:** Introduce options for different classes (e.g., 1st class, 2nd class), each with its own per-kilometer rate[cite: 178, 179].
* [cite_start]**Multi-Currency Support:** Adapt the system to accept payments in multiple currency types[cite: 181, 182].
* [cite_start]**Graphical Interface:** Connect the system to a VGA screen to simulate a more advanced graphical display panel[cite: 183, 184].
