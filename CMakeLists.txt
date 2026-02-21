cmake_minimum_required(VERSION 3.10)
project(SFML_Simulation LANGUAGES CXX)

# 1. Emacs IntelliSense Support
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# 2. Compiler Flags (from your CXXFLAGS)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_compile_options(-Wall)

# 3. SFML Configuration (using your custom path)
set(SFML_DIR "$ENV{HOME}/sfml_install/lib/cmake/SFML")
find_package(SFML 3.0 COMPONENTS Graphics Window System REQUIRED)

# 4. Source Files (from your SRC and IMGUI_SRC)
set(IMGUI_DIR "libs/imgui-1.91.1")
set(IMGUI_SFML_DIR "libs/imgui-sfml")

set(SOURCES
    main.cpp
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_SFML_DIR}/imgui-SFML.cpp
)

# 5. Define Executable
add_executable(sfml-app ${SOURCES})

# 6. Include Directories (from your -I flags)
target_include_directories(sfml-app PRIVATE 
    ${IMGUI_DIR} 
    ${IMGUI_SFML_DIR}
    ${SFML_INCLUDE_DIR}
)

# 7. Linking (from your LDFLAGS)
# Note: CMake handles SFML and OpenGL dependencies automatically via find_package
target_link_libraries(sfml-app PRIVATE 
    SFML::Graphics 
    SFML::Window
    SFML::System
    "-framework OpenGL"
)
