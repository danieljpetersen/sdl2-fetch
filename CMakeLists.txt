cmake_minimum_required(VERSION 3.20)
set(PROJECT_NAME "sdl_fetch")
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")
set(FETCHCONTENT_QUIET FALSE)
set(SDL2IMAGE_INSTALL OFF)
set(BUILD_SHARED_LIBS FALSE)
option(GLM_TEST_ENABLE "Disable" OFF)

include(FetchContent)
FetchContent_Declare(
        SDL2
        GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
        GIT_TAG release-2.26.3
        GIT_SHALLOW TRUE
        GIT_PROGRESS TRUE
)
FetchContent_Declare(
        SDL2_image
        GIT_REPOSITORY https://github.com/libsdl-org/SDL_image.git
        GIT_TAG release-2.6.3
        GIT_SHALLOW TRUE
        GIT_PROGRESS TRUE
)
FetchContent_Declare(glad GIT_REPOSITORY https://github.com/Dav1dde/glad.git GIT_TAG df8e9e16110b305479a875399cee13daa0ccadd9)
FetchContent_Declare(glm_external GIT_REPOSITORY https://github.com/g-truc/glm.git GIT_TAG 9749727c2db4742369219e1d452f43e918734b4e GIT_PROGRESS TRUE)
FetchContent_MakeAvailable(sdl2 SDL2_image glad glm_external)

find_package(Threads REQUIRED)

add_executable(sdl_fetch main.cpp)
target_link_libraries(sdl_fetch SDL2::SDL2main SDL2::SDL2-static SDL2_image::SDL2_image-static glad Threads::Threads)

target_include_directories(${PROJECT_NAME} SYSTEM PRIVATE ${glm_external_SOURCE_DIR})
