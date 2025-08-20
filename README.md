# 🧠 I²C Controller in Verilog

This project implements a complete **I²C (Inter-Integrated Circuit) Controller** in Verilog HDL, consisting of:

- 🧭 I²C Master
- 🛑 I²C Slave
- 🔗 Top-level integration (`i2c_top.v`)

The system models a basic I²C communication setup where a master initiates communication with a slave device via shared `SDA` and `SCL` lines. The slave includes a 128-byte internal memory and supports read/write transactions with optional clock stretching.

---

## 📁 Project Structure

i2c-controller/
├── i2c_master.v # I²C Master Controller
├── i2c_slave.v # I²C Slave with memory & clock stretching
├── i2c_top.v # Top-level module connecting master and slave
├── testbench.v # Testbench 
├── tb_with_clock_strecthing # Waveform output from simulation
└── README.md 


## 🚦 System Overview

### 📦 I²C Master (`i2c_master.v`)
- Generates I²C start/stop conditions
- Sends 7-bit address and R/W bit
- Transfers 8-bit data (read/write)
- Checks for acknowledgment
- Provides `busy`, `done`, and `ack_err` flags

### 📦 I²C Slave (`i2c_slave.v`)
- Monitors SDA/SCL to detect addressing
- Matches its own address (7-bit)
- Stores/loads data from a 128-byte internal memory
- Supports clock stretching via `stretch` input
- Generates `ack_err` flag if protocol fails

### 🔗 Top Module (`i2c_top.v`)
- Connects `i2c_master` and `i2c_slave`
- Shares `sda` and `scl` wires
- Handles acknowledgment OR logic
- Exposes clean interface to external signals

## 🧪 Simulation Instructions

### 🔧 Requirements
- [Icarus Verilog](http://iverilog.icarus.com/)
- [GTKWave](http://gtkwave.sourceforge.net/)
- Vivado for Synthesis

🧠 Key Features
✅ Fully synthesizable RTL

✅ 7-bit address support (per I²C spec)

✅ Supports write and read operations

✅ Optional clock stretching in slave

✅ Modular design: easy to extend

✅ Clean top-level abstraction for SoC-level integration

🧩 Top Module Ports (i2c_top.v)
Port	Direction	Description
clk	input	System clock
rst	input	Reset (active high)
newd	input	Trigger new transaction
op	input	Operation: 0=write, 1=read
stretch	input	Enable slave clock stretching
addr[6:0]	input	7-bit I²C address to access
din[7:0]	input	Data to write
dout[7:0]	output	Data read from slave
busy	output	Master is busy
ack_err	output	Acknowledgment error
done	output	Transaction complete

🧰 Use Cases

FPGA-based I²C interfacing

Academic learning and teaching of I²C protocol

Simulation and waveform analysis
