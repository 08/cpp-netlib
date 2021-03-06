# Copyright (c) Glyn Matthews 2012.
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)

if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
  if (HAVE_STD11)
    set(CPP-NETLIB_CXXFLAGS "-Wall -std=c++11")
  elseif (HAVE_STD0X)
    set(CPP-NETLIB_CXXFLAGS "-Wall -std=c++0x")
  endif()
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
  CHECK_CXX_COMPILER_FLAG(-std=c++11 HAVE_STD11)
  set(CPP-NETLIB_CXXFLAGS "-Wall -std=c++11 -stdlib=libc++")
  set(CPP-NETLIB_CXXFLAGS "-Wall -std=c++11 -stdlib=libc++")
endif()

include_directories(${CPP-NETLIB_SOURCE_DIR}/uri/src ${CPP-NETLIB_SOURCE_DIR}/message/src)

set(CPP-NETLIB_MESSAGE_SRCS message.cpp)
add_library(cppnetlib-message ${CPP-NETLIB_MESSAGE_SRCS})
add_dependencies(cppnetlib-message cppnetlib-uri)
target_link_libraries(cppnetlib-message cppnetlib-uri)
foreach (src_file ${CPP-NETLIB_MESSAGE_SRCS})
if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
endif()
endforeach(src_file)

set(CPP-NETLIB_MESSAGE_DIRECTIVES_SRCS directives.cpp)
add_library(cppnetlib-message-directives ${CPP-NETLIB_MESSAGE_DIRECTIVES_SRCS})
foreach (src_file ${CPP-NETLIB_MESSAGE_DIRECTIVES_SRCS})
if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
endif()
endforeach(src_file)

set(CPP-NETLIB_MESSAGE_WRAPPERS_SRCS wrappers.cpp)
add_library(cppnetlib-message-wrappers ${CPP-NETLIB_MESSAGE_WRAPPERS_SRCS})
foreach (src_file ${CPP-NETLIB_MESSAGE_WRAPPERS_SRCS})
if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
    set_source_files_properties(${src_file}
        PROPERTIES COMPILE_FLAGS ${CPP-NETLIB_CXXFLAGS})
endif()
endforeach(src_file)

