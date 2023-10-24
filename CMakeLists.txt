cmake_minimum_required(VERSION 3.27)

project(dmenu
        VERSION 5.2
        LANGUAGES C
        )

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED True)

include_directories(/usr/X11R6/include
                    /usr/include/freetype2
                    )

link_directories(/usr/X11R6/lib)

link_libraries(X11 fontconfig Xft)

add_compile_definitions(VERSION="${PROJECT_VERSION}"
                        _DEFAULT_SOURCE _BSD_SOURCE _XOPEN_SOURCE=700 _POSIX_C_SOURCE=200809L
                        )

add_compile_options(-pedantic
                    -Wall -Wno-deprecated-declarations
                    -Os
                    )

# Xinerama, comment if you don't want it
# link_libraries(Xinerama)
# add_compile_definitions(XINERAMA)

add_executable(dmenu dmenu.c drw.c util.c)
add_executable(stest stest.c)


install(TARGETS dmenu stest DESTINATION bin)
install(PROGRAMS dmenu_path dmenu_run DESTINATION bin)
install(FILES dmenu.1 stest.1 DESTINATION share/man/man1)
