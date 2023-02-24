# GetStarted project

This project prints "GetStarted World" and a counter value via semihosting output. It is configured for Arm Virtual Hardware (Cortex-M3).

## Prerequisites

### Tools

- [CMSIS-Toolbox 1.5.0](https://github.com/Open-CMSIS-Pack/devtools/releases) or later
- [GNU Arm Embedded Toolchain 10.3.1](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) or later
- [Keil MDK 5.38a](https://www2.keil.com/mdk5/) or later
  - Arm Compiler 6.18 (part of MDK, Eval Version sufficient for compilation)
  - Arm Virtual Hardware for Cortex-M55 v11.18.1 (requires MDK - Professional)

### Packs

Required packs are listed in the file [`get_started.csolution.yml`](./get_started.csolution.yml)

## Project Structure

The project is generated using the [CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/Overview.md) and is defined in [`csolution`](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/YML-Format.md) format:

- [`get_started.csolution.yml`](./get_started.csolution.yml) lists the required packs and defines the hardware target and build-types (along with the compiler).
- [`hello/hello.cproject.yml`](./hello/hello.cproject.yml) defines the source files and the project.

## Build Solution/Project

Use the `cbuild` command from CMSIS-Toolbox to generate and build one or all configurations of the solution:

```bash
./ $ cbuild get_started.csolution.yml --packs --configuration .debug+vht

info cbuild: Build Invocation 1.5.0 (C) 2023 Arm Ltd. and Contributors
ARM::CMSIS
 :
info cbuild: Building context: "hello.debug+vht"
================================================

M650: Command completed successfully.

M652: Generated file for project build: 'hello/tmp/hello/debug/vht/CMakeLists.txt'
 :
info cbuild: build finished successfully!
```

> **Note:** During the build process required packs may be downloaded.

## Execute Project

The project is configured for execution on Arm Virtual Hardware which removes the requirement for a physical hardware board.

```bash
./ $ VHT_MPS2_Cortex-M3 -f vht-config.txt -a hello/out/hello/debug/vht/debug+vht.elf
```
