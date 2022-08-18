cmake_minimum_required(VERSION 3.8)
project(PARMETIS_PROJ LANGUAGES C)

set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

set(CMAKE_C_STANDARD 11)

add_subdirectory(../METIS_cmake ${CMAKE_CURRENT_BINARY_DIR}/METIS)

file(GLOB sources ${PROJECT_SOURCE_DIR}/src/*.c)
file(GLOB headers ${PROJECT_SOURCE_DIR}/include/*.h)

add_library(ParMETIS ${sources})
target_include_directories(ParMETIS PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_link_libraries(ParMETIS PUBLIC METIS)

if (ENABLE_PROGRAMS)
  add_subdirectory(programs)
endif()

if (ENABLE_TESTING)
  enable_testing()
  add_subdirectory(tests)
endif()
