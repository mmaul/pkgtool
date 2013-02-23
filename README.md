NAME: pkgtool

DESCRIPTION: Packaging Management Tool

VERSION: .02

AUTHOR:  Mike Maul

PKG_URL: https://github.com/mmaul/pkgtool

CATEGORY: UTIL

LIBDIR: PKGTOOL
-----

PKGTOOL is what happens when a build system, a package manager and a test 
framework meet up at a bar and have a few too many drinks. Seriously though
pkgtool is a underlying framwork that contains the common aspects of the
different facets. As an aside the flx compiler frontend happend by at the bar 
towards the end and got in on the fun.

Specialization of the facets is presented to the user at the interface level.
Two user interfaces exist, the package manager ''scoop'' and the build framework 
SetupTool. The package manager ''scoop'' exists as an independant executable 
while SetupTool exists as a user implementable framework for package build 
management.

Features
=======

* Package build framework
* Package test framework
* Package installation framework
* Distributed remote package repository framework
* Distributed package management application
* Centeralized package directory
* Programatic frendly inter face to the flx compiler frontend.

Installation
============

Installation is simple because PkgTool uses pkgtool for build and installation.
All that is needed is:

    flx setup install

This will build the PkgTool executables and install the executables and library
components in in the Felix INSTALL_ROOT directory. The scoop executable is also
installed in the /usr/local/bin directory by default.  You will need sufficient access priviledges to write to INSTALL_ROOT and /usr/local/bin.
when runing this.

Packages
========
Packages exist as independant remote git repositories which conform to certain 
structure dependant on their function. There are three types of packages:

* Applications
* Libraries
* Web Applications

Each of the different package types exhibit certain common preferences that 
created the need for thir distinction.

* Applications have a need for one or more user executables
* Libraries hae a need to present one or more API interfaces
* Web Applications have a need to present one executable along with associated content

Usage
=====
## scoop - package manager 
Scoop is the user interface to to distributed package management aspect of
PkgTool.  

### Scoop commands are presented below:

    scoop get     [package]  Pull package from litterbox to current working directory
    scoop list               Lists all packages on litterbox
    scoop search  [package]  Searches for package on litterbox
    scoop info    [package]  Displays package info
    scoop install [package]  Pull, builds and install package
    scoop force   [package]  Pull, builds and install skipping tests phase
    scoop refresh            Refreshes litterbox package directory cache
    scoop help               Displays this message
    scoop help    [command]  Displays detailed help for command

### Scoop commands can be followed by options

    --litterbox-url=<remote repository>  Remote repository  containing package README.md's

    --litterbox=<location>               Location to create local package directory 
                                         repo if HOME/.felix/litterbox is unacceptable

    --degitify                           Remove .git directory from downloaded packages
    
    -L[C/C++ library paths]

    -I[C/C++ library paths]

    --dry-run                             Don't actuall install, but tell us where you would.





