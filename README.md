# core-i18n-qt

Qt QML plugin for [core-i18n](https://github.com/core-i18n/core-i18n), split out of the main repository.

## Build

Requires core-i18n (found via `pkg-config core-i18n`) and Qt 5 or Qt 6 with Qml.

    cmake -B build && cmake --build build && sudo cmake --install build

## Usage

Import `CoreI18n` in a QML file to call `core_i18n()` as a global function:

    import QtQuick
    import CoreI18n 1.0

    Text {
        text: core_i18n("Cancel")
    }

The function uses the same current locale and gettext catalogs as the core-i18n C API.
When running from the build tree, add `build/qml` to the QML import path.
