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

然后安装中文字体：

```bash
apt install fonts-noto-color-emoji
cd /usr/share/fonts/meme-fonts && fc-cache -fv
```
