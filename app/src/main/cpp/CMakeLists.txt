cmake_minimum_required(VERSION 3.22.1)
project("pinpad")

add_library(pinpad SHARED native-lib.cpp)

find_library(log-lib log)

add_library(mbedcrypto SHARED IMPORTED)
set_target_properties(mbedcrypto PROPERTIES IMPORTED_LOCATION
        ${CMAKE_CURRENT_SOURCE_DIR}/libs/mbedtls/build/${ANDROID_ABI}/library/libmbedcrypto.so)
target_include_directories(pinpad PUBLIC  ${CMAKE_CURRENT_SOURCE_DIR}/libs/mbedtls/mbedtls/include)

target_link_libraries(pinpad mbedcrypto ${log-lib})