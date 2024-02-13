# Visual Studio Code get started solution

This repository builds an ELF file that prints "GetStarted World" and a counter value via semihosting output on an Arm Virtual Hardware model (Cortex-M3).

## How to setup your CMSIS Csolution CLI Environment

Refer to the [installation guide of CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/installation.md#vcpkg---setup-using-cli).

## How to setup your CMSIS Csolution Development Environment

1. Download & Install [Microsoft Visual Studio Code](https://code.visualstudio.com/download) for your operating system.
2. Launch Visual Studio Code. From the 'View' menu open 'Extensions' (ctrl+shift+x). Search for "Keil Studio Pack" and select the install button.
3. From the 'View' menu open 'Source Control'. Select 'Clone Repository' and copy the url: https://github.com/Open-CMSIS-Pack/vscode-get-started into the input dialog
4. Specify the destination folder to clone to and select 'Open' when asked 'Would you like to open the cloned directory?'
5. Open the 'Explorer' view (ctrl-shift-e) and select the file 'vcpkg-configuration.json'. This file instructs [Microsoft vcpkg](https://github.com/microsoft/vcpkg-tool#vcpkg-artifacts) to install the prerequisite artifacts required for building the solution and puts it into the PATH: cmake, ninja, cmsis-toolbox as well as arm-none-eabi-gcc.
6. Open the 'CMSIS' view from the side bar and press the 'Build' button. The last line of the ninja build output will tell you where you can
find the application elf file. Alternatively you can select 'Build' or 'Rebuild' from the context menu of the `*.csolution.yml` file of the solution context
(e.g. get_started.csolution.yml) to build all contexts of the solution.

Note: Any terminal that is opened within VSCode after vcpkg got activated for the folder, will have all the above tools added to the path.
This allows you to run tools from the [CMSIS-Toolbox](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md) like:

- [`cpackget`](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md#cpackget-invocation) for installing and uninstalling CMSIS-Packs
- [`csolution`](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md#csolution-invocation) for updating, validating and converting from the CMSIS Project Management [YML input format](https://github.com/Open-CMSIS-Pack/devtools/blob/main/tools/projmgr/docs/Manual/YML-Input-Format.md#yaml-input-format)
  to the CMSIS Build [XML `cprj` format](https://open-cmsis-pack.github.io/devtools/buildmgr/latest/element_cprj.html) used by `cbuildgen`.
- [`cbuild`](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/build-tools.md#cbuild-invocation) for an orchestrated build of one or more `configurations` of a csolution.

## Additional Tools

- Other Arm Tools available via [vcpkg](https://www.keil.arm.com/packages/) e.g.:
  - Models: [Arm Virtual Hardware for Cortex-M based on FastModels](https://www.keil.arm.com/packages/#models/arm/avh-fvp)
  - Toolchain: [Arm Compiler for Embedded](https://www.keil.arm.com/packages/#compilers/arm/armclang)
  - Debugger: [Arm Debugger](https://www.keil.arm.com/artifacts/#debuggers/arm/armdbg)

## Project Structure

The project is written in the [`CMSIS-Toolbox Project Format`](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md):

- [`cdefault.yml`] is located in the ./etc directory of the CMSIS-Toolbox. It sets the default toolchain specific command line options for supported toolchains.
  In case a solution specific version is required, you can copy the file locally and it will be used by the tools instead.
- [`get_started.csolution.yml`](./get_started.csolution.yml) lists and defines the required packs, hardware targets, build-types and projects.
- [`hello/hello.cproject.yml`](./hello/hello.cproject.yml) defines components and source files.

## Build Solution/Project

Use the `cbuild` command from CMSIS-Toolbox to generate and build one or all configurations of the solution:

- find out which `contexts` are specified by the solution:

  ```bash
  cbuild list contexts get_started.csolution.yml
  hello.debug+avh
  hello.release+avh
  ```

- build the context `hello.debug+avh` and install the required CMSIS Packs if not installed:

  ```bash
  cbuild get_started.csolution.yml --packs --update-rte --context hello.debug+avh
  info cbuild: Build Invocation 2.2.1 (C) 2023 Arm Ltd. and Contributors
  /tmp/vscode-get-started/get_started.cbuild-idx.yml - info csolution: file generated successfully
  /tmp/vscode-get-started/hello/hello.debug+avh.cbuild.yml - info csolution: file generated successfully
  /tmp/vscode-get-started/get_started.cbuild-pack.yml - info csolution: file is already up-to-date
  /tmp/vscode-get-started/hello/hello.debug+avh.cprj - info csolution: file generated successfully
  info cbuild: Processing 1 context(s)
  info cbuild: Retrieve build information for context: "hello.debug+avh"
  ======================================================
  info cbuild: (1/1) Building context: "hello.debug+avh"

  M650: Command completed successfully.

  M652: Generated file for project build: '/tmp/vscode-get-started/tmp/hello/avh/debug/CMakeLists.txt'
  :
  info cbuild: build finished successfully!
  ```

- build the configuration `.debug+avh` using Arm Compiler 6 (AC6)
  Add the Arm Compiler for Embedded 6 e.g. via vcpkg (`vcpkg use armclang`) and rebuild the context specifying
  `--rebuild` and the required compiler `--toolchain AC6`:

  ```bash
  cbuild get_started.csolution.yml --context .debug+avh --packs --update-rte --rebuild --toolchain AC6
  ```

## Execute Project

The project is configured for execution on Arm Virtual Hardware (AVH) modelling an MPS2 board running an Arm Cortex-M3 processor.
This model is part of the MDK Professional Edition and removes the requirement for a physical hardware board. It *DOES NOT WORK* with the 
MDK Community Edition.

Note: depending on the toolchain used the extension of the application file is either `elf` (GCC, Clang) or `axf` (AC6):

```bash
FVP_MPS2_Cortex-M3 -f vht-config.txt -a out/hello/avh/debug/hello.axf
```
