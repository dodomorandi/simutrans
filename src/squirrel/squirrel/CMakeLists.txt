target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/sqapi.cc
	${CMAKE_CURRENT_LIST_DIR}/sqclass.cc
	${CMAKE_CURRENT_LIST_DIR}/sqdebug.cc
	${CMAKE_CURRENT_LIST_DIR}/sqlexer.cc
	${CMAKE_CURRENT_LIST_DIR}/sqobject.cc
	${CMAKE_CURRENT_LIST_DIR}/sqtable.cc
	${CMAKE_CURRENT_LIST_DIR}/sqbaselib.cc
	${CMAKE_CURRENT_LIST_DIR}/sqcompiler.cc
	${CMAKE_CURRENT_LIST_DIR}/sqfuncstate.cc
	${CMAKE_CURRENT_LIST_DIR}/sqmem.cc
	${CMAKE_CURRENT_LIST_DIR}/sqstate.cc
	${CMAKE_CURRENT_LIST_DIR}/sqvm.cc
)
