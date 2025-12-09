set(TEST_RUNNER_NAME bitcastTest)

add_executable(${TEST_RUNNER_NAME})
target_sources(${TEST_RUNNER_NAME} PRIVATE ./main.cpp ./bitcastTest.cpp)

target_compile_options(${TEST_RUNNER_NAME} PRIVATE -Wall -Wextra -pedantic -g3
                                                   -fdiagnostics-color=always)

target_link_libraries(${TEST_RUNNER_NAME} PRIVATE gtest bitcast)

add_test(NAME bitcastTest COMMAND bitcastTest)
