cmake_minimum_required(VERSION 3.7.0)

project(qDBManager LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)

add_library(${PROJECT_NAME} STATIC
        criteriabuilder.cpp
        entityfactory.cpp
        qdbmanager.cpp
        tpmanager.cpp
        entities/baseEntity.cpp
        entities/abstractEntity.cpp
        interfaces/qsqlite.cpp
        )
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

if(NOT QT_DEFAULT_MAJOR_VERSION)
    set(QT_DEFAULT_MAJOR_VERSION 5 CACHE STRING "Qt version to use (5 or 6), defaults to 5")
endif()

# Find dependencies
set(QT_COMPONENTS Core Sql)
set(QT_LIBRARIES Qt${QT_DEFAULT_MAJOR_VERSION}::Core Qt${QT_DEFAULT_MAJOR_VERSION}::Sql)

find_package(Qt${QT_DEFAULT_MAJOR_VERSION} COMPONENTS ${QT_COMPONENTS} REQUIRED)

target_link_libraries(${PROJECT_NAME} PUBLIC ${QT_LIBRARIES})

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})