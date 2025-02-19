cmake_minimum_required(VERSION 3.30)
project(Chroma_Hunter)

set(CMAKE_CXX_STANDARD 20)

# **Quan trọng: Định nghĩa SDL_MAIN_HANDLED**
add_definitions(-DSDL_MAIN_HANDLED)
# hoặc
# add_compile_definitions(SDL_MAIN_HANDLED)

# Tìm và thêm thư viện SDL2
find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)
find_package(SDL2_mixer REQUIRED)
find_package(SDL2_ttf REQUIRED)

# Include directories
include_directories(
        ${SDL2_INCLUDE_DIRS}
        ${SDL2_IMAGE_INCLUDE_DIRS}
        ${SDL2_MIXER_INCLUDE_DIRS}
        ${SDL2_TTF_INCLUDE_DIRS}
        ${CMAKE_SOURCE_DIR}/src
)

# Thêm executable
file(GLOB_RECURSE SOURCES ${CMAKE_SOURCE_DIR}/src/*.cpp ${CMAKE_SOURCE_DIR}/src/**/*.cpp)
add_executable(Chroma_Hunter ${SOURCES})

# Loại bỏ SDL2main khỏi danh sách liên kết (nếu cần)
foreach(LIB ${SDL2_LIBRARIES})
    if(${LIB} MATCHES "SDL2main")
        list(REMOVE_ITEM SDL2_LIBRARIES ${LIB})
    endif()
endforeach()

# Liên kết các thư viện SDL
target_link_libraries(Chroma_Hunter
        ${SDL2_LIBRARIES}
        ${SDL2_IMAGE_LIBRARIES}
        ${SDL2_MIXER_LIBRARIES}
        ${SDL2_TTF_LIBRARIES}
)