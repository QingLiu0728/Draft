# extract librpc.a file to get .so files
# execute_process(COMMAND mkdir -p ${USIMAPI_BINARY_DIR}/temp/obj)
# execute_process(COMMAND cp ${USIMAPI_SOURCE_DIR}/3rdparty/rpc/lib_x86/librpc.a ${USIMAPI_BINARY_DIR})
# execute_process(COMMAND ar x ${USIMAPI_BINARY_DIR}/librpc.a)
# file(GLOB obj_files "${USIMAPI_BINARY_DIR}/*.o")
# execute_process(COMMAND mv ${obj_files} librpc.a ${USIMAPI_BINARY_DIR}/temp/obj)

# extract librpc_shared.a to get .so files
# execute_process(COMMAND mkdir -p ${USIMAPI_BINARY_DIR}/temp/shared_obj)
# execute_process(COMMAND cp ${USIMAPI_SOURCE_DIR}/3rdparty/rpc/lib_x86/librpc_shared.a ${USIMAPI_BINARY_DIR})
# execute_process(COMMAND ar x ${USIMAPI_BINARY_DIR}/librpc_shared.a)
# file(GLOB obj_files "${USIMAPI_BINARY_DIR}/*.o")
# execute_process(COMMAND mv ${obj_files} librpc_shared.a ${USIMAPI_BINARY_DIR}/temp/shared_obj)

<!-- add_custom_command(TARGET usim POST_BUILD
    COMMAND ar rcs ${USIMAPI_BINARY_DIR}/lib/libusim.a ${USIMAPI_BINARY_DIR}/temp/obj/*.o)
    message(STATUS "test BUILD DYNAMIC") -->

如果需要将第三方编译好的库文件加入到自己的库文件中，唯一的方法就是将对方的库文件解压成.o文件，通过ar命令把.o文件合并到自己的库文件中去。


您只需将这些libA.so和libB.so构建为静态库（归档），即libA.a和libB.a，然后将它们链接到您自己的libstuff.so中如果这个第三方项目的CMakeLists没有为您提供将它们构建为静态的选项，那么您必须自己修改它来添加这个选项，但是只要您不是CMake的完全新手，这就相对容易了。


cmake修改option中的默认值
option(BUILD_SHARED_LIBS "Build jsoncpp_lib as a shared library." OFF)
cmake -DBUILD_SHARED_LIBS=ON ..

Cmake in Windows
cmake -G "Visual Studio 16 2019" -A x64 ..
cmake --build . --target <INSTALL | ALL_BUILD> --config <Release | Debug>


cmake -DCMAKE_BUILD_TYPE=Release ..
make
make install 

## Ifdef VAR
For ifdef var
add_definitation(-DVAR=1) 
or
cmake -Dvar=1 ..

Install
1. set install prefix 
    a. cmake -DCMAKE_INSTALL_PREFIX="/path"
    b. set(CMAKE_INSTALL_PREFIX PATH)
2. install(TARGETS xxx DESTINATION lib)
3. install(FILES xx xx DESTINATION include)

## Set Compiler (https://gitlab.kitware.com/cmake/community/-/wikis/FAQ#how-do-i-use-a-different-compiler)
1. cmake -D CMAKE_C_COMPILER=gcc-4.2 -D CMAKE_CXX_COMPILER=g++-4.2 ..
2. avoid using set()
    set(CMAKE_C_COMPILER "gcc-4.2")
    set(CMAKE_CXX_COMPILER "/usr/bin/g++-4.2")

    project("YourProjectName")
    This must be done before any language is set (ie before any project() or enable_language() command).
3. a rough way: clean all files in build dir before cmake



-fPIC 作用于编译阶段，告诉编译器产生与位置无关代码(Position-Independent Code)，
  则产生的代码中，没有绝对地址，全部使用相对地址，故而代码可以被加载器加载到内存的任意
  位置，都可以正确的执行。这正是共享库所要求的，共享库被加载时，在内存的位置不是固定的。

使用-fPIC生成的.a函数库会有效率下降的问题

add -fPIC option:

add_library(lib1 SHARED lib1.cpp)
set_property(TARGET lib1 PROPERTY POSITION_INDEPENDENT_CODE ON)


## CPack
set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_FILE_NAME "${PROJECT_NAME}-${vTimeStamp}-${vGitBranch}-${vGitCommit}")
include(CPack)


## Merge libs
1. (https://stackoverflow.com/questions/2152077/is-it-possible-to-get-cmake-to-build-both-a-static-and-shared-version-of-the-sam/29824424#29824424)
```
# list of source files
set(libsrc source1.c source2.c)

# this is the "object library" target: compiles the sources only once
add_library(objlib OBJECT ${libsrc})

# shared libraries need PIC
set_property(TARGET objlib PROPERTY POSITION_INDEPENDENT_CODE 1)

# shared and static libraries built from the same object files
add_library(MyLib_shared SHARED $<TARGET_OBJECTS:objlib>)
add_library(MyLib_static STATIC $<TARGET_OBJECTS:objlib>)

$<TARGET_OBJECTS:objlib> is a collection of *.o files.

The price you pay is that the object files must be built as position-independent code because shared libraries need this (static libs don't care). Note that position-independent code may be less efficient, so if you aim for maximal performance then you'd go for static libraries. Furthermore, it is easier to distribute statically linked executables.
```

2. for pre-compiled lib


## link library
1. link library built by this project
add_executable(main main.cpp)
target_link_libraries(main libtest-lib)

2. link library not built by this project (https://gitlab.kitware.com/cmake/community/-/wikis/doc/tutorials/Exporting-and-Importing-Targets)
add_library(testlib SHARED IMPORTED) 
set_property(TARGET testlib PROPERTY IMPORTED_LOCATION "/projectspath/LinkTest/TestLib/app/build/intermediates/cmake/debug/obj/armeabi-v7a/libtest-lib.so")


set_target_properties(Target PROPERTIES
ARCHIVE_OUTPUT_DIRECTORY "${SFML_BUILD_OUTPUT}/lib"
LIBRARY_OUTPUT_DIRECTORY "${SFML_BUILD_OUTPUT}/lib"
RUNTIME_OUTPUT_DIRECTORY "${SFML_BUILD_OUTPUT}/bin"
)

install(DIRECTORY "path/src/assets" DESTINATION "path/dest/assets")


## add pthread lib
find_package (Threads)
add_executable (myapp main.cpp ...)
target_link_libraries (myapp ${CMAKE_THREAD_LIBS_INIT})

possible problem: not found pthread lib on ubuntu
https://stackoverflow.com/questions/15193785/how-to-get-cmake-to-recognize-pthread-on-ubuntu


## add pdb info for Release build on Windows (https://stackoverflow.com/questions/28178978/how-to-generate-pdb-files-for-release-build-with-cmake-flags)
if(CMAKE_CXX_COMPILER_ID MATCHES "MSVC" AND CMAKE_BUILD_TYPE MATCHES "Release")
   target_compile_options(${TARGET_NAME} PRIVATE /Zi)

   # Tell linker to include symbol data
    set_target_properties(${TARGET_NAME} PROPERTIES 
        LINK_FLAGS "/INCREMENTAL:NO /DEBUG /OPT:REF /OPT:ICF"
    )

    # Set file name & location
    set_target_properties(${TARGET_NAME} PROPERTIES 
        COMPILE_PDB_NAME ${TARGET_NAME} 
        COMPILE_PDB_OUTPUT_DIR ${CMAKE_BINARY_DIR}
    )
endif()

or, simply add those lines

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /Zi")
set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "${CMAKE_SHARED_LINKER_FLAGS_RELEASE} /DEBUG /OPT:REF /OPT:ICF")
set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS_RELEASE} /DEBUG /OPT:REF /OPT:ICF")



## Find Package
### Common 

### Python
(https://cmake.org/cmake/help/git-stage/module/FindPython3.html#module:FindPython3)
find_package (Python2 COMPONENTS Interpreter Development NumPy)
find_package (Python3 COMPONENTS Interpreter Development NumPy)
    Result Variables:
        1. Python<2|3>_FOUND
        2. Python<>_EXECUTABLE
        3. Python_INCLUDE_DIRS
        4. Python_LIBRARY_DIRS
        5. Python_LIBRARIES
        6. Python_VERSION Python_VERSION_MAJOR Python_VERSION_MINOR
        7. Python_NumPy_INCLUDE_DIRS

### Boost
https://cmake.org/cmake/help/v3.15/module/FindBoost.html
find_package(Boost REQUIRED)
find_package(Boost COMPONENTS python)
Boost_INCLUDE_DIRS
Boost_LIBRARY_DIRS


### 血与泪的教训
CMAKE_BINARY_DIR 尽量使用该变量而不是 ProjectName_BINARY_DIR，如果更改了项目名称会非常容易导致奇怪的问题出现。也非常的难以找到问题。