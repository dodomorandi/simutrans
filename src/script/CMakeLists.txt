target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/api_class.cc
	${CMAKE_CURRENT_LIST_DIR}/api_function.cc
	${CMAKE_CURRENT_LIST_DIR}/api_param.cc
	${CMAKE_CURRENT_LIST_DIR}/dynamic_string.cc
	${CMAKE_CURRENT_LIST_DIR}/export_objs.cc
	${CMAKE_CURRENT_LIST_DIR}/script.cc
)

add_subdirectory(api)
