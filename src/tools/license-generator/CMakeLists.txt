

include_directories(${Boost_INCLUDE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
link_directories ("F:\\boost_1_55_0\\stage\\lib\\")

message("license-generator boost_library_dir"  ${Boost_LIBRARY_DIR})
message("license-generator boost_include_dir"  ${Boost_INCLUDE_DIR})

ADD_LIBRARY(
    license_generator_lib STATIC
    license-generator.cpp
)


target_link_libraries(
     license_generator_lib
     tools_base
     license++_static
     $<$<CONFIG:Debug>:libboost_system-vc-mt-sgd-1_55.lib>
     $<$<NOT:$<CONFIG:Debug>>:libboost_system-vc-mt-s-1_55>	 
	 $<$<CONFIG:Debug>:libboost_program_options-vc-mt-sgd-1_55.lib>
     $<$<NOT:$<CONFIG:Debug>>:libboost_program_options-vc-mt-s-1_55>	 
    #  libboost_system-vc-mt-s-1_55
    #  libboost_program_options-vc-mt-s-1_55
	
     ${EXTERNAL_LIBS}
)

message("external_libs: "  ${EXTERNAL_LIBS})
message("CMAKE_LIBRARY_PATH " ${CMAKE_LIBRARY_PATH})

add_executable(
 license_generator
 license-generator-main.cpp
)

target_link_libraries(
    license_generator
    license_generator_lib
)
add_dependencies( license_generator private_key )

install(TARGETS license_generator RUNTIME DESTINATION bin)

#SET_TARGET_PROPERTIES(license_generator PROPERTIES LINK_SEARCH_START_STATIC ON)
#SET_TARGET_PROPERTIES(license_generator PROPERTIES LINK_SEARCH_END_STATIC ON)
