cmake_minimum_required(VERSION 3.16.0)

project(jwsmtp)

set(JWSMTP_ROOT ${CMAKE_CURRENT_SOURCE_DIR})
set(SRC_FILES 
  ${JWSMTP_ROOT}/jwsmtp/jwsmtp/base64.cpp
  ${JWSMTP_ROOT}/jwsmtp/jwsmtp/compat.cpp
  ${JWSMTP_ROOT}/jwsmtp/jwsmtp/mailer.cpp
)

add_library(${PROJECT_NAME} SHARED ${SRC_FILES})
add_library(${PROJECT_NAME}Static STATIC ${SRC_FILES})

set(TEST_FILES
  ${JWSMTP_ROOT}/jwsmtp/demo1.cpp
)

include_directories(${JWSMTP_ROOT}/jwsmtp/jwsmtp)
add_executable(${PROJECT_NAME}test1 ${TEST_FILES})
target_link_libraries(${PROJECT_NAME}test1 jwsmtp)

install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/jwsmtp/jwsmtp"
    DESTINATION ${CMAKE_INSTALL_PREFIX}/include
    FILES_MATCHING PATTERN "*.h")

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}-targets
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(TARGETS ${PROJECT_NAME}Static
    EXPORT ${PROJECT_NAME}Static-targets
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)