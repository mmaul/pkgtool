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
different facets. As an aside the flx compiler API interface happend by at 
the bar towards the end and got in on the fun.

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
installed in the /usr/local/bin directory by default.  You will need sufficient 
access priviledges to write to INSTALL_ROOT and /usr/local/bin. when runing this.

Package Management
==================
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

Independant package repositories are usless if you don't know where they are, and even if you do
it's inconvient. Which is why the ''litterbox'' central package index exists. Litterbox contains 
the package README.md in side a directory for each package. Litterbox is self is housed is a remote 
git repository on github.com. One particularly nice feature is the packages are easly browsable simple
by going to the the litterbox repositirey with a web browser and being able to access the package README.md's
with few clicks. The other nice thing is there is no seperate package meta-data. THe package meta-data is 
contained at the top of the package README.md. In fact you can see the package metadata for PkgTool simply by 
looking at the top of this file.

scoop - package manager
=====
Scoop is the user interface to to distributed package management aspect ofPkgTool. Scoop allows you to view the
contents of the litterbox package index, get and install packages from remote git repositories.

### Scoop commands are presented below:

    scoop refresh            <options> Refreshes litterbox package directory cache
    scoop list               <options> Lists all packages on litterbox
    scoop search  <package>  <options> Searches for package on litterbox
    scoop info    <package>  <options> Displays package info
    scoop get     <package>  <options> [destination]Pull package from litterbox to current working directory
    scoop install <package>  <options> Pull, builds and install package
    scoop help    [command]  <options> Displays detailed help for command

### Scoop commands can be followed by options

    --litterbox-url=<remote repository>  Remote package directory

    --litterbox=<location>               Location to create local package directory 
                                         repo if HOME/.felix/litterbox is unacceptable

    --degitify                           Remove .git directory from downloaded packages
    
    --force                              Proceed with installation even if tests fail
    
    -L[C/C++ library paths]              Supply additional C/C++ include paths

    -I[C/C++ library paths]              Supply sdditional C/C++ library paths

    --dry-run                             Don't actuall install, but tell us where you would.


### Environmental Variables ###
    LITTERBOX= Location to create local package directory repo if HOME/.felix/litterbox is unacceptable
    LITTERBOX_URL=  Remote package directory


SetupTool - Build and Testing Framework
=======================================
So one can write programs with out build and test frameworks just fine. But if you want to share your software
with others it really helps to have a build and test framework. If there is something wrong you can fix it, if you
need to move an executable to some location or other you can do it. Once your code has gone out into the world
you can't. That is why a test framework can shake out problems that might surface after release. A build frame
work while it does make it easier to automate your builds, makes it easier for other people to build your code, or 
easier for you to assemble binary or source distributions.

SetupTool it PkgTool's solution to this. SetupTool is presented to the user as a Felix source file called 
''setup.flx'' located in the top level of the package directory. This is used to instantiate the build system and
allow for user customizations to the build system. If you are note deviating from the standard behaviors your
setup.flx file can be quite small. Below is a minimum setup.flx
  include "PKGTOOL/pkgtool";
  BUILD_LIKE = App;
  SetupTool::run();
That is all you need to build a Felix Application with Setup tool. What does that actually do for you?
Profiding you are conforming to the App directory structure for your project it wil:
* Compile all felix source in the bin directory to a static binary executable
* Execute tests source located in the test directory report the results and stop the build on errors.
* Allow you to install your application to the file system 
* Allow you to create a binary distribution



### SetupTool commands are presented below:

    flx setup build    [options]      performs config and build tasks
    flx setup test     [options]      performs config, build and test tasks
    flx setup install  [options]      performs config, build, test and install tasks
    flx setup dist     [options]      performs config, build, test and install to the dist directory
    flx setup force    [options]      performs config, build and install tasks
    flx setup info     [options]      will display package information
    flx setup clean    [options]      will delete generated files
    flx setup degitify [options]      removes git info from package dir
    flx setup help     [command]      will display detailed help for command

### Scoop commands can be followed by options
    --degitify                           Remove .git directory from downloaded packages
    
    --force                              Proceed with installation even if tests fail
    
    -L[C/C++ library paths]              Supply additional C/C++ include paths

    -I[C/C++ library paths]              Supply sdditional C/C++ library paths

    --dry-run                             Don't actuall install, but tell us where you would.
