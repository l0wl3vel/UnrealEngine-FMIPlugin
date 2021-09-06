# WIP: FMI-UE4: Execute Co-Simulation FMUs in UE4

- Cross-Platform (At least Win64 (Untested) and Linux64)
- Simulate Co-Simulation FMUs within the Unreal Engine environment.

- This MVP relies on the [FMIKit repositorty](https://github.com/CATIA-Systems/FMIKit-Simulink) (non-simulink portion)
- Special thanks to Torsten Sommer for his work on FMIKit!
- Architecture and some of the code (XML parser) based on: [ORNL-Modelica/UnrealEngine-FMIPlugin](https://github.com/ORNL-Modelica/UnrealEngine-FMIPlugin)

- Thanks to the Chair of Mechatronics at the University Augsburg, Germany for allowing me to work on this as a research project.

# Prerequistes

This work was tested using the following. It may work on something else but no gurantees.

- Arch Linux rolling (should not matter, since UE4 ships its own toolchain on linux)
- Unreal Engine 4.24 source build
- [ue4cli](https://github.com/adamrehn/ue4cli)
- [Conan UE4 Cli](https://github.com/adamrehn/conan-ue4cli) and l0wl3vels fork of [ue4-conan-recipes](https://github.com/l0wl3vel/ue4-conan-recipes)
- IDE: VS Code

# Installation

This repo contains the pre-compiled dependencies for UE4.24. For any other version you need to clone and build the dependencies libzip and elzip from [my ue4-conan-recipes fork](https://github.com/l0wl3vel/ue4-conan-recipes)

Follow the following steps to get this project up and running on your own computer.

- Download and unzip the folder into your desired location **OR** clone the repository.
- Generate VSCode project files :

  pathtoUE/GenerateProjectFiles.sh -projectfiles -project='pathto/UnrealEngine-FMIPlugin/FMIPlugin/FMIPlugin.uproject' -game -rocket -progress -VSCode

- Open the FMIPlugin/FMIPlugin.code-workspace in VS Code
- Press CTRL+Shift+P and select "Task: Run Build Task" and select "FMIPlugin Linux Development Build" **and** "FMIPluginEditor Linux Development Build"
- When the build finished successfully open the FMIPlugin.uproject in UE4 `cd ~/UnrealEngine_4.24/Engine/Binaries/Linux && ./UE4Editor`
- When warned about the engine version click on "more options" and "Convert in place" (This may take a while)

# Included FMUs

The Modelica files are included in the `Modelica` folder.

FMUs are generated using openmodelica 1.17.0 with modelica-4.0.0 with source code included, so a tool like [fmpy](https://github.com/CATIA-Systems/FMPy) can be used to easily recompile on other platforms.

- PT2.fmu
- Radaufhaengung.fmu: Wheel suspension with one point fixed (Did not get this to work)
- RadaufhaengungNeu.fmu: New different implementation of a wheel suspension

# Todo

- ~~Ship with Conan dependency prebuilts~~
- ~~Standalone Play does not work currently~~
- Implement distinctions for causality and variability for FMI variables
- Update documentation
- Write test cases
- ~~Support more variable types~~
- ~~Support multiple FMU instances~~
- Build better example projects
- ~~Better simulation parameter setup~~
- Validate Windows support
