set(TARGET_NAME CigiMiniHost)

file(GLOB_RECURSE CIGI_MINI_HOST_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_CURRENT_SOURCE_DIR}/source/*.cpp"
)

add_executable(${TARGET_NAME}
    ${CIGI_MINI_HOST_SOURCES}
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

add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${CMAKE_CURRENT_SOURCE_DIR}/MiniHost.def"
        "$<TARGET_FILE_DIR:${TARGET_NAME}>/MiniHost.def"
    COMMENT "Copy MiniHost.def next to ${TARGET_NAME}"
)
