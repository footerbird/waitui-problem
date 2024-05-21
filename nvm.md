## NVM作为nodejs版本控制器的应用
下载安装使用NVM
```
# 下载nvm源代码
git clone https://github.com/nvm-sh/nvm.git

# 进入nvm目录
cd nvm

# 编译和安装nvm
./install.sh

# 打开.bash_profile文件配置环境变量
vim ~/.bash_profile

# 添加nvm到环境变量，
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# 运行以下命令来使nvm加载到bash中
source ~/.bash_profile
```

nvm命令，注意这里的use命令在终端窗口关闭后会失效，如果要长期使用某个版本，需要用nvm alias default
```
# nvm ls: 列出所有已安装的Node.js版本。
nvm ls

# nvm ls-remote: 列出可供安装的所有Node.js版本。
nvm ls-remote

# nvm install <version>: 安装指定版本的Node.js。
nvm install 16.20.2
nvm install 18.20.3
nvm install 20.13.1

# nvm use <version>: 切换到指定版本的Node.js。
nvm use 20

# nvm alias <name> <version>: 创建一个别名，指向特定的Node.js版本。
nvm alias mynode v18.20.3

# nvm uninstall <version>: 卸载指定版本的Node.js。
nvm uninstall 20.13.1

# nvm current: 显示当前正在使用的Node.js版本。
nvm current

# nvm alias default <version>: 设置默认的Node.js版本。
nvm alias default v16.20.2
```
