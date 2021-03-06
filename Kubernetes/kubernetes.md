**kubernetes**
* kubernetes简介
   * 初体验
   * kubernetes基本概念和组件
* Kubernetes安装
   * minikube
   * kubeadm
   * 我的第一个应用
* Pod---运行中的kubernetes容器
   * pod介绍
   * Yaml file
   * 标签
   * 注解
   * namespace
   * 停止和移除pod
* 部署pod 
   * Pod健康检查
   * ReplicationController
   * DaemonSet
   * Job
   * 服务
   * 创建服务
   * 服务发现
   * 连接集群外部的服务
   * 将服务暴露给外部
   * Ingress服务暴露
   * Engress访问外部服务
   * headless服务
*卷
   * 容器之间共享数据
   * 挂载节点文件的数据文件
   * 持久化存储
* ConfigMap & Secret
   * 利用configMap解耦配置
   * 利用Secret传送敏感数据
   * RBAC
* 应用访问pod元数据
   * Downward API 传送元数据
   * 与kubernetes API服务器交互
* Deployment
   * Pod内应用程序更新
   * 使用RC滚动升级
   * 使用deployment声明式升级应用
* StatefulSet 有状态的多副本应用
   * 了解StatefullSet
   * 使用StatefullSet
* 计算资源管理
* POD自动伸缩
* Pod高级调度
* 最佳实践
* kubernetes应用扩展