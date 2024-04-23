### Editor shortcuts
Vim
Ctrl + A # jump to the start
Ctrl + E # jump to the end
G # start
GG # end

Bash cmd line
Ctrl + A # jump to the start
Ctrl + E # jump to the end

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
Experimental
https://askubuntu.com/questions/1440887/can-i-install-wechat-in-ubuntu-22-04 

Wine - windows, said the UI was buggy

Web version, said it was taken down by TenCent

### Feishu | Lark
[web download, linux](https://www.feishu.cn/download)

[doc](https://www.feishu.cn/hc/zh-CN/articles/360025035993-%E4%B8%8B%E8%BD%BD%E5%92%8C%E5%AE%89%E8%A3%85%E9%A3%9E%E4%B9%A6%E5%AE%A2%E6%88%B7%E7%AB%AF#tabs0|lineguid-A4xFb)

```
sudo dpkg -i Feishu-linux_x64-7.11.9.deb

Output:

Selecting previously unselected package bytedance-feishu-stable.
(Reading database ... 166376 files and directories currently installed.)
Preparing to unpack Feishu-linux_x64-7.11.9.deb ...
Unpacking bytedance-feishu-stable (7.11.9-0) ...
Setting up bytedance-feishu-stable (7.11.9-0) ...
update-alternatives: using /usr/bin/bytedance-feishu-stable to provide /usr/bin/bytedance-feishu (bytedance-feishu) in auto mode
Processing triggers for gnome-menus (3.13.3-11ubuntu1.1) ...
Processing triggers for desktop-file-utils (0.23-1ubuntu3.18.04.2) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...

```

### 1Psw ubuntu desktop
https://support.1password.com/install-linux/#debian-or-ubuntu

```
# Duplicates with 1Psw CLI step # 1, 2, 3, skipped

# 1
curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg

# 2
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/amd64 stable main' | sudo tee /etc/apt/sources.list.d/1password.list

# 3
sudo mkdir -p /etc/debsig/policies/AC2D62742012EA22/
 curl -sS https://downloads.1password.com/linux/debian/debsig/1password.pol | sudo tee /etc/debsig/policies/AC2D62742012EA22/1password.pol
 sudo mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22
 curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg

# 4
sudo apt update && sudo apt install 1password

```

### 1Psw CLI
#### Official (Link)[https://developer.1password.com/docs/cli/get-started/#install]
```
sudo -s \
curl -sS https://downloads.1password.com/linux/keys/1password.asc | \
gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/$(dpkg --print-architecture) stable main" |
tee /etc/apt/sources.list.d/1password.list
mkdir -p /etc/debsig/policies/AC2D62742012EA22/
curl -sS https://downloads.1password.com/linux/debian/debsig/1password.pol | \
tee /etc/debsig/policies/AC2D62742012EA22/1password.pol
mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22
curl -sS https://downloads.1password.com/linux/keys/1password.asc | \
gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg
apt update && apt install 1password-cli
```
#### Modified
```
# 1
sudo curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg

# 2
sudo echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/$(dpkg --print-architecture) stable main" | sudo tee /etc/apt/sources.list.d/1password.list

sirius@sirius-ThinkPad-X1-Extreme:~/workspace$ ls /etc/apt/sources.list.d/
1password.list  apolloauto.list  nvidia-container-toolkit.list

# 3
sudo mkdir -p /etc/debsig/policies/AC2D62742012EA22/
sudo mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22

# 4
sudo curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg

# 5
sudo apt update && sudo apt install 1password-cli

# 6 check version [2.27.0]
op --version

# 7 shell completion feature with tab, Add this line to .bashrc
source <(op completion bash)
```

#### 1Psw CLI cmd [reference](https://developer.1password.com/docs/cli/reference/)

```
# list all vaults
op vault list

# list all items
op item list

op item list --vault Private
op item list --vault servers

op item get z690 --vault servers
```

```
op vault --help

Manage permissions and perform CRUD operations on your 1Password vaults.

Usage:  op vault [command] [flags]

Management Commands:
  group       Manage group vault access
  user        Manage user vault access

Commands:
  create      Create a new vault
  get         Get details about a vault
  edit        Edit a vault's name, description, icon, or Travel Mode status
  delete      Remove a vault
  list        List all vaults in the account

Flags:
  -h, --help   help for vault

To list the global flags available on every command, run  'op --help'.

Run 'op vault [command] --help' for more information on the command.

```

```
op item --help

Perform CRUD operations on the 1Password items in your vaults.

Usage:  op item [command] [flags]

Management Commands:
  template    Manage templates

Commands:
  create      Create an item
  get         Get an item's details
  edit        Edit an item's details
  delete      Delete or archive an item
  list        List items
  move        Move an item between vaults
  share       Share an item

Flags:
  -h, --help   help for item

To list the global flags available on every command, run  'op --help'.

Run 'op item [command] --help' for more information on the command.

```

[secret references without plaintxt](https://developer.1password.com/docs/cli/secret-references/)
```
e.g.

# 1
docker login -u $(op read op://prod/docker/username) -p $(op read op://prod/docker/password)

# 2
export DB_USER="op://app-dev/db/user"
export DB_PASSWORD="op://app-dev/db/password"

# 3
database:
    host: http://localhost
    port: 5432
    username: op://prod/mysql/username
    password: op://prod/mysql/password
```
[### nvidia container toolkit
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
Experimental
https://askubuntu.com/questions/1440887/can-i-install-wechat-in-ubuntu-22-04 

Wine - windows, said the UI was buggy

Web version, said it was taken down by TenCent

[url1](https://web.wechat.com/)

[url2](https://web1.wechat.com/cgi-bin/mmwebwx-bin/webwxindex?t=v2/index)

### 1Psw ubuntu desktop
https://support.1password.com/install-linux/#debian-or-ubuntu

```
# Duplicates with 1Psw CLI step # 1, 2, 3, skipped

# 1
curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg

# 2
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/amd64 stable main' | sudo tee /etc/apt/sources.list.d/1password.list

# 3
sudo mkdir -p /etc/debsig/policies/AC2D62742012EA22/
 curl -sS https://downloads.1password.com/linux/debian/debsig/1password.pol | sudo tee /etc/debsig/policies/AC2D62742012EA22/1password.pol
 sudo mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22
 curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg

# 4
sudo apt update && sudo apt install 1password

```

### 1Psw CLI
#### Official (Link)[https://developer.1password.com/docs/cli/get-started/#install]
```
sudo -s \
curl -sS https://downloads.1password.com/linux/keys/1password.asc | \
gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/$(dpkg --print-architecture) stable main" |
tee /etc/apt/sources.list.d/1password.list
mkdir -p /etc/debsig/policies/AC2D62742012EA22/
curl -sS https://downloads.1password.com/linux/debian/debsig/1password.pol | \
tee /etc/debsig/policies/AC2D62742012EA22/1password.pol
mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22
curl -sS https://downloads.1password.com/linux/keys/1password.asc | \
gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg
apt update && apt install 1password-cli
```
#### Modified
```
# 1
sudo curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/keyrings/1password-archive-keyring.gpg

# 2
sudo echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/$(dpkg --print-architecture) stable main" | sudo tee /etc/apt/sources.list.d/1password.list

sirius@sirius-ThinkPad-X1-Extreme:~/workspace$ ls /etc/apt/sources.list.d/
1password.list  apolloauto.list  nvidia-container-toolkit.list

# 3
sudo mkdir -p /etc/debsig/policies/AC2D62742012EA22/
sudo mkdir -p /usr/share/debsig/keyrings/AC2D62742012EA22

# 4
sudo curl -sS https://downloads.1password.com/linux/keys/1password.asc | sudo gpg --dearmor --output /usr/share/debsig/keyrings/AC2D62742012EA22/debsig.gpg

# 5
sudo apt update && sudo apt install 1password-cli

# 6 check version [2.27.0]
op --version

# 7 shell completion feature with tab, Add this line to .bashrc
source <(op completion bash)
```

#### 1Psw CLI cmd [reference](https://developer.1password.com/docs/cli/reference/)

```
# list all vaults
op vault list

# list all items
op item list

op item list --vault Private
op item list --vault servers

op item get z690 --vault servers
```

```
op vault --help

Manage permissions and perform CRUD operations on your 1Password vaults.

Usage:  op vault [command] [flags]

Management Commands:
  group       Manage group vault access
  user        Manage user vault access

Commands:
  create      Create a new vault
  get         Get details about a vault
  edit        Edit a vault's name, description, icon, or Travel Mode status
  delete      Remove a vault
  list        List all vaults in the account

Flags:
  -h, --help   help for vault

To list the global flags available on every command, run  'op --help'.

Run 'op vault [command] --help' for more information on the command.

```

```
op item --help

Perform CRUD operations on the 1Password items in your vaults.

Usage:  op item [command] [flags]

Management Commands:
  template    Manage templates

Commands:
  create      Create an item
  get         Get an item's details
  edit        Edit an item's details
  delete      Delete or archive an item
  list        List items
  move        Move an item between vaults
  share       Share an item

Flags:
  -h, --help   help for item

To list the global flags available on every command, run  'op --help'.

Run 'op item [command] --help' for more information on the command.

```

[secret references without plaintxt](https://developer.1password.com/docs/cli/secret-references/)
```
e.g.

# 1
docker login -u $(op read op://prod/docker/username) -p $(op read op://prod/docker/password)

# 2
export DB_USER="op://app-dev/db/user"
export DB_PASSWORD="op://app-dev/db/password"

# 3
database:
    host: http://localhost
    port: 5432
    username: op://prod/mysql/username
    password: op://prod/mysql/password
```
[TODO 1password ssh agent](https://developer.1password.com/docs/ssh/agent/?utm_medium=organic&utm_source=oph&utm_campaign=linux)
so far, ssh github key is usable, so I'm gonna ignore it for now;

### orb-slam
~/workspace/orb-slam

Pangolin
OpenCV
    apt install 

### apollo 8.0
[Doc](https://apollo.baidu.com/community/Apollo-Homepage-Document/Apollo_Doc_CN_8_0)

### Apollo Studio
[Hardware Platform](https://apollo.baidu.com/community/hardware)
[Simulation platform](https://apollo.baidu.com/workspace)
[Doc Overall](https://apollo.baidu.com/community/Apollo-Homepage-Document?doc=BYFxAcGcC4HpYIbgPYBtXIHQCMEEsATAV0wGNkBbWA5UyRFdZWVBEAU0hFjwDsD2AD0ygKqIA)
[Doc Simulation Platform](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E6%A6%82%E8%A7%88/)

[Simulation Local Env Install, Apollo + Dreamview](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E5%AE%89%E8%A3%85%E6%9C%AC%E5%9C%B0%E4%BB%BF%E7%9C%9F%E7%B3%BB%E7%BB%9F)

[Simulation local tuning](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E8%B0%83%E8%AF%95%E6%9C%AC%E5%9C%B0%E4%BB%BF%E7%9C%9F%E7%B3%BB%E7%BB%9F)

[My local simulation combo xh_2024, 6 total, with parking challenge](https://apollo.baidu.com/workspace/scenario-manage/sence-preview-collection/66261ebc3d60cd7f678d919b)

[Lidar Calibration](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/Fuel%E7%A0%94%E5%8F%91%E4%BA%91%E5%B9%B3%E5%8F%B0/%E6%84%9F%E7%9F%A5%E6%A0%87%E5%AE%9A/%E6%BF%80%E5%85%89%E9%9B%B7%E8%BE%BE%E5%A4%96%E5%8F%82%E6%A0%87%E5%AE%9A)
[Camera Calibration](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/Fuel%E7%A0%94%E5%8F%91%E4%BA%91%E5%B9%B3%E5%8F%B0/%E6%84%9F%E7%9F%A5%E6%A0%87%E5%AE%9A/%E7%9B%B8%E6%9C%BA%E5%A4%96%E5%8F%82%E6%A0%87%E5%AE%9A)

Note: use 15012731636 to login, this has teacher priviledge, github also works, but it's not binded to Apollo teacher certificate training on 04202024-04212024.

### apollo 9.0
[Release Conference](https://apollo.baidu.com/community/article/1221)
[Installation Guide](https://apollo.baidu.com/community/Apollo-Homepage-Document?doc=BYFxAcGcC4HpYIbgPYBtXIHQCMEEsATAV0wGNkBbWA5UyRFdZWVBEAU0hFgoIH0adPgCY%2BADwCiAVnEBBCeIAcATnETFcgMxKZkgGxKAwkoDsa3YoAi45WdGSLxsYt0SzY%2BXICMa98oAMSgYALF7%2B2NhemsLBJsrCYZqKwors7AikBIp6miYmpFJSXpigFKgAxAhEIMg1pHy8mv5AA)

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
#### buildtool output core -- partial
```
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
Extracting Bazel installation...
Starting local Bazel server and connecting to it...
(11:49:51) INFO: Current date is 2024-04-23
(11:50:10) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (6 packages loaded, 11 targets configured).
(11:50:10) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install_src up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install_src
(11:50:10) INFO: Elapsed time: 23.984s, Critical Path: 0.03s
(11:50:10) INFO: 4 processes: 4 internal.
(11:50:10) INFO: Build completed successfully, 4 total actions
(11:50:10) INFO: Build completed successfully, 4 total actions
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(11:50:11) INFO: Current date is 2024-04-23
(11:50:11) INFO: Analyzed target //dev/buildtool/mock:mock_install (0 packages loaded, 5 targets configured).
(11:50:11) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install
(11:50:11) INFO: Elapsed time: 0.459s, Critical Path: 0.02s
(11:50:11) INFO: 4 processes: 4 internal.
(11:50:11) INFO: Build completed successfully, 4 total actions
(11:50:11) INFO: Build completed successfully, 4 total actions
Installing the project stripped...
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 11:50:11 INFO compilation done!
```

](https://developer.1password.com/docs/ssh/agent/?utm_medium=organic&utm_source=oph&utm_campaign=linux)

### orb-slam
~/workspace/orb-slam

Pangolin
OpenCV
    apt install 
