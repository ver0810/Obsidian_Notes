
> [!Info] Hyprland 在高分辨率下的某些软件会出现模糊

解决办法禁用xwayland缩放，在*~/.config/hypr/hyprland.conf*

```conf
xwayland {
	force_zero_scaling = true
}
```
