cmake_minimum_required(VERSION 3.5)
# FindBoost gained imported targets in CMake 3.5

## OPTIONS
option(AUTOLINK "Compile with autolink support on MSVC" ON)
option(STATIC "Compile against static libraries" OFF)
## END OPTIONS

set(Boost_DEBUG ON)
set(Boost_USE_STATIC_RUNTIME OFF)
if(STATIC)
  set(Boost_USE_STATIC_LIBS ON)
endif()
find_package(Boost REQUIRED COMPONENTS date_time)

add_executable(datetime_1 datetime_1.cpp)
target_link_libraries(datetime_1 PUBLIC Boost::date_time)

if(AUTOLINK)
  target_link_libraries(datetime_1 PUBLIC Boost::diagnostic_definitions)
else()
  target_link_libraries(datetime_1 PUBLIC Boost::disable_autolinking)
endif()

if(NOT STATIC)
  target_link_libraries(datetime_1 PUBLIC Boost::dynamic_linking)
endif()
