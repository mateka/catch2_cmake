cmake_minimum_required(VERSION 3.8 FATAL_ERROR)


project(catch VERSION 2.0.0.0 LANGUAGES CXX)

find_path(CATCH_INCLUDE_DIR catch.hpp)

add_library(catch INTERFACE)
target_include_directories(catch INTERFACE ${CATCH_INCLUDE_DIR})

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/catch/catch-config-version.cmake"
    VERSION ${catch_VERSION}
    COMPATIBILITY AnyNewerVersion
)

add_library(catch::catch ALIAS catch)
install(TARGETS catch EXPORT catch-targets)
install(
    EXPORT catch-targets
    FILE catch-targets.cmake
    NAMESPACE catch::
    DESTINATION lib/cmake/catch
)
configure_file(
    cmake/catch-config.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/catch/catch-config.cmake"
    COPYONLY
)
install(
    FILES cmake/catch-config.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/catch/catch-config-version.cmake"
    DESTINATION lib/cmake/catch
)

# This makes the project importable from the build directory
export(TARGETS catch FILE catch-targets.cmake)
