cmake_minimum_required(VERSION 3.0.0)
project(interpolation VERSION 0.1.0)

find_package( OpenCV REQUIRED )

include(CTest)
enable_testing()

include_directories("../utility")

add_executable(interpolation main.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

install(TARGETS interpolation
		RUNTIME DESTINATION bin)

install(FILES "${PROJECT_SOURCE_DIR}/../resources/interpolation.jpg" DESTINATION bin)

target_link_libraries(interpolation ${OpenCV_LIBS} utility)

add_custom_command ( TARGET interpolation POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different "${PROJECT_SOURCE_DIR}/../resources/interpolation.jpg"  ${CMAKE_BINARY_DIR}/interpolation
)