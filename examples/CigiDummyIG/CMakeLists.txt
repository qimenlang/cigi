set(TARGET_NAME CigiDummyIG)

file(GLOB_RECURSE CIGI_DUMMY_IG_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_CURRENT_SOURCE_DIR}/source/*.cpp"
)

add_executable(${TARGET_NAME}
    ${CIGI_DUMMY_IG_SOURCES}
)

target_include_directories(${TARGET_NAME}
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/source
)

target_link_libraries(${TARGET_NAME}
    PRIVATE
        cigicl-static
        tinyxml
)

if(WIN32)
    target_link_libraries(${TARGET_NAME} PRIVATE ws2_32)
endif()
