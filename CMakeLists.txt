cmake_minimum_required (VERSION 3.16)

project(libstudxml VERSION 1.1.0)


message(STATUS "Configuring for libstudxml version ${PROJECT_VERSION}")

option(LIBSTUDXML_STATIC_LIB "Build static library" ON)

if(LIBSTUDXML_STATIC_LIB)
  set(LIBSTUDXML_STATIC_BUILD ON)
  message(STATUS "Building static library")
endif()

add_library(libstudxml)

target_sources(libstudxml
  PRIVATE
    libstudxml/parser.cxx
    libstudxml/qname.cxx
    libstudxml/serializer.cxx
    libstudxml/value-traits.cxx
    libstudxml/details/genx/char-props.c
    libstudxml/details/genx/genx.c
    libstudxml/details/expat/xmlparse.c
    libstudxml/details/expat/xmlrole.c
    libstudxml/details/expat/xmltok.c
)

target_include_directories(libstudxml
 PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}
)

target_compile_definitions(libstudxml PUBLIC LIBSTUDXML_STATIC_BUILD)

set_target_properties(libstudxml PROPERTIES C_STANDARD 11)
set_target_properties(libstudxml PROPERTIES CXX_STANDARD 11)
