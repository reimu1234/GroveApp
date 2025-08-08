cmake_minimum_required(VERSION 3.22.1)
project(grove_app_lib)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 创建一个示例源文件
file(WRITE ${CMAKE_CURRENT_SOURCE_DIR}/native-lib.cpp
"#include <jni.h>
#include <string>

extern \"C\" JNIEXPORT jstring JNICALL
Java_com_groveapp_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = \"Hello from C++\";
    return env->NewStringUTF(hello.c_str());
}")

# 添加库
add_library(${PROJECT_NAME} SHARED
    native-lib.cpp
)

# 查找并链接需要的库
find_library(log-lib log)

target_link_libraries(${PROJECT_NAME}
    ${log-lib}
)
