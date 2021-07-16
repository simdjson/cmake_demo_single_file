# Copy this file as CMakeLists.txt in
# some directory. With a recent CMake
# (at least 3.15), in this directory do
#
# cmake -B build .
# cmake --build build
# ./build/repro
#
#
cmake_minimum_required(VERSION 3.15)

project(CrashRepro VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_FLAGS_DEBUG "-Wno-deprecated-declarations")
set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

include(FetchContent)

FetchContent_Declare(
  simdjson
  GIT_REPOSITORY https://github.com/simdjson/simdjson.git
  GIT_SHALLOW TRUE
  GIT_TAG tags/v0.9.6
  )

FetchContent_MakeAvailable(simdjson)



file(WRITE main.cpp "
  #include \"simdjson.h\"
  #include <iostream>


  int main(void) {

    auto cars_json = R\"( [
      { \"make\": \"Toyota\", \"model\": \"Camry\",  \"year\": 2018, \"tire_pressure\": [ 40.1, 39.9, 37.7, 40.4 ] },
      { \"make\": \"Kia\",    \"model\": \"Soul\",   \"year\": 2012, \"tire_pressure\": [ 30.1, 31.0, 28.6, 28.7 ] },
      { \"make\": \"Toyota\", \"model\": \"Tercel\", \"year\": 1999, \"tire_pressure\": [ 29.8, 30.0, 30.2, 30.5 ] }
    ] )\"_padded;
    std::cout << \"parsing : \" << cars_json << std::endl;
    simdjson::dom::parser parser;
    simdjson::dom::array obj;
    auto err = parser.parse(cars_json).get(obj);
    if (err) {
      std::cerr << \"Failed to parse json\" << std::endl;
      std::cerr << err << std::endl;
      return EXIT_FAILURE;
    }
    std::cout << \"Success\" << std::endl;
    return EXIT_SUCCESS;
  }")



add_executable(repro main.cpp)
target_link_libraries(repro PUBLIC simdjson)
