| Name | Purpose | Primary Part | Backup Part |
| --- | --- | --- | --- |
| `U1` | LED constant-current driver for both lamps in series | `TPS923654HMDMTR` | `TPS923654DMTR` |
| `L1` | Power inductor for LED boost / buck-boost stage | `IHLP3232DZER5R6M11` | `IHLP3232DZER5R6M11` |
| `D1` | Schottky diode for LED power stage | `STPS5H100B-TR` | `SK510` |
| `R_SENSE` | LED current sense resistor, about `0.67 A` target string current | `HoLRT1206-1W-300mR-1%` | `3 x PE1206FRF470R1L in series` |
| `R_FSET` | LED-driver switching-frequency set resistor | `0805W8F2202T5E` | `ERA-6AEB2212V` |
| `R_TEMP` | LED-driver local thermal foldback resistor | `0402WGF1003TCE` | `0402WGF1003TCE` |
| `R_OVP_TOP` | Upper resistor of OVP / open-load divider | `0402WGF2003TCE` | `RC0201FR-07200KL` |
| `R_OVP_BOT` | Lower resistor of OVP / open-load divider | `0402WGF1002TCE` | `RC0402FR-0710KL` |
| `C_IN_MAIN` | Main input bulk capacitance on `12 V` rail | `CL21A226MAQNNNE` | `CL21A226MAQNNNE` |
| `C_IN_HF` | High-frequency input bypass | `CC0805KRX7R9BB104` | `GRM033R61E104KE14D` |
| `C_VCC` | Local decoupling for LED-driver low-voltage rail | `CL05A105KA5NQNC` | `CL05A105KP5NNNC` |
| `C_OUT` | LED output capacitance | `GRM21BR61H106KE43L` | `CL21A106KBYQNNE` |
| `C_OUT_HF` | High-frequency output bypass | `CC0805KRX7R9BB104` | `CL31B104KBCNNNL` |
| `C_SENSE` | Current-sense path filtering / stabilization | `GRM21BR61H106KE43L` | `CL21A106KBYQNNE` |
| `R_COMP` | Compensation network resistor | `0402WGF1000TCE` | `ERA-3AEB101V` |
| `C_COMP` | Compensation network capacitor | `CL10B102KB8NNNC` | `GRM155R71H102KA01D` |
| `R_DAMP` | Compensation / damping auxiliary resistor | `0402WGF1004TCE` | `ERJ-P08J105V` |
| `R_FLT` | Fault-pin RC filter resistor | `0402WGF1000TCE` | `ERA-3AEB101V` |
| `C_FLT` | Fault-pin RC filter capacitor | `CL10B102KB8NNNC` | `GRM155R71H102KA01D` |
| `Q1` | PWM level shifter from `DRV8908` to LED-driver dim pin | `NTZD3154NT1G` | `NTZD3154NT1G` |
| `R_GATE` | PWM level-shifter gate/input resistor | `0402WGF1001TCE` | `ERJ-3EKF1001V` |
| `R_GATE_PD` | PWM level-shifter gate pull-down | `0402WGF1003TCE` | `0402WGF1003TCE` |
| `R_ADIM_PULLUP` | Pull-up for LED-driver dimming/control pin | `0402WGF1002TCE` | `RC0402FR-0710KL` |
| `R_FAULT_PULLUP` | Pull-up for LED-driver fault output | `0402WGF1002TCE` | `RC0402FR-0710KL` |
| `U2` | 4-channel I2C ADC for NTC temperature sensing | `ADS1015IDGSR` | `TLA2024IRUGR` |
| `C_ADC_VDD` | ADC supply decoupling | `CC0805KRX7R9BB104` | `GRM033R61E104KE14D` |
| `R_I2C_SCL` | Optional I2C SCL pull-up | `0402WGF4701TCE` | `do not stuff if bus already has pull-ups` |
| `R_I2C_SDA` | Optional I2C SDA pull-up | `0402WGF4701TCE` | `do not stuff if bus already has pull-ups` |
| `R_NTC_REFx` | Reference resistor for each NTC divider | `0402WGF1002TCE` | `ERA-6AED103V` |
| `R_NTC_FILTx` | Series resistor into each ADC channel | `0402WGF1000TCE` | `ERA-3AEB101V` |
| `C_NTC_FILTx` | RC filter capacitor at each ADC channel | `CL10B103KB8NFNC` | `CC0402KRX7R9BB103` |
| `NTCx` | Temperature sensor for heatsink or other thermal points | `NCP18XH103F03RB` | `103JG1K` |
| `U3` | Board EEPROM for identity, config, and calibration | `M24M01E-FDW6TP` | `M24M01-RMN6TP` |
| `C_EE_VCC` | EEPROM supply decoupling | `CC0805KRX7R9BB104` | `GRM033R61E104KE14D` |
| `R_WP_CFG` | Optional EEPROM write-protect strap | `0402WGJ0000TCE` | `solder bridge / direct strap` |
