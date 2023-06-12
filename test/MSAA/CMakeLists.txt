file(GLOB testSrc
	"*.h"
	"*.cpp"
)

add_executable(MSAA ${testSrc} )

target_link_libraries(MSAA vulkan $<TARGET_OBJECTS:QPUassembler>)
add_dependencies(MSAA QPUassembler)

add_testcase(MSAA)
