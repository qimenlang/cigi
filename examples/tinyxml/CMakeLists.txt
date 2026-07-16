set(TARGET_NAME tinyxml)

add_library(${TARGET_NAME} STATIC
    source/tinystr.cpp
    source/tinyxml.cpp
    source/tinyxmlerror.cpp
    source/tinyxmlparser.cpp
)

target_include_directories(${TARGET_NAME}
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/source
)

# Cigi examples compile against the STL-enabled TinyXML API.
target_compile_definitions(${TARGET_NAME}
    PUBLIC
        TIXML_USE_STL
)

add_executable(xmltest
    source/xmltest.cpp
)

target_link_libraries(xmltest
    PRIVATE
        ${TARGET_NAME}
)
