include(CommonModularInterface)
INCLUDE_DIRECTORIES(${RUBY_INCLUDE_DIRS} ${RUBY_NARRAY_INCLUDE_DIR})

GENERATE_MODULAR_TARGET(ruby ${CMAKE_CURRENT_SOURCE_DIR} ${RUBY_LIBRARY})
set_target_properties(ruby_modular PROPERTIES PREFIX "")

SET(RUBY_MODULAR_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR} PARENT_SCOPE)
SET(RUBY_MODULAR_BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR} PARENT_SCOPE)
EXECUTE_PROCESS(COMMAND ${RUBY_EXECUTABLE} -r rbconfig -e "print RbConfig::CONFIG['sitearchdir']"
		OUTPUT_VARIABLE RUBY_SITE_ARCH_DIR
		ERROR_QUIET)

INSTALL(FILES ${CMAKE_CURRENT_SOURCE_DIR}/modshogun.rb
	DESTINATION ${RUBY_SITE_ARCH_DIR}
	COMPONENT ruby)

INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/modshogun.so
	DESTINATION ${RUBY_SITE_ARCH_DIR}
	COMPONENT ruby
	RENAME modshogun${EXT_LIB_SWIG_RUBY_MODULAR})
