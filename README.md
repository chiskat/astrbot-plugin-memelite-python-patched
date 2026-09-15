# astrbot-plugin-memelite-python-patched

[astrbot_plugin_memelite](https://github.com/Zhalslar/astrbot_plugin_memelite) 的 fork，基于旧 Python 版但处理 `Pillow` 依赖链，使它和最新版 Astrbot 兼容。

文档请参考原始仓库，本文仅作补充。

# 使用方法

GitHub 点击 “Code” 按钮，下拉菜单中选择 “Download ZIP” 下载压缩包；Astrbot 插件管理页面右下角 “安装插件”，选中压缩包即可安装。

# 更新说明

此项目将原始上游依赖 Python 版 [meme-generator](https://github.com/MemeCrafters/meme-generator) 替换为了由我 fork 的 [meme-generator-next](https://github.com/chiskat/meme-generator-next) v0.2.3，它的 `Pillow` 版本已兼容 Astrbot，且支持通过环境变量自定义配置文件路径。

# 疑难解答

## 依赖项 `pycairo` 安装失败

因为部分表情包需要 `pycairo` 依赖，因此依赖项 `meme-generator-next` 依赖了 `pycairo`；而 PyPI 只提供 Windows 的 wheel，在 Linux/ARM 容器中会从源码编译，因此需要 `pkg-config` 和 Cairo 开发头文件。

如果安装插件时报错：

```text
Dependency lookup for cairo with method 'pkg-config' failed
```

则可以安装开发头文件：

```bash
apt update
apt install -y --no-install-recommends pkg-config libcairo2-dev
```

## Docker 中运行失败

补全一些图形相关软件包：

```bash
chmod 1777 /tmp
apt update
apt install -y libgl1 libglib2.0-0 libgl1-mesa-dev
```

## 处理中文字体和 Emoji

解决方式：

```bash
export LANG=en_US.UTF-8
```

如果是 Docker 部署，修改 `docker-compose.yml` 为：

```yaml
services:
  astrbot:
    entrypoint: ['bash', '-c', 'export LANG=en_US.UTF-8 && python main.py']
```

然后进入容器内，创建字体目录：

```bash
cd /usr/share/fonts
mkdir meme-fonts
```

将 [meme-generator 字体目录](https://github.com/chiskat/meme-generator-next/src/branch/main/resources/fonts) 中的字体拷贝到此目录中。

然后刷新字体缓存：

```bash
cd /usr/share/fonts/meme-fonts
fc-cache -fv
```

---

如果是 Linux 系统，需要用到 emoji 字体，可以这样安装：

```bash
apt install fonts-noto-color-emoji
```
