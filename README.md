# astrbot-plugin-memelite-python-patched

[astrbot_plugin_memelite](https://github.com/Zhalslar/astrbot_plugin_memelite) 的 fork，基于旧 Python 版但处理 `Pillow` 依赖链，使它和最新版 Astrbot 兼容。

文档请参考原始仓库，本文仅作补充。

# 使用方法

GitHub 点击 “Code” 按钮，下拉菜单中选择 “Download ZIP” 下载压缩包；Astrbot 插件管理页面右下角 “安装插件”，选中压缩包即可安装。

# 更新说明

此项目将原始上游依赖 Python 版 [meme-generator](https://github.com/MemeCrafters/meme-generator) 替换为了由我 fork 的 [meme-generator-next](https://github.com/chiskat/meme-generator-next) v0.1.18，它的 `Pillow` 版本已兼容 Astrbot，且支持通过环境变量自定义配置文件路径。

# 疑难解答

Docker 部署的 AstrBot，直接安装本插件可能会报错，可能是缺系统依赖，进入容器执行：

```bash
chmod 1777 /tmp
apt update
apt install -y libgl1 libglib2.0-0 libgl1-mesa-dev
```

---

出现中文乱码时，修改 `docker-compose.yml` 为：

```yaml
services:
  astrbot:
    entrypoint: ['bash', '-c', 'export LANG=en_US.UTF-8 && python main.py']
```

进入容器内，创建字体目录：

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

如果需要用到 emoji 字体，可以这样安装：

```bash
apt install fonts-noto-color-emoji
```
