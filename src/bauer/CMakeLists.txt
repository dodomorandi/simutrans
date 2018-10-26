target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/brueckenbauer.cc
	${CMAKE_CURRENT_LIST_DIR}/fabrikbauer.cc
	${CMAKE_CURRENT_LIST_DIR}/hausbauer.cc
	${CMAKE_CURRENT_LIST_DIR}/tunnelbauer.cc
	${CMAKE_CURRENT_LIST_DIR}/vehikelbauer.cc
	${CMAKE_CURRENT_LIST_DIR}/goods_manager.cc
	${CMAKE_CURRENT_LIST_DIR}/wegbauer.cc
)
