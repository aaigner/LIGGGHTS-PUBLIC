```
----------------------------------------------------------------------
This is the

██╗     ██╗ ██████╗  ██████╗  ██████╗ ██╗  ██╗████████╗███████╗
██║     ██║██╔════╝ ██╔════╝ ██╔════╝ ██║  ██║╚══██╔══╝██╔════╝
██║     ██║██║  ███╗██║  ███╗██║  ███╗███████║   ██║   ███████╗
██║     ██║██║   ██║██║   ██║██║   ██║██╔══██║   ██║   ╚════██║
███████╗██║╚██████╔╝╚██████╔╝╚██████╔╝██║  ██║   ██║   ███████║
╚══════╝╚═╝ ╚═════╝  ╚═════╝  ╚═════╝ ╚═╝  ╚═╝   ╚═╝   ╚══════╝®

DEM simulation engine, released by 
DCS Computing Gmbh, Linz, Austria
www.dcs-computing.com, office@dcs-computing.com

LIGGGHTS® is open-source, distributed under the terms of the GNU Public 
License, version 2 or later.

LIGGGHTS® is part of CFDEM®project: 
www.liggghts.com | www.cfdem.com

Core developer and main author:
Christoph Kloss, christoph.kloss@dcs-computing.com

LIGGGHTS® and CFDEM® are registered trade marks of DCS Computing GmbH, 
the producer of the LIGGGHTS® software and the CFDEM®coupling software
See http://www.cfdem.com/terms-trademark-policy for details.

----------------------------------------------------------------------
Copyright 2012-     DCS Computing GmbH, Linz
Copyright 2009-2015 JKU Linz
Some parts of LIGGGHTS® are based on LAMMPS and Copyright on these
parts is held by Sandia Corporation and other parties. Info on LAMMPS below
Some parts of LIGGGHTS® are contributied by other parties, which are
holding the Copyright. This is listed in each file of the distribution.
----------------------------------------------------------------------

The LIGGGHTS® distribution includes the following files and directories:

README          this file
LICENSE         the GNU General Public License (GPL)
doc             documentation
examples        simple example simulation setups
lib             libraries LIGGGHTS® can be linked with
python          Python wrapper on LIGGGHTS® as a library
src             source files

Point your browser at any of these files to get started:

doc/Manual.html	           the manual
doc/Section_intro.html	   hi-level introductio
doc/Section_start.html	   how to build and use

----------------------------------------------------------------------

Some parts of LIGGGHTS® are based on LAMMPS
LAMMPS stands for Large-scale Atomic/Molecular Massively Parallel
Simulator. 

LAMMPS is Copyright (2003) Sandia Corporation.  Under the terms of Contract
DE-AC04-94AL85000 with Sandia Corporation, the U.S. Government retains
certain rights in this software.  This software is distributed under
the GNU General Public License.

LAMMPS is a classical molecular dynamics simulation code designed to
run efficiently on parallel computers.  It was developed at Sandia
National Laboratories, a US Department of Energy facility, with
funding from the DOE.  It is an open-source code, distributed freely
under the terms of the GNU Public License (GPL).

The primary author of LAMMPS is Steve Plimpton, who can be emailed
at sjplimp@sandia.gov.  The LAMMPS WWW Site at lammps.sandia.gov has
more information about the code and its uses.

```

# LIGGGHTS under WINDOWS

This fork of the LIGGGHTS software package is **my working fork** for a compilation under Windows.
It uses the original LIGGGHTS-PUBLIC and some input from the LIGGGHTS-PUBLIC fork of ParticulateFlow.

**Table of Contents:**

* [Prerequisites](#prerequisites)
* [Installation](#installation)
  * [CMake Compilation](#cmake-compilation)
  * [Classic Compilation (discouraged)](#classic-compilation)
* [Using Binaries created with CMake](#using-cmake-binaries)
  
----------------------------------------------------------------------

<a name="prerequisites"></a>

## Prerequisites

* A C++11 and OpenMP >= 3 compliant compiler (e.g. GCC 4.8)

For Windows:
* Visual Studio (tested with VS 2015)
* for parallel computation [MS MPI](https://msdn.microsoft.com/en-us/library/bb524831%28v=vs.85%29.aspx)
* [Cygwin](https://www.cygwin.com/) with GIT and CMAKE package
* Any git tool, e.g. [git-for-windows](https://git-for-windows.github.io/)
    * Take care that you checkout **as-is** and push **unix-style**.
	  The shell-scripts that are necessary for compilation work only with unix-style line endings!

<a name="installation"></a>

## Installation

There are two ways of compiling this LIGGGHTS version. The classic method of using a
customized Makefile and a newer (recommended) way of using CMake.

<a name="cmake-compilation"></a>

### CMake Compilation
The benefit of using CMake is that it works on more platforms and it can automatically
detect the paths of required libraries. E.g. on Linux it will find the VTK library if
it is installed:

1. Configure using CMake (in the terminal or cygwin)

	```bash
	mkdir src-build
  cd src-build
  cmake ../src
	```

#### Windows

2. Compile using Visual Studio

    Open the visual studio file that was generated in your build directory (src-build).
	Change the build to RELEASE and build the whole project map. This will generate the 
	executable `liggghts.exe` in your build directory.

#### Linux

2. Compile using Make

	Serial compilation:
	```bash
	make
	```

	Parallel compilation (e.g. 4 processes):
	```bash
	make -j 4
	```
	
	Note that unlike the LIGGGHTS-PUBLIC fork of ParticulateFlow, this will create
	again one big binary file `liggghts`, because the required code change for Windows would be to big (annoying ;) ) .
	
3. Installation (optional)

	To install the generated LIGGGHTS binary to a specific location,
	an installation prefix can be defined during CMake configuration. E.g.

	```bash
	cmake ../src -DCMAKE_INSTALL_PREFIX=/opt/liggghts/
	```
	Using this configuration, compile using make and install to the target location using

	```bash
	make install
	```

<a name="classic-compilation"></a>

### Classic Compilation (discouraged - Linux only)

The classic LIGGGHTS Makefile "ubuntu" still works to compile LIGGGHTS.
This will create one large binary called `lmp_ubuntu`. Before compilation
the file `MAKE/Makefile.ubuntu` has to be edited manually to correct any library
installation paths.

```bash
cd src
make ubuntu
```
----------------------------------------------------------------------

Core developer and main author of LIGGGHTS®:
Christoph Kloss, christoph.kloss@dcs-computing.com
