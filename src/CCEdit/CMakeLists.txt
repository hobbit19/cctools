find_package(Qt4 COMPONENTS QtCore QtGui QtXml QtMain REQUIRED)
include(${QT_USE_FILE})

include_directories(${QT_INCLUDES} ${CMAKE_CURRENT_SOURCE_DIR})

set(CCEdit_SOURCES
    ../Stream.cpp
    ../Levelset.cpp
    ../Tileset.cpp
    ../DacFile.cpp
    ../IniFile.cpp
    ../ChipsHax.cpp
    ../GameLogic.cpp
    ../CCMetaData.cpp
    CCEdit.cpp
    EditorWidget.cpp
    LayerWidget.cpp
    TileWidgets.cpp
    LevelsetProps.cpp
    History.cpp
    AdvancedMechanics.cpp
    TestSetup.cpp
    ErrorCheck.cpp
    Organizer.cpp
)

if(WIN32)
    set(CCEdit_SOURCES ${CCEdit_SOURCES} CCEdit.rc)
endif()

set(CCEdit_MOCS
    ../Tileset.h
    CCEdit.h
    EditorWidget.h
    LayerWidget.h
    TileWidgets.h
    LevelsetProps.h
    AdvancedMechanics.h
    TestSetup.h
    ErrorCheck.h
    Organizer.h
)

set(CCEdit_RCCS
    CCEdit.qrc
)

qt4_wrap_cpp(CCEdit_MOCSRC ${CCEdit_MOCS})
qt4_add_resources(CCEdit_RCCSRC ${CCEdit_RCCS})
add_executable(CCEdit WIN32 MACOSX_BUNDLE
               ${CCEdit_SOURCES} ${CCEdit_MOCSRC} ${CCEdit_RCCSRC})
target_link_libraries(CCEdit ${QT_LIBRARIES})

if(APPLE)
    set(MACOSX_BUNDLE true)
    set(MACOSX_BUNDLE_NAME CCEdit)
    set(MACOSX_BUNDLE_INFO_STRING "CCEdit 2.1")
    set(MACOSX_BUNDLE_LONG_VERSION_STRING "2.0.95")
    set(MACOSX_BUNDLE_SHORT_VERSION_STRING "2.0.95")
    set(MACOSX_BUNDLE_COPYRIGHT "Copyright (C) 2010 Michael Hansen")
    set(MACOSX_BUNDLE_ICON_FILE "boot.icns")

    install(TARGETS CCEdit
            BUNDLE DESTINATION .
    )
    install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/icons/boot.icns
            DESTINATION CCEdit.app/Contents/Resources
    )
elseif(WIN32)
    install(TARGETS CCEdit
            RUNTIME DESTINATION .
    )
else()
    install(TARGETS CCEdit
            RUNTIME DESTINATION bin
    )
endif()
