project(PID)

cmake_minimum_required (VERSION 3.5)

add_definitions(-std=c++11)
add_compile_definitions(OPENSSL_ROOT_DIR=$ENV{OPENSSL_ROOT_DIR})
add_compile_definitions(OPENSSL_LIBRARIES=$ENV{OPENSSL_LIBRARIES})

set(CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS "${CXX_FLAGS}")


include_directories(/usr/local/include)
link_directories(/usr/local/lib)

add_subdirectory(uWebSockets)
if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin") 

include_directories(/usr/local/opt/openssl/include)
link_directories(/usr/local/opt/openssl/lib)
link_directories(/usr/local/Cellar/libuv/1*/lib)

endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin") 


include_directories(include)
set(sources src/PID.cpp src/main.cpp)
add_executable(pid ${sources})

target_link_libraries(pid z ssl uv uWS)
