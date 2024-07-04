# GROMACS_2024.2_on_Windows
The native compiled GROMACS on Win11 with double precision

![image](https://github.com/slweng0321/GROMACS_2024_on_Windows/assets/126021966/48da5636-cd73-45e3-8132-04ac659b6522)

Gromacs source code and releases can be found in https://gitlab.com/gromacs/gromacs.

# Usage:
Download and extract the file. Open terminal and run gmx.exe in bin.

Or you can add the path (< path-to-extact-folder >/bin) to the enviroment variables.

# Compile instruction
For those who want to compile in their own machine.
  ## Requirements
  ### Visual Studio Installer https://visualstudio.microsoft.com/zh-hant/downloads/ 
  
  Install Visual Studio Communoty 2022. Click Modify, select Desktop Development with C++.

  ### Intel OneAPI Math Kernel Library https://www.intel.com/content/www/us/en/developer/tools/oneapi/toolkits.html#base-kit
  
  Install Math Kernel Library only. The DPC++/C++ Compiler can't work normally with the current cmake.

  ### (Optional) Ninjia

  Nijia can increase the speed of compiling parallelly. If you want to use Nijia, after the installation of Nijia, replace -G"NMake Makefiles" to -GNinja in the configuration step and replace nmake to ninja -j #n, where #n is the number of core that  Ninjia uses to compile.

  ### (Optional) FFTW3

  FFTW3 could be the alternative for Intel MKL, which may not work on AMD CPU. I didn't try FFTW3.
  
  ## Steps
  After installation, open <x64 Native Tools Command Prompt for VS 2022> with Administrator from the start menu.

  ### 1. Configure

    cmake -G"NMake Makefiles" -S. -B./build -DCMAKE_C_COMPILER=cl -DCMAKE_CXX_COMPILER=cl -DGMX_FFT_LIBRARY=mkl -DGMX_DOUBLE=on

  May change some configure option:
  
    -DGMX_GPU=CUDA, not tried since I don't have a NVIDIA GPU.
    
    -DGMX_GPU=SYCL, failed. It requires Clang or DPC++/C++ Compiler but they don't work.
    
    -DGMX_GPU=OpenCL, suceessfully built, compiled, and ran, but the current OpenCL seems not to works on my device.
    
  Check Gromacs website for other options. Notably, if you are using -DGMX_GPU option, set -DGMX_DOUBLE=off.

  ### 2. Compile

    cd build

    nmake

  After make, the compiled gmx.exe should uccur in the build/bin folder

    

  
  
