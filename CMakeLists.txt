# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (cmake_practice)

# 查找当前目录下的所以源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

# 添加 math 子目录
add_subdirectory(math)

# 指定生成目标
add_executable(main ${DIR_SRCS})

# 添加链接库
target_link_libraries(main MathFunctions)

# 启用测试
enable_testing()

# 测试程序是否成功运行
add_test(test_run main 5 2)

# 测试帮助信息是否可以正常显示
add_test(test_usage main)
set_tests_properties(test_usage PROPERTIES PASS_REGULAR_EXPRESSION "Usage: .* base exponent")

# # 测试 5 的平方
# add_test(test_5_2 main 5 2)
# set_tests_properties(test_5_2 PROPERTIES PASS_REGULAR_EXPRESSION "is 25")

# # 测试 10 的 5 次方
# add_test(test_10_2 main 10 5)
# set_tests_properties(test_10_2 PROPERTIES PASS_REGULAR_EXPRESSION "is 100000")

# # 测试 2 的 10 次方
# add_test(test_2_10 main 2 10)
# set_tests_properties(test_2_10 PROPERTIES PASS_REGULAR_EXPRESSION "is 1024")

# 定义一个宏，用来简化测试工作
macro(do_test arg1 arg2 result)
  add_test(test_${arg1}_${arg2} main ${arg1} ${arg2})
  set_tests_properties(test_${arg1}_${arg2} PROPERTIES PASS_REGULAR_EXPRESSION ${result})
    
endmacro(do_test)


# 使用宏进行一系列的数据测试
do_test(5 2 "is 25")
do_test(10 5 "is 100000")
do_test(2 10 "is 1024")
