### 一、为什么你的Git总出问题？（安装前的灵魂拷问）

每次代码写完，`Ctrl + Z` 按多了导致回退过度？亦或者是不小心删掉了某一行但是记不起来？又或者是这个版本代码出问题了想要回退？在没有 `Git` 时想做到上述实现会非常难受。但是一旦有了 `Git` 

每次看到新手在[命令行](https://so.csdn.net/so/search?q=%E5%91%BD%E4%BB%A4%E8%A1%8C&spm=1001.2101.3001.7020)里疯狂敲git却报错的样子（真的又心疼又好笑），我发现90%的问题都出在安装配置环节！！！今天就手把手教大家从零开始搞定Git安装，让你少走三年弯路！

### 二、三大系统安装攻略（必做）

#### 2.1 Windows篇：别再用绿色版了！

1. 访问官网下载：[https://git-scm.com/download/win](https://git-scm.com/download/win)  ，或者直接点击[Git for Windows/x64 Setup (github.com)](https://github.com/git-for-windows/git/releases/download/v2.49.0.windows.1/Git-2.49.0-64-bit.exe)下载。==如果你的下载速度太慢，请自己尝试分析原因（自己分析不出来把你的情况复述给AI让他分析）==
    （认准这个域名！网上很多山寨网站会捆绑垃圾软件）
    
2. 双击安装时特别注意：
    
    - 勾选`Add to PATH`（环境变量自动配置）
    - 选择默认编辑器（Vim劝退新手，建议选VS Code）
    - 换行符设置选`Checkout as-is, commit Unix-style`（跨平台协作必备）
3. 验证安装是否成功：
    
    ```bash
    git --version
    ```
    
    看到类似`git version 2.41.0`的输出就对了！
    

#### 2.2 macOS篇：两种姿势任你选

👉 **Homebrew大法**（推荐给技术控）：

```bash
brew install git
```

👉 **官方安装包**（适合小白）：  
直接下载`.dmg`文件双击安装，全程下一步就行（记得允许系统权限）

#### 2.3 Linux篇：一行命令搞定

```bash
sudo apt-get install git  # Ubuntu/Debian
sudo yum install git      # CentOS/RedHat
```

### 三、必做的初始配置（必做）

#### 3.1 全局用户配置（必做）

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

注意：这里的邮箱要和GitHub/GitLab注册邮箱一致！！！

#### 3.2 项目级配置（选做）

进入项目目录后执行：

```bash
git config user.name "项目专用马甲"
git config user.email "project@example.com"
```

#### 3.3 让命令行更友好（选做）

```bash
git config --global color.ui auto  # 彩色输出
git config --global core.autocrlf input  # 智能换行符处理
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"  # 超强日志别名

```

#### 3.4  让命令行学会代理（必做）  


### 四、SSH密钥配置（选做）

#### 4.1 生成密钥对

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

连按三次回车（不要设密码！后面会教你怎么安全保存）

#### 4.2 添加密钥到Git服务

- 查看公钥：
    
    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```
    
- 复制到GitHub/GitLab的SSH Keys设置页面

#### 4.3 测试连接

```bash
ssh -T git@github.com
```

看到`You've successfully authenticated`就是成功啦！

### 五、常见翻车现场救援指南

#### 5.1 报错：git不是内部命令

说明环境变量没配置好！重新安装时务必勾选`Add to PATH`，或者手动添加安装目录到系统Path

#### 5.2 中文乱码问题

在git bash里执行：

```bash
git config --global core.quotepath false
```

#### 5.3 记住密码的正确姿势

别再用明文存储密码了！推荐使用官方的Git Credential Manager：

```bash
git config --global credential.helper manager
```

### 六、新手必备工具推荐

👉 **Git图形化客户端**：

- GitHub Desktop（适合纯小白）
- Fork（功能强大颜值高）

👉 **.gitconfig配置文件**：  
把我的常用配置拿去用（放到用户目录下）：

```ini
[alias]
    st = status
    ci = commit
    br = branch
    co = checkout
    df = diff
    lol = log --graph --decorate --oneline
    lola = log --graph --decorate --oneline --all
```

### 七、Git 命令行完整测试（必做）

完成所有步骤后，在命令行依次执行：

```bash
mkdir test-project # 初始化项目文件夹
cd test-project    # 进入项目文件夹
git init           # git 初始化
echo "Hello Git" > README.md #  
git add .          # 将所有文件添加到暂存区
git commit -m "初始提交" # 将暂存区内的文件提交
```

如果顺利看到类似`[main (root-commit) 5f4b5c6] 初始提交`的提示，恭喜你正式加入Git玩家行列！

（偷偷说）其实[Git安装](https://so.csdn.net/so/search?q=Git%E5%AE%89%E8%A3%85&spm=1001.2101.3001.7020)只是万里长征第一步，后面还有分支管理、冲突解决等硬核内容等着你。不过别担心，先点个收藏，下期我们继续攻克Git的进阶操作！

### 八、VsCode Git 完整测试 （必做）