set(PROJECT_NAME libhello)
project(${PROJECT_NAME})

set(LIB_SRC hello.cpp)

#add new target "libhello"
#生成静态库：设置目标属性修改生成的静态库的库名
add_library(${PROJECT_NAME}_static ${LIB_SRC})
set_target_properties(${PROJECT_NAME}_static PROPERTIES OUTPUT_NAME "hello")

#生成动态库；设置目标属性修改生成的动态库的库名
add_library(${PROJECT_NAME} SHARED ${LIB_SRC})
#set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

#set lib name to hello.so or libhello.a 
set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "hello")


# 设置库版本号：VERSION 指代动态库版本,SOVERSION 指代 API 版本
set(HELLOLIB_VERSION_MAJOR 1)
set(HELLOLIB_VERSION_MINOR 0)
set(HELLOLIB_SOVERSION 1)

set_target_properties(${PROJECT_NAME} PROPERTIES VERSION ${HELLOLIB_VERSION_MAJOR}.${HELLOLIB_VERSION_MINOR} SOVERSION ${HELLOLIB_SOVERSION})

###########################################################
# 安装脚本
###########################################################
install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}_static
  LIBRARY DESTINATION "lib"
  ARCHIVE DESTINATION "lib/static")

install(FILES hello.h 
	DESTINATION include)