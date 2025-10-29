# Visual Studio Code get started solution

The example in this repository builds an ELF file that prints "Hello World" and a counter value via semihosting output on an Arm Virtual Hardware model (Cortex-M3).

## Quick Start

1. Install [Keil Studio for VS Code](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) from the VS Code marketplace.
2. In VS Code, either clone this Git repository or (if downloaded as ZIP file) open the top-level folder.
3. Open the [CMSIS View](https://mdk-packs.github.io/vscode-cmsis-solution-docs/userinterface.html#2-main-area-of-the-cmsis-view) in VS Code and use the ... menu to choose an example via Select Active Solution from workspace.
4. The related tools and software packs are downloaded and installed. Review progress with View - Output - CMSIS Solution.
5. In the CMSIS view, use the [Action buttons](https://github.com/ARM-software/vscode-cmsis-csolution?tab=readme-ov-file#action-buttons) to build and run the example on the FVP model.

## Project Structure

The project is written in the [`CMSIS-Toolbox Project Format`](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md):

- [`cdefault.yml`] is located in the root directory of this repository. It sets the default toolchain specific command line options for supported toolchains.
- [`get_started.csolution.yml`](./get_started.csolution.yml) lists and defines the required packs, hardware targets, build-types and projects.
- [`hello/hello.cproject.yml`](./hello/hello.cproject.yml) defines components and source files.

## Build Solution/Project

In the CMSIS view, click the `Manage Solution Settings` button to open the Manage Solution GUI to verify the selected active Target Type and Build Type for the example project. Then, click on the `Build Solution` button to build the project.

## Execute Project

The project is configured for execution on an Arm MPS2 Cortex-M3 FVP model using Arm CMSIS Debugger extension.
This model is part of the MDK Professional Edition and removes the requirement for a physical hardware board. It *DOES NOT WORK* with the 
MDK Community Edition.

In the CMSIS view, click the `Manage Solution Settings` button to open the Manage Solution GUI. Under **Debug Adapter for avh** select `Arm-FVP` as the debug adapter. In the **Config File** field click `Select` to select the fvp-config.txt file from the root directory of this repository. Then, click on **Save** to save the debug configuration.

Finally, in the CMSIS view, click the ´Load & Run application` button to start the execution of the example application running on the Arm MPS2 Cortex-M3 FVP model. 

In the Terminal window of VS Code, you should be able to see the semihosting output from the the Arm MPS2 Cortex-M3 FVP model
```
Info: FVP_MPS2_Cortex_M3: telnetterminal0: Listening for serial connection on port 5000

Info: FVP_MPS2_Cortex_M3: telnetterminal2: Listening for serial connection on port 5001

Info: FVP_MPS2_Cortex_M3: telnetterminal1: Listening for serial connection on port 5002
Hello World 0
Hello World 1
Hello World 2
Hello World 3
Hello World 4
Hello World 5
Hello World 6
Hello World 7
Hello World 8
Hello World 9
Hello World 10
Hello World 11
...
Hello World 96
Hello World 97
Hello World 98
Hello World 99

Info: /OSCI/SystemC: Simulation stopped by user.
 *  Terminal will be reused by tasks, press any key to close it.
```
