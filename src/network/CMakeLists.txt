target_sources(simutrans PRIVATE
	${CMAKE_CURRENT_LIST_DIR}/checksum.cc
	${CMAKE_CURRENT_LIST_DIR}/memory_rw.cc
	${CMAKE_CURRENT_LIST_DIR}/network.cc
	${CMAKE_CURRENT_LIST_DIR}/network_address.cc
	${CMAKE_CURRENT_LIST_DIR}/network_cmd.cc
	${CMAKE_CURRENT_LIST_DIR}/network_cmd_ingame.cc
	${CMAKE_CURRENT_LIST_DIR}/network_cmd_scenario.cc
	${CMAKE_CURRENT_LIST_DIR}/network_cmp_pakset.cc
	${CMAKE_CURRENT_LIST_DIR}/network_file_transfer.cc
	${CMAKE_CURRENT_LIST_DIR}/network_packet.cc
	${CMAKE_CURRENT_LIST_DIR}/network_socket_list.cc
	${CMAKE_CURRENT_LIST_DIR}/pakset_info.cc
	${CMAKE_CURRENT_LIST_DIR}/pwd_hash.cc
)
