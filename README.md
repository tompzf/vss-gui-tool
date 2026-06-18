# Notes
## Documentation Generation

This repository supports documentation generation using the [Eclipse S-CORE Docs-As-Code](https://eclipse-score.github.io/docs-as-code) approach. For more information and guidance, visit the official docs-as-code site.

## Dev Container Usage

This repository provides a pre-configured development container [Eclipse S-CORE DevContainer](https://github.com/eclipse-score/devcontainer) for a consistent and reproducible development environment. To use the dev container:

1. Open the project in Visual Studio Code.
2. Install the "Dev Containers" extension if not already installed.
3. Edit Line 7 in file `.devcontainer/prepare_workspace.sh`. Do not check in this change.
4. Open the Command Palette (Shift + Ctrl + P) and select “Dev Containers: Rebuild and Reopen in Container”.
5. Lower left corner: `Dev Container: eclipse-s-core` should be visible.
6. Run `bazel run //:live_preview` in terminal to create the documentation in folder `_build`.

The dev container automatically prepares the workspace, including CA bundle setup and system trust updates if configured. See `.devcontainer/prepare_workspace.sh` for details.


# Introduction 
This repository contains the GUI tool for the selection and addition of signals to the Vehicle Signal Specification (VSS). The tool is used to select signals (data or parameters) from hundreds of signals defined in VSS bassed on the requirements of an application. 

# Getting started 
## Dependencies 
1. The VSS GUI tool runs in Ubuntu (tested in Ubuntu 22.04). 
2. The GUI tool is based on Python (tested in v3.10) and the following libraries: 
    - Tkinter 
    - Anytree
    - Pyyaml 
    - Screeninfo
3. The GUI tool is also dependent on the .vspec files defined in the <a href="https://github.com/COVESA/vehicle_signal_specification">Vehicle Signal Specification</a> repository and the corresponding <a href="https://github.com/COVESA/vss-tools">VSS-tools</a> repository. 

## Structure of the repository 
1. [container](./container) - Contains the Docker recipe for building and running the GUI environment. 
2. [scripts](./scripts) - Contains the Python GUI scripts and the VSS submodule. 
3. [docs](./docs) - Contains the Sphinx documentation for the project. 

## Running the GUI locally on Linux
1. Update the submodules linked to the repository:
   - `git submodule update --init --recursive`
2. Create and activate a Python virtual environment:
   - `python3 -m venv .venv`
   - `source .venv/bin/activate`
3. Install the required Python packages:
   - `pip install --upgrade pip`
   - `pip install anytree PyYAML screeninfo graphql-core`
4. You can go to 5 and start the GUI, in case python3-tk is missing:
   - `sudo apt install python3-tk`   
5. Start the GUI script:
   - `.venv/bin/python scripts/gui/vss_gui.py`

## Running the GUI locally on windows
1. Update the submodules linked to the repository:
   - `git submodule update --init --recursive`
2. Create and activate a Python virtual environment:
   - `python3 -m venv .venv`
   - `.venv\bin\activate`
3. Install the required Python packages:
   - `pip install --upgrade pip`
   - `pip install anytree PyYAML screeninfo graphql-core`
4. You can go to 5 and start the GUI, in case python3-tk is missing:
   - `sudo apt install python3-tk`   
5. Start the GUI script:
   - `.venv\bin\python scripts\gui\vss_gui.py`   

## Running the GUI in Docker 
1. Update the repository submodules:
   - `git submodule update --init --recursive`
2. Build the container image:
   - `cd container`
   - `./build.sh`
3. Run the container with X11 forwarding enabled:
   - `docker run -ti -e DISPLAY=$(hostname).local:0 -it vss_gui:latest`
4. Inside the running container, start the GUI:
   - `python /app/gui/vss_gui.py`

## Notes 
- The GUI depends on the `scripts/vss` submodule from the Vehicle Signal Specification repository and the `vss-tools` package contained therein.
- The local Docker setup already installs `python3-tk`, so the GUI can run with Tkinter support.

## Dependencies to other repositories
This tool can be used in combination with application framework: https://github.com/eclipse-autoapiframework/application-framework
