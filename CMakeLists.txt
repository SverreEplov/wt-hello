PROJECT(PackageTest)
cmake_minimum_required(VERSION 2.8.12)


if(NOT CMAKE_BUILD_TYPE)
  message(STATUS "Setting build type to 'Release' as none was specified.")
  set(CMAKE_BUILD_TYPE "Release")
endif()

################## automatically execute conan install ##################################################
# Download automatically, you can also just copy the conan.cmake file
if (NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
    message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
    file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/master/conan.cmake" "${CMAKE_BINARY_DIR}/conan.cmake")
endif ()

include(${CMAKE_BINARY_DIR}/conan.cmake)

conan_cmake_run(CONANFILE conanfile.txt
        BASIC_SETUP KEEP_RPATHS
        BUILD missing)
################## automatically execute conan install ##################################################

#if (APPLE)
#    set(CMAKE_INSTALL_RPATH "@executable_path/../lib")
#else()
#    set(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")
#endif()
#SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)

set(CMAKE_CXX_STANDARD 17)

IF(CMAKE_BUILD_TYPE MATCHES Release)
    set(WT_LIBNAME "wthttp")
  ELSE()
    set(WT_LIBNAME "wthttpd")
ENDIF(CMAKE_BUILD_TYPE MATCHES Release)

ADD_EXECUTABLE(example example.cpp)
TARGET_LINK_LIBRARIES(example ${WT_LIBNAME} ${CONAN_LIBS} pthread)
