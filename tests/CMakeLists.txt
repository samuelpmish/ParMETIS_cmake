file(GLOB_RECURSE test_files ${PROJECT_SOURCE_DIR}/tests/*.c)

foreach(filename ${test_files})		

  # remove the filetype suffix		
  string(REPLACE ".c" "" testname ${filename})		

  # remove the prefix		
  string(REPLACE ${PROJECT_SOURCE_DIR}/tests/ "" testname ${testname})		

  # use the remaining string to name the binary file		
  add_executable(${testname} ${filename})
  add_test(${testname} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${testname})		

  target_link_libraries(${testname} PUBLIC ParMETIS)

endforeach(filename ${test_files})
