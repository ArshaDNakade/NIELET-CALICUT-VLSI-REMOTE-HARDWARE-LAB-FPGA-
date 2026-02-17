# NIELET-CALICUT-VLSI-REMOTE-HARDWARE-LAB-FPGA-

# VIRTUAL HARDWARE LAB EXPERIENCE REPORT

**NIELIT Calicut – Remote FPGA Laboratory**

---

## 1. Objective

To understand the complete FPGA design flow using a remote hardware platform by:

* Writing a Verilog HDL program
* Synthesizing and implementing the design in Vivado
* Generating bitstream
* Configuring a remote FPGA board
* Observing real hardware output through live camera feed

---

## 2. Software and Hardware Used

**Software**

* Xilinx Vivado 2022.2
* NIELIT Remote Hardware Lab Portal (VNC Based Access)

**Hardware**

* Xilinx Artix-7 FPGA board (xc7a100tcsg324-1)
* On-board clock oscillator
* On-board LED
* Remote camera monitoring system

---

## 3. Theory

An FPGA (Field Programmable Gate Array) is a programmable integrated circuit that can implement digital logic hardware using Hardware Description Languages (HDL) like Verilog.

Unlike microcontrollers (which execute instructions sequentially), FPGA creates actual hardware circuits such as:

* Flip flops
* Counters
* Logic gates
* State machines

In this experiment, a **clock divider circuit** was implemented to blink an LED.
Since the FPGA clock operates at very high frequency (≈100 MHz), it must be divided to human-visible frequency (~1 Hz).

[T = \frac{Counter\ Value}{Clock\ Frequency}]

This produces a slow signal used to toggle the LED.

---

## 4. Verilog Program

```verilog
module arshad (
    input clk,
    input reset,
    output reg led
);

reg [26:0] counter;

always @(posedge clk or posedge reset)
begin
    if(reset)
    begin
        counter <= 0;
        led <= 0;
    end
    else
    begin
        counter <= counter + 1;

        if(counter == 50000000)
        begin
            led <= ~led;
            counter <= 0;
        end
    end
end

endmodule
```

---

## 5. Procedure

### Step 1 – Login to Remote Lab

* Accessed NIELIT Calicut remote hardware lab portal
* Connected to remote Linux system via browser VNC interface
* Launched Vivado environment

### Step 2 – Project Creation

* Created new RTL project
* Selected target FPGA device: **xc7a100tcsg324-1**
* Added Verilog source file

### Step 3 – Synthesis

* Ran synthesis
* Verified no syntax errors
* Observed generated RTL schematic

### Step 4 – Implementation

* Ran implementation
* Initially received placement error due to incorrect clock pin mapping
* Understood importance of dedicated clock routing in FPGA
* Corrected constraints

### Step 5 – Bitstream Generation

* Successfully generated bitstream after fixing constraints
* Hardware configuration file created

### Step 6 – Programming FPGA

* Opened Hardware Manager
* Connected to remote FPGA board
* Programmed device with generated bitstream

### Step 7 – Hardware Verification

* Observed live camera feed
* LED blinking confirmed successful hardware execution

---

## 6. Observations

| Stage          | Observation                              |
| -------------- | ---------------------------------------- |
| RTL Design     | Counter based sequential circuit created |
| Synthesis      | Logic converted into flip flops and LUTs |
| Implementation | Mapped to FPGA fabric                    |
| Error Faced    | Clock placement routing error            |
| Fix            | Proper clock constraint understanding    |
| Final Output   | LED blinking visible on remote hardware  |

---

## 7. Result

The LED blinking circuit was successfully implemented and executed on a real FPGA board using a remote hardware laboratory. The design demonstrated the practical conversion of HDL code into physical hardware behavior.

---

## 8. Learning Outcomes

* Understood difference between simulation and real hardware execution
* Learned FPGA design flow: HDL → Synthesis → Implementation → Bitstream → Hardware
* Understood importance of clock routing in FPGA
* Experienced remote hardware programming
* Observed real-time hardware behavior via camera

---

## 9. Conclusion

The experiment successfully demonstrated the working of FPGA-based digital hardware using Verilog HDL in a remote laboratory environment. The virtual hardware lab effectively provided practical exposure to real hardware programming without physical access to the board.

---
