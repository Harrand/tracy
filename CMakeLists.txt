cmake_minimum_required(VERSION 3.10)

# Tracy Client Library (Based on tracy.pdf from May 19, 2021)
add_library(TracyClient
    TracyClient.cpp
)
target_include_directories(TracyClient PUBLIC ./)
target_compile_options(TracyClient PUBLIC -DTRACY_ENABLE)

# Tracy Server Executable (Based on same tracy.pdf)
# Requires installation of various dependencies on each platform.
# We will do a local installation within the project directory - No other changes to the machine are made.
if(WIN32)
    # There is a magic script we can run.
    add_custom_command(TARGET TracyServerDepInstall
        POST_BUILD
        COMMAND cmd //C ./vcpkg)
elseif(UNIX)
    # We require pkg-config.
else()
    message(STATUS "Warning: Tracy Server is not supported for this platform")
endif()

# TODO: Create TracyServer target.