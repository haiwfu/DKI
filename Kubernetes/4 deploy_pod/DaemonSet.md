# DaemonSet 

## DaemonSet 的使用
通过该控制器的名称我们可以看出它的用法：Daemon，就是用来部署守护进程的，`DaemonSet`用于在每个`Kubernetes`节点中将守护进程的副本作为后台进程运行，说白了就是在每个节点部署一个`Pod`副本，当节点加入到`Kubernetes`集群中，`Pod`会被调度到该节点上运行，当节点从集群只能够被移除后，该节点上的这个`Pod`也会被移除，当然，如果我们删除`DaemonSet`，所有和这个对象相关的`Pods`都会被删除。

在哪种情况下我们会需要用到这种业务场景呢？其实这种场景还是比较普通的，比如：

* 集群存储守护程序，如`glusterd`、`ceph`要部署在每个节点上以提供持久性存储；
* 节点监视守护进程，如`Prometheus`监控集群，可以在每个节点上运行一个`node-exporter`进程来收集监控节点的信息；
* 日志收集守护程序，如`fluentd`或`logstash`，在每个节点上运行以收集容器的日志

这里需要特别说明的一个就是关于`DaemonSet`运行的`Pod`的调度问题，正常情况下，`Pod`运行在哪个节点上是由`Kubernetes`的调度器策略来决定的，然而，由`DaemonSet`控制器创建的`Pod`实际上提前已经确定了在哪个节点上了（`Pod`创建时指定了`.spec.nodeName`），所以：

* `DaemonSet`并不关心一个节点的`unshedulable`字段，这个我们会在后面的调度章节和大家讲解的。
* `DaemonSet`可以创建`Pod`，即使调度器还没有启动，这点非常重要。

下面我们直接使用一个示例来演示下，在每个节点上部署一个`Nginx Pod`：(nginx-ds.yaml)
```yaml
kind: DaemonSet
apiVersion: apps/v1
metadata:
  name: nginx-ds
  labels:
    k8s-app: nginx
spec:
  selector:
    matchLabels:
      k8s-app: nginx
  template:
    metadata:
      labels:
        k8s-app: nginx
    spec:
      containers:
      - image: nginx:1.7.9
        name: nginx
        ports:
        - name: http
          containerPort: 80
```

然后直接创建即可：
```shell
$ kubectl create -f nginx-ds.yaml
```

然后我们可以观察下`Pod`是否被分布到了每个节点上：
```shell
$ kubectl get nodes
$ kubectl get pods -o wide
```