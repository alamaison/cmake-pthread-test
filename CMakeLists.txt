cmake_minimum_required(VERSION 2.8)

project(cmake-pthread-test)

add_library(foo foo.cpp)

find_package(Threads REQUIRED)
if(THREADS_HAVE_PTHREAD_ARG)
  set_property(TARGET foo PROPERTY COMPILE_OPTIONS "-pthread")
  set_property(TARGET foo PROPERTY INTERFACE_COMPILE_OPTIONS "-pthread")
endif()
if(CMAKE_THREAD_LIBS_INIT)
  target_link_libraries(foo "${CMAKE_THREAD_LIBS_INIT}")
endif()

add_library(boo boo.cpp)
target_link_libraries(boo foo)

add_executable(bam bam.cpp)
target_link_libraries(bam boo)