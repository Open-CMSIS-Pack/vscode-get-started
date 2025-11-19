# Get started with Visual Studio Code

This repository contains an application that runs in simulation on an Arm Fixed Virtual Platform (Arm FVP) model. The
application prints "Hello World" and a counter value in the Terminal output window using semihosting.

## Quick start

1. Install [Keil Studio for VS Code](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) from the
   VS Code marketplace.
2. Clone this Git repository into a VS Code workspace.
3. The related tools and software packs are downloaded and installed. Review progress with
   *View - Output - CMSIS Solution*.
4. In the **CMSIS** view, use the
   [Action buttons](https://github.com/ARM-software/vscode-cmsis-csolution?tab=readme-ov-file#action-buttons) to build
   and run the example in simulation.

> [!NOTE]
> Other Arm Tools will be installed via [vcpkg](https://www.keil.arm.com/packages/). These are:
> - Models: [Arm Virtual Hardware for Cortex-M based on FastModels](https://www.keil.arm.com/packages/#models/arm/avh-fvp)
> - Toolchain: [Arm Compiler for Embedded](https://www.keil.arm.com/packages/#compilers/arm/armclang)
> - Debugger: [Arm Debugger](https://www.keil.arm.com/artifacts/#debuggers/arm/armdbg)

## Project structure

The project is written in
[`CSolution Project Format`](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/):

- The [`get_started.csolution.yml`](./get_started.csolution.yml) file lists and defines the required packs, target and
  build types, as welll as projects.
- The [`hello/hello.cproject.yml`](./hello/hello.cproject.yml) file defines components and source files.
- The [`vcpkg-configuration.json`](./vcpkg-configuration.json) file orchestrates the installation of all required tools
  locally or [in the cloud](#run-in-github-codespaces).

### Toolchain settings

The example is using the
[Arm Compiler for Embedded](https://developer.arm.com/dev2/Tools%20and%20Software/Arm%20Compiler%20for%20Embedded) as
the build toolchain. It is prepared to run on the
[Arm GNU Toolchain](https://developer.arm.com/dev2/Tools%20and%20Software/GNU%20Toolchain) and the
[Arm Toolchain for Embedded](https://developer.arm.com/dev2/Tools%20and%20Software/Arm%20Toolchain%20for%20Embedded) as
well. If you want to use one of these, do the following:

- Uncomment the `-compiler:` setting in the `get_started.csolution.yml` file.
- Add the compiler in the `vcpkg-configuration.json` file.
- Select the compiler once prompted.
- *Optional*: add the new compiler to the [build.yml](.github/workflows/build.yml) file to run automated tests.

## Build the solution

In the **CMSIS** view, use the build button (hammer icon) to build the solution. In the background,
[`cbuild`](https://open-cmsis-pack.github.io/cmsis-toolbox/build-tools/#cbuild-invocation) will be run:

```txt
Execute: cbuild /Users/user/vscode-get-started/get_started.csolution.yml --rebuild --active Corstone-300-FVP --packs
+-----------------------------------------------------
(1/1) Cleaning context: "hello.debug+Corstone-300-FVP"
+-----------------------------------------------------
(1/1) Building context: "hello.debug+Corstone-300-FVP"
Using AC6 V6.24.0 compiler, from: '/Users/user/.vcpkg/artifacts/2139c4c6/compilers.arm.armclang/6.24.0/bin/'
Building CMake target 'hello.debug+Corstone-300-FVP'
[1/20] Building C object CMakeFiles/Group_Source.dir/Users/user/vscode-get-started/hello/main.o
[2/20] Building C object CMakeFiles/ARM_CMSIS_OS_Tick_SysTick_1_0_5.dir/Users/user/.cache/arm/packs/ARM/CMSIS/6.1.0/CMSIS/RTOS2/Source/os_systick.o
[3/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_memory.o
[4/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_delay.o
[5/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_lib.o
[6/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_evr.o
[7/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_kernel.o
[8/20] Building ASM object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/GCC/irq_armv8mml.o
[9/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_evflags.o
[10/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_mempool.o
[11/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_mutex.o
[12/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_msgqueue.o
[13/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/vscode-get-started/hello/RTE/CMSIS/RTX_Config.o
[14/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_semaphore.o
[15/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_system.o
[16/20] Building C object CMakeFiles/ARM_Device_Startup_C_Startup_2_0_0.dir/Users/user/vscode-get-started/hello/RTE/Device/SSE-300-MPS3/system_SSE300MPS3.o
[17/20] Building C object CMakeFiles/ARM_Device_Startup_C_Startup_2_0_0.dir/Users/user/vscode-get-started/hello/RTE/Device/SSE-300-MPS3/startup_SSE300MPS3.o
[18/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_timer.o
[19/20] Building C object CMakeFiles/ARM_CMSIS_RTOS2_Keil_RTX5_Source_5_9_0.dir/Users/user/.cache/arm/packs/ARM/CMSIS-RTX/5.9.0/Source/rtx_thread.o
[20/20] Linking C executable /Users/user/vscode-get-started/out/hello/Corstone-300-FVP/debug/hello.axf
Program Size: Code=14030 RO-data=974 RW-data=188 ZI-data=29312  
+------------------------------------------------------------
Build summary: 1 succeeded, 0 failed - Time Elapsed: 00:00:02
+============================================================
Completed: cbuild succeed with exit code 0
Build complete
```

## Run in simulation

The project is configured for execution on the Corstone-300 Arm FVP running an Arm Cortex-M55 processor.
This model is available free-of-charge and removes the requirement for a physical hardware board. It can be used with
the [MDK-Community](https://keil.arm.com/mdk-community) edition.

In the **CMSIS** view, press the **Load & Run application** button (the play icon). In the background,
the following will be run:

```txt
 *  Executing task: FVP_Corstone_SSE-300 -f fvp-config.txt --simlimit 60 -a out/hello/Corstone-300-FVP/debug/hello.axf  

Info: FVP_MPS3_Corstone_SSE_300: telnetterminal0: Listening for serial connection on port 5000
Info: FVP_MPS3_Corstone_SSE_300: telnetterminal1: Listening for serial connection on port 5001
Info: FVP_MPS3_Corstone_SSE_300: telnetterminal2: Listening for serial connection on port 5002
Info: FVP_MPS3_Corstone_SSE_300: telnetterminal5: Listening for serial connection on port 5003

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

Info: Simulation is stopping. Reason: Simulated time has been exceeded.

Info: /OSCI/SystemC: Simulation stopped by user.
```

## Run in GitHub Codespaces

This repository is prepared to run in [GitHub Codespaces](https://github.com/features/codespaces), your development
environment in the cloud. This eliminated the necessity to install any tools on your local machine.

To start your Codespace through your browser, click on `<> Code`, switch to the **Codespaces** tab and select
**Create Codespace on main**. A new window opens and your environment will be set up. Allow a couple of minutes to
finish. If you reopen the Codespace later, it will be much faster.

Use the Codespace in the same way as you have done in the [Quick Start](#quick-start) chapter.
