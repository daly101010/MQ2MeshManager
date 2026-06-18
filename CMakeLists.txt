# Generated from MQ2MeshManager.vcxproj
# This file is designed to work with add_subdirectory()

# ---------------------------------------------------------------------
# Props file includes
# ---------------------------------------------------------------------
include("../../src/Plugin.cmake")

# ---------------------------------------------------------------------
# Header files
# ---------------------------------------------------------------------
set(MQ2MeshManager_HEADERS
    "resource.h"
)

source_groups("Header Files" ${MQ2MeshManager_HEADERS})

# ---------------------------------------------------------------------
# Other files
# ---------------------------------------------------------------------
set(MQ2MeshManager_OTHERFILES
    "MQ2MeshManager.rc"
    "README.md"
)

source_group("Resource Files" FILES ${MQ2MeshManager_OTHERFILES})

# ---------------------------------------------------------------------
# Source files
# ---------------------------------------------------------------------
set(MQ2MeshManager_SOURCES
    "MQ2MeshManager.cpp"
)

source_groups("Source Files" ${MQ2MeshManager_SOURCES})

# ---------------------------------------------------------------------
# Target definition
# ---------------------------------------------------------------------
add_library(MQ2MeshManager SHARED
    ${MQ2MeshManager_HEADERS}
    ${MQ2MeshManager_OTHERFILES}
    ${MQ2MeshManager_SOURCES}
)

set_target_properties(MQ2MeshManager PROPERTIES FOLDER "external")

# ---------------------------------------------------------------------
# Apply props file configurations
# ---------------------------------------------------------------------
target_Plugin_props(MQ2MeshManager)

# ---------------------------------------------------------------------
# Project dependencies
# ---------------------------------------------------------------------
target_link_libraries(MQ2MeshManager PRIVATE MQ2Main)

# ---------------------------------------------------------------------
# Link libraries
# ---------------------------------------------------------------------
target_link_libraries(MQ2MeshManager PRIVATE
    "Ws2_32.lib"
    "$<$<CONFIG:Release>:zlib.lib>"
    "$<$<CONFIG:Debug>:zlibd.lib>"
    "$<$<CONFIG:Release>:libcurl.lib>"
    "Iphlpapi.lib"
    "Secur32.lib"
    "crypt32.lib"
    "cryptopp.lib"
    "$<$<CONFIG:Debug>:libcurl-d.lib>"
)

# ---------------------------------------------------------------------
# PRE_BUILD events
# ---------------------------------------------------------------------

add_custom_command(TARGET MQ2MeshManager PRE_BUILD
    COMMAND powershell.exe -ExecutionPolicy Bypass -NoProfile -NonInteractive -File "${CMAKE_SOURCE_DIR}/tools/build_scripts/Plugin_Versioning.ps1" -ProjectName "${PROJECT_NAME}" -ProjectDirectory "${CMAKE_CURRENT_SOURCE_DIR}/"
    COMMENT "Updating version resource for ${PROJECT_NAME}..."
    VERBATIM
)

# ============================================================================
# MANUAL CONVERSION NOTES
# ============================================================================
#
# - Review and adjust as needed
