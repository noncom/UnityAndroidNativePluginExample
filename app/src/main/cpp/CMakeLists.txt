# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.10.2)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
        RenderingPlugin

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        #native-lib.cpp

        source/gl3w/glcorearb.h
        source/gl3w/gl3w.h
        source/gl3w/gl3w.c

        source/Unity/IUnityInterface.h
        source/Unity/IUnityGraphics.h
        source/Unity/IUnityGraphicsD3D9.h
        source/Unity/IUnityGraphicsD3D11.h
        source/Unity/IUnityGraphicsD3D12.h
        source/Unity/IUnityGraphicsMetal.h
        source/Unity/IUnityGraphicsVulkan.h

        source/RenderAPI.h
        source/RenderAPI.cpp
        source/RenderAPI_D3D11.cpp
        source/RenderAPI_D3D12.cpp
        source/RenderingPlugin.cpp
        source/RenderAPI_OpenGLCoreES.cpp
        source/RenderAPI_Vulkan.cpp
        )

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

#find_library(
#        gles-v2
#        sdfsfsdfwefs
#)

#message("GLES2_LIBRARY: ")
#message(${GLES2_LIBRARY})
#message("GLES3_LIBRARY: ")
#message(${GLES3_LIBRARY})
#message("GLES LIB 2: ")
#message(${gles-v2})

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        RenderingPlugin

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib}
        #${GLES3_LIBRARY}
        GLESv2
        #${gles-v2}
        )