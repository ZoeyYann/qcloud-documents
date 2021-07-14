## 简介

本文档介绍如何管理AI环境，包括创建AI环境、调整AI环境以及删除AI环境

### 创建AI环境
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的【集群】。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的【节点管理】>【节点池】，进入“节点池列表”页面。
4. 单击【新建节点池】，进入“新建节点池”页面，参考以下提示进行设置。如下图所示：
![](https://main.qcloudimg.com/raw/2089e540c584e6c6691a3552b04154a3.png)
 - **节点池名称**：自定义，可根据业务需求等信息进行命名，方便后续资源管理。
 - **节点池类型**：目前支持【云服务器】和【虚拟节点】和【第三方节点】三种类型。当开启第三方节点功能后，仅支持【第三方节点】类型。
 - **容器目录**：勾选即可设置容器和镜像存储目录，建议存储到数据盘。例如 /var/lib/docker。
 - **运行时组件**：容器运行时组件，当前支持【docker】和【containerd】。
 - **运行时版本**：容器运行时组件的版本。
  - **封锁初始节点**：勾选【开启封锁】后，将不接受新的 Pod 调度到该节点，需要手动取消封锁的节点，或在自定义数据中执行 [取消封锁命令](https://cloud.tencent.com/document/product/457/18824)，请按需设置。
  - **Label**：单击【新增Label】，即可进行 Label 自定义设置。该节点池下所创建的节点均将自动增加此处设置的 Label，可用于后续根据 Label 筛选、管理第三方节点。
<dx-alert infotype="explain" title="">
必填 Label 说明（**仅填写 value，请勿更改 key**）：
- tke.cloud.tencent.com/location
- 如果容器网络模式设置为 **Cilium BGP** 模式，还需填写如下两组 Label：
  - infra.tce.io/as 为节点所属交换机的 BGP AS 号，请根据业务环境设置。
  - infra.tce.io/switch-ip 为节点所属交换机的交换机 IP，请根据业务环境配置。
</dx-alert>
 - **Taints**：节点属性，通常与 `Tolerations` 配合使用。此处可为节点池下的所有节点设置 Taints，确保不符合条件的 Pod 不能够调度到这些节点上，且这些节点上已存在的不符合条件的 Pod 也将会被驱逐。
Taints 内容一般由 `key`、`value` 及 `effect` 三个元素组成。其中 `effect` 可取值通常包含以下三种：
    - **PreferNoSchedule**：非强制性条件，尽量避免将 Pod 调度到设置了其不能容忍的 taint 的节点上。
    - **NoSchedule**：当节点上存在 taint 时，没有对应容忍的 Pod 一定不能被调度。
    - **NoExecute**：当节点上存在 taint 时，对于没有对应容忍的 Pod，不仅不会被调度到该节点上，该节点上已存在的 Pod 也会被驱逐。以设置 Taints `key1=value1:PreferNoSchedule` 为例，控制台配置如下图所示：
  ![](https://main.qcloudimg.com/raw/e554317ef5c178297d34eef3f9a7bfa7.png)
 - **自定义数据**：指定自定义数据来配置节点，即当节点启动后运行配置的脚本。需确保脚本的可重入及重试逻辑，脚本及其生成的日志文件可在节点的 `/usr/local/qcloud/tke/userscript` 路径查看。
5. 单击【创建节点池】即可创建AI环境。

### 查看AI环境

成功创建AI环境后，






### 调整AI环境

1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的【集群】。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的【节点管理】>【节点池】，进入“节点池列表”页面。
4. 在“节点池名片页”中，选择计划修改的类型为【第三方节点】的节点池，单击【编辑】。
5. 在“调整AI环境配置”弹窗中，支持修改节点池名称、Labels、Taints 等信息。如下图所示：
<dx-alert infotype="notice" title="">
Labels、Taints 相关的修改会在节点池中的所有第三方节点上生效，如果有特殊调度策略请务必谨慎操作。
</dx-alert>

![](https://main.qcloudimg.com/raw/0551132d444ba69dbb804cf9431bedda.png)


### 删除AI环境

1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的【集群】。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的【节点管理】>【节点池】，进入“节点池列表”页面。
4. 选择计划删除节点池名片页右上角的【删除】。
5.  在“删除AI环境”弹窗中，单击【确认】删除节点池。
<dx-alert infotype="notice" title="">
- 删除AI环境后，池内所有第三方节点仅会被移出集群，不会清除节点上运行的 Pod。
- 删除节点后为了保证安全，建议重装节点或者执行以下命令删除节点上 kube-apiserver 访问配置：
```
