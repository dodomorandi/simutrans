target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/sq_extensions.cc
)

add_subdirectory(squirrel)
add_subdirectory(sqstdlib)
