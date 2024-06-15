# arm64架构的MacBook，软件安装和配置记录

↩️[返回主页]

## 1.软件安装

### 1.1.App store

* 微信
* QQ
* 百度网盘
* 剪映专业版
* 腾讯会议
* 全能解压
* iBar (管理顶部标签栏)

### 1.2.安装包（dmg、pkg文件）

* Chrome
* Edge
* ClashX (🪜)
* Office 365 (含office三件套，onedrive)
* NDM (Neat Download Manager)(mac上的idm，配合浏览器下载插件使用)
* Adobe
* chatGPT (使用web端时提示下载)
* Termius (mac上取代mobaXterm)
* 阿里云盘
* IINA (播放器)
* VSCode
* Tencent Lemon (mac版电脑管家)
* OrbStack (替代docker desktop，资源消耗更少)
* LocalSend (局域网内文件传输)
* Snipaste (截图)
* Scroll Reverser (外接鼠标时，修正鼠标滚轮反向的问题)

### 1.3.终端指令

* oh-my-zsh (美化mac的zsh终端并安装好用的插件：zsh-autosuggestions、zsh-syntax-highlighting)
* Homebrew (包管理器，类似于ubuntu的apt)
* qt (使用brew安装qt和qt-creator)([Mac安装并配置qt])

## 2.docker相关

### 2.1.前提条件

*使用OrbStack平台来运行docker*

### 2.2.镜像架构

1. 直接使用linux/amd64架构的镜像也能够正常运行，但是可能会消耗更多资源
2. 直接使用linux/arm64结构的镜像

### 2.3.额外说明

1. 对于mysql系统，可以直接使用arm64架构的镜像，开发端和应用端的数据交互可以通过sql文件来实现。具体可参考，[linux导出导入sql文件]。

2. 对于js开发，例如使用vue编译。可以使用arm64架构的镜像。不过需要注意的是node_modules需要在对应镜像执行安装才可用。
    ```sh
    npm install
    ```
3. 如果使用dockerfile来创建新镜像，那么文件中涉及安装不同架构安装包或者程序的语句，需要修改架构。若是没有对应架构的安装包或者程序的，需要查找其他安装的办法，包括源码编译等

## 3.杂项记录

### 3.1.QT6安装使用webengine

尝试brew直接安装失败，因此尝试使用源码编译安装：

```sh
wget https://download.qt.io/official_releases/qt/6.6/6.6.0/submodules/qtwebengine-everywhere-src-6.6.0.tar.xz
tar -xf qtwebengine-everywhere-src-6.6.0.tar.xz
mkdir qtwebengine-everywhere-src-6.6.0/build && cd qtwebengine-everywhere-src-6.6.0/build
```

没有cmake、xcode和ninja的话需要先安装

```sh
brew install cmake
xcode-select --install
brew install ninja
```

然后编译并安装

```sh
cmake .. -G "Ninja" \
    -DCMAKE_PREFIX_PATH=/opt/homebrew/opt/qt \
    -DCMAKE_C_COMPILER=$(which clang) \
    -DCMAKE_CXX_COMPILER=$(which clang++) \
    -DCMAKE_MAKE_PROGRAM=$(which ninja)
ninja
ninja install
```

**使用webengine**
pro工程文件中添加

```pro
QT += core gui webenginewidgets
```

h头文件引入

```cpp
#include <QWebEngineView>
QWebEngineView *webEngineView;
```

cpp文件中使用

```cpp
ui->setupUi(this);

// 创建 QWebEngineView 并将其添加到主窗口
webEngineView = new QWebEngineView(this);
setCentralWidget(webEngineView);

// 加载网页
webEngineView->load(QUrl("https://www.example.com"));
```

[返回主页]:../README.md
[linux导出导入sql文件]:https://blog.csdn.net/guo_qiangqiang/article/details/85789735
[Mac安装并配置qt]:https://blog.csdn.net/weixin_46958677/article/details/130271259