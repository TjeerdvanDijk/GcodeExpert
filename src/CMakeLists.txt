include_directories(/usr/local/include)

find_package(SFML 2.5 COMPONENTS system window graphics network audio REQUIRED)
include_directories(${SFML_INCLUDE_DIRS})

# Add header file
set(GLEW_H /usr/local/Cellar/glew/2.2.0_1/include/GL)
set(GLFW_H /usr/local/Cellar/glfw/3.3.4/include/GLFW)
include_directories(${GLEW_H} ${GLFW_H})

# Add target link
set(GLEW_LINK /usr/local/Cellar/glew/2.2.0_1/lib/libGLEW.2.2.0.dylib)
set(GLFW_LINK /usr/local/Cellar/glfw/3.3.4/lib/libglfw.3.dylib)
link_libraries(${OPENGL} ${GLEW_LINK} ${GLFW_LINK})

# Execute compilation command
set(SOURCE_FILES main.cpp)
add_executable(GcodeExpert ${SOURCE_FILES})
target_compile_features(GcodeExpert PRIVATE cxx_std_17)

target_link_libraries(GcodeExpert sfml-system sfml-window sfml-graphics sfml-audio sfml-network)
if (APPLE)
    target_link_libraries(GcodeExpert "-framework OpenGL")
    target_link_libraries(GcodeExpert "-framework GLUT")
endif()