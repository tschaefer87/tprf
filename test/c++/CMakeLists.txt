# Copy h5 files to binary dir
FILE(GLOB all_h5_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.h5)
file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/${all_h5_files} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

include_directories(${CMAKE_SOURCE_DIR}/c++)

#triqs_add_all_cpp_tests_in_current_dir()

set(SIMPLE_TESTS linalg_ops bubble gf_inverse gk_to_from_gr chi0k_to_from_chi0r)

foreach(t ${SIMPLE_TESTS})
  add_executable(${t} ${CMAKE_CURRENT_SOURCE_DIR}/${t}.cpp)
  target_link_libraries (${t} ${TRIQS_LIBRARY_ALL} gtest tprf_c)
  add_test(${t} ${CMAKE_CURRENT_BINARY_DIR}/${t})
endforeach(t)
