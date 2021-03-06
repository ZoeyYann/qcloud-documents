## 概述

AI环境是云原生AI服务的重要抽象概念。一个AI环境运行在特定集群(TKE/EKS)容器集群上，运维人员可按需管理AI环境的生命周期。例如，针对不同的上层AI业务，AI运维方可以基于不同组件搭建符合不同业务需求的AI环境。

## 相关概念

#### 容器服务TKE

为帮助您高效管理 Kubernetes 集群内节点，腾讯云容器服务引入节点池概念，节点池利用节点模板，来管理一组同质节点。借助节点池基本功能，您可以方便快捷地创建、管理和销毁节点，以及实现节点的动态扩缩容。详情请参见 [节点池概述](https://cloud.tencent.com/document/product/457/43719)

#### 弹性容器服务EKS

## 注意事项

- 目前AI环境仅支持与TKE集群
- 目前暂不支持在同一集群内混部第三方节点和云上节点，所以在使用第三方节点池功能前，请您封锁集群内所有腾讯云上节点（CVM、裸金属等)， 如下图所示：
 ![](https://main.qcloudimg.com/raw/41f7a33a46121d89661d85599a9bf8d6.png)
- 第三方节点功能仅支持在版本为**1.18及以上**，且部署模式为**“托管集群”**的 TKE 集群中使用。
- 为了保障第三方节点的稳定性，第三方节点仅支持内网连接。


