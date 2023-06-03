腾讯云建机器 T4

装docker,装 nvidia-container-toolkit
https://docs.docker.com/engine/install/ubuntu/

``` shell
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
 sudo install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  sudo chmod a+r /etc/apt/keyrings/docker.gpg
  
echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \ 
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)       && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo g
pg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg       && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia
-container.list |             sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' |             sudo tee /et
c/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker

# 重启
 
    
```

下我的镜像
`` docker pull tianyu5/nv-tensorrt-8.5-build ``

下代码,挂盘
```shell
fdisk -l
mkdir /data/ai
mount /dev/vdb /data/ai
df -TH

rm -rf /root/.cache
ln -sf /data/ai/.cache/ /root/.cache

git clone https://github.com/tianyu-sz/TensorRT.git -b ty-8.5

```


`` docker run --name nv-tensorrt-8.5-build-0 -it --gpus all -v $PWD:/workspace -v /data/ai/.cache:/root/.cache tianyu5/nv-tensorrt-8.5-build /bin/bash ``

follow the readme


```shell
LD_PRELOAD=${PLUGIN_LIBS} python3 demo-diffusion.py "very complex hyper-maximalist overdetailed cinematic tribal darkfantasy closeup portrait of a malignant beautiful young dragon queen goddess megan fox with long black windblown hair and dragon scale wings, Magic the gathering, pale skin and dark eyes,flirting smiling succubus confident seductive, gothic, windblown hair, vibrant high contrast, by andrei riabovitchev, tomasz alen kopera,moleksandra shchaslyva, peter mohrbacher, Omnious intricate, octane, moebius, arney freytag, Fashion photo shoot, glamorous pose, trending on ArtStation, dramatic lighting, ice, fire and smoke, orthodox symbolism Diesel punk, mist, ambient occlusion, volumetric lighting, Lord of the rings, BioShock, glamorous, emotional, tattoos,shot in the photo studio, professional studio lighting, backlit, rim lightingDeviant-art, hyper detailed illustration, 8k" --build-static-batch --build-dynamic-shape --height=768 --width=512 --seed=4
```


完事传 COS ,直接上传hugging face ,腾讯云机器太慢