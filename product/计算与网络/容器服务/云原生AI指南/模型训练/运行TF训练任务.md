## 前置条件

- AI环境中已经安装了[TF Operator]()。
- AI环境中有GPU资源。

## 操作指南
以下操作指南参考`TF-Operator` 官方提供的PS/Worker 模式的[分布式训练案例](https://github.com/kubeflow/tf-operator/tree/master/examples/v1/dist-mnist)。

### 准备训练代码

本示例中我们使用 Kubeflow官方提供的示例代码：[`dist_mnist.py`](https://github.com/kubeflow/tf-operator/blob/master/examples/v1/dist-mnist/dist_mnist.py)

### 制作训练镜像

镜像的制作过程非常简单。用户只需基于一个 TensorFlow （1.5.0） 的官方镜像，并将代码复制到镜像内，并配置好 `entrypoint` 即可。
>? 如果不配置 entrypoint，用户也可以在提交 TFJob 的时配置容器的启动命令。

### 任务提交

1. 准备一个 TFJob 的 [yaml 文件](https://raw.githubusercontent.com/kubeflow/tf-operator/master/examples/v1/dist-mnist/tf_job_mnist.yaml)：定义 2 个 PS 和 4 个 Worker。
>? 请注意，用户需要用上传后的训练镜像地址替换 <训练镜像> 所在占位。

```yaml
apiVersion: "kubeflow.org/v1"
kind: "TFJob"
metadata:
  name: "dist-mnist-for-e2e-test"
spec:
  tfReplicaSpecs:
    PS:
      replicas: 2
      restartPolicy: Never
      template:
        spec:
          containers:
            - name: tensorflow
              image: <训练镜像>
    Worker:
      replicas: 4
      restartPolicy: Never
      template:
        spec:
          containers:
            - name: tensorflow
              image: <训练镜像>
```

2. 通过 `kubectl` 提交该 TFJob：

```shell
kubectl create -f ./tf_job_mnist.yaml
```

3. 查看任务状态
```shell
kubectl get tfjob dist-mnist-for-e2e-test -o yaml
kubectl get pods -l pytorch_job_name=pytorch-tcp-dist-mnist 
```

