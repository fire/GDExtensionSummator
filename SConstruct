"""
# MIT License

Copyright (c) 2017-2022 Godot Engine contributors.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

"""

#!/usr/bin/env python
import os
import sys

env = SConscript("godot-cpp/SConstruct")

# For the reference:
# - CCFLAGS are compilation flags shared between C and C++
# - CFLAGS are for C-specific compilation flags
# - CXXFLAGS are for C++-specific compilation flags
# - CPPFLAGS are for pre-processor flags
# - CPPDEFINES are for pre-processor defines
# - LINKFLAGS are for linking flags

# tweak this if you want to use different folders, or more folders, to store your source code in.
env.Append(CPPPATH=["extension/src/"])
env.Append(CXXFLAGS=["-Wl,--wrap,memset,--wrap,memcpy,--wrap,memmove,--wrap,memcmp "])
env.Append(CXXFLAGS=["-Wl,--wrap,strlen,--wrap,strcmp,--wrap,strncmp "])
env.Append(CXXFLAGS=["-Wl,--wrap,malloc,--wrap,calloc,--wrap,realloc,--wrap,free "])
env.Append(CXXFLAGS=["-static"])
sources = Glob("extension/src/*.cpp")

if env["platform"] == "osx":
    program = env.Program(
        "game/bin/summator/libgdsummator.{}.{}.framework/libgdsummator.{}.{}".format(
            env["platform"], env["target"], env["platform"], env["target"], ".elf"
        ),
        source=sources,
        libs=env["LIBS"],
    )
else:
    program = env.Program(
        "game/bin/summator/libgdsummator.{}.{}.{}{}".format(
            env["platform"], env["target"], env["arch_suffix"], ".elf"
        ),
        source=sources,
        libs=env["LIBS"],
    )

Default(program)
