---
{"tags":["命令行","Linux"],"source":["自学","实验"],"dg-publish":true,"permalink":"/Knowledge Garden/01_Research/Linux/cmd learning/","dgPassFrontmatter":true,"created":"2026-04-22T23:03:18.994+08:00","updated":"2026-04-27T11:10:40.566+08:00","dg-note-properties":{"tags":["命令行","Linux"],"source":["自学","实验"]}}
---

# 开源软件通用编译
1. 更新系统源
```
   sudo apt update && sudo apt update -y
   // -y意为默认选择yes
```

2. 安装通用的编译工具链
```
	sudo apt install -y build-essential cmake git pkg-config
	// pkg-config可以理解为一个查询接口，帮助找到已安装的库的信息（路径、链接参数等等）
```

3. 下载源码，往往通过`git clone`。当缺失子模块时，需要进行补充。常见命令为
```
    git clone --recursive <url>  
    git submodule update --init --recursive
    // --init选项大概就是告知子模块存在（注册）  --recursive递归拉取，确保子模块都补充完整
```
 
 4. 安装项目依赖
    阅读项目的`README.md`文件，查看如何编译部署。

5. 创建build目录，进行编译out-of-source编译，build目录不污染源码目录，删除掉build就等于clean
```
	 mkdir build && cd build
	 cmake ..  // cmake .. 去上一级目录找到cmakeLists.txt，依据此生成合适的makefile
	 make -j$(nproc)  // -j jobs,并行编译 $(nproc==CPU的核心数量) 接近最快
	 sudo make install
```

6. 测试安装是否成功
```
	  which 程序名
	  程序名 --version
```

## 卸载已经编译安装的软件
1. 进入编译目录
```
	cd ~/软件名/build 
```

2. 自动卸载（彻底干净）
```
    sudo make uninstall
```

3. 清理编译残留
```
    cd ..
    rm -rf build
```

4. 删除源码
```
    cd ~
    rm -rf 软件名
```

