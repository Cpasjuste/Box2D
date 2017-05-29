# Hello World examples
include_directories(${Box2D_SOURCE_DIR})

add_executable(HelloWorldVita Main.cpp Test.cpp Tests/TestEntries.cpp DebugDraw.cpp)

target_link_libraries(HelloWorldVita Box2D
        vita2d
        SceDisplay_stub SceGxm_stub SceSysmodule_stub
        SceCtrl_stub ScePgf_stub SceCommonDialog_stub
        psp2shell SceNetCtl_stub SceNet_stub SceAppMgr_stub
        )

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D__VITA__")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D__VITA__")

## Create Vita files
vita_create_self(HelloWorldVita.self HelloWorldVita UNSAFE)
# The FILE directive lets you add additional files to the VPK, the syntax is
# FILE src_path dst_path_in_vpk. In this case, we add the LiveArea paths.
vita_create_vpk(HelloWorldVita.vpk "VBOX2D123" HelloWorldVita.self
        VERSION "01.00"
        NAME "HelloWorldVita"
        )