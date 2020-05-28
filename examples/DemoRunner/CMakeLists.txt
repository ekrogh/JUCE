# ==============================================================================
#
#  This file is part of the JUCE 6 technical preview.
#  Copyright (c) 2020 - Raw Material Software Limited
#
#  You may use this code under the terms of the GPL v3
#  (see www.gnu.org/licenses).
#
#  For this technical preview, this file is not subject to commercial licensing.
#
#  JUCE IS PROVIDED "AS IS" WITHOUT ANY WARRANTY, AND ALL WARRANTIES, WHETHER
#  EXPRESSED OR IMPLIED, INCLUDING MERCHANTABILITY AND FITNESS FOR PURPOSE, ARE
#  DISCLAIMED.
#
# ==============================================================================

juce_add_gui_app(DemoRunner
    BUNDLE_ID                       com.juce.demorunner
    ICON_BIG                        ${CMAKE_CURRENT_SOURCE_DIR}/Source/JUCEAppIcon.png
    NEEDS_CURL                      TRUE
    NEEDS_WEB_BROWSER               TRUE
    MICROPHONE_PERMISSION_ENABLED   TRUE
    CAMERA_PERMISSION_ENABLED       TRUE
    BLUETOOTH_PERMISSION_ENABLED    TRUE
    FILE_SHARING_ENABLED            TRUE
    DOCUMENT_BROWSER_ENABLED        TRUE)

juce_generate_juce_header(DemoRunner)

target_sources(DemoRunner PRIVATE
    Source/Demos/DemoPIPs1.cpp
    Source/Demos/DemoPIPs2.cpp
    Source/Demos/JUCEDemos.cpp
    Source/Main.cpp
    Source/UI/DemoContentComponent.cpp
    Source/UI/MainComponent.cpp)

target_compile_definitions(DemoRunner PRIVATE
    PIP_JUCE_EXAMPLES_DIRECTORY_STRING="${JUCE_SOURCE_DIR}/examples"
    JUCE_ALLOW_STATIC_NULL_VARIABLES=0
    JUCE_DEMO_RUNNER=1
    JUCE_STRICT_REFCOUNTEDPOINTER=1
    JUCE_UNIT_TESTS=1
    JUCE_USE_CAMERA=1
    JUCE_USE_CURL=1
    JUCE_USE_MP3AUDIOFORMAT=1
    JUCE_WEB_BROWSER=1)

target_link_libraries(DemoRunner PRIVATE
    juce::juce_analytics
    juce::juce_audio_utils
    juce::juce_blocks_basics
    juce::juce_box2d
    juce::juce_dsp
    juce::juce_opengl
    juce::juce_osc
    juce::juce_product_unlocking
    juce::juce_video
    juce::juce_recommended_config_flags
    juce::juce_recommended_lto_flags
    juce::juce_recommended_warning_flags)

juce_add_bundle_resources_directory(DemoRunner ../Assets)