# macOS 终端美化配置总结

本文记录一套基于 **iTerm2 + Zsh + Oh My Zsh + Powerlevel10k + Nerd Font + Zsh Plugins** 的 macOS 终端配置过程，并说明各组件之间的关系、主要配置文件位置，以及配置过程中遇到的问题和解决方法。

---

# 1. 主要配置流程

## 1.1 整体配置链路

最终使用的组件关系如下：

```text
macOS
  │
  ├── iTerm2 / Terminal.app / VS Code Terminal
  │       │
  │       └── zsh
  │             │
  │             ├── ~/.zshrc
  │             │
  │             └── Oh My Zsh
  │                    │
  │                    ├── Powerlevel10k
  │                    └── Plugins
  │
  └── MesloLGS NF
          └── 提供 Powerlevel10k 使用的 Nerd Font 图标
```

各组件职责：

|组件|作用|
|---|---|
|Terminal.app|macOS 自带终端模拟器|
|iTerm2|第三方终端模拟器，负责窗口、字体、颜色等|
|Zsh|真正解析和执行命令的 Shell|
|`.zshrc`|Zsh 的用户配置文件|
|Oh My Zsh|Zsh 的配置框架，用于管理主题、插件等|
|Powerlevel10k|Prompt 主题，控制路径、Git 状态等提示符外观|
|MesloLGS NF|Nerd Font，提供 Powerlevel10k 所需图标|
|Zsh Plugins|自动建议、语法高亮、Git 扩展等功能|
|iTerm2 Color Scheme|控制背景、前景和 ANSI 颜色|

---

## 1.2 安装 Oh My Zsh

执行：

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


---

## 1.3 清理原 `.zshrc`

原配置包含：

```bash
source /Users/lyh/software/cangjie/envsetup.sh

alias codenew='open -n "/Applications/Visual Studio Code New.app"'

alias code1982='open -n "/Applications/Visual Studio Code 1.98.2.app" --args --user-data-dir "$HOME/software/vscode-1982-data" --extensions-dir "$HOME/software/vscode-1982-extensions"'

alias tailscale="/Applications/Tailscale.app/Contents/MacOS/Tailscale"

export PATH="/Users/lyh/.antigravity-ide/antigravity-ide/bin:$PATH"
```

其中 Antigravity IDE 已经删除，因此移除：

```bash
export PATH="/Users/lyh/.antigravity-ide/antigravity-ide/bin:$PATH"
```

---

## 1.4 仓颉环境改成按需加载

原来：

```bash
source /Users/lyh/software/cangjie/envsetup.sh
```

意味着每次打开新的 Zsh 都会执行整个仓颉初始化脚本。

该脚本不仅设置：

```text
CANGJIE_HOME
PATH
DYLD_LIBRARY_PATH
SDKROOT
```

还会执行：

```bash
xattr
codesign
```

因此没有必要每次启动终端都自动执行。

最终改为：

```bash
alias cangjie-on='source /Users/lyh/software/cangjie/envsetup.sh'
```

需要仓颉开发环境时再运行：

```bash
cangjie-on
```

这样普通终端环境更加干净。

---

## 1.5 加入 Oh My Zsh

`.zshrc` 中加入：

```bash
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="robbyrussell"

plugins=(git)

source $ZSH/oh-my-zsh.sh
```

此时结构变成：

```text
zsh
 ↓
~/.zshrc
 ↓
Oh My Zsh
```

---

## 1.6 安装 Powerlevel10k

Powerlevel10k 作为 Oh My Zsh 的主题使用。

安装后将：

```bash
ZSH_THEME="robbyrussell"
```

修改为：

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

随后执行：

```bash
source ~/.zshrc
```

或者重新打开终端。

首次启动 Powerlevel10k 时会进入：

```bash
p10k configure
```

配置向导。

---

## 1.7 配置 Powerlevel10k

Powerlevel10k 主要负责 Prompt，例如：

```text
  ~/Dev/Technical-Learning-Notes   main ❯
```

它可以显示：

```text
当前目录
Git 仓库
Git branch
未提交文件
未 push commit
命令执行状态
运行时间
Python / Node 环境
```

如果需要重新调整：

```bash
p10k configure
```

例如将 Prompt：

```text
两行
```

改成：

```text
一行
```

应该修改 **Powerlevel10k**，而不是修改 iTerm2。

---

## 1.8 Nerd Font

Powerlevel10k 会使用特殊图标，例如：

```text




```

因此需要安装 Nerd Font。

当前使用：

```text
MesloLGS NF
```

iTerm2 中设置：

```text
iTerm2
→ Settings
→ Profiles
→ Text
→ Font
→ MesloLGS NF
```

VS Code Terminal 中设置：

```json
"terminal.integrated.fontFamily": "MesloLGS NF"
```

---

## 1.9 Zsh Plugins

Oh My Zsh 可以加载插件，例如：

```bash
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  web-search
)
```

各插件作用：

### git

提供 Git alias、补全等功能。

例如：

```bash
gst
```

相当于：

```bash
git status
```

### zsh-autosuggestions

根据历史命令自动显示灰色建议。

例如输入：

```text
git
```

可能自动提示：

```text
git status
```

### zsh-syntax-highlighting

根据命令是否合法进行语法着色。

例如：

```text
有效命令 → 正常/绿色
错误命令 → 红色
```

### web-search

允许直接：

```bash
google powerlevel10k
```

调用浏览器搜索。

---

# 2. 最终运行结构和文件位置

## 2.1 最终运行结构

终端启动过程可以理解为：

```text
iTerm2
  │
  │ 启动
  ↓
zsh
  │
  │ 读取
  ↓
~/.zshrc
  │
  ├── 用户 Alias
  │
  ├── 加载 Oh My Zsh
  │
  └── 加载 Plugins
          │
          ↓
      Powerlevel10k
          │
          │ 读取
          ↓
      ~/.p10k.zsh
```

视觉显示过程则是：

```text
Powerlevel10k
     │
     │ 输出特殊字符
     ↓
MesloLGS NF
     │
     │ 渲染
     ↓
iTerm2 / Terminal / VS Code
```

---

# 2.2 主要文件位置

### Zsh 主配置

```text
~/.zshrc
```

实际路径：

```text
/Users/lyh/.zshrc
```

主要管理：

```text
环境变量
PATH
alias
Oh My Zsh
主题
Plugins
```

---

### Oh My Zsh

```text
~/.oh-my-zsh
```

实际路径：

```text
/Users/lyh/.oh-my-zsh
```

---

### Powerlevel10k 配置

```text
~/.p10k.zsh
```

主要负责：

```text
Prompt 内容
Prompt 布局
颜色
Git 信息
图标
左右 Prompt
```

---

### Powerlevel10k Theme

通常位于：

```text
~/.oh-my-zsh/custom/themes/powerlevel10k
```

---

### Zsh Plugin

一般位于：

```text
~/.oh-my-zsh/custom/plugins/
```

例如：

```text
~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

---

### Nerd Font

macOS 用户字体通常位于：

```text
~/Library/Fonts
```

可以检查：

```bash
ls ~/Library/Fonts | grep -i Meslo
```

---

### VS Code 配置

默认 VS Code：

```text
~/Library/Application Support/Code/User/settings.json
```

即：

```text
/Users/lyh/Library/Application Support/Code/User/settings.json
```

当前添加：

```json
"terminal.integrated.fontFamily": "MesloLGS NF"
```

---

### 独立 VS Code 1.98.2 配置

因为启动时指定了：

```bash
--user-data-dir "$HOME/software/vscode-1982-data"
```

因此其配置文件是：

```text
~/software/vscode-1982-data/User/settings.json
```

而不是默认 VS Code 配置目录。

---

### 仓颉环境

```text
/Users/lyh/software/cangjie/envsetup.sh
```

现在通过：

```bash
cangjie-on
```

按需加载。

---

# 2.3 当前 `.zshrc` 基础结构

当前配置可以整理为：

```bash
# Cangjie - 按需加载
alias cangjie-on='source /Users/lyh/software/cangjie/envsetup.sh'

# VS Code
alias codenew='open -n "/Applications/Visual Studio Code New.app"'

alias code1982='open -n "/Applications/Visual Studio Code 1.98.2.app" --args --user-data-dir "$HOME/software/vscode-1982-data" --extensions-dir "$HOME/software/vscode-1982-extensions"'

# Tailscale
alias tailscale="/Applications/Tailscale.app/Contents/MacOS/Tailscale"

# Oh My Zsh
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(
  git
)

source $ZSH/oh-my-zsh.sh
```

安装更多插件后再扩展：

```bash
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  web-search
)
```

Powerlevel10k 通常还会加入：

```bash
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```

---


# 3.以后排查问题时，可以按这个逻辑判断：

```text
命令 / PATH 有问题
→ ~/.zshrc

Oh My Zsh 有问题
→ ~/.oh-my-zsh

Prompt 样式有问题
→ Powerlevel10k / ~/.p10k.zsh

自动提示、语法高亮有问题
→ Plugins

图标乱码
→ Nerd Font

字体大小不对
→ iTerm2 / Terminal / VS Code

背景或普通文字颜色不对
→ Terminal Emulator 的 Colors

只有 VS Code 显示异常
→ VS Code terminal settings
```

这套划分基本就是以后维护这套终端环境时最重要的思路。