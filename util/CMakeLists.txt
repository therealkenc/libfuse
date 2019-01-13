add_executable(fusermount3 fusermount.c ../lib/mount_util.c)
target_compile_definitions(fusermount3 PUBLIC 
    FUSE_CONF="/etc/fuse.conf"
    linux
)
target_include_directories(fusermount3 PRIVATE "../lib" "../lib/config")

#    _FILE_OFFSET_BITS=64 
#    FUSE_USE_VERSION=${FUSE_USE_VERSION}
