**1、在线安装超时无法安装**

我们往往在国内环境下安装k3s服务，k3s在安装时会从docker或者github源地址上下载某些依赖，但是因为网络问题会导致下载超时，这就导致k3s安装失败。

解决办法：离线安装，从k3s官方github仓库的Releases发行里下载离线依赖镜像包，需要注意版本号，下载和你安装的k3s版本对应的镜像包。

k3s离线镜像仓库地址：https://github.com/k3s-io/k3s/releases

```
// 导入离线镜像命令
sudo k3s ctr images import k3s-airgap-images-amd64.tar
```
![image](https://github.com/user-attachments/assets/f833b006-9c67-449f-a179-0d3db81994f7)


2、运行一段时间，更新我们的pod后，会出现拉取镜像失败导致pod无法启动，状态显示ContainerCreating

![image](https://github.com/user-attachments/assets/382076c4-17a2-434d-9f89-f9c4eae18b61)


解决办法：

```
// 执行下面命令查看pod拉取失败的日志
kubectl describe pods (你的pod名称)-deployment
```
拉取失败常见问题如下：

get sandbox image "rancher/mirrored-pause:3,1": failed to pull image 

![image](https://github.com/user-attachments/assets/8d20f0ac-2d68-4789-8bd5-a038f1455e81)


遇到上面问题说明在pod拉取过程中k3s依赖的一个服务"rancher/mirrored-pause:3.1"   pull失败（网络原因）

我们找到了问题原因，那么我们手动去拉取一下这个服务。

```
// 1、拉取对应版本
ctr images pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/rancher/mirrored-pause:3.1
```

```
// 2、给镜像包添加一个新的标签，便于引用
ctr images tag  swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/rancher/mirrored-pause:3.1  docker.io/rancher/mirrored-pause:3.1
```


```
// 3、重启pod
kubectl rollout restart deployment xx-prod-deployment
```


这里我推荐一个国内同步镜像站地址：

```
// 缺少哪个依赖去下面网址找，没有可以请求同步一下
https://docker.aityp.com/r/docker.io/rancher/mirrored-pause
```