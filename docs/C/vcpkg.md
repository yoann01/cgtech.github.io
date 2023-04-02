# Get started with vcpkg

visit [vcpkg](https://vcpkg.io/en/index.html)

!!! info
    vcpkg is a free C/C++ package manager for acquiring and managing libraries. 
    Choose from over 1500 open source libraries to download and build in a single 
    step or add your own private libraries to simplify your build process. 
    Maintained by the Microsoft C++ team and open source contributors.


## Install vcpkg
Installing vcpkg is a two-step process: first, clone the repo, then run the bootstrapping script to produce the vcpkg binary. 
The repo can be cloned anywhere, and will include the vcpkg binary after bootstrapping as well as any libraries that are installed from the command line. 

It is recommended to clone vcpkg as a submodule for CMake projects, but to install it globally for MSBuild projects. If installing globally,
we recommend a short install path like: ```sh C:\src\vcpkg``` or ```sh C:\dev\vcpkg ```, since otherwise you may run into path issues for some port build systems.

**Step 1: Clone the vcpkg repo**

```sh
git clone https://github.com/Microsoft/vcpkg.git
```

Make sure you are in the directory you want the tool installed to before doing this.

**Step 2: Run the bootstrap script to build vcpkg**

```sh
.\vcpkg\bootstrap-vcpkg.bat
```

**Install libraries for your project**

```sh
vcpkg install [packages to install]
```

**Using vcpkg with MSBuild / Visual Studio (may require elevation)**

```sh
vcpkg integrate install
```

After this, you can create a new project or open an existing one in the IDE. All installed libraries should already be discoverable by IntelliSense and usable in code without additional configuration.

**Using vcpkg with CMake**

In order to use vcpkg with CMake outside of an IDE, you can use the toolchain file:

```sh
cmake -B [build directory] -S . -DCMAKE_TOOLCHAIN_FILE=[path to vcpkg]/scripts/buildsystems/vcpkg.cmake
```

Then build with:

```sh
cmake --build [build directory]
```

With CMake, you will need to use find_package() to reference the libraries in your Cmakelists.txt files.