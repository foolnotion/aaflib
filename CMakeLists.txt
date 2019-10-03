cmake_minimum_required(VERSION 3.11)

project(
    aaflib
    VERSION 0.1
    DESCRIPTION "An affine arithmetic C++ library"
    LANGUAGES CXX
    )

SET(AAF_HEADER aa.h aa_aaf.h aa_exceptions.h aa_interval.h aa_rounding.h)
SET(AAF_SOURCE aa_rounding.cpp aa_interval.cpp aa_aaftrigo.cpp aa_aafapprox.cpp aa_aafarithm.cpp aa_aafcommon.cpp aa_exceptions.cpp aa_aafspecial.cpp)

add_library(
    aaf.lin64
    SHARED 
    ${AAF_SOURCE}
)
target_compile_definitions(aaf.lin64 PRIVATE LIN64 USE_AAF_EXTENSIONS)
target_compile_options(aaf.lin64 PRIVATE -Wall -Weffc++ -Wno-deprecated -O3)

add_library(
    aaf.lin64.static
    STATIC 
    ${AAF_SOURCE}
)
target_compile_definitions(aaf.lin64.static PRIVATE LIN64 USE_AAF_EXTENSIONS)
target_compile_options(aaf.lin64.static PRIVATE -Wall -Weffc++ -Wno-deprecated -O3)
set_target_properties(aaf.lin64.static PROPERTIES OUTPUT_NAME aaf.lin64)

include(GNUInstallDirs)
install(FILES ${AAF_HEADER} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR} COMPONENT devel)
install(TARGETS aaf.lin64 DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT core)
install(TARGETS aaf.lin64.static DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT core)

