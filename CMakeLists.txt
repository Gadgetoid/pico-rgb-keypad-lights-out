cmake_minimum_required(VERSION 3.12)

# Change your executable name to something creative!
set(NAME pico-rgb-keypad-lights-out)

# Include the Pimoroni Pico libraries
# By default they assume `pimoroni-pico` is stored alongside your project
include(pimoroni_pico_import.cmake)

# Include the Pico SDK
include(pico_sdk_import.cmake)

# Gooey boilerplate
project(${NAME} C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

# Add your source files
add_executable(${NAME}
    main.cpp # <-- Add source files here!
)

# Include required libraries
include(libraries/pico_rgb_keypad/pico_rgb_keypad)

# Don't forget to link the libraries you need!
target_link_libraries(${NAME}
    pico_rgb_keypad
)

# create map/bin/hex file etc.
pico_add_extra_outputs(${NAME})

# Set up files for the release packages
install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${NAME}.uf2
    ${CMAKE_CURRENT_LIST_DIR}/README.md
    DESTINATION .
)

set(CPACK_INCLUDE_TOPLEVEL_DIRECTORY OFF)
set(CPACK_GENERATOR "ZIP" "TGZ")
include(CPack)
