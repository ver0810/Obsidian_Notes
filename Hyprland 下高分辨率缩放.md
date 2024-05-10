
> [!Info] Hyprland 在高分辨率下的某些软件会出现模糊

解决办法禁用xwayland缩放，在*~/.config/hypr/hyprland.conf*

```bash
# 先禁用XWayland的缩放
# unscale XWayland
xwayland {
  force_zero_scaling = true
}

# toolkit-specific scale
env = GDK_SCALE,2
env = XCURSOR_SIZE,32

```

```bash
# 然后设置DPI为两倍（96是一倍，144是1.5倍，192是2倍）
nano ~/.Xresources
# 输入
Xft.dpi: 192
# 应用效果
xrdb -merge ~/.Xresources
```

> [!Note] 在设置上述后，会出现输入法的框错位的情况

**对于electron**
可以单个给软件设置命令行参数，或者时全局配置

将/usr/share/applicatios 复制到 家目录下的 ~/.local/share/applications 可以防止