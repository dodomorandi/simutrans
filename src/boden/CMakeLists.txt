target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/boden.cc
	${CMAKE_CURRENT_LIST_DIR}/brueckenboden.cc
	${CMAKE_CURRENT_LIST_DIR}/fundament.cc
	${CMAKE_CURRENT_LIST_DIR}/grund.cc
	${CMAKE_CURRENT_LIST_DIR}/monorailboden.cc
	${CMAKE_CURRENT_LIST_DIR}/tunnelboden.cc
	${CMAKE_CURRENT_LIST_DIR}/wasser.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/kanal.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/maglev.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/monorail.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/narrowgauge.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/runway.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/schiene.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/strasse.cc
	${CMAKE_CURRENT_LIST_DIR}/wege/weg.cc
)

add_subdirectory(wege)
