# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initalize pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "/usr/share/pico-sdk")

# Pull in Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(WS2812_Example C CXX ASM)

set(PICO_CXX_ENABLE_EXCEPTIONS 1)

set(PICO_CXX_ENABLE_RTTI 1)

# Initialise the Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(WS2812_Example 
        example.cpp
        WS2812.cpp
)

pico_generate_pio_header(WS2812_Example ${CMAKE_CURRENT_LIST_DIR}/WS2812.pio)

pico_set_program_name(WS2812_Example "WS2812 Example")
pico_set_program_version(WS2812_Example "1.0")

pico_enable_stdio_uart(WS2812_Example 1)
pico_enable_stdio_usb(WS2812_Example 1)

# Add the standard library to the build
target_link_libraries(WS2812_Example 
        pico_stdlib
)

# Add any user requested libraries
target_link_libraries(WS2812_Example
        hardware_pio
)

pico_add_extra_outputs(WS2812_Example)

