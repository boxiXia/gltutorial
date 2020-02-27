cmake_minimum_required(VERSION 3.15)
project(example)

set(CMAKE_CXX_STANDARD 20)

find_package(glm CONFIG REQUIRED)
find_package(GLEW REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
#find_package(OPENGL REQUIRED)

set(ALL_GL_LIBS GLEW::GLEW glm glfw glad::glad)
set(CMAKE_INCLUDE_CURRENT_DIR ON)


list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")

# Compile external dependencies
add_subdirectory (external)

include_directories(
        external/AntTweakBar-1.16/include/
        external/assimp-3.0.1270/include/
        external/bullet-2.81-rev2613/src/
        .
)




add_executable(boing boing.c)
target_link_libraries(boing PRIVATE ${ALL_GL_LIBS})

add_executable(gears gears.c)
target_link_libraries(gears PRIVATE ${ALL_GL_LIBS})

add_executable(heightmap heightmap.c)
target_link_libraries(heightmap PRIVATE ${ALL_GL_LIBS})

add_executable(wave wave.c)
target_link_libraries(wave PRIVATE ${ALL_GL_LIBS})

add_executable(splitview splitview.c)
target_link_libraries(splitview PRIVATE ${ALL_GL_LIBS})

add_executable(triangle triangle-opengl.c)
target_link_libraries(triangle PRIVATE ${ALL_GL_LIBS})

add_executable(sharing sharing.c)
target_link_libraries(sharing PRIVATE ${ALL_GL_LIBS})

# Tutorial 1
add_executable(tutorial01_first_window
        tutorial01_first_window/tutorial01.cpp)
target_link_libraries(tutorial01_first_window ${ALL_GL_LIBS})
target_include_directories(tutorial01_first_window PRIVATE ${OPENGL_INCLUDE_DIRS})
set_property(TARGET tutorial01_first_window PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/tutorial01_first_window")


#add_library(shader SHARED common/shader.cpp common/shader.hpp)
#target_link_libraries(shader PUBLIC ${ALL_GL_LIBS})

set(SHADER_HELPER common/shader.cpp common/shader.hpp)
set(SHADER_TEXTURE_HELPER
        common/shader.cpp common/shader.hpp
        common/texture.cpp common/texture.hpp)


# Tutorial 2
add_executable(tutorial02_red_triangle
        tutorial02_red_triangle/tutorial02.cpp
        ${SHADER_HELPER}
        tutorial02_red_triangle/SimpleFragmentShader.fragmentshader
        tutorial02_red_triangle/SimpleVertexShader.vertexshader
        )
target_link_libraries(tutorial02_red_triangle ${ALL_GL_LIBS})

# Tutorial 3
add_executable(tutorial03_matrices
        tutorial03_matrices/tutorial03.cpp
        ${SHADER_HELPER}
        tutorial03_matrices/SimpleTransform.vertexshader
        tutorial03_matrices/SingleColor.fragmentshader
        )
target_link_libraries(tutorial03_matrices ${ALL_GL_LIBS})

# Tutorial 4
add_executable(tutorial04_colored_cube
        tutorial04_colored_cube/tutorial04.cpp
        ${SHADER_HELPER}
        tutorial04_colored_cube/TransformVertexShader.vertexshader
        tutorial04_colored_cube/ColorFragmentShader.fragmentshader
        )
target_link_libraries(tutorial04_colored_cube
        ${ALL_GL_LIBS}
        )

# Tutorial 5
add_executable(tutorial05_textured_cube
        tutorial05_textured_cube/tutorial05.cpp
        ${SHADER_TEXTURE_HELPER}
        tutorial05_textured_cube/TransformVertexShader.vertexshader
        tutorial05_textured_cube/TextureFragmentShader.fragmentshader)
target_link_libraries(tutorial05_textured_cube
        ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program

# Tutorial 6
add_executable(tutorial06_keyboard_and_mouse
        tutorial06_keyboard_and_mouse/tutorial06.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        tutorial06_keyboard_and_mouse/TransformVertexShader.vertexshader
        tutorial06_keyboard_and_mouse/TextureFragmentShader.fragmentshader
        )
target_link_libraries(tutorial06_keyboard_and_mouse ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program

# Tutorial 7
add_executable(tutorial07_model_loading
        tutorial07_model_loading/tutorial07.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        tutorial07_model_loading/TransformVertexShader.vertexshader
        tutorial07_model_loading/TextureFragmentShader.fragmentshader
        )
target_link_libraries(tutorial07_model_loading ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program


# Tutorial 8
add_executable(tutorial08_basic_shading
        tutorial08_basic_shading/tutorial08.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        tutorial08_basic_shading/StandardShading.vertexshader
        tutorial08_basic_shading/StandardShading.fragmentshader
        )
target_link_libraries(tutorial08_basic_shading ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program


# Tutorial 9
add_executable(tutorial09_vbo_indexing
        tutorial09_vbo_indexing/tutorial09.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        tutorial09_vbo_indexing/StandardShading.vertexshader
        tutorial09_vbo_indexing/StandardShading.fragmentshader
        )
target_link_libraries(tutorial09_vbo_indexing ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program



## Tutorial 9 - AssImp model loading
#add_executable(tutorial09_AssImp
#        tutorial09_vbo_indexing/tutorial09_AssImp.cpp
#        common/shader.cpp common/shader.hpp
#        common/controls.cpp common/controls.hpp
#        common/texture.cpp common/texture.hpp
#        common/objloader.cpp common/objloader.hpp
#        tutorial09_vbo_indexing/StandardShading.vertexshader
#        tutorial09_vbo_indexing/StandardShading.fragmentshader
#        )
#find_package(assimp CONFIG REQUIRED) #not working..
#target_link_libraries(tutorial09_AssImp ${ALL_GL_LIBS} assimp::assimp)

# Tutorial 9 - several objects
add_executable(tutorial09_several_objects
        tutorial09_vbo_indexing/tutorial09_several_objects.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        tutorial09_vbo_indexing/StandardShading.vertexshader
        tutorial09_vbo_indexing/StandardShading.fragmentshader
        )
target_link_libraries(tutorial09_several_objects ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program


# Tutorial 10
add_executable(tutorial10_transparency
        tutorial10_transparency/tutorial10.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        tutorial10_transparency/StandardShading.vertexshader
        tutorial10_transparency/StandardTransparentShading.fragmentshader
        )
target_link_libraries(tutorial10_transparency ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program

# Tutorial 11
add_executable(tutorial11_2d_fonts
        tutorial11_2d_fonts/tutorial11.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        common/text2D.hpp common/text2D.cpp
        tutorial11_2d_fonts/StandardShading.vertexshader
        tutorial11_2d_fonts/StandardShading.fragmentshader
        tutorial11_2d_fonts/TextVertexShader.vertexshader
        tutorial11_2d_fonts/TextVertexShader.fragmentshader)
target_link_libraries(tutorial11_2d_fonts ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program

# Tutorial 12
add_executable(tutorial12_extensions
        tutorial12_extensions/tutorial12.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        common/text2D.hpp common/text2D.cpp

        tutorial12_extensions/StandardShading.vertexshader
        tutorial12_extensions/StandardShading_WithSyntaxErrors.fragmentshader
        )
target_link_libraries(tutorial12_extensions  ${ALL_GL_LIBS})
## NOTE you must manually set the working directory of the program


# Tutorial 13
add_executable(tutorial13_normal_mapping
        tutorial13_normal_mapping/tutorial13.cpp
        common/shader.cpp common/shader.hpp
        common/controls.cpp common/controls.hpp
        common/texture.cpp common/texture.hpp
        common/objloader.cpp common/objloader.hpp
        common/vboindexer.cpp common/vboindexer.hpp
        common/text2D.hpp common/text2D.cpp
        common/tangentspace.hpp common/tangentspace.cpp
        tutorial13_normal_mapping/NormalMapping.vertexshader
        tutorial13_normal_mapping/NormalMapping.fragmentshader
        )
target_link_libraries(tutorial13_normal_mapping ${ALL_GL_LIBS})

# Tutorial 14
add_executable(tutorial14_render_to_texture
        tutorial14_render_to_texture/tutorial14.cpp
        common/shader.cpp
        common/shader.hpp
        common/controls.cpp
        common/controls.hpp
        common/texture.cpp
        common/texture.hpp
        common/objloader.cpp
        common/objloader.hpp
        common/vboindexer.cpp
        common/vboindexer.hpp
        common/text2D.hpp
        common/text2D.cpp

        tutorial14_render_to_texture/StandardShadingRTT.vertexshader
        tutorial14_render_to_texture/StandardShadingRTT.fragmentshader
        tutorial14_render_to_texture/Passthrough.vertexshader
        tutorial14_render_to_texture/WobblyTexture.fragmentshader
        )
target_link_libraries(tutorial14_render_to_texture
        ${ALL_GL_LIBS}
        )

# Tutorial 15
add_executable(tutorial15_lightmaps
        tutorial15_lightmaps/tutorial15.cpp
        common/shader.cpp
        common/shader.hpp
        common/controls.cpp
        common/controls.hpp
        common/texture.cpp
        common/texture.hpp
        common/objloader.cpp
        common/objloader.hpp
        common/vboindexer.cpp
        common/vboindexer.hpp

        tutorial15_lightmaps/TransformVertexShader.vertexshader
        tutorial15_lightmaps/TextureFragmentShaderLOD.fragmentshader
        )
target_link_libraries(tutorial15_lightmaps
        ${ALL_GL_LIBS}
        )

# Tutorial 16, simple version
add_executable(tutorial16_shadowmaps_simple
        tutorial16_shadowmaps/tutorial16_SimpleVersion.cpp
        common/shader.cpp
        common/shader.hpp
        common/controls.cpp
        common/controls.hpp
        common/texture.cpp
        common/texture.hpp
        common/objloader.cpp
        common/objloader.hpp
        common/vboindexer.cpp
        common/vboindexer.hpp

        tutorial16_shadowmaps/ShadowMapping_SimpleVersion.vertexshader
        tutorial16_shadowmaps/ShadowMapping_SimpleVersion.fragmentshader
        tutorial16_shadowmaps/DepthRTT.vertexshader
        tutorial16_shadowmaps/DepthRTT.fragmentshader
        )
target_link_libraries(tutorial16_shadowmaps_simple
        ${ALL_GL_LIBS}
        )

# Tutorial 16
add_executable(tutorial16_shadowmaps
        tutorial16_shadowmaps/tutorial16.cpp
        common/shader.cpp
        common/shader.hpp
        common/controls.cpp
        common/controls.hpp
        common/texture.cpp
        common/texture.hpp
        common/objloader.cpp
        common/objloader.hpp
        common/vboindexer.cpp
        common/vboindexer.hpp

        tutorial16_shadowmaps/ShadowMapping.vertexshader
        tutorial16_shadowmaps/ShadowMapping.fragmentshader
        tutorial16_shadowmaps/DepthRTT.vertexshader
        tutorial16_shadowmaps/DepthRTT.fragmentshader
        tutorial16_shadowmaps/Passthrough.vertexshader
        tutorial16_shadowmaps/SimpleTexture.fragmentshader
        )
target_link_libraries(tutorial16_shadowmaps
        ${ALL_GL_LIBS}
        )

## Tutorial 17
#add_executable(tutorial17_rotations
#        tutorial17_rotations/tutorial17.cpp
#        common/shader.cpp
#        common/shader.hpp
#        common/controls.cpp
#        common/controls.hpp
#        common/texture.cpp
#        common/texture.hpp
#        common/objloader.cpp
#        common/objloader.hpp
#        common/vboindexer.cpp
#        common/vboindexer.hpp
#        common/quaternion_utils.cpp
#        common/quaternion_utils.hpp
#
#        tutorial17_rotations/StandardShading.vertexshader
#        tutorial17_rotations/StandardShading.fragmentshader
#        )
#target_link_libraries(tutorial17_rotations
#        ${ALL_GL_LIBS}
#        ANTTWEAKBAR_116_OGLCORE_GLFW
#        )

# tutorial 18
add_executable(tutorial18_billboards
        tutorial18_billboards_and_particles/tutorial18_billboards.cpp
        common/shader.cpp
        common/shader.hpp
        common/texture.cpp
        common/texture.hpp
        common/controls.cpp
        common/controls.hpp
        tutorial18_billboards_and_particles/Billboard.fragmentshader
        tutorial18_billboards_and_particles/Billboard.vertexshader)

target_link_libraries(tutorial18_billboards
        ${ALL_GL_LIBS})