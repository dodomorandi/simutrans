
add_executable(nettool
	nettool.cc
)

target_compile_definitions(nettool PRIVATE NETTOOL=1)

# these source files produce the same object code in nettool and simutrans
target_sources(nettool PRIVATE
	../dataobj/freelist.cc
	../network/memory_rw.cc
	../network/network_address.cc
	../network/network_cmd.cc
	../network/network_packet.cc
	../network/network_socket_list.cc
	../network/pwd_hash.cc
	../simdebug.cc
	../simmem.cc
	../utils/simstring.cc
	../utils/fetchopt.cc
	../utils/sha1.cc
)

# these source files produce different object code in nettool and simutrans
target_sources(nettool PRIVATE
	../utils/log.cc
	../network/network.cc
	../network/network_file_transfer.cc
)
