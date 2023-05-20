# 记录日志

* stable-diffusion-with-tensorrt:8.6.1 跑 tensorRT 8.6
* nvcr.io/nvidia/tensorrt:22.10-py3 跑 tensorRT 8.5
* 容器里需要重新编译so文件
* 参考shell history 文件

# tensorRT 8.5 
```shell 
docker run --name nv-tensorrt-85-build -it --gpus all -v $PWD:/workspace -v /data/ai/.cache:/root/.cache   nvcr.io/nvidia/tensorrt:22.10-py3 /bin/bash
```

```shell

```