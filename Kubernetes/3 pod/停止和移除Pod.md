# 停止和移除Pod
* 按名称删除  kubectl delete pod $POD_NAME
* 使用标签选择器删除Pod   kubectl delete pod -l  creation_method=manual
* 通过删除整个命名空间开删除pod   kubectl delete ns $NS_NAME
* 删除命名空间中的所有pod,但是保留命名空间   kubectl delete pod -all
* 删除命名空间中的几乎所有资源   kuebctl delete all -all