# astrbot-plugin-memelite-fix-deps

[astrbot_plugin_memelite](https://github.com/Zhalslar/astrbot_plugin_memelite) 的 fork，基于旧 Python 版但处理 Pillow 依赖链，使它和最新版 Astrbot 兼容。

# 使用方法

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

将 [meme-generator 字体目录](https://git.paperplane.cc/chiskat/meme-generator-fix-deps/src/branch/main/resources/fonts) 中的字体拷贝到此目录中。

然后刷新字体缓存：

```bash
cd /usr/share/fonts/meme-fonts
fc-cache -fv
```

如果需要用到 emoji 字体，可以这样安装：

```bash
apt install fonts-noto-color-emoji
```
