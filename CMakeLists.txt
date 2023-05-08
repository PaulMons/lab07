cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(print)

include_directories(base)
add_library(lib lib/print.cpp)
add_executable(printer printer/main.cpp)
target_link_libraries(printer lib) 
install(TARGETS printer RUNTIME DESTINATION bin)

target_include_directories(lib PUBLIC
  $<BUILD_INTERFACE:/base>
  $<INSTALL_INTERFACE:base>
)

install(TARGETS lib
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY base/ DESTINATION base)
install(EXPORT print-config DESTINATION cmake)
