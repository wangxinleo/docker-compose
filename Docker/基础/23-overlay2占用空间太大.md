# `/var/lib/docker/overlay2`磁盘空间占用太大问题

> tips: 千万不要直接删除掉！！！ 
> 只能去删除无用镜像或其相关日志信息...
> 如果不懂此操作，建议先存个快照，避免删除重要数据！！！

### 查看docker所占的硬盘大小

```shell
docker system df
# TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
# Images          19        4         8.339GB   7.514GB (90%)
# Containers      4         4         6B        0B (0%)
# Local Volumes   1389      1         3.012GB   3.012GB (100%)
# Build Cache     0         0         0B        0B
```

### 清理悬挂的容器（即已停止的容器）

```shell
docker container prune

# 不用输入y确认
# docker container prune -f
```

### 清理未使用的镜像（不包括标签为':'的镜像）

```shell
docker image prune -a
```

### 清理未使用的网络

```shell
docker network prune
```

### 清理未使用的卷

```shell
docker volume prune
```

### 清理所有未被容器使用的镜像、网络和卷

```shell
docker system prune
```

### 清理所有未被容器使用的镜像、网络、卷、构建缓存

```shell
docker system prune -a
```

---

在docker中，默认启用了 overlay2作为文件管理系统

- lower-id 文件里面记录的是镜像层的顶层ID，也就是此层的基层 ，OverlayFS概念中的 lowerdir;
- upper 文件夹就是本层的可读写层（在 overlay2中的变成了diff）,它也就是 OverlayFS概念中的 upperdir;
- merged 文件夹是和文件夹的联合挂载，在运行中的容器看过去的文件系统就是它;
- work 文件夹则是OverlayFS内部文件;

