set(OpenGL_GL_PREFERENCE LEGACY)

find_package(OpenMP REQUIRED)

if(NOT TARGET OpenMP::OpenMP_CXX)
    find_package(Threads REQUIRED)
    add_library(OpenMP::OpenMP_CXX IMPORTED INTERFACE)
    set_property(TARGET OpenMP::OpenMP_CXX
                 PROPERTY INTERFACE_COMPILE_OPTIONS ${OpenMP_CXX_FLAGS})
    set_property(TARGET OpenMP::OpenMP_CXX
                 PROPERTY INTERFACE_LINK_LIBRARIES ${OpenMP_CXX_FLAGS} Threads::Threads)

endif()

find_package(OpenGL REQUIRED)
find_package(glfw3 3.3 REQUIRED)

add_executable(${PROJECT_NAME}  main.cpp)
target_link_libraries(${PROJECT_NAME} 
    PRIVATE 
        LRE::linalg
        SFML::Graphics
        SFML::Window
        SFML::System
)