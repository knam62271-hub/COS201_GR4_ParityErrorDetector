# COS201 – Parity Error Detector

Parity Error Detector for 8-bit data, written in Verilog.
The design creates an even parity bit, can flip one bit of the data, and checks if there is an error.

More details are in the Report.

---

## Overview

| Item | Description |
|---|---|
| Language | Verilog |
| Data width | 8 bits |
| Parity type | Even parity |
| Error | Flip bit 5 |
| Golden model | Python |

---

## System Flow

<img width="898" height="1048" alt="694b92aa-2f1c-4b47-97c2-7c8a7574294e" src="https://github.com/user-attachments/assets/1169617f-87f8-4dc2-a92a-d85ab915e191" />


Data goes through the parity generator, then the channel, then the parity checker. `error_flag = 0` means OK, `error_flag = 1` means error.

---

## System Architecture

### High-level

<img width="1009" height="1012" alt="high_level" src="https://github.com/user-attachments/assets/2db07e09-61cc-4817-a97a-508ae2c485fd" />

### Low-level

<img width="1606" height="913" alt="low_level" src="https://github.com/user-attachments/assets/225c3f34-68a3-4244-9702-e3f95df91af3" />


| Module | Function |
|---|---|
| `parity_generator` | Makes the even parity bit |
| `error_injector` | Flips bit 5 when `error_enable = 1` |
| `parity_checker` | Checks the data and parity, gives `error_flag` |
| `top` | Connects the 3 modules |

---

## Interface (top module)

| Signal | Dir | Width | Description |
|---|---|---|---|
| `data_in` | in | 8 | Input data |
| `error_enable` | in | 1 | `1` = flip bit 5 |
| `parity_bit` | out | 1 | Parity bit |
| `data_rx` | out | 8 | Received data |
| `error_flag` | out | 1 | `1` = error, `0` = OK |

---

## Operation

| `error_enable` | `data_rx` | `error_flag` |
|---|---|---|
| 0 | Same as `data_in` | 0 |
| 1 | Bit 5 flipped | 1 |

---

## Repository Structure

```text
COS201_ParityErrorDetector/
├── Golden_model/
│   └── golden_model.py
│
├── Result/
│   ├── error_injector.jpg
│   ├── parity_checker.jpg
│   ├── parity_generator.jpg
│   ├── top.jpg
│   ├── system_flow.png
│   ├── high_level.png
│   └── low_level.png
│
├── Rtl/
│   ├── error_injector.v
│   ├── parity_checker.v
│   ├── parity_generator.v
│   └── top.v
│
├── Testbench/
│   ├── tb_error_injector.v
│   ├── tb_parity_checker.v
│   ├── tb_parity_generator.v
│   └── tb_top.v
│
├── Parity_Error_Detector_References.md
├── README.md
└── Report
```

---

## Verification

- Each module has its own testbench, `tb_top.v` tests the whole design.
- Test with `error_enable = 0` and `error_enable = 1`.
- Results are compared with the Python golden model.

---

## References

See [Parity_Error_Detector_References.md](Parity_Error_Detector_References.md).
