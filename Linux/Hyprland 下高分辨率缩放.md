
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

### electron

> [!Note] 以下的解决方案来自 archwiki

可以单个给软件设置命令行参数，或者时全局配置
将**/usr/share/applicatios/.desktop** 启动文件 复制到 家目录下的 **~/.local/share/applications** 可以防止系统在更新时覆盖。在启动时添加该行参数。

为每个应用单独添加命令行参数或者编写全局配置文件，可以为 Electron 应用添加 Wayland 支持。
命令行参数

为了让基于 electron包 的应用在 Wayland 下运行，必须添加这些命令行参数 (例如 Electron 20 中): **--ozone-platform-hint=auto**

如果运行时发现应用没有标题栏，请将上述参数修改为**--enable-features=WaylandWindowDecorations**。此特性从 electron17 开始支持，且对于 GNOME 尤其必要。

一个技巧是将命令行参数添加到 **.desktop** 文件中 并将上述命令行参数添加到 Exec= 行的末尾。
警告： 诸如 visual-studio-code-binAUR (bug report) 的一些应用在启动时不会将命令行参数传递给 Electron，此问题需要由应用的开发者才能解决。
配置文件

新建或修改 **${XDG_CONFIG_HOME}/electron-flags.conf** (默认是 **.config/electron-flags.conf** ) ，添加以下内容：

**~/.config/electron-flags.conf**

> --enable-features=WaylandWindowDecorations
> --ozone-platform-hint=auto

注意： 这些配置文件只对官方仓库的 Electron 软件包和使用这些 Electron 包的应用程序有效。对于自带 Electron 的软件包 (如 slack-desktopAUR) 来说，这些配置文件是无效的。不过在某些情况下也有替代品，如 slack-electronAUR 。
旧版本 Electron
注意： 旧版本的 Electron 需要单独设置 **electron<version>-flags.conf** 文件，创建到 **${XDG_CONFIG_HOME}/electron-flags.conf** 的符号链接是比较推荐的做法。

旧版本 Electron 需要的参数也不同，例如 Electron 13 需要:

**~/.config/electron13-flags.conf**

> --enable-features=UseOzonePlatform
> --ozone-platform=wayland

对于中文用户
KDE Plasma 5.27 合并了 text-input-v1。在 5.27 及以上版本的 KDE Plasma 中，通过启动 Electron 应用程序时添加 **--enable-wayland-ime**，可以在 Wayland 下使用中文输入法