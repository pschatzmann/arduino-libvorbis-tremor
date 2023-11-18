cmake_minimum_required(VERSION 3.16)

# set the project name
project(arduino_libvorbis C)

# we use FetchContent to install 
include(FetchContent)

# lots of warnings and all warnings as errors
## add_compile_options(-Wall -Wextra )

FetchContent_Declare(arduino_libopus GIT_REPOSITORY https://github.com/pschatzmann/arduino-libopus.git GIT_TAG main  )
FetchContent_GetProperties(arduino_libopus)
if(NOT arduino_libopus_POPULATED)
    FetchContent_Populate(arduino_libopus)
    add_subdirectory(${arduino_libopus_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR}/arduino_libopus)
endif()

file(GLOB_RECURSE SRC_LIST_C CONFIGURE_DEPENDS  "${PROJECT_SOURCE_DIR}/*.c" )

# define libraries
add_library (arduino_libvorbis ${SRC_LIST_C})

#target_compile_options(arduino_libvorbis PRIVATE -Wdouble-promotion)
#target_compile_definitions(arduino_libvorbis PUBLIC -DARDUINO -DOPUS_BUILD )
target_link_libraries(arduino_libvorbis PRIVATE arduino_libopus)


# define location for header files
target_include_directories(arduino_libvorbis PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src )
