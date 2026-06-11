..
   # *******************************************************************************
   # Copyright (c) 2026 Contributors to the Eclipse Foundation
   #
   # See the NOTICE file(s) distributed with this work for additional
   # information regarding copyright ownership.
   #
   # This program and the accompanying materials are made available under the
   # terms of the Apache License Version 2.0 which is available at
   # https://www.apache.org/licenses/LICENSE-2.0
   #
   # SPDX-License-Identifier: Apache-2.0
   #
   # Contributors:
   #   Thomas Pfleiderer - added getting started
   # *******************************************************************************

Getting started 
===============

Dependencies
------------

1. The VSS GUI tool runs in Ubuntu (tested in Ubuntu 22.04). 

2. The GUI tool is based on Python (tested in v3.10) and the following libraries: 

    - Tkinter 
    - Anytree
    - Pyyaml 
    - Screeninfo

3. The GUI tool is also dependent on the .vspec files defined in the <a href="https://github.com/COVESA/vehicle_signal_specification">Vehicle Signal Specification</a> repository and the corresponding <a href="https://github.com/COVESA/vss-tools">VSS-tools</a> repository. 

Structure of the repository 
---------------------------

1. [container](./container) - Contains the Docker recipe for building and running the GUI environment. 
2. [scripts](./scripts) - Contains the Python GUI scripts and the VSS submodule. 
3. [docs](./docs) - Contains the Sphinx documentation for the project. 

Running the GUI locally 
-----------------------

1. Update the submodules linked to the repository:
   - `git submodule update --init --recursive`
  
2. Create and activate a Python virtual environment:
   
   - `python3 -m venv .venv`
   - `source .venv/bin/activate`
  
3. Install the required Python packages:
   
   - `pip install --upgrade pip`
   - `pip install anytree PyYAML screeninfo graphql-core`
  
4. Start the GUI script:
   
   - `.venv/bin/python scripts/gui/vss_gui.py`

Running the GUI in Docker 
-------------------------

1. Update the repository submodules:
   - `git submodule update --init --recursive`
2. Build the container image:
   - `cd container`
   - `./build.sh`
3. Run the container with X11 forwarding enabled:
   - `docker run -ti -e DISPLAY=$(hostname).local:0 -it vss_gui:latest`
4. Inside the running container, start the GUI:
   - `python /app/gui/vss_gui.py`

Notes 
-----

- The GUI depends on the `scripts/vss` submodule from the Vehicle Signal Specification repository and the `vss-tools` package contained therein.
- The local Docker setup already installs `python3-tk`, so the GUI can run with Tkinter support.

Dependencies to other repositories
----------------------------------

This tool can be used in combination with application framework: https://github.com/eclipse-autoapiframework/application-framework
