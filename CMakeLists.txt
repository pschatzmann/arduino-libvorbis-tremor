cmake_minimum_required(VERSION 3.16)

# set the project name
project(arduino_libvorbis C)

# we use FetchContent to install 
include(FetchContent)

# lots of warnings and all warnings as errors
## add_compile_options(-Wall -Wextra )

FetchContent_Declare(codec-ogg GIT_REPOSITORY https://github.com/pschatzmann/codec-ogg.git GIT_TAG main  )
FetchContent_GetProperties(codec-ogg)
if(NOT codec-ogg_POPULATED)
    FetchContent_Populate(codec-ogg)
    add_subdirectory(${codec-ogg_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR}/codec-ogg)
endif()

file(GLOB_RECURSE SRC_LIST_C CONFIGURE_DEPENDS  "${PROJECT_SOURCE_DIR}/src/*.c" )

# define libraries
add_library (arduino_libvorbis ${SRC_LIST_C})

#target_compile_options(arduino_libvorbis PRIVATE -Wdouble-promotion)
#target_compile_definitions(arduino_libvorbis PUBLIC -DARDUINO -DOPUS_BUILD )
target_link_libraries(arduino_libvorbis PUBLIC codec-ogg)


# define location for header files
target_include_directories(arduino_libvorbis PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src )
