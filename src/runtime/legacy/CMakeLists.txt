configure_file(config.h.in config.h)

set(SRC
    lfortran_intrinsics.c
)

add_library(lfortran_runtime SHARED ${SRC})
#target_include_directories(lfortran_runtime BEFORE PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(lfortran_runtime BEFORE PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
set_target_properties(lfortran_runtime PROPERTIES
  LIBRARY_OUTPUT_DIRECTORY ..)

add_library(lfortran_runtime_static STATIC ${SRC})
#target_include_directories(lfortran_runtime_static BEFORE PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(lfortran_runtime_static BEFORE PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
set_target_properties(lfortran_runtime_static PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ..)

install(TARGETS lfortran_runtime_static
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    ARCHIVE DESTINATION share/lfortran/lib
    LIBRARY DESTINATION share/lfortran/lib
)

install(TARGETS lfortran_runtime
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
  ARCHIVE DESTINATION share/lfortran/lib
  LIBRARY DESTINATION share/lfortran/lib
)

# Install the header
install(
    FILES lfortran_intrinsics.h
    DESTINATION share/lfortran/lib/impure
)
