# check if GLEW is already installed in the system - using CMake's built in script FindGLEW
find_package(GLEW QUIET)

if(GLEW_FOUND)
    message(STATUS "Found preinstalled GLEW libraries at ${GLEW_LIBRARIES}")
    add_library(GLEW_external INTERFACE)
else()
    message(STATUS "Preinstalled GLEW not found.")
    message(STATUS "Will download and install GLEW in ${STAGED_INSTALL_PREFIX}")

    include(ExternalProject)
    ExternalProject_Add(GLEW_external
        URL
        https://github.com/nigels-com/glew/releases/download/glew-2.2.0/glew-2.2.0.zip
        SOURCE_SUBDIR
        build/cmake
        UPDATE_COMMAND
        ""
        CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=${STAGED_INSTALL_PREFIX}
        -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
        $<$<PLATFORM_ID:Linux>:-DGLEW_EGL=ON>
        TEST_AFTER_INSTALL
        0
        DOWNLOAD_NO_PROGRESS
        1
        LOG_CONFIGURE
        1
        LOG_BUILD
        1
        LOG_INSTALL
        1
    )

    set(GLEW_DIR "${STAGED_INSTALL_PREFIX}/lib/cmake/glew")
    file(TO_NATIVE_PATH "${GLEW_DIR}" GLEW_DIR)
    set(GLEW_DIR ${GLEW_DIR} CACHE INTERNAL "GLEW installation dir")
endif()