if(ESP_PLATFORM)
    # for arduino as component ESP-IDF
    get_filename_component(dir ${CMAKE_CURRENT_LIST_FILE} PATH)
    FILE(GLOB_RECURSE app_sources ${dir}/src/*.c*)

    idf_component_register(SRCS ${app_sources}      
                        INCLUDE_DIRS "src"
                        PRIV_REQUIRES arduino lvgl
)
else()
    cmake_minimum_required(VERSION 3.12)

    include_directories(
        ./src
    )

    file(GLOB_RECURSE SOURCES
        ./src/*.cpp
        ./src/*.c
    )

    ADD_LIBRARY(esp32_smartdisplay STATIC ${SOURCES})

    target_include_directories(esp32_smartdisplay SYSTEM PUBLIC ./src)
endif()

project(esp32_smartdisplay)