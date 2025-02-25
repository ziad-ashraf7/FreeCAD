
add_subdirectory(App)
if(BUILD_GUI)
    add_subdirectory(Gui)
endif(BUILD_GUI)

set(Sketcher_Scripts
    Init.py
    SketcherExample.py
    TestSketcherApp.py
    Profiles.py
)

set(Sketcher_TestScripts
    SketcherTests/__init__.py
    SketcherTests/TestSketchFillet.py
    SketcherTests/TestSketcherSolver.py
    SketcherTests/TestSketchExpression.py
    SketcherTests/TestSketchValidateCoincidents.py
)

if(BUILD_GUI)
    list (APPEND Sketcher_Scripts
          InitGui.py
          TestSketcherGui.py
    )
endif(BUILD_GUI)

set(Sketcher_Profiles
    ProfileLib/Hexagon.py
    ProfileLib/RegularPolygon.py
    ProfileLib/__init__.py
)

add_custom_target(SketcherScripts ALL
    SOURCES ${Sketcher_Scripts} ${Sketcher_Profiles} ${Sketcher_TestScripts}
)
include_directories(
        ${EIGEN3_INCLUDE_DIR}
)
fc_target_copy_resource(SketcherScripts
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}/Mod/Sketcher
    ${Sketcher_Scripts}
    ${Sketcher_Profiles}
    ${Sketcher_TestScripts}
)

INSTALL(
    FILES
        ${Sketcher_Scripts}
    DESTINATION
        Mod/Sketcher
)

INSTALL(
    FILES
        ${Sketcher_Profiles}
    DESTINATION
        Mod/Sketcher/ProfileLib
)

INSTALL(
    FILES
        ${Sketcher_TestScripts}
    DESTINATION
        Mod/Sketcher/SketcherTests
       )
