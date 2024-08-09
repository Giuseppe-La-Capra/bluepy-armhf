bluepy-armhf
======

This is a project to provide the bluepy python package to armhf boards like the STM32MP157F-DK2

This package requires the setup of a cross-compile enviroment in order to cross-compile the C files
for the armhf architecture. Once done you can install the bluepy package to the board.

NOTE: this was tested working on Debian 12.6, on Ubuntu 24.04 I was unable to set up the cross-compile env
    due to missing packages in the ubuntu repositories.
    
Cross-Compiler Setup
------------

add a new architecture to dpkg
    $ dpkg --add-architecture armhf
update apt
    $ sudo apt update
install the cross-compiler
    $ sudo apt install crossbuild-essential-armhf
install the needed armhf lib
    $ sudo apt install libglib2.0-dev:armhf

Installation
------------

The code needs an executable `bluepy-helper` to be compiled from C source. This needs to be done
with the cross-compiler. 
Once the .o file has beeen created, the entire project can be moved to the arm board where the 
python package can be installed.

    $ git clone https://github.com/Giuseppe-La-Capra/bluepy-armhf.git
    $ cd bluepy-armhf
    $ python3 setup.py build

Note that the makefile is hard coded to get the right libs.
Check the CPPFLAGS in the makefile if you have problems with lib header files.
The makefile is also hardcoded to use the arm-linux-gnueabihf-gcc cross-compiler.

Now move the entire bluepy-armhf directory to the ARM board where you would like to install the 
bluepy python package.

    $ cd bluepy-armhf
    $ python3 setup.py install
    
