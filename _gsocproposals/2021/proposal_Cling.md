---
title: Add support to resolve symbols from a static library to the Cling C++ interpreter
layout: gsoc_proposal
project: ROOT
year: 2021
organization:
    - CERN
---

## Description
ROOT is an open-source data analysis framework used by many software stacks in High Energy Physics (HEP) experiments, at CERN and other particle physics laboratories. It provides fundamental components for the entire data processing chain, from particle collisions to final publications, including final user data analysis and modern machine learning techniques. ROOT provides an interactive C++ interpreter that is ideal for fast prototyping and can be used from the command line, a Jupyter notebook, or through the provided Python bindings. Cling, the bundled C++ interpreter is a thin layer atop of Clang/LLVM that deals with aspects derived from making C++ an interpreted language. In general, Cling may transform otherwise ill-formed code so that it becomes parseable by Clang; afterward, it is just-in-time compiled and linked by LLVM, and executed.

On the other hand, devtoolset (Developer Toolset) is a family of packages included in CentOS/RedHat Enterprise Linux software collections that provides updated versions of a GCC-based C/C++ toolchain, GDB, and other development and debugging tools. To allow the generated binaries to work on older RedHat-based operating systems that do not have devtoolset installed, these packages provide updates to libstdc++ in form of a `.a` static library that is linked to other object files to generate the final executable file. While this ensures backwards compatibility of binaries generated by the updated toolchain provided by devtoolset, it might create additional issues.

One of this issues, is that Cling instructs the LLVM linker to look for C++ standard library symbols on `libstdc++.so`, but not on the static `.a` library provided on systems that have devtoolset installed. This translates into linking failures when trying to use modern features not included in the libstdc++ provided by the system.

## Task ideas
 * Investigate about devtoolset to gain insight on its working principles.
 * Familiarize with Cling architecture and how it interacts with Clang/LLVM.
 * Patch Cling so that symbol relocation takes into account symbols provided by the devtoolset static library (if installed).

## Expected results
The expected result is a patch to Cling that allows the use of modern libstdc++ features provided by the devtoolset static library (if installed on the system). The student should be prepared to write a progress report and present the results at the end of the summer.

## Evaluation Task
Interested students please contact Javier (j.lopez@cern.ch) for a warm-up and evaluation task.

## Requirements
 * C++, strong knowledge on compilers (particularly Clang/LLVM) and GNU/Linux.

## Mentors
 * **[Javier Lopez-Gomez](mailto:j.lopez@cern.ch)**
 * [Axel Naumann](mailto:Axel.Naumann@cern.ch)

## Links
 * [ROOT](https://root.cern/)
 * [Cling introduction](https://root.cern/primer/#learn-c-at-the-root-prompt)
 * [Devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) <!-- markdown-link-check-disable-line -->
 * [LLVM](https://llvm.org/)
 * [Clang](https://clang.llvm.org/)
 * [Cling sources](https://github.com/root-project/cling/)
