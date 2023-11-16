cmake_minimum_required (VERSION 3.12)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("profilling-tools")

# Add source files
set(SOURCES
	"src/timer.cpp"
)

# Add library
add_library(profilling-tools ${SOURCES})


# Set C++ standard and compile options
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
target_compile_features(profilling-tools PRIVATE cxx_std_20)


 # Add include directories
target_include_directories(profilling-tools PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)


# Add example executable
add_executable(test-profilling-tools
	test-timer.cpp
)

target_link_libraries(test-profilling-tools PRIVATE profilling-tools)


# Set C++ standard and compile options
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
target_compile_features(test-profilling-tools PRIVATE cxx_std_20)

# if (CMAKE_VERSION VERSION_GREATER 3.12)
  # set_property(TARGET profilling-tools PROPERTY CXX_STANDARD 20)
# endif()