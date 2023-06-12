file(GLOB testSrc
	"*.h"
	"*.cpp"
)

add_executable(varyings ${testSrc} )

target_link_libraries(varyings vulkan $<TARGET_OBJECTS:QPUassembler>)
add_dependencies(varyings QPUassembler)

add_testcase(varyings)
