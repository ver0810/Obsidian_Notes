## archlinstall安装

**步骤1： 安装yay必要的软件包

安装软件包
```
sudo pacman -Sy yay
```

安装所需的 `base-devel`（包含 `makepkg` 等工具）和 `git`（克隆 yay 的 Git 仓库所需的）。

```
sudo pacman -S --needed base-devel git
```

现在你已经有了所需的软件包，是时候在你的系统上安装 [Yay](https://link.zhihu.com/?target=https%3A//github.com/Jguer/yay)。

**步骤 2：克隆 Yay Git 仓库并切换到它**

[使用 git 命令](https://link.zhihu.com/?target=https%3A//itsfoss.com/basic-git-commands-cheat-sheet/)“克隆” Yay 仓库。你可以在系统中的任何位置执行此操作，无论是主目录还是其他目录。

```
git clone https://aur.archlinux.org/yay.git
```

完成后，切换到克隆的目录：

```
cd yay
```

**步骤3： 安装yay

```
makepkg -si
```

### 常用软件

- shell:zsh,fish
- terminal: kitty, alacritty, wezterm
- editor: vscode, neovim, vim
- file manerge: ranger
- other:neofetch, git, wofi, 


> [!Info] archlinux 长时间不更新会导致软件更新错误
> *解决办法* 删除/var/pacman/db.lck

