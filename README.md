# Metis installation on Windows: The Epic Battle Guide

Before we start, make sure you’ve got these tools in your inventory:

- **CMake (with CMake GUI)**
- **Visual Studio**
- **Git**

### First things first, clone these two repos:

```bash
git clone https://github.com/KarypisLab/METIS.git
git clone https://github.com/KarypisLab/GKlib.git
```

### Tame the right hand of our beast - GKlib

1. I am no terminal nerd, so let’s do this the easy way - via CMake GUI. Set your source directory to the `GKlib` folder and create a new build directory (`GKlib-build`) to hold the cmake build files

2. Hit the `Configure` button and let CMake do its thing. When it asks for your Visual Studio version, make sure you don’t accidentally choose the wrong one—this is no time for mindless fumbles.

3. With configuration done, click `Generate`. This will prepare your solution files for the next step.

4. Double-click that `GKlib.sln` file like it owes you money. Visual Studio will open, ready for action.

5. In Visual Studio, select `ALL_BUILD` and give it the command to build. Watch as it compiles with utmost anxiety.

6. Install Project? More Like Install Fail:( When you try to build the `INSTALL` project, it’ll likely throw a tantrum.) Don’t stress! We’ll do this the old-fashioned way. Create a new directory named `GKlib-install` with the following structure:

   ```plaintext
   GKlib-install
   ├── include
   └── lib
   ```
   - Drag and drop all the header files from the `GKlib` directory into `include` folder.
   - Copy `GKlib.lib` from `GKlib-build/Release/` into the `lib` folder.

And just like that, GKlib is tamed and ready to serve!

### Tame the Beast – Metis

1. Before even thinking about touching CMake, run that `vsgen.bat` file lurking in the Metis directory. It’ll prepare some directories that cmake needs.

2. Point CMake to the Metis source directory, and prepare another build directory (`METIS-build`). 

3.  Make sure to set these CMake Flags or else prepare yourself for 584 errors glaring at you.
   - `shared=1`
   - `gklib_path=[THE PATH TO THE GKLIB INSTALL DIR YOU SLAVED OVER]`
   - `i64=1` 
   - `r64=1` 

4. Once those flags are in place, hit `Configure`, choose your Visual Studio version, and `Generate` the files.

5. If the build screams at you about `mpmetis.c:191`, `gpmetis.c:242`, or `ndmetis.c:175`, it’s time to show it who’s boss. Change `#ifndef MACOS` to `#if !defined(MACOS) && !defined(WIN32)`. No more complaints after this!

6. With the errors squashed, command Visual Studio to build the Metis project.

7. Make a new directory called `Metis-install` with this layout:

   ```plaintext
   Metis-install
   ├── include
   └── lib
   ```
   - Drop all Metis header files into `include`.
   - Copy `metis.lib` from `METIS-build/Release/` and stash it in `lib`.

## Victory!

Congratulations! You’ve successfully installed Metis on Windows and lived to tell the tale. Your GKlib and Metis libraries are ready to rock. Now go forth and conquer your projects with these mighty tools in hand!
