cmake_minimum_required(VERSION 3.16)

project(Qontrejour VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(libs/QDmxLib)

find_package(Qt6 REQUIRED COMPONENTS Widgets LinguistTools Network SerialPort)

set(TS_FILES Qontrejour_fr_GF.ts)

set(RES_FILES resources/resources.qrc)

set(DATA_FILES README.md TODO LICENSE)

set(PROJECT_SOURCES
  src/main.cpp
  src/qontrejour.h
  src/core/dmxvalue.h
  src/core/dmxvalue.cpp
  src/core/dmxmanager.h
  src/core/dmxmanager.cpp
  src/core/dmxengine.h
  src/core/dmxengine.cpp
  src/core/interpreter.h
  src/core/interpreter.cpp
  src/gui/mainwindow.h
  src/gui/mainwindow.cpp
  src/gui/universewidget.h
  src/gui/universewidget.cpp
  src/gui/sequencerwidget.h
  src/gui/sequencerwidget.cpp
  src/gui/valuetablewidget.h
  src/gui/valuetablewidget.cpp
  src/gui/valuesliderswidget.h
  src/gui/valuesliderswidget.cpp
  #        src/gui/valueeditwidget.h
  #        src/gui/valueeditwidget.cpp
  src/gui/keypadwidget.h
  src/gui/keypadwidget.cpp
  ${TS_FILES}
  ${RES_FILES}
  ${DATA_FILES}
)

qt_add_executable(Qontrejour MANUAL_FINALIZATION ${PROJECT_SOURCES})

qt_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})

target_link_libraries(Qontrejour PRIVATE Qt6::Widgets QDmxLib Qt6::Network Qt6::SerialPort)

set_target_properties(Qontrejour PROPERTIES
    ${BUNDLE_ID_OPTION}
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

include(GNUInstallDirs)
install(TARGETS Qontrejour
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_finalize_executable(Qontrejour)
