# Build.Guide

This document is a guide to building certain C language projects.

## NanoVG

NanoVG is a cross platform vector graphics library designed to work against several OpenGL backends, including GLESv2 and GL3. 

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
