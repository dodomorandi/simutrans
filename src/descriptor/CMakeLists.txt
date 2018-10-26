target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/image.cc
	${CMAKE_CURRENT_LIST_DIR}/bridge_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/factory_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/ground_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/building_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/obj_base_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/sound_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/tunnel_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/vehicle_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/goods_desc.cc
	${CMAKE_CURRENT_LIST_DIR}/way_desc.cc
)

add_subdirectory(reader)
add_subdirectory(writer)
