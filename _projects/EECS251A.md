---
title: "EECS251LB : Field Programmable Gate Array Laboratory"
layout: single
collection: projects
type: "Graduate Design Project"
permalink: /projects/EECS251A
venue: "University of California, Berkeley"
date: 2025-12-12
location: "Berkeley, California, USA"
---

I won the Apple Design Competition for this Design!

<h1>Introduction</h1>

This project implements a 32-bit RISC-V core with a 3-stage pipeline, synchronous instruction/data memories, with minimal stalling and an integer cycles per instruction of 1. In addition to integer operations, the processor also supports floating point operations with a floating point CPI of slightly greater than 1. UART is used to interface the core with the real world. This RISC-V core was fully implemented on a PYNQ-Z1 board as shown in Figure 1. 

<div style="display: flex; gap: 10px; text-align: center;">
  <figure style="width: 100%; margin: 0;">
    <img src="/images/EECS151-1.png" style="width: 100%;">
    <figcaption>Figure 1 : Project Overview</figcaption>
  </figure>
</div>

<h1>3 Stage Pipeline</h1>

The three stage pipeline is divided into three phases : 
<ul>
<li>F : Instruction Fetch </li>
<li>DX : Decode and Execute </li>
<li>MW : Memory and Write-Back</li>
</ul>

Figure 2 shows the Block Diagram of our three stage pipeline with Floating Point Unit in parallel to the ALU. The Floating Point Unit (FPU) is pipelined with 2 st 0.ages for floating point addition and 3 stages for floating point mul nbgtds   tiplication and accumulation. 

<div style="display: flex; gap: 10px; text-align: center;">
  <figure style="width: 100%; margin: 0;">
    <img src="/images/Block_Diagram.jpg" style="width: 100%;">
    <figcaption>Figure 2 : Block Diagram of the three stage pipelined core</figcaption>
  </figure>
</div>

In the F stage, the IMEM, PC and pipeline register are clocked simultaneously. Between the DX and MW stage, the DMEM and pipeline registers are clocked together. Extensive forwarding is employed to ensure that ALU-ALU hazards, MEM-ALU hazards and ALU-MEM hazards do not encounter any stalls.  The PC Select Mux takes one of its input right from the output of the ALU. In case of a branch instruction, the ALU output is directly forwarded to the IMEM address, thus reducing any branch misprediction and having a resultant integer CPI of 1.

Due to the long critical path of the floating point unit, it has been pipelined to 2 stages for floating point addition and 3 stages for floating point multiplication and accumulation to ensure high frequency of operation. 

<h1>Memory Mapped IO</h1>

A memory mapped IO is used to map the different memory locations to IMEM, BIOS, DMEM and UART modules. Figure 3 shows the MMIO mapping of the RISC-V core. 

<div style="display: flex; gap: 10px; text-align: center;">
  <figure style="width: 100%; margin: 0;">
    <img src="/images/MMIO.png" style="width: 100%;">
    <figcaption>Figure 3 : Memory Mapped IO</figcaption>
  </figure>
</div>

<h1>Resource Utilization</h1>

<h3>FPGA Usage</h3>

<table>
  <thead>
    <tr>
      <th>FPGA Resource</th>
      <th>No. of Units</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LUTs</td>
      <td>2589</td>
    </tr>
    <tr>
      <td>SLICE registers</td>
      <td>567</td>
    </tr>
    <tr>
      <td>BRAMs</td>
      <td>34</td>
    </tr>
    <tr>
      <td>DSP Blocks</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

<h3>Critical Path</h3>

The timing of the critical path is 15.744 ns. 

<h1>Results</h1>

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Integer CPI (mmult)</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Integer CPI (bdd)</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Floating Point CPI (fpmmult)</td>
      <td>1.33</td>
    </tr>
    <tr>
      <td>Clock Frequency</td>
      <td>62 MHz</td>
    </tr>
    <tr>
      <td>Cost</td>
      <td>4138844</td>
    </tr>
    <tr>
      <td>Figure of Merit (FoM)</td>
      <td>22.96</td>
    </tr>
  </tbody>
</table>

The achieved **Figure of Merit (FoM) is 22.96!**