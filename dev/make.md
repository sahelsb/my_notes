
## Make

You should call the compiler to compile your program , **g++ (gcc tool)** is the compiler you can use **on your linux or windows** , when you compile the program with g++ it will give you a binary fiel to execute (first you need to install g++ compiler on your machine)

**build your c++ program with g++, on linux and windows** : 

By default, g++ will create an executable file named a.out. You can change the output file name by passing the name to the -o flag.

        g++ -o hello hello.cpp


This will compile hello.cpp to an executable named hello
You can also use another compiler from microsoft called **CL (cl.exe)**

**run your program** :
    ./hello 


Although the compilation can be done with one command, the compilation process can be divided into four distinct phases:

- Preprocessing
- Compilation
- Assembly
- Linking


But If you have more files, or using libraries, then you need to list all of them, while taking care to set the correct include paths and library paths. and in this way the compiling command would be very messy as :

    g++ -o hello hello.cpp func.cpp app.cpp

**In order to avoid this : we use Make or CMake**

## CMake

CMake is a **build system generator**,  it provides a family of tools and a domain-specific language (DSL) to describe what the build system should achieve when the appropriate build tools are invoked. The DSL is platform- and compiler-agnostic: you can reuse the same CMake scripts to obtain native build systems on any platform.

CMake stands for Cross-platform Make. CMake recognizes which compilers to use for a given kind of source.
All the usual compiler/linker flags dealing with the inclusion of header files, libraries, etc are replaced by platform independent and build system independent commands. Debugging flags are included by either setting the variable CMAKE_BUILD_TYPE to “Debug”, or by passing it to CMake when invoking the program:

cmake -DCMAKE_BUILD_TYPE:STRING=Debug.
CMake also offers the platform independent inclusion of the ‘-fPIC’ flag (via the POSITION_INDEPENDENT_CODE property) and many others.

If we want to run c++ programs on different platforms, we use CMake with CMakelists.txt that you will specify the specification of your project, headers, which compile you use and ...

What you make out of CMake (CMake engine) is not a build of your C++ but it makes you some files based on the platform you are running on that(linux , windows) you can use then easily to build the program, after building it will give you a binary file you can execute on your machine

But if you use CMake , you do not need to directly call different compilers by different commands that are there for different platforms and different compile

<img src="././images/build-systems.svg" style="display:block;float:none;margin-left:auto;margin-right:auto;width:30%">

On GNU/Linux, the native build system will be a collection of Makefile-s. The make build tool uses these Makefile-s to transform sources to executables and libraries. CMake abstracts the process of generating the Makefile-s away into a generic DSL

**Now** imagine you want to run c++ on your vscode as an editor , so you need to set the configurations to let vscode know how to interpret your code, so to know which c++ compiler and which c++ version you want to use for your c++ code and this configuartions you specify in **C/C++ configurations file** in VScode (ctrl+shift+p) there you have the compiler path and c++ standard settings and so on, and this setting will create a .vscode folder for you including your configurations

Here in **cofigure includepath :**  **C++ IntelliSense engine** needs additional information about the paths in which your include files (used libraries in your porject) are located.

And The include paths are defined in the **"includePath"**  **setting** in a file called **c_cpp_properties.json** located in the . **vscode directory** in the opened folder.

### CMakeLists.txt

    #requirement on minimum version of CMake
    cmake_minimum_required(version 3.10)

    set(CMAKE_CXX_STANDARD 14)

    #declare our project, version and its programming language
    project(project_name version 1.10 Languages CXX)

    #which other CMake packages that need to be found to build our project 
    find_package(Eigen3 REQUIRED)

    #set source files
    set(source_files hello.cpp hello-test.cpp)

### specify targets

    #create an executable target by providing list of source files to compile
    add_executable(project_name ${source_files})

    #create a library target
    add_library(library_name ${source_files})


    #Add the given directories to those the compiler uses to search for include files. Relative paths are interpreted as relative to the current source directory
    include_directories(${eigen3_include_directories})

### linking
Once you have several targets, you can describe the relationship between them with target_link_libraries and a keyword; one of PUBLIC, PRIVATE, and INTERFACE

    #tell CMake about dependencies ands libraries we needed wen build
    target_link_libraries(hello dlib::dlib)
    
    #from inside build directory
    #The cmake .. command looks in the parent folder for a file named CMakeLists.txt, reads it, and sets up everything needed to build program
    cmake ..

    #or from anywhere 
    cmake -S path/to/myProject -B path/to/build

When you add your CMakelists.txt to your project then you can use cmake to build your project **by the command cmake .** and **it will create build files** in your project (please create build files in a seperate folder called build)

Now you can use build tools (visual studio IDE) to build your project using the build files cmake gives you ( **.sln file** ), **you will open .sln file in visual studio** and use build solutions opetion in visual studio to build this file ---\> this will generate the binary file

Instead of using visual studio you can also use another build tool, but you should use windows developer powershell---\> then in the build directory **use the command "msbuild helloapp.sln"**

---\> it is called out of source build ---\> so you have **src folder** containing your sourde files and a **build folder** containing your build files

## Make :
The reason we need “Make” is because it enables the end user to **build and install your package** without knowing the details of how it’s done

Make is a tool that controls the generation of executables and other non-source files of a program from the program’s source files.
The Make tool needs to know how to build your program. It gets its knowledge of how to build your program from a file called the “makefile”. This makefile lists each of the non-source files and how to compute it from other files. When you write a program, you should write a makefile for it, so that it is possible to use “Make” to build and install the program.

Recompiling the entire program every time we change a small part of the system would be inefficient. Hence, if you change a few source files and then run “Make”, it doesn’t recompile the whole thing. It updates only those non-source files that depend directly or indirectly on the source files that you changed. Pretty neat! 
“Make” is not limited to any particular language. For each non-source file in the program, the makefile **specifies the shell commands to compute it**. These shell commands can run a compiler to produce an object file, the linker to produce an executable, ar to update a library, Makeinfo to format documentation, etc. “Make” is not limited to just building a package either. You can also use “Make” to control installing or uninstalling a package

## Build a c++ project

        cd projectDir
        mkdir build & cd build
        cmake ..
        make
        cd projectDir
        hello


**Note : you need to create Makefiles to use make to build your program (actually the make command will run the Makefile you creeated and build the system basaed on that) OR you can use cmake that will automatically generate Makefiles for you based oin the instructions in CMakelists.txt and then you use make command that use that generated Makefiles and build your program**


**Gcc** : compiler for c

**G++** \> compiler for C++

So in c++ you have a series of source files and then give this to the compiler and it provides a binary file that can be a library or executable program.

Two most important compilers for c++ are G++ , Clang