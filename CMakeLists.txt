cmake_minimum_required(VERSION 3.15)
set_property(GLOBAL PROPERTY USE_FOLDERS YES)
set(JUCE_ENABLE_MODULE_SOURCE_GROUPS ON CACHE BOOL "" FORCE)
set (CMAKE_CXX_STANDARD 20)
set (CMAKE_POSITION_INDEPENDENT_CODE ON)

project(Gin VERSION 1.0.0)

set (CMAKE_OSX_DEPLOYMENT_TARGET 10.13)

if (TARGET juce::juce_core)
    # JUCE is already included by parent (AXR), do nothing
elseif (DEFINED JUCE_SOURCE_DIR)
    # point to JUCE provided by parent(to which this is being added as Submodule)
    add_subdirectory(${JUCE_SOURCE_DIR} ${CMAKE_BINARY_DIR}/JUCE)
else()
    # Fallback: assume JUCE is required separately inside Gin itself
    add_subdirectory(juce)
endif()

add_subdirectory(modules)
add_subdirectory(examples/Demo)
add_subdirectory(examples/Effect)
add_subdirectory(examples/Synth)
add_subdirectory(examples/UnitTests)
