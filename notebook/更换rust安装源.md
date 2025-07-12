# 使用国内源安装 Rust

使用官方脚本:`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh` 但是这个安装过程非常慢，且没有进度条，估计是下载速度不行。

参照网上的做法，可以先下载官方的安装脚本，然后将其中的下载源替换为国内的源即可。

1. 所以，先保存 Rust 官方的安装脚本:
    `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > rust.sh`
    当前文件夹会生成一个`rust.sh`文件

2. 替换国内源
    打开 rust.sh，替换 `RUSTUP_UPDATE_ROOT` 为：`RUSTUP_UPDATE_ROOT="https://mirrors.aliyun.com/rust-static/rustup"`
    保存退出。

3. 然后修改环境变量：
    `export RUSTUP_DIST_SERVER=https://mirrors.aliyun.com/rustup`

4. 安装
    给安装脚本加上可执行权限，然后执行即可开始下载并安装 Rust：

    `chmod +x rust.sh`
    `./rust.sh`
    根据安装提示：使用默认设置，敲回车即可。

    如果出现`Rust is installed now. Great!`表示安装成功

5. 查看版本
    `cargo --version`
    注：cargo 是官方的 Rust 包管理工具。

6. 配置文件
    ~/.cargo/config

    ``` bash
    [source.crates-io]
    registry = "https://github.com/rust-lang/crates.io-index"
    # 指定镜像
    replace-with = 'tuna' # 如：tuna、sjtu、ustc，或者 rustcc

    # 注：以下源配置一个即可，无需全部

    # 中国科学技术大学
    [source.ustc]
    registry = "https://mirrors.ustc.edu.cn/crates.io-index"

    # 上海交通大学
    [source.sjtu]
    registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index/"

    # 清华大学
    [source.tuna]
    registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

    # rustcc社区
    [source.rustcc]
    registry = "https://code.aliyun.com/rustcc/crates.io-index.git"
    ```

7 . rustup update 也缓慢 同样更新:

```bush
~/.bash_profile

修改 export RUSTUP_UPDATE_ROOT="https://mirrors.aliyun.com/rust-static/rustup"
修改 export RUSTUP_DIST_SERVER="https://mirrors.aliyun.com/rustup"

source ~/.bash_profile
```

## 安装包时候慢的方法

1. 步骤一：进入Cargo配置目录
    打开终端或命令提示符，进入用户主目录下的.cargo文件夹。在Windows系统中，主目录通常是C:\Users\用户名\，而在类Unix系统中，主目录是/home/用户名/。

    > cd $HOME/.cargo

2. 步骤二：删除.package-cache文件
    在.cargo目录中，找到并删除名为.package-cache的文件。

    > rm .package-cache

3. 步骤三：创建并编辑配置文件
    创建一个名为config的文件，注意不要加文件后缀。

    > touch config

    使用文本编辑器打开config文件，并将以下内容添加到文件中：

    ```bush
    [source.crates-io]
    replace-with = 'aliyun' # 指定使用下面哪个源，修改为source.后面的内容即可
    #阿里云
    [source.aliyun]
    registry = "sparse+https://mirrors.aliyun.com/crates.io-index/"
    # 中国科学技术大学
    [source.ustc]
    registry = "https://mirrors.ustc.edu.cn/crates.io-index"
    # 上海交通大学
    [source.sjtu]
    registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index/"
    # 清华大学
    [source.tuna]
    registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"
    # rustcc社区
    [source.rustcc]
    registry = "https://code.aliyun.com/rustcc/crates.io-index.git"
    ```

    保存并关闭文件。
