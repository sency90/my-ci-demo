cmake_minimum_required(VERSION 3.16)
project(hello_ci LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)

add_executable(hello src/main.cpp)

# 간단 테스트: 빌드 결과 실행만 해도 성공으로 간주
enable_testing()
add_test(NAME smoke COMMAND hello)

