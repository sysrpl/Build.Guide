# Build.Guide

This document is a guide to building certain C language projects.

## NanoVG

NanoVG is a cross platform 2D vector graphics library designed to work on top of several OpenGL backends, including GLESv2 and GL3. It does not provide any mechanism to create an OpenGL context, create a window, or handle input. It only provides a 2D graphics.

To work with NanoVG first clone its repository:

````
git clone https://github.com/memononen/nanovg.git
cd nanovg/src
````

If you want to created a shared libary file for the GL3 backend, touch `gl3.c` and palce this C code inside:

````c
#include <stdio.h>
#include <string.h>
#include <float.h>

#define GL_GLEXT_PROTOTYPES
#include <GL/gl.h>
#include <GL/glext.h>
#include "nanovg.h"
#define NANOVG_GL3_IMPLEMENTATION
#include "nanovg.c"
#include "nanovg_gl.h"
````

Build with `gcc` using the following command:

````
gcc -shared -o libnanovg.so gl3.c -lGL
````

For the GLESv2 vesion touch `gles2.c` abd place this inside it:

````c
#include <stdio.h>
#include <string.h>
#include <float.h>

#include <GLES2/gl2.h>
#include "nanovg.h"
#define NANOVG_GLES2_IMPLEMENTATION
#include "nanovg.c"
#include "nanovg_gl.h"
````

Build with `gcc` using the following command:

````
gcc -shared -o libnanovg.so gles2.c -lGLESv2
````

## Raylib

Raylib is a cross platform toolkit designed to simplify creating a window, handling user intput, and drawing graphics and 3D models.

To build Raylib for Linux DRM (Linux direct rendering manager without a running desktop environment), first install the follow requirements:

````
sudo apt install build-essential cmake libasound2-dev libpulse-dev libvorbis-dev libopenal-dev libdrm-dev libgles2-mesa-dev libudev-dev libgbm-dev
git clone --branch 4.5.0 https://github.com/raysan5/raylib.git 
cd raylib
````

To create a shared libary file that uses the Linux DRM system, build using th following commands:

````
mkdir build
cd build
cmake .. -DPLATFORM=DRM -DGRAPHICS=TRUE -DBUILD_SHARED_LIBS=ON
make -j4
````
