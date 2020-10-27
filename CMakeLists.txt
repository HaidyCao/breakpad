# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.10.2)

# Declares and names the project.

project("breakpad")

enable_language(ASM_NASM)
enable_language(ASM)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

message(-----------------------------------------${CMAKE_ANDROID_ARCH_ABI})

if ("${CMAKE_ANDROID_ARCH_ABI}" STREQUAL "armeabi-v7a")

endif ()

SET(
        BREAKPAD_SOURCE

        src/client/linux/crash_generation/crash_generation_client.cc
        src/client/linux/dump_writer_common/thread_info.cc
        src/client/linux/dump_writer_common/ucontext_reader.cc
        src/client/linux/handler/exception_handler.cc
        src/client/linux/handler/minidump_descriptor.cc
        src/client/linux/log/log.cc
        src/client/linux/microdump_writer/microdump_writer.cc
        src/client/linux/minidump_writer/linux_dumper.cc
        src/client/linux/minidump_writer/linux_ptrace_dumper.cc
        src/client/linux/minidump_writer/minidump_writer.cc
        src/client/minidump_file_writer.cc
        src/common/convert_UTF.cc
        src/common/md5.cc
        src/common/string_conversion.cc
        src/common/linux/breakpad_getcontext.S
        src/common/linux/elfutils.cc
        src/common/linux/file_id.cc
        src/common/linux/guid_creator.cc
        src/common/linux/linux_libc_support.cc
        src/common/linux/memory_mapped_file.cc
        src/common/linux/safe_readlink.cc
)

include_directories(. src src/common/android/include)
add_library(
        breakpad_static
        STATIC

        ${BREAKPAD_SOURCE}
)

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries(
        breakpad_static

        ${log-lib}
)
