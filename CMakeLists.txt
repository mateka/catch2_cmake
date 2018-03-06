cmake_minimum_required(VERSION 3.8 FATAL_ERROR)


project(catch VERSION 2.0.0.0 LANGUAGES CXX)

find_path(CATCH_INCLUDE_DIR catch.hpp)

add_library(catch INTERFACE)
target_include_directories(catch INTERFACE ${CATCH_INCLUDE_DIR})

add_library(catch::catch ALIAS catch)
install(
    TARGETS catch EXPORT catchTargets
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)
install(
    EXPORT catchTargets
    FILE catchTargets.cmake
    NAMESPACE catch::
    DESTINATION lib/cmake/catch
)

# This makes the project importable from the build directory
export(TARGETS catch FILE catchTargets.cmake)
