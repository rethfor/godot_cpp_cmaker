cmake_minimum_required(VERSION 3.16)

add_subdirectory(godot-cpp SYSTEM)
get_target_property(GODOTCPP_SUFFIX godot::cpp GODOTCPP_SUFFIX)
set(GODOTCPP_SUFFIX ${GODOTCPP_SUFFIX} CACHE INTERNAL "Godot CPP Suffix")

project(godot_cpp_cmaker VERSION 0.1.0)
set(GODOTCPPMAKER_DIR ${CMAKE_CURRENT_SOURCE_DIR} CACHE INTERNAL "Godot CPP Maker Directory")

function(gdextension library_target)
	if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/game")
		set(OUT_DIR "${CMAKE_CURRENT_SOURCE_DIR}/game/bin")
	else()
		set(OUT_DIR "${CMAKE_BINARY_DIR}/bin")
	endif()

	target_link_libraries(${library_target} PRIVATE godot::cpp)
	set_target_properties(${library_target} PROPERTIES OUTPUT_NAME "${library_target}${GODOTCPP_SUFFIX}")
	set_target_properties(${library_target} PROPERTIES 
		RUNTIME_OUTPUT_DIRECTORY "${OUT_DIR}"
		RUNTIME_OUTPUT_DIRECTORY_DEBUG "${OUT_DIR}"
		RUNTIME_OUTPUT_DIRECTORY_RELEASE "${OUT_DIR}"
		RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO "${OUT_DIR}"
		RUNTIME_OUTPUT_DIRECTORY_MINSIZEREL "${OUT_DIR}"
	)
	configure_file(
		"${GODOTCPPMAKER_DIR}/gdextension.in"
		"${OUT_DIR}/${library_target}.gdextension"
		@ONLY
	)
endfunction()