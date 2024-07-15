> **执行安装脚本**

```
sudo apt install curl 
curl https://raw.gitmirror.com/creationix/nvm/master/install.sh | bash
```


> 如果报443执行下面命令

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

> 环境变量生效
`source ~/.bashrc`

> 检验是否安装成功
`nvm -v`

> 查看可在线安装的NodeJS版本
`nvm list available`

> Example:

  ```
nvm install 8.0.0                     Install a specific version number

  nvm use 8.0                           Use the latest available 8.0.x release

  nvm run 6.10.3 app.js                 Run app.js using node 6.10.3

  nvm exec 4.8.3 node app.js            Run `node app.js` with the PATH pointing to node 4.8.3

  nvm alias default 8.1.0               Set default node version on a shell

  nvm alias default node                Always default to the latest available node version on a shell

  nvm install node                      Install the latest available version

  nvm use node                          Use the latest version

  nvm install --lts                     Install the latest LTS version

  nvm use --lts                         Use the latest LTS version

  nvm set-colors cgYmW                  Set text colors to cyan, green, bold yellow, magenta, and white
```

> 示例

```
比如：我要使用12.18.1

nvm install 12.18.1

比如：我要使用16.15.0

nvm install node -v                                                                                                                                   

v12.18.1

现在想换回12.18.1

nvm use 12.18.1

查看当前所使用的版本：

node -v 

v12.18.1

永久默认
使用的过程中我发现，使用以下命令后，只能临时有效。重新打开新的终端版本又变回原来的了。
nvm use 12.22.0

如果让设置永久生效呢？nvm alias default xx.xx.x

nvm use 12.22.0

nvm alias default 12.22.0

执行这两条命令就可以了。
```

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
/