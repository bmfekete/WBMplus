cmake_minimum_required(VERSION 3.10)
project(WBM30)

set(CMAKE_C_FLAGS   "${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

if(${GHAASDIR})
    include_directories(${GHAASDIR}/include)
    link_directories(${GHAASDIR}/lib)
else(${GHAASDIR})
    include_directories(/usr/local/share/ghaas/include)
    link_directories(/usr/local/share/ghaas/lib)
endif(${GHAASDIR})

FILE(GLOB sources src/*.c)
add_executable(WBM30 ${sources})

if(${CMAKE_HOST_APPLE})
    target_link_libraries(WBM30 MF30 CM30 m)
else(${CMAKE_HOST_APPLE})
    target_link_libraries(WBM30 MF30 CM30 m -pthread)
endif(${CMAKE_HOST_APPLE})

target_include_directories(WBM30 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
install (TARGETS WBM30 RUNTIME DESTINATION ghaas/bin)
