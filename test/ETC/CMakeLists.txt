file(GLOB testSrc
	"*.h"
	"*.cpp"
)

add_executable(ETC ${testSrc} )

target_link_libraries(ETC vulkan $<TARGET_OBJECTS:QPUassembler>)
add_dependencies(ETC QPUassembler)

add_testcase(ETC)
