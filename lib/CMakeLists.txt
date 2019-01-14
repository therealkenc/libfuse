set(LIBFUSE_SRC
    modules/iconv.c
    modules/subdir.c
    buffer.c
    cuse_lowlevel.c
    fuse_loop_mt.c
    fuse_loop.c
    fuse_lowlevel.c
    fuse_opt.c
    fuse_signals.c
    fuse.c
    helper.c
    mount_util.c
    mount.c
)
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/config")
add_library(fuse3 SHARED ${LIBFUSE_SRC})
target_compile_definitions(fuse3 PRIVATE 
    _FILE_OFFSET_BITS=64 
    FUSE_USE_VERSION=${FUSE_USE_VERSION}
    FUSERMOUNT_DIR="${CMAKE_RUNTIME_OUTPUT_DIRECTORY}"
)
target_link_libraries(fuse3
    dl
    pthread
)
set(CMAKE_SHARED_LINKER_FLAGS "-Wl,--version-script=${CMAKE_CURRENT_SOURCE_DIR}/fuse_versionscript")
set_property(TARGET fuse3 PROPERTY SOVERSION "${LIBFUSE_SOVERSION_MAJOR}")
set_property(TARGET fuse3 PROPERTY VERSION "${LIBFUSE_SOVERSION}")
