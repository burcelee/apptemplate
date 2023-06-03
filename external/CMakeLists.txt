

#### SDL ####
set(SDL_PATH "SDL2-2.26.5")
add_subdirectory(${SDL_PATH} EXCLUDE_FROM_ALL)
# SDL2::SDL2main may or may not be available. It is e.g. required by Windows GUI applications  
if(TARGET SDL2::SDL2main)
    # It has an implicit dependency on SDL2 functions, so it MUST be added before SDL2::SDL2 (or SDL2::SDL2-static)
    target_link_libraries(${CMAKE_PROJECT_NAME}  PRIVATE SDL2::SDL2main)
endif()
# Link to the actual SDL2 library. SDL2::SDL2 is the shared SDL library, SDL2::SDL2-static is the static SDL libarary.
target_link_libraries(${CMAKE_PROJECT_NAME}  PRIVATE SDL2::SDL2-static)
#### END SDL ####

#### IMGUI ####
set(IMGUI_PATH "imgui-1.89.6")
set(IMGUI_SDL_PATH "${IMGUI_PATH}/sdl-backend")
add_library(imgui STATIC    ${IMGUI_PATH}/imgui.cpp
                            ${IMGUI_PATH}/imgui_tables.cpp
                            ${IMGUI_PATH}/imgui_widgets.cpp
                            ${IMGUI_PATH}/imgui_draw.cpp
                            ${IMGUI_PATH}/imgui_demo.cpp
                            ${IMGUI_SDL_PATH}/imgui_impl_sdl2.cpp
                            ${IMGUI_SDL_PATH}/imgui_impl_sdlrenderer2.cpp
                            )
target_include_directories(imgui PUBLIC  ${IMGUI_PATH}
                                    ${IMGUI_SDL_PATH}
                                    )
                                    
target_link_libraries(imgui PRIVATE SDL2::SDL2)

target_link_libraries(${CMAKE_PROJECT_NAME}  PRIVATE imgui)
#### END IMGUI ####