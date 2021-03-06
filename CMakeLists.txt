project(pcro)

find_package(Qt4 4.6.0 REQUIRED)

find_package(KDE4 REQUIRED)

link_directories(/usr/local/lib)

include_directories(/usr/include/sphinxbase)
include_directories(/usr/local/include/pocketsphinx)
set(pcro_SRS    alsasoundcard.cpp
                main.cpp
                mainwindow.cpp
                qcustomplot.cpp
                voicerecognition.cpp
                           
                alsasoundcard.h
                mainwindow.h
                qcustomplot.h
                ui_mainwindow.h
                voicerecognition.h
                )

INCLUDE(${QT_USE_FILE})
ADD_DEFINITIONS(${KDE4_ENABLE_EXCEPTIONS})
ADD_DEFINITIONS(${QT_DEFINITIONS})

KDE4_ADD_UI_FILES(pcro_SRS mainwindow.ui)

KDE4_ADD_EXECUTABLE(pcro ${pcro_SRS})

target_link_libraries(pcro    ${KDE4_KDECORE_LIBS}
                              ${KDE4_KDEUI_LIBS}
                              ${QT_QTCORE_LIBRARY}
                              ${QT_QTGUI_LIBRARY}
                              asound
                              sphinxbase
                              pocketsphinx
                              sphinxad
                              )
INSTALL(FILES ${CMAKE_CURRENT_SOURCE_DIR}/mylm.lm
              ${CMAKE_CURRENT_SOURCE_DIR}/mydict.dic
        DESTINATION ~/.kde4/share/apps/voicerecognition/)
