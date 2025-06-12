# 项目说明
> fork from:  https://github.com/ctrox


# 修改内容
在用户重复使用同一个bucket 路径创建 volume 的时候挂载到pod的时候， 会出现下面错误
```shell
Volume with the same name: bucket-user-gsmini/dataset but with smaller size already exist

```
> 这个路径之前被别的pod挂载过，新创建的pod volume的 pvc的 capacity.storage 存储大小比当前的小

删除该规则校验，用户端传过来的 pvc的 capacity.storage大小就为实际bucket 路径大小(创建前用户端自己先判断当前目标bucket路径大小)，即兼容允许同一个bucket 路径允许多个不同的pod挂载


```shell
make container
docker tag a0491baede5a registry.cn-shenzhen.aliyuncs.com/gsmini/csi-s3:local-build
docker push registry.cn-shenzhen.aliyuncs.com/gsmini/csi-s3:local-build
kubectl replace -f ai-on-k8s/ai-architecture/minio-k8s/csi-s3/csi-s3.yaml
```