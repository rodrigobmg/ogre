# Configure Mesh Lod demo build

set(HEADER_FILES include/MeshLod.h)
set(SOURCE_FILES src/MeshLodPlugin.cpp src/MeshLod.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
ogre_add_component_include_dir(MeshLodGenerator)

ogre_add_library_to_folder(Samples Sample_MeshLod ${OGRE_LIB_TYPE} ${SOURCE_FILES} ${HEADER_FILES})

target_link_libraries(Sample_MeshLod ${OGRE_LIBRARIES} ${SDL2_LIBRARY} ${OGRE_MeshLodGenerator_LIBRARIES})
ogre_config_sample_lib(Sample_MeshLod)

if (APPLE AND NOT APPLE_IOS)
    # Set the INSTALL_PATH so that Samples can be installed in the application package
    set_target_properties(Sample_MeshLod
       PROPERTIES BUILD_WITH_INSTALL_RPATH 1
       INSTALL_NAME_DIR "@executable_path/../Plugins"
    )
endif()

