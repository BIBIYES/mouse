![image](https://ohmyz.sh/img/themes/omz-update.png)

# Ohmyzsh安装配置指南

## 1 安装

要想在终端中使用 `ohmyzsh`​ 你需要完成如下操作

1. 安装 `git`​

    ```bash
    apt install git
    ```

2. 安装 `zsh`​

    ```bash
    apt install zsh
    ```

3. 执行如下脚本安装来安装 `ohmyzsh`​

    ```sh
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

## 2 安装插件

1. 安装高亮插件

    输入该命令将**插件** clone 到 root 根目录下

    ```bash
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    ```

2. 安装代码补全插件

    输入该命令将**插件** clone 到 root 根目录下

    ```bash
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    ```

    1. 部分补全

        当输入一段命令时，按下 `tab`​ 键会补全所有命令，按下 `esc`​ 再按下 `f`​ 可以补全前端一小段命

3. 将插件克隆下来后需要修改 `zsh`​ 配置来启用

    ```bash
    vim ~/.zshrc
    ```

    1. 将插件配置中添加插件名称以 `空格`​ 隔开

        ![image](assets/image-20250217171702-q5zw3ze.png)

## 3 皮肤

点击链接来查看 `ohmyzsh`​ 官方支持的主题

[ohmyzsh 主题列表](https://github.com/ohmyzsh/ohmyzsh/wiki/themes)

1. 在配置文件中替换主题的**名称**即可

    ```bash
    vim ~/.zshrc
    ```

2. 重新启用配置

    ```bash
    source ~/.zshrc
    ```

‍
