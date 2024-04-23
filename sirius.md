### nvidia container toolkit
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installing-with-apt
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html

### sunlogin
https://sunlogin.oray.com/download/linux?type=personal&ici=sunlogin_navigation

sudo dpkg -i xxx.deb

To start
    /usr/local/sunlogin/bin/sunloginclient

To remove
    sudo dpkg -r sunloginclient

Fix problems
https://service.oray.com/question/11969.html 

### Tencent Meeting
sudo dpkg -i xxx.deb

### WeChat
https://askubuntu.com/questions/1440887/can-i-install-wechat-in-ubuntu-22-04 

### orb-slam
~/workspace/orb-slam

Pangolin
OpenCV
    apt install 

### apollo 9.0 Installation

Guide
https://apollo.baidu.com/community/Apollo-Homepage-Document?doc=BYFxAcGcC4HpYIbgPYBtXIHQCMEEsATAV0wGNkBbWA5UyRFdZWVBEAU0hFgoIH0adPgCY%2BADwCiAVnEBBCeIAcATnETFcgMxKZkgGxKAwkoDsa3YoAi45WdGSLxsYt0SzY%2BXICMa98oAMSgYALF7%2B2NhemsLBJsrCYZqKwors7AikBIp6miYmpFJSXpigFKgAxAhEIMg1pHy8mv5AA

#### 添加 gpg key
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://apollo-pkg-beta.cdn.bcebos.com/neo/beta/key/deb.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/apolloauto.gpg
sudo chmod a+r /etc/apt/keyrings/apolloauto.gpg
```

#### 设置源并更新
```
echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/apolloauto.gpg] https://apollo-pkg-beta.cdn.bcebos.com/apollo/core"\
    $(. /etc/os-release && echo "$VERSION_CODENAME") "main" | \
    sudo tee /etc/apt/sources.list.d/apolloauto.list
sudo apt-get update
```

Note：如果之前已经安装过8.0版本的apollo的话，在宿主机上的/etc/apt/sources.list文件中会有形如 deb https://apollo-pkg-beta.cdn.bcebos.com/neo/beta bionic main的配置，可以直接删除，宿主机上的apollo源配置仅用于安 装aem工具 

```
sirius@sirius-ThinkPad-X1-Extreme:~$ ls /etc/apt/sources.list.d/
apolloauto.list  nvidia-container-toolkit.list
```

```
sudo apt install apollo-neo-env-manager-dev --reinstall
aem -h
```

```
git clone https://github.com/ApolloAuto/application-core.git application-core
```

```
# 先进入工程目录
cd application-core
# 环境设置：识别主机系统是x86_64还是aarch64, 并修改对应的.env和.workspace.json配置
bash setup.sh
# 启动容器
aem start
```

#### docker pull output -- partial, skipped download
```
Digest: sha256:a40252872d2815b0a9e8fae35487e0d04f7131d5b64e7e73c3a3640d845368cc
Status: Downloaded newer image for registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest
registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest
[INFO] Remove existing Apollo Development container ...
[INFO] Starting Docker container "apollo_neo_dev_9.0.0_rc_r10_core" ...
+ docker run --gpus all -itd --privileged --name apollo_neo_dev_9.0.0_rc_r10_core --label owner=root -e DISPLAY=:0 -e CROSS_PLATFORM=0 -e DOCKER_USER=sirius -e USER=sirius -e DOCKER_USER_ID=1000 -e HISTFILE=/apollo_workspace/.cache/.bash_history -e DOCKER_GRP=sirius -e DOCKER_GRP_ID=1000 -e DOCKER_IMG=registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest -e USE_GPU_HOST=1 -e NVIDIA_VISIBLE_DEVICES=all -e NVIDIA_DRIVER_CAPABILITIES=compute,video,graphics,utility -e APOLLO_ENV_CONTAINER_IMAGE=registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest -e APOLLO_ENV_CONTAINER_PREFIX=apollo_neo_dev_ -e APOLLO_ENV_CONTAINER_REPO=registry.baidubce.com/apollo/apollo-env-gpu -e APOLLO_ENV_CONTAINER_REPO_ARM=registry.baidubce.com/apollo/apollo-env-arm -e APOLLO_ENV_CONTAINER_REPO_X86=registry.baidubce.com/apollo/apollo-env-gpu -e APOLLO_ENV_CONTAINER_TAG=9.0-latest -e APOLLO_ENV_NAME=9.0.0_rc_r10_core -e APOLLO_ENV_WORKLOCAL=1 -e APOLLO_ENV_WORKROOT=/apollo_workspace -e APOLLO_ENV_WORKSPACE=/home/sirius/workspace/apollo_9.0/application-core -v /home/sirius/.apollo:/home/sirius/.apollo -v /dev:/dev -v /media:/media -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v /etc/localtime:/etc/localtime:ro -v /usr/src:/usr/src -v /lib/modules:/lib/modules -v apollo_neo_dev_9.0.0_rc_r10_core_apollo:/apollo -v apollo_neo_dev_9.0.0_rc_r10_core_opt:/opt -v /home/sirius/workspace/apollo_9.0/application-core:/apollo_workspace -v /home/sirius/workspace/apollo_9.0/application-core/data:/apollo/data -v /home/sirius/workspace/apollo_9.0/application-core/output:/apollo/output -v /home/sirius/workspace/apollo_9.0/application-core/data/log:/opt/apollo/neo/data/log -v /home/sirius/workspace/apollo_9.0/application-core/data/calibration_data:/apollo/modules/calibration/data -v /home/sirius/workspace/apollo_9.0/application-core/data/map_data:/apollo/modules/map/data -v /opt/apollo/neo/packages/env-manager-dev/9.0.0-rc1-r1:/opt/apollo/neo/packages/env-manager-dev/9.0.0-rc1-r1 --net host -w /apollo_workspace --add-host in-dev-docker:127.0.0.1 --add-host sirius-ThinkPad-X1-Extreme:127.0.0.1 --hostname in-dev-docker --shm-size 2G --pid=host -v /dev/null:/dev/raw1394 registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest /bin/bash
25c6f74e04a9bb7fa3e68454eba3263beff88afe8be8dcde2348033b312dc2ed
+ '[' 0 -ne 0 ']'
+ set +x
mkdir: created directory '/opt/apollo/neo/etc'

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

Hit:1 http://mirrors.aliyun.com/ubuntu bionic InRelease
Get:2 http://mirrors.aliyun.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://mirrors.aliyun.com/ubuntu bionic-backports InRelease [83.3 kB]
Get:4 http://mirrors.aliyun.com/ubuntu bionic-security InRelease [88.7 kB]
Get:5 https://apollo-pkg-beta.cdn.bcebos.com/apollo/core bionic InRelease [1389 B]
Get:6 http://mirrors.aliyun.com/ubuntu bionic-updates/main amd64 Packages [3786 kB]
Get:7 https://apollo-pkg-beta.cdn.bcebos.com/apollo/core bionic/main amd64 Packages [286 kB]
Get:8 http://mirrors.aliyun.com/ubuntu bionic-updates/universe amd64 Packages [2411 kB]
Get:9 http://mirrors.aliyun.com/ubuntu bionic-security/universe amd64 Packages [1637 kB]
Get:10 http://mirrors.aliyun.com/ubuntu bionic-security/main amd64 Packages [3373 kB]
Fetched 11.8 MB in 10s (1223 kB/s)
Reading package lists...
Building dependency tree...
Reading state information...
74 packages can be upgraded. Run 'apt list --upgradable' to see them.

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

Reading package lists...
Building dependency tree...
Reading state information...
Skipping apollo-neo-cyber, it is not installed and only upgrades are requested.
Skipping apollo-neo-common, it is not installed and only upgrades are requested.
Skipping apollo-neo-common-msgs, it is not installed and only upgrades are requested.
The following package was automatically installed and is no longer required:
  libsqlite3-dev
Use 'apt autoremove' to remove it.
The following packages will be upgraded:
  apollo-neo-buildtool
1 upgraded, 0 newly installed, 0 to remove and 73 not upgraded.
Need to get 127 kB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://apollo-pkg-beta.cdn.bcebos.com/apollo/core bionic/main amd64 apollo-neo-buildtool amd64 9.0.0-rc1-r14 [127 kB]
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (This frontend requires a controlling tty.)
debconf: falling back to frontend: Teletype
dpkg-preconfigure: unable to re-open stdin: 
Fetched 127 kB in 0s (285 kB/s)
(Reading database ... 19802 files and directories currently installed.)
Preparing to unpack .../apollo-neo-buildtool_9.0.0-rc1-r14_amd64.deb ...
Unpacking apollo-neo-buildtool (9.0.0-rc1-r14) over (9.0.0-alpha3-r3) ...
Setting up apollo-neo-buildtool (9.0.0-rc1-r14) ...
[INFO] start to create symbolic links of buildtool
[WARN] the links of pre-version will be overwrited!
[INFO] symbolic links of buildtool created.
Adding group `sirius' (GID 1000) ...
Done.
Adding user `sirius' ...
Adding new user `sirius' (1000) with group `sirius' ...
adduser: Warning: The home directory `/home/sirius' does not belong to the user you are currently creating.
The home directory `/home/sirius' already exists.  Not copying from `/etc/skel'.
**************************************************************
  Congratulations! 🎉 Apollo Dev Environment is set up.
 To login into the newly created apollo_neo_dev_9.0.0_rc_r10_core container.
   Please run the following command: 🌟 aem enter 🌟  
          Enjoy your coding journey! ✨
                         _ _          ___   ___  
                        | | |        / _ \ / _ \ 
        __ _ _ __   ___ | | | ___   | (_) | | | |
       / _` | '_ \ / _ \| | |/ _ \   \__, | | | |
      | (_| | |_) | (_) | | | (_) |    / /| |_| |
       \__,_| .__/ \___/|_|_|\___/    /_(_)\___/ 
            | |                                  
            |_|                                   
**************************************************************
[INFO] Query new version of aem...

```

```
# 先进入工程目录
cd application-core
# 进入容器
sudo aem enter
```

(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$

```
# 示例工程中包含一个名为 core 目录，其中 core/cyberfile.xml 文件中描述了工程所依赖软件包，可以通过 buildtool 工具进行依赖包的安装
buildtool build -p core
```