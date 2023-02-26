# Visual Studio Code get started solution
This repository builds an ELF file that prints "GetStarted World" and a counter value via semihosting output on an Arm Virtual Hardware model (Cortex-M3).

## How to setup your CMSIS Csolution Development Environment:
1. Download & Install [Microsoft Visual Studio Code](https://code.visualstudio.com/download) for your operating system.
2. Launch Visual Studio Code. From the 'View' menu open 'Extensions' (ctrl+shift+x). Search for "Keil Studio Pack" and select the install button.
3. From the 'View' menu open 'Source Control'. Select 'Clone Repository' and copy the url: https://github.com/Open-CMSIS-Pack/vscode-get-started into the input dialog
4. Specify the destination folder to clone to and select 'Open' when asked 'Would you like to open the cloned directory?'
5. Open the 'Explorer' view (ctrl-shift-e) and select the file 'vcpkg-configuration.json'. This file instructs [Microsoft vcpkg](https://github.com/microsoft/vcpkg-tool#vcpkg-artifacts) to install the prerequisite artifacts required for building the solution.
  - ctools 1.5.0  (CMSIS-Toolbox)
  - cmake 3.24.2
  - ninja 1.10.2
  - arm-none-eabi-gcc 10.3.1-2021.10 (GNU Arm Embedded Toolchain 10.3.1)
6. In case vcpkg shows an error in the VSCode status bar, you can see furth information in the "OUTPUT" for 'vcpkg'.
In case of 'Error: Unable to resolve dpendency ... in <registry>' you may need to update the registry by running 'vcpkg: Run vcpkg command'
from the 'View' menu's 'Command Palette...' (ctrl+shift+p) typing: `z-ce update <registry>`. 
7. Open the 'CMSIS' view from the side bar and press the 'Build' button. The last line of the ninja build output will tell you where you can
find the application elf file.

Note: Any terminal that is openened after vcpkg got activated for the folder, will have the above tools set in the path. This allows you to run tools
from the [CMSIS-Toolbox]( like cbuild, cpackget, csolution, etc. manually 
   
## Additional Tools
- [Keil MDK 5.38a](https://www2.keil.com/mdk5/) or later
  - VHT_MPS2_Cortex-M3: Arm Virtual Hardware for Cortex-M3 (v11.19.23 - Windows only - requires MDK-Professional license)
  - Arm Compiler 6.19 (part of MDK, Eval and Community Edition are sufficient for building the solution)
    - set environment variable AC6_TOOLCHAIN_6_19_0 to point to the bin directory of the installed toolchain to register the Arm Compiler 6.

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
