set(UE4_PLUGINS_DIR ${PROJECT_SOURCE_DIR}/Unreal/CarlaUE4/Plugins)


set(STREETMAP_SRC ${CMAKE_CURRENT_LIST_DIR}/StreetMap)
set(STREETMAP_PKG_NAME StreetMap)
set(STREETMAP_PLUGIN_NAME Streetmap)

add_custom_target(
    install_stree_map
    COMMAND rm -Rf ${UE4_PLUGINS_DIR}/${STREETMAP_PLUGIN_NAME}
    COMMAND cp -R ${STREETMAP_SRC} ${UE4_PLUGINS_DIR}
    COMMAND mv ${UE4_PLUGINS_DIR}/${STREETMAP_PKG_NAME} ${UE4_PLUGINS_DIR}/${STREETMAP_PLUGIN_NAME}
    WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
)


set(HOUDINI_SRC ${CMAKE_CURRENT_LIST_DIR}/HoudiniEngineForUnreal)
set(HOUDINI_PKG_NAME HoudiniEngineForUnreal)
set(HOUDINI_PLUGIN_NAME HoudiniEngine)

add_custom_target(
    install_houdini
    COMMAND rm -Rf ${UE4_PLUGINS_DIR}/${HOUDINI_PLUGIN_NAME}
    COMMAND cp -R ${HOUDINI_SRC} ${UE4_PLUGINS_DIR}
    COMMAND mv ${UE4_PLUGINS_DIR}/${HOUDINI_PKG_NAME} ${UE4_PLUGINS_DIR}/${HOUDINI_PLUGIN_NAME}
    WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
)


add_custom_target(
    install_extra_plugins
    DEPENDS install_houdini install_stree_map
)
