# RobotCANControl Project

RobotCANcontrol is a free and open source robotic development software stack. The project has been under development at the University of Melbourne in partnership with Fourier Intelligence for use with their X2 exoskeleton. The software has been designed to be extensible to any embeeded linux and CANopen enabled Robotic platform.

---

NOTE: This version of the software has only been tested virtually, further hardware testing is required.
This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

## The RobotCANcontrol project is made up of:

- Extensible Framework to represent most multi body robotic systems.
- Event driven State machine to develop custom applications for your Robot.
- Implementation of [Canopen Socket](https://github.com/CANopenNode/CANopenSocket) to provide an interface between CAN enabled embedded linux system and Canopen configured motor drivers/sensors.
- Documentation
- Fully functional application examples.

## Getting started with RobotCANControl

We will be running through building and testing a simple test statemachine (ExoTestMachine.cpp), the source code can be found in the apps folder of the root directory.

The current recommened and tested environemnt is Debian jesse 9.5 on a Beagle Bone black [Firmware](http://beagleboard.org/latest-images). Theoretically, we can build on other distros and linux platforms as well, but they have not been testd.

Workbench build environments for most platforms can be found [here](https://embeded.readthedocs.io/en/latest/workbench/)

### How to get the Project

Clone the project and CANopenSocket from git repository(CANopenSocket used in robot homing sequence):

    $ git clone https://github.com/capstonealex/exo.git

### Build ExoTestMachine

    $ cd /GitHub/exo/
    $ make exe

### Transfer files to Linux platform

- Download [FileZilla](https://filezilla-project.org/) and connect to Beagle bone.

  > Username: debian

  > Password: temppwd

  > Transfer executible and initRobot folders.

## Run Virtual ExoTestMachine

- SSH into Beagle Bone ([tutorial](https://elinux.org/Beagleboard:Terminal_Shells)) or similar linux board, use same user and pswrd as above.
- Initialize Virutal CAN device to bind to and run candump([candump manpage](https://manpages.debian.org/testing/can-utils/candump.1.en.html)) on the VCAN interface.

```bash
  cd initRobot
  ./initVCAN
```

- Launch second instance of terminal and ssh into device to Launch application

```bash
  cd build
  sudo ./EXO_APP
```

- Terminal one should display CAN message output on VCAN from our EXO_APP application output. On startup init PDO messaging should be sent and appear as follows:

```bash
vcan0 704 [1] 00
vcan0 184 [2] 00 00 # PDO message
vcan0 704 [1] 05
```

Follow terminal instructions using your keyboard to run through test stateMachine.

```bash
==================================
 WELCOME TO THE TEST STATE MACHINE
==================================
==================================
 PRESS S to start program
==================================

```

Notice that terminal one(candump) sends out messages coresponding with application movement commands as follows:

```bash
vcan0  601   [8]  2F 60 60 00 01 00 00 00 #initi position control SDO
vcan0  764   [1]  05
vcan0  601   [8]  80 60 60 00 00 00 04 05 #initi position control SDO
```

<!-- ## Run ExoTestMachine on X2

Running on the X2 Robot is very similar to the virutal CAN set up, with one adjustment and -->

<!-- ### TODO: Event Driven State machine
explain me -->

## Developer Information

- Detailed Documentation: https://exoembedded.readthedocs.io/en/latest/
- Source code documenrtation: https://capstonealex.github.io/exo/index.html
- Project Repository: https://github.com/capstonealex/exo
- CanOpen Socket: https://github.com/CANopenNode/CANopenSocket

## License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

<!-- ## Maintainers -->
