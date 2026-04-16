# PiSubmarine Repository Dependency Graph

This document summarizes repository-level dependencies extracted from `PiSubmarineAddDependency(...)` calls in `CMakeLists.txt` files.

The extraction excludes generated and local-only directories such as `out`, `.git`, `.vs`, `.idea`, and vendored `_deps` copies.

## Main Graph

Solid arrows represent `src` or root-level dependencies.

```mermaid
flowchart LR
  "Bq25792" --> "I2C.Api"
  "Bq25792" --> "RegUtils"
  "Bq25792" --> "Units"

  "Chipset.Api" --> "Error.Api"
  "Chipset.Api" --> "RegUtils"
  "Chipset.Api" --> "Units"

  "Chipset.Client.I2C" --> "Chipset.Api"
  "Chipset.Client.I2C" --> "Error.Api"
  "Chipset.Client.I2C" --> "I2C.Api"
  "Chipset.Client.I2C" --> "Time.Tickable.Api"

  "Chipset.Engineering" --> "Bq25792"
  "Chipset.Engineering" --> "Max1726"

  "Drv8908" --> "GPIO.Api"
  "Drv8908" --> "RegUtils"
  "Drv8908" --> "SPI.Api"
  "Drv8908" --> "Units"

  "Drv8908.Cli" --> "Drv8908"
  "Drv8908.Cli" --> "GPIO.Linux"
  "Drv8908.Cli" --> "SPI.Linux"

  "Drv8908.PowerManager" --> "Drv8908"

  "GPIO.Linux" --> "GPIO.Api"

  "I2C.Api" --> "Error.Api"

  "I2C.Linux" --> "Error.Api"
  "I2C.Linux" --> "I2C.Api"

  "Max17261" --> "I2C.Api"
  "Max17261" --> "RegUtils"
  "Max17261" --> "Units"

  "Motor.Bidirectional.Api" --> "Units"

  "Motor.Drv8908" --> "Drv8908"
  "Motor.Drv8908" --> "Drv8908.PowerManager"
  "Motor.Drv8908" --> "Motor"
  "Motor.Drv8908" --> "Motor.Bidirectional.Api"
  "Motor.Drv8908" --> "Motor.Telemetry.Api"
  "Motor.Drv8908" --> "Motor.Unidirectional.Api"
  "Motor.Drv8908" --> "Time.Tickable.Api"

  "Motor.Unidirectional.Api" --> "Units"

  "PWM.Api" --> "Error.Api"
  "PWM.Api" --> "Units"

  "PWM.Linux" --> "Error.Api"
  "PWM.Linux" --> "PWM.Api"

  "RPi.Main" --> "Chipset.Api"
  "RPi.Main" --> "Drv8908"
  "RPi.Main" --> "Max1726"
  "RPi.Main" --> "RPi.Logging"
  "RPi.Main" --> "Units"

  "SPI.Linux" --> "SPI.Api"

  "Servo.Api" --> "Error.Api"
  "Servo.Api" --> "Units"

  "Servo.SG90" --> "Error.Api"
  "Servo.SG90" --> "PWM.Api"
  "Servo.SG90" --> "Servo.Api"

  "Units" --> "Exceptions"
```

## App And Test Edges

Dashed arrows represent non-library dependencies used only by apps or tests.

```mermaid
flowchart LR
  "Chipset" -.app.-> "Bq25792"
  "Chipset" -.app.-> "Chipset.Api"

  "Chipset.Client.I2C" -.app.-> "I2C.Linux"

  "Motor.Drv8908" -.app.-> "GPIO.Linux"
  "Motor.Drv8908" -.app.-> "SPI.Linux"

  "Servo.SG90" -.app.-> "PWM.Linux"
  "Servo.SG90" -.test.-> "PWM.Api"
```

## Per-Repository Summary

- `Bq25792`: `I2C.Api`, `RegUtils`, `Units`
- `Chipset`: app-only: `Bq25792`, `Chipset.Api`
- `Chipset.Api`: `Error.Api`, `RegUtils`, `Units`
- `Chipset.Client.I2C`: `Chipset.Api`, `Error.Api`, `I2C.Api`, `Time.Tickable.Api`; app-only: `I2C.Linux`
- `Chipset.Engineering`: `Bq25792`, `Max1726`
- `Drv8908`: `GPIO.Api`, `RegUtils`, `SPI.Api`, `Units`
- `Drv8908.Cli`: `Drv8908`, `GPIO.Linux`, `SPI.Linux`
- `Drv8908.PowerManager`: `Drv8908`
- `GPIO.Linux`: `GPIO.Api`
- `I2C.Api`: `Error.Api`
- `I2C.Linux`: `Error.Api`, `I2C.Api`
- `Max17261`: `I2C.Api`, `RegUtils`, `Units`
- `Motor.Bidirectional.Api`: `Units`
- `Motor.Drv8908`: `Drv8908`, `Drv8908.PowerManager`, `Motor`, `Motor.Bidirectional.Api`, `Motor.Telemetry.Api`, `Motor.Unidirectional.Api`, `Time.Tickable.Api`; app-only: `GPIO.Linux`, `SPI.Linux`
- `Motor.Unidirectional.Api`: `Units`
- `PWM.Api`: `Error.Api`, `Units`
- `PWM.Linux`: `Error.Api`, `PWM.Api`
- `RPi.Main`: `Chipset.Api`, `Drv8908`, `Max1726`, `RPi.Logging`, `Units`
- `SPI.Linux`: `SPI.Api`
- `Servo.Api`: `Error.Api`, `Units`
- `Servo.SG90`: `Error.Api`, `PWM.Api`, `Servo.Api`; app-only: `PWM.Linux`; test-only: `PWM.Api`
- `Units`: `Exceptions`

## Repositories With No Declared Internal PiSubmarine Dependencies

- `Error.Api`
- `Exceptions`
- `GPIO.Api`
- `ModuleTemplate`
- `Motor`
- `Motor.Telemetry.Api`
- `RPi.Logging`
- `SPI.Api`
- `Time.Tickable.Api`

## Notes

- `RPi.Main` and `Chipset.Engineering` currently reference `Max1726`, while the repository present in this workspace is `Max17261`. This may be a stale dependency name.
- The graph is based on declared build dependencies, not on include analysis or runtime composition.
