cmake_minimum_required(VERSION 3.14)
project(core-i18n-qt VERSION 0.1.0 LANGUAGES CXX)

include(GNUInstallDirs)
find_package(PkgConfig REQUIRED)
pkg_check_modules(CORE_I18N REQUIRED IMPORTED_TARGET core-i18n)

find_package(QT NAMES Qt6 Qt5 COMPONENTS Core Qml REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core Qml REQUIRED)

set(CORE_I18N_QML_DIR "${CMAKE_CURRENT_BINARY_DIR}/qml/CoreI18n")
file(MAKE_DIRECTORY "${CORE_I18N_QML_DIR}")
configure_file(qml/CoreI18n/qmldir "${CORE_I18N_QML_DIR}/qmldir" COPYONLY)

add_library(core-i18n-qml MODULE src/core-i18n-qml.cpp)
set_target_properties(core-i18n-qml PROPERTIES
  AUTOMOC ON
  PREFIX ""
  OUTPUT_NAME corei18nplugin
  LIBRARY_OUTPUT_DIRECTORY "${CORE_I18N_QML_DIR}")
target_link_libraries(core-i18n-qml PRIVATE
  PkgConfig::CORE_I18N
  Qt${QT_VERSION_MAJOR}::Core
  Qt${QT_VERSION_MAJOR}::Qml)

install(TARGETS core-i18n-qml
  LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/CoreI18n"
  RUNTIME DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/CoreI18n")
install(FILES qml/CoreI18n/qmldir
  DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/CoreI18n")
