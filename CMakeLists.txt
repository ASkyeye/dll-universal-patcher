cmake_minimum_required(VERSION 3.16)
project(dll_universal_patcher)

set(CMAKE_CXX_STANDARD 20)

add_subdirectory(phnt)

add_library(tiny-json STATIC tiny-json/tiny-json.c)
target_include_directories(tiny-json PUBLIC tiny-json)

add_library(dll_universal_patcher SHARED src/library.cpp)
target_compile_options(dll_universal_patcher PRIVATE
        /GS-
)
target_link_options(dll_universal_patcher PRIVATE
        /NODEFAULTLIB
        /ENTRY:dll_entry
)
target_link_libraries(dll_universal_patcher PRIVATE
        tiny-json
        phnt
        ntdll
        ntdllp
)

