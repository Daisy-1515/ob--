#  翻墙官方文档

###  使用方法
首先想办法将这个项目解压在autodl-tmp文件夹下，然后执行以下
####  1. 安装代理软件

使用的是 v2raya，文档[点这里](https://v2raya.org/docs/prologue/introduction/)
可以直接dpkg -i *.deb
```bash

sudo apt install /root/autodl-tmp/autodl_proxy/installer_debian_x64_2.2.7.1.deb
sudo apt install /root/autodl-tmp/autodl_proxy/v2ray_5.37.0_amd64.deb
sudo apt install /root/autodl-tmp/autodl_proxy/xray_25.8.3_amd64.deb



v2raya
```
开启端口转发在本机电脑打开：
ssh -L 2017:localhost:2017 user@remote_server
==此处看后面的ai对话==

http://127.0.0.1:2017

####  2. 使用代理
开启代理：

```bash
export http_proxy="http://127.0.0.1:20171" && export https_proxy="http://127.0.0.1:20171"
```

关闭代理：

```bash
unset http_proxy && unset https_proxy
```
### 进阶使用方法，将代理开关添加到 `~/.bashrc` 中

可以直接将 `pon` 和 `poff` 命令加入到 `~/.bashrc` 中，这样您可以在每次启动新终端时通过输入 `pon` 或 `poff` 来启用或禁用代理。

以下是具体步骤：

#### 1. 编辑 `~/.bashrc` 文件

```bash
vim ~/.bashrc
```

#### 2. 在文件末尾添加以下内容

```bash
# Function to enable proxy
function pon() {
    export http_proxy="http://127.0.0.1:20171"
    export https_proxy="http://127.0.0.1:20171"
    echo "Proxy enabled: $http_proxy"
    
    # Check connection to Google
    if curl -s --head --request GET http://www.google.com | grep "200 OK" > /dev/null; then 
        echo "Connection to Google successful"
    else
        echo "Failed to connect to Google"
    fi
}

# Function to disable proxy
function poff() {
    unset http_proxy
    unset https_proxy
    echo "Proxy disabled"
}
```

#### 3. 保存并退出编辑器

按 `Esc` 键，然后输入 `:wq` 并按 `Enter` 键保存并退出编辑器。

#### 4. 使更改生效

运行以下命令使更改立即生效：

```bash
source ~/.bashrc
```

#### 5. 使用 `pon` 和 `poff` 控制代理

现在，您可以在终端中使用 `pon` 和 `poff` 命令来启用或禁用代理：

启用代理：

```bash
pon
```

禁用代理：

```bash
poff
```

这样，您就可以方便地在终端中控制代理的开关，而无需每次都编辑脚本文件。

### 设置开机自启动
```bash
sudo systemctl start v2raya.service #启动
sudo systemctl enable v2raya.service #自启动
```




### Q&A

#### 开启端口转发在本机电脑打开：$ssh -L 2017:localhost:2017 user@remote_server$
   这一步是**关键步骤**，它的目的是把你**本地电脑（你现在的电脑）的一个端口，和AutoDL 服务器**的端口连接起来。

请注意：**这条命令不是在 AutoDL 的黑色终端界面里输入的，而是在你自己的电脑上输入的。**

你需要根据你使用的工具，选择下面其中一种方法：

##### 方法一：如果你使用 Windows 的 PowerShell/CMD 或 Mac 的终端

这是最通用的方法，直接修改你平时的登录命令。

1. 找到你的 AutoDL 登录指令：
    
    去 AutoDL 控制台，找到“SSH指令”并复制它。它看起来像这样：
    
    ssh -p 12345 root@region-45.autodl.com
    
    (其中 12345 是端口号，region-45... 是主机名)
    
2. 修改指令：
    
    在原本的指令中间，插入 -L 2017:localhost:2017。
    
    修改后的指令长这样（注意空格）：



ssh -p 10432 root@connect.cqa1.seetacloud.com




    Bash
    
    ```
    ssh -L 2017:127.0.0.1:2017 -p 12345 root@region-45.autodl.com
    ```
    
    请把 `12345` 和 `region-45.autodl.com` 替换成你自己的实际信息。==注意root@不能掉==
    
2. **执行指令**：
    
    - 打开你**本机电脑**的终端（Windows 按 Win+R 输入 `powershell`，Mac 打开 Terminal）。
    - 粘贴上面修改好的那行长命令，回车。
    - 输入密码登录。
    - **注意**：登录成功后，不要关闭这个黑框框，把它最小化放在一边。
        
3. 打开浏览器：
    在你本机电脑的浏览器（Chrome/Edge）里输入：http://127.0.0.1:2017
    你就能看到 v2raya 的界面了。

---

##### 方法二：如果你使用 VS Code (推荐)

如果你是用 VS Code 远程连接 AutoDL 的，这个方法最简单，不用敲命令。

1. 确保你已经用 VS Code 连接上了 AutoDL 服务器。
2. 在 VS Code 底部面板，找到 **“端口 (Ports)”** 选项卡（如果没有，点击顶部菜单 `查看(View)` -> `终端(Terminal)`，然后在底部面板找）。
3. 点击 **“添加端口 (Add Port)”**。
4. 输入 **2017** 并回车。
5. 你会看到列表中出现了 2017，此时点击那个 **“地球图标”** 或者直接在浏览器输入 `http://127.0.0.1:2017` 即可。
    

---
##### 成功后的操作

一旦你能在浏览器里看到 **v2raya** 的界面：

1. 创建一个管理员账号和密码（自己随便设）。
2. 进入后，点击导入节点，把你的**机场订阅链接**粘贴进去。
3. 点击“启动”或“Ping”测试一下。
4. **重要**：确保勾选左上角的设置，端口设置要是 `20171`（与 README 里的环境变量对应）


我设置123 账号 123456 密码

# 端口转发的jupyter

在 JupyterLab 中，“是否显示隐藏文件”主要是一个**前端（界面）设置**，它通常会**自动记忆**你上一次的选择（只要你不重置系统盘）。

因此，通常**不需要**每次启动都加特殊指令。只要你在菜单里勾选过一次（如上一个回答所示），下次启动它应该还在。

不过，如果你是指**强制后端允许访问隐藏文件**，或者是通过命令行启动时确保配置正确，可以使用以下参数：

### 1. 启动时的命令行参数

如果你是在终端（SSH）手动输入命令启动 Jupyter，可以加上 `--ContentsManager.allow_hidden=True`。

完整常用启动命令如下：

Bash

```
jupyter lab --allow-root --ContentsManager.allow_hidden=True
```

- `--allow-root`: 允许以 root 用户运行（AutoDL 必需）。
    
- `--ContentsManager.allow_hidden=True`: 允许后端服务处理隐藏文件（通常默认已开启，但此参数可强制开启）。
    

---

### 2. 通过配置文件永久生效 (推荐)

如果你不想每次都输长命令，可以修改配置文件。

1. **生成配置文件**（如果还没有的话）：
    
    Bash
    
    ```
    jupyter lab --generate-config
    ```
    
2. 修改配置文件：
    
    该文件通常位于 ~/.jupyter/jupyter_lab_config.py 或 ~/.jupyter/jupyter_server_config.py。
    
    你可以使用 vim 或双击文件打开编辑，加入（或取消注释）这一行：
    
    Python
    
    ```
    c.ContentsManager.allow_hidden = True
    ```
    

---

### 3. 高级：通过脚本强制开启前端“显示”选项

如果你是想通过脚本（比如 AutoDL 的启动脚本）**强制把那个 UI 复选框勾上**，这比较复杂，因为那是存储在 JSON 文件里的前端状态。

你需要修改（或覆盖）这个文件：

/root/.jupyter/lab/user-settings/@jupyterlab/filebrowser-extension/browser.jupyterlab-settings

在该文件中写入：

JSON

```
{
    "showHiddenFiles": true
}
```

总结：

通常在 AutoDL 上，只需要在界面上手动勾选一次 View -> Show Hidden Files，系统就会记住这个设置，下次重启实例也不需要额外指令。

### 方法一：使用命令行（最通用，Windows/Mac 均可）

你需要知道你这台 AutoDL 机器的 **公网 IP** 和 **SSH 端口**（注意：**不是** 8889，而是你平时登录服务器用的那个端口，比如 12345 或 22）。

1. **打开本地电脑的终端**（Windows 打开 CMD 或 PowerShell，Mac 打开 Terminal）。
    
2. **输入以下命令**（请替换 `<...>` 为你的实际信息）：
    
    Bash
    
    ```
    ssh -L 8889:localhost:8889     -p <服务器SSH端口>   root@<服务器IP>

    ```
    
    - **解释**：
        
        - `-L 8889:localhost:8889`：把**本地**的 8889 端口映射到**服务器**的 8889 端口。
            
        - `-p <服务器SSH端口>`：这是 AutoDL 分配给你的登录端口（通常在网页控制台的“SSH指令”里能看到，比如 `ssh -p 12345 root@...` 中的 12345）。
            
1. 打开浏览器：
    
    现在，不要关闭刚才的黑框口，打开本地浏览器，访问服务器刚才给你的链接：
    例如
    http://127.0.0.1:8889/lab?token=8c777ac7f71ab6b5673425bf223bac9a98ef3ad37c8239ae
    

---

### 方法二：使用 VS Code（如果你用 VS Code 远程开发）

如果你已经用 VS Code 的 Remote-SSH 插件连接到了服务器：

1. 在 VS Code 底部面板找到 **PORTS (端口)** 选项卡（如果没有，点击菜单 `View` -> `Open View...` -> `Ports`）。
    
2. 点击 **Forward a Port (转发端口)** 按钮。
    
3. 在输入框里输入 `8889` 并回车。
    
4. 列表里会出现 `8889`，点击它旁边的“小地球”图标（Open in Browser），VS Code 会自动帮你打开浏览器并连接。
    

---

### 常见疑问

- **为什么不用 AutoDL 网页上的“JupyterLab”按钮？**
    
    - 因为那个按钮默认连接的是服务器的 `8888` 端口。而你刚才手动启动的新服务是在 `8889` 端口，所以网页按钮连不上这个新进程。
        
- **操作完怎么关闭？**
    
    - 用完后，在刚才那个“没有任何反应”的命令行窗口里，按 `Ctrl+C` 即可断开映射。



1. 测试访问 Google
2.  curl -I https://www.google.com