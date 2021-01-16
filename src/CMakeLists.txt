cmake_minimum_required(VERSION 3.0.0)
add_definitions(-DWIN32 -DWIN32_LEAN_AND_MEAN -D_WIN32_WINNT=0x501)
#目录下所以源文件
set(SRC_FILES)
file(GLOB_RECURSE SRC_FILES ${PROJECT_SOURCE_DIR}/src/*)
#从变量中排除指定文件不参与编译
list(REMOVE_ITEM SRC_FILES ${PROJECT_SOURCE_DIR}/src/CMakeLists.txt)
#遍历所以子目录
set(SUB_INCLUDE_DIR)
file(GLOB children ${PROJECT_SOURCE_DIR}/src/*)
#把子目录添加到引入头文件目录
foreach(child ${children})
    if(IS_DIRECTORY ${child})
        list(APPEND SUB_INCLUDE_DIR ${child})
    endif()
endforeach()
list(APPEND SUB_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/src)
# 引入头文件目录
set(THIRDPARTY_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/thirdparty/include)
#第三方库请编译好放在这里
set(THIRDPARTY_LIB_DIR ${PROJECT_SOURCE_DIR}/thirdparty/lib)
include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(${THIRDPARTY_INCLUDE_DIR})
include_directories(${SUB_INCLUDE_DIR})
#生成静态库
add_library(librocketmq STATIC ${SRC_FILES})
#引入依赖库
target_link_libraries(librocketmq STATIC 
jsoncpp_lib_static.lib
event.lib
event_core.lib
event_extra.lib
event_openssl.lib
event_mbedtls.lib
)

