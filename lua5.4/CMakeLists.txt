######################################################################################################################
#           1,CMAKE_BINARY_DIR
#             PROJECT_BINARY_DIR
#            <projectname>_BINARY_DIR
#           这三个变量指代的内容是一致的,如果是 in source 编译,指得就是工程顶层目录,如果是 out-of-source 编译,
#           指的是工程编译发生的目录。PROJECT_BINARY_DIR 跟其他指令稍有区别,现在,你可以理解为他们是一致的。
#           2,CMAKE_SOURCE_DIR
#              PROJECT_SOURCE_DIR
#              <projectname>_SOURCE_DIR
#           这三个变量指代的内容是一致的,不论采用何种编译方式,都是工程顶层目录。
#           也就是在 in source 编译时,他跟 CMAKE_BINARY_DIR 等变量一致。
#           PROJECT_SOURCE_DIR 跟其他指令稍有区别,现在,你可以理解为他们是一致的。
#           
#           3,CMAKE_CURRENT_SOURCE_DIR
#           指的是当前处理的 CMakeLists.txt 所在的路径,比如上面我们提到的 src 子目录。
#             
#           4.CMAKE_CURRENT_BINARY_DIR
#           如果是 in-source 编译,它跟 CMAKE_CURRENT_SOURCE_DIR 一致,如果是 out-of-source ,他指的是 target 编译目录。
#           使用我们上面提到的 ADD_SUBDIRECTORY(src bin)可以更改这个变量的值。
#           使用 SET(EXECUTABLE_OUTPUT_PATH <新路径>)并不会对这个变量造成影响,它仅仅修改了最终目标文件存放的路径。
#           
#           5,CMAKE_CURRENT_LIST_FILE
#           输出调用这个变量的 CMakeLists.txt 的完整路径
#            
#           6,CMAKE_CURRENT_LIST_LINE
#           输出这个变量所在的行# 
       
#           SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /NODEFAULTLIB:msvcrt.lib ")
#           SET(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} /NODEFAULTLIB:msvcrt.lib ") 
######################################################################################################################

 

#当前目录
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})
#编译生成中间文件目录
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR} )

set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib)

# 修改 CPP 使用SEH
SET(SRCS

    lapi.c
    lauxlib.c
    lbaselib.c
    lcode.c
    lcorolib.c
    lctype.c
    ldblib.c
    ldebug.c
    ldo.c
    ldump.c
    lfunc.c
    lgc.c
    linit.c
    liolib.c
    llex.c
    lmathlib.c
    lmem.c
    loadlib.c
    lobject.c
    lopcodes.c
    loslib.c
    lparser.c
    lstate.c
    lstring.c
    lstrlib.c
    ltable.c
    ltablib.c
    ltm.c
    lundump.c
    lutf8lib.c
    lvm.c
    lzio.c



)
#aux_source_directory(. SRCS)
#MESSAGE(${SRCS})

 
add_library(lua STATIC 
    ${SRCS}
)
 
#生成WINDOWS应用程序,不启动 console 
#set_target_properties(lua PROPERTIES LINK_FLAGS "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup")

#引用 .lib 库
#TARGET_LINK_LIBRARIES(lua ${QT_LIBRARIES})

#INSTALL(TARGETS lua
#    RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/bin
#    ARCHIVE DESTINATION ${PROJECT_SOURCE_DIR}/bin
#    LIBRARY DESTINATION ${PROJECT_SOURCE_DIR}/lib
#)


#引用 .lib 库


add_executable( luac 
    luac.c
)

target_link_libraries(luac lua)
add_dependencies( luac lua)

#INSTALL(TARGETS lua
#    RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/bin
#    ARCHIVE DESTINATION ${PROJECT_SOURCE_DIR}/bin
#    LIBRARY DESTINATION ${PROJECT_SOURCE_DIR}/lib
#)

