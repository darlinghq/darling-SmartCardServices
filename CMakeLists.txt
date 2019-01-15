project(SmartCardServices)

add_compile_options(
	-nostdinc
	-fblocks
	-Wno-gcc-compat
)

add_definitions(
	-DPCSC_DEBUG=1
	-DUSE_SYSLOG=1
	-DUSE_DAEMON=1
)

include_directories(BEFORE
	${CMAKE_CURRENT_SOURCE_DIR}/src/PCSC
	#${CMAKE_SOURCE_DIR}/src/external/libcxx/include
)

set(DYLIB_COMPAT_VERSION "1.0.0")
set(DYLIB_CURRENT_VERSION "1.0.0")

add_framework(PCSC
	FAT
	CURRENT_VERSION
	VERSION "A"

	SOURCES
		src/PCSC/readerstate.cpp
		src/PCSC/thread_macosx.c
		src/PCSC/musclecard.c
		src/PCSC/dyn_macosx.c
		src/PCSC/winscard_msg.cpp
		src/PCSC/tokenfactory.c
		src/PCSC/sys_unix.c
		src/PCSC/tokenparser.c
		src/PCSC/winscard_clnt.c
		src/PCSC/debug.c
		src/PCSC/error.c
		src/PCSC/pcscd_reader.cpp
		src/PCSC/readerfactory.c
		src/PCSC/atrhandler.c
		src/PCSC/configfile.c
		src/PCSC/eventhandler.cpp
		src/PCSC/ifdwrapper.c

	DEPENDENCIES
		system
		CoreFoundation
		security_utilities
		Security
		cxx
)

set_source_files_properties(src/PCSC/tokenparser.c APPEND_STRING PROPERTIES COMPILE_DEFINIONS -DYY_NO_UNPUT)
