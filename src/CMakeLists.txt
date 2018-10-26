add_executable(simutrans
	freight_list_sorter.cc
	old_blockmanager.cc
	simcity.cc
	simconvoi.cc
	simdebug.cc
	simdepot.cc
	simobj.cc
	simevent.cc
	simfab.cc
	simhalt.cc
	siminteraction.cc
	simintr.cc
	simio.cc
	simline.cc
	simlinemgmt.cc
	simloadingscreen.cc
	simmain.cc
	simmem.cc
	simmenu.cc
	simmesg.cc
	simplan.cc
	simskin.cc
	simsound.cc
	simsys.cc
	simticker.cc
	simtool.cc
	simware.cc
	simworld.cc
	unicode.cc
)

if (WIN32)
	target_sources(simutrans PRIVATE clipboard_w32.cc)
else (WIN32)
	target_sources(simutrans PRIVATE clipboard_internal.cc)
endif (WIN32)


if (SIMUTRANS_BUILD_HEADLESS)
	target_sources(simutrans PRIVATE display/simgraph0.cc)
	target_compile_definitions(simutrans PRIVATE COLOUR_DEPTH=0)
else (SIMUTRANS_BUILD_HEADLESS)
	target_sources(simutrans PRIVATE display/simgraph16.cc)
	target_compile_definitions(simutrans PRIVATE COLOUR_DEPTH=16)
endif (SIMUTRANS_BUILD_HEADLESS)


# Backup sound and music routines if the selected backend does not provide any routines
if (WIN32 OR MINGW)
	set(BACKUP_SOUND sound/win32_sound.cc)
	set(BACKUP_MUSIC music/w32_midi.cc)
else (WIN32 OR MINGW)
	set(BACKUP_SOUND sound/no_sound.cc)
	set(BACKUP_MUSIC music/no_midi.cc)
endif (WIN32 OR MINGW)


if (SIMUTRANS_BACKEND STREQUAL "sdl")
	target_sources(simutrans PRIVATE simsys_s.cc sound/sdl_sound.cc ${BACKUP_MUSIC})
	target_include_directories(simutrans PRIVATE ${SDL_INCLUDE_DIR})
	target_link_libraries(simutrans ${SDL_LIBRARY})

elseif (SIMUTRANS_BACKEND STREQUAL "mixer_sdl")
	target_sources(simutrans PRIVATE simsys_s.cc sound/sdl_mixer_sound.cc music/sdl_midi.cc)
	target_include_directories(simutrans PRIVATE ${SDL_INCLUDE_DIR} ${SDL_MIXER_INCLUDE_DIRS})
    target_link_libraries(simutrans PRIVATE ${SDL_LIBRARY} ${SDL_MIXER_LIBRARIES})

elseif (SIMUTRANS_BACKEND STREQUAL "sdl2")
	target_sources(simutrans PRIVATE simsys_s2.cc ${BACKUP_SOUND} ${BACKUP_MUSIC})
	target_include_directories(simutrans PRIVATE ${SDL2_INCLUDE_DIRS})
	target_link_libraries(simutrans PRIVATE ${SDL2_LIBRARIES})

elseif (SIMUTRANS_BACKEND STREQUAL "allegro")
	target_sources(simutrans PRIVATE simsys_d.cc sound/allegro_sound.cc music/allegro_midi.cc)
	target_link_libraries(simutrans Allegro::Allegro)

elseif (SIMUTRANS_BACKEND STREQUAL "opengl")
	target_sources(simutrans PRIVATE simsys_opengl.cc sound/sdl_sound.cc ${BACKUP_MUSIC})
	target_include_directories(simutrans PRIVATE ${SDL_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR})
	target_link_libraries(simutrans ${SDL_LIBRARY} ${OPENGL_LIBRARIES} GLEW::GLEW)
endif ()

add_subdirectory(bauer)
add_subdirectory(boden)
add_subdirectory(dataobj)
add_subdirectory(descriptor)
add_subdirectory(display)
add_subdirectory(finder)
add_subdirectory(gui)
add_subdirectory(network)
add_subdirectory(obj)
add_subdirectory(player)
add_subdirectory(script)
add_subdirectory(squirrel)
add_subdirectory(utils)
add_subdirectory(vehicle)

#
# Nettool/Makeobj
#
if (SIMUTRANS_BUILD_MAKEOBJ)
	add_subdirectory(makeobj)
endif (SIMUTRANS_BUILD_MAKEOBJ)


if (SIMUTRANS_BUILD_NETTOOL)
	add_subdirectory(nettools)
endif (SIMUTRANS_BUILD_NETTOOL)

#
# Link dependencies
#
target_link_libraries(simutrans PRIVATE
	ZLIB::ZLIB
	PNG::PNG
	BZip2::BZip2
)

if (SIMUTRANS_USE_FREETYPE)
	target_compile_options(simutrans PRIVATE -DUSE_FREETYPE=1)
	target_include_directories(simutrans PRIVATE ${FREETYPE_INCLUDE_DIRS})
	target_link_libraries(simutrans PRIVATE ${FREETYPE_LIBRARIES})
endif (SIMUTRANS_USE_FREETYPE)

if (SIMUTRANS_USE_UPNP)
	target_compile_definitions(simutrans PRIVATE USE_UPNP=1)
	target_link_libraries(simutrans PRIVATE MiniUPNP::MiniUPNP)
endif (SIMUTRANS_USE_UPNP)

if (SIMUTRANS_MULTI_THREAD)
	target_compile_definitions(simutrans PRIVATE MULTI_THREAD)
	target_link_libraries(simutrans PRIVATE Threads::Threads)
endif (SIMUTRANS_MULTI_THREAD)

#
# compile options
#
if (SIMUTRANS_BIG_ENDIAN)
	add_definitions(simutrans PRIVATE SIM_BIG_ENDIAN)
endif ()

if (SIMUTRANS_VALGRIND_SUPPORT)
	add_definitions(-DUSE_VALGRIND_MEMCHECK=1)
endif ()

if (SIMUTRANS_ENABLE_PROFILING)
	add_definitions(-DPROFILE=1)
endif ()

include(simutrans-compile-options)
target_compile_options(simutrans PRIVATE ${SIMUTRANS_COMMON_COMPILE_OPTIONS})

if (NOT CMAKE_SIZEOF_VOID_P EQUAL 4)
	if (SIMUTRANS_BUILD_32BIT)
		target_compile_options(simutrans PRIVATE -m32)
		set_target_properties(simutrans PROPERTIES LINK_FLAGS "-m32")
	else ()
		# For now, emit a warning when compiling as 64 bit binary
		message(WARNING "Simutrans is preferrably compiled as a 32 bit binary!")
	endif (SIMUTRANS_BUILD_32BIT)
endif (NOT CMAKE_SIZEOF_VOID_P EQUAL 4)


target_compile_definitions(simutrans PRIVATE $<IF:$<CONFIG:Debug>,DEBUG=1,NDEBUG>)
target_compile_definitions(simutrans PRIVATE ENABLE_WATERWAY_SIGNS=0 AUTOJOIN_PUBLIC=0)

if (SIMUTRANS_WITH_REVISION)
	target_compile_definitions(simutrans PRIVATE REVISION=${SIMUTRANS_WC_REVISION})
endif ()

