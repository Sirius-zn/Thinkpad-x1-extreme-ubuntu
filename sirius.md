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

### Google chrome
[Download .deb](https://www.google.com/chrome/next-steps.html?platform=linux&statcb=0&installdataindex=empty&defaultbrowser=0)
```
sudo apt install libvulkan1
sudo dpkg -i xxx.deb
```

### Ubuntu hardware temp monitoring
https://askubuntu.com/questions/15832/how-do-i-get-the-cpu-temperature
sensors

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
  Catch2: https://github.com/catchorg/Catch2.git | latest is v3
      Catch2 [git checkout v2.x]
  [find_package Error: unable to locate Catch2]

  vcpkg route
  https://github.com/Microsoft/vcpkg 

  ```
  git clone https://github.com/Microsoft/vcpkg.git
  cd vcpkg
  ./bootstrap-vcpkg.sh
  ./vcpkg integrate install
  ./vcpkg install pangolin
  ```

  ```
  vcpkg Ouput

sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ./bootstrap-vcpkg.sh
Downloading vcpkg-glibc...
vcpkg package management program version 2024-04-23-d6945642ee5c3076addd1a42c331bbf4cfc97457

See LICENSE.txt for license information.
Telemetry
---------
vcpkg collects usage data in order to help us improve your experience.
The data collected by Microsoft is anonymous.
You can opt-out of telemetry by re-running the bootstrap-vcpkg script with -disableMetrics,
passing --disable-metrics to vcpkg on the command line,
or by setting the VCPKG_DISABLE_METRICS environment variable.

Read more about vcpkg telemetry at docs/about/privacy.md
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ./vcpkg integrate install
Applied user-wide integration for this vcpkg root.
CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=/home/sirius/workspace/vcpkg/scripts/buildsystems/vcpkg.cmake"

sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ./vcpkg install pangolin

(...) skipped

CMake Error at packages/vcpkg-tool-meson_x64-linux/share/vcpkg-tool-meson/vcpkg-port-config.cmake:60 (message):
  Found Python version '3.6.9 at /usr/bin/python3' is insufficient for meson.
  meson requires at least version '3.7'
Call Stack (most recent call first):
  ports/vcpkg-tool-meson/portfile.cmake:39 (include)
  scripts/ports.cmake:175 (include)

-------------------------------------
(fix)
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ sudo apt install python3.7
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ sudo ln -sf /usr/bin/python3.7 /usr/bin/python3
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ which python3
/usr/bin/python3
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ls -l /usr/bin/python3
lrwxrwxrwx 1 root root 18 Apr 29 15:07 /usr/bin/python3 -> /usr/bin/python3.7

(after upgrading to python 3, apt-get and terminal will have problem opening)
sudo apt-get --reinstall install python3-minimal will fix the problem but reset python3 symbolic link back to python3.6

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2

sudo update-alternatives --config python3
-------------------------

sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ./vcpkg install pangolin

(...) skipped

-- Using source at /home/sirius/workspace/vcpkg/buildtrees/ffmpeg/src/n6.1.1-bf510528a2.clean
CMake Error at scripts/cmake/vcpkg_find_acquire_program.cmake:166 (message):
  Could not find nasm.  Please install it via your package manager:

      sudo apt-get install nasm
Call Stack (most recent call first):
  ports/ffmpeg/portfile.cmake:29 (vcpkg_find_acquire_program)
  scripts/ports.cmake:175 (include)

(fix)
sudo apt-get install nasm

sirius@sirius-ThinkPad-X1-Extreme:~/workspace/vcpkg$ ./vcpkg install pangolin

Building ffmpeg for release... [cpu blasting...]

CMake Warning at ports/glew/portfile.cmake:2 (message):
  glew requires the following libraries from the system package manager:

      libxmu-dev
      libxi-dev
      libgl-dev

(fix)
sudo apt-get install libxmu-dev libxi-dev libgl-dev
sudo apt-get install libgl1-mesa-dev
sudo apt install libglu1-mesa-dev

./vcpkg install pangolin [succeed]

  ```

(How to build with vcpkg managed C++ packages)[https://github.com/Microsoft/vcpkg]

When using vcpkg as a submodule of your project, you can add the following to your CMakeLists.txt before the first project() call, instead of passing CMAKE_TOOLCHAIN_FILE to the cmake invocation.

```
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
  CACHE STRING "Vcpkg toolchain file")
```

or

```
-DCMAKE_TOOLCHAIN_FILE=/home/sirius/workspace/vcpkg/scripts/buildsystems/vcpkg.cmake
CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=/home/sirius/workspace/vcpkg/scripts/buildsystems/vcpkg.cmake"
```

DBoW2 && g2o
  Both modified version is included in the Thirdparty folder;

Eigen
    sudo apt-get install libeigen3-dev
    Get:1 http://mirrors.tuna.tsinghua.edu.cn/ubuntu bionic/universe amd64 libeigen3-dev all 3.3.4-4 [810 kB]

    [Don't build from src yet]

OpenCV
    https://opencv.org/get-started/
    Python | pip3 install opencv-python
    C++ | apt install libopencv-dev
      libopencv-dev is already the newest version (3.2.0+dfsg-4ubuntu0.1)

    Needs 4.4.0;

    [Don't build from src yet]

    [Let's build from src]

    sudo apt remove libopencv* [remove openCV 3.2]

    [actually, try vcpkg 1st]
    ./vcpkg search opencv

    (missing dependencies)
    sudo apt-get install autoconf
    sudo apt install libdbus-1-dev
    sudo apt install python3-pip [switched back to python3.6 using python alternative]
    pip3 install jinja2
    sudo update-alternatives --config python3
    pip3 show jinja2 [for 3.6 Location: /home/sirius/.local/lib/python3.6/site-packages, for 3.7 Location: /home/sirius/.local/lib/python3.7/site-packages]
    sudo apt-get install bison
    sudo apt-get install libxi-dev libxtst-dev
    sudo apt install libx11-dev libxft-dev libxext-dev
    sudo apt-get install libxrandr-dev

    ./vcpkg install opencv4

Stored binaries in 1 destinations in 25 s.
Elapsed time to handle opencv4:x64-linux: 12 min
opencv4:x64-linux package ABI: 48cab8742662ef661c1abb39bac7c669bb420b8953c063fbad564bc73f64503e
Total install time: 21 min
If you do not install the meta-port *opencv*, the package opencv4 is compatible with CMake
if you set the OpenCV_DIR *before* the find_package call

    set(OpenCV_DIR "${VCPKG_INSTALLED_DIR}/x64-linux/share/opencv4")
    find_package(OpenCV REQUIRED)

ORB-SLAM3
    sudo apt install libboost-all-dev
    chmod +x build.sh
    Add the following line to build.sh
      -DCMAKE_TOOLCHAIN_FILE=/home/sirius/workspace/vcpkg/scripts/buildsystems/vcpkg.cmake

[g2o warning]

In file included from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/types_seven_dof_expmap.h:35:0,                                                    
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/types_seven_dof_expmap.cpp:27:               
/home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/../core/base_binary_edge.h:60:80: warning: ‘Eigen::AlignedBit’ is deprecated [-Wdeprecated-declarations]
       typedef Eigen::Map<Matrix<double, Dj, Di>, Matrix<double, Dj, Di>::Flags & AlignedBit ? Aligned : Unaligned > HessianBlockTransposedType;                           
                                                  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~                                                                               
In file included from /usr/include/eigen3/Eigen/Core:344:0,                                                                           
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/../core/jacobian_workspace.h:30,                                             
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/../core/optimizable_graph.h:41,                                                   
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/../core/base_vertex.h:30,                                                     
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/types_seven_dof_expmap.h:34,   
                 from /home/sirius/workspace/orb-slam/ORB_SLAM3/Thirdparty/g2o/g2o/types/types_seven_dof_expmap.cpp:27:                                                    
/usr/include/eigen3/Eigen/src/Core/util/Constants.h:162:37: note: declared here                                                                 
 EIGEN_DEPRECATED const unsigned int AlignedBit = 0x80;

### cpu frequency
sudo apt install cpufrequtils
watch -n 1 cpufreq-info
sudo cpufreq-set -r -g performance
sudo cpufreq-set -r -g powersave

### apollo 8.0
[Doc](https://apollo.baidu.com/community/Apollo-Homepage-Document/Apollo_Doc_CN_8_0)

### apollo 9.0
[Doc](https://apollo.baidu.com/docs/apollo/latest/index.html)
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
sudo aem start
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

### Apollo Studio
[Hardware Platform](https://apollo.baidu.com/community/hardware)
[Simulation platform](https://apollo.baidu.com/workspace)
[Doc Overall](https://apollo.baidu.com/community/Apollo-Homepage-Document?doc=BYFxAcGcC4HpYIbgPYBtXIHQCMEEsATAV0wGNkBbWA5UyRFdZWVBEAU0hFjwDsD2AD0ygKqIA)
[Doc Simulation Platform](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E6%A6%82%E8%A7%88/)

[Simulation Local Env Install, Apollo + Dreamview](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E5%AE%89%E8%A3%85%E6%9C%AC%E5%9C%B0%E4%BB%BF%E7%9C%9F%E7%B3%BB%E7%BB%9F)

#### Simulation Local Env Install, Apollo + Dreamview + local simulation binding to the cloud, one time;
```
# Key for the simulation platform over the cloud, run inside docker
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ curl -fsSL -o /tmp/apollo-studio-connector-install.sh "http://bj.bcebos.com/apollo-studio/archive/apps/profile/studio_connector_installer/35214804/install.5.5c525332-7d27-4f28-8987-614859da871c.sh?authorization=bce-auth-v1%2F31e5c09d20bb4a4cbad2e1f4f8b230a1%2F2024-04-23T06%3A51%3A38Z%2F300%2F%2Fc7467f8522da493015f2a9651a664be88efda054a0b392f61645150c3cb2f993" && bash /tmp/apollo-studio-connector-install.sh

# Output
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ curl -fsSL -o /tmp/apollo-studio-connector-install.sh "http://bj.bcebos.com/apollo-studio/archive/apps/profile/studio_connector_installer/35214804/ins
tall.5.5c525332-7d27-4f28-8987-614859da871c.sh?authorization=bce-auth-v1%2F31e5c09d20bb4a4cbad2e1f4f8b230a1%2F2024-04-23T06%3A51%3A38Z%2F300%2F%2Fc7467f8522da493015f2a9651a664be88efda054a0b392f61645150c3c
b2f993" && bash /tmp/apollo-studio-connector-install.sh
studio_connector/
studio_connector/libstudio_connector_component.so
studio_connector/package/
studio_connector/package/studio_connector_plugin_config_8.0.pb.txt
studio_connector/package/studio_connector.conf
studio_connector/package/studio_connector_plugin_config_9.0.pb.txt
studio_connector/package/studio_connector.dag
studio_connector/package/studio_connector.launch
./studio_connector/server.crt
./studio_connector/AUTH_ID
./studio_connector/client.key
./studio_connector/client.crt
./sim_obstacle/sim_obstacle
mkdir: created directory '/home/sirius/.apollo/dreamview'
mkdir: created directory '/home/sirius/.apollo/dreamview/plugins'
mkdir: created directory '/home/sirius/.apollo/dreamview/plugins/studio_connector'
'/tmp/apollo-studio-connector-install-pkg-kd0Vmo42k1/studio_connector/AUTH_ID' -> '/home/sirius/.apollo/dreamview/plugins/studio_connector/AUTH_ID'
'/tmp/apollo-studio-connector-install-pkg-kd0Vmo42k1/studio_connector/client.crt' -> '/home/sirius/.apollo/dreamview/plugins/studio_connector/client.crt'
'/tmp/apollo-studio-connector-install-pkg-kd0Vmo42k1/studio_connector/client.key' -> '/home/sirius/.apollo/dreamview/plugins/studio_connector/client.key'
'/tmp/apollo-studio-connector-install-pkg-kd0Vmo42k1/studio_connector/server.crt' -> '/home/sirius/.apollo/dreamview/plugins/studio_connector/server.crt'

# 启动 Apollo 环境容器成功后，在当前命令窗口下，安装仿真需要的模块。[legacy optional, outdated for apollo 9.0 seems like, `buildtool build -p core` from above already has everything bundled together]
aem init && buildtool install --legacy dreamview-dev && buildtool install --legacy monitor-dev && buildtool install planning-dev routing-dev

# Output
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ aem init && buildtool install --legacy dreamview-dev && buildtool install --legacy monitor-dev && buildtool install planning-dev routing-dev
[buildtool] 2024-04-23 15:00:52 INFO Reconfigure apollo enviroment setup
[INFO] Query new version of aem...
[buildtool] 2024-04-23 15:00:57 INFO update repo apollo-tools
[buildtool] 2024-04-23 15:00:57 INFO update complete
[buildtool] 2024-04-23 15:00:57 INFO update repo apollo-core
[buildtool] 2024-04-23 15:00:57 INFO update complete
[buildtool] 2024-04-23 15:00:57 INFO Reconfigure apollo enviroment setup
[buildtool] 2024-04-23 15:00:57 ERROR Encounter ErrCode.ParamErr
[buildtool] 2024-04-23 15:00:57 ERROR hint: dreamview-dev is not an apollo package, skip it
[buildtool] 2024-04-23 15:01:08 INFO No package will be processed
[buildtool] 2024-04-23 15:01:11 INFO update repo apollo-tools
[buildtool] 2024-04-23 15:01:11 INFO update complete
[buildtool] 2024-04-23 15:01:11 INFO update repo apollo-core
[buildtool] 2024-04-23 15:01:11 INFO update complete
[buildtool] 2024-04-23 15:01:11 INFO Reconfigure apollo enviroment setup
[buildtool] 2024-04-23 15:01:11 ERROR Encounter ErrCode.ParamErr
[buildtool] 2024-04-23 15:01:11 ERROR hint: monitor-dev is not an apollo package, skip it
[buildtool] 2024-04-23 15:01:22 INFO No package will be processed
[buildtool] 2024-04-23 15:01:25 INFO update repo apollo-tools
[buildtool] 2024-04-23 15:01:25 INFO update complete
[buildtool] 2024-04-23 15:01:25 INFO update repo apollo-core
[buildtool] 2024-04-23 15:01:25 INFO update complete
[buildtool] 2024-04-23 15:01:25 INFO Reconfigure apollo enviroment setup
[buildtool] 2024-04-23 15:01:25 ERROR Encounter ErrCode.ParamErr
[buildtool] 2024-04-23 15:01:25 ERROR hint: planning-dev is not an apollo package, skip it
[buildtool] 2024-04-23 15:01:25 ERROR Encounter ErrCode.ParamErr
[buildtool] 2024-04-23 15:01:25 ERROR hint: routing-dev is not an apollo package, skip it
[buildtool] 2024-04-23 15:01:35 INFO No package will be processed

Note: seems like application-core build already has everything built by `buildtool build -p core` from above;
```

[Simulation Local Tuning](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/%E4%BB%BF%E7%9C%9F%E5%B9%B3%E5%8F%B0/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E8%B0%83%E8%AF%95%E6%9C%AC%E5%9C%B0%E4%BB%BF%E7%9C%9F%E7%B3%BB%E7%BB%9F)

#### Simulation Local Tuning
```
# cyber_launch missing, fix

sudo buildtool build

# output
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ buildtool build                                                                                                                                       
[buildtool] 2024-04-23 15:15:10 INFO update repo apollo-tools                                                                                                                                               
[buildtool] 2024-04-23 15:15:10 INFO update complete
[buildtool] 2024-04-23 15:15:10 INFO update repo apollo-core
[buildtool] 2024-04-23 15:15:11 INFO update complete
[buildtool] 2024-04-23 15:15:11 INFO Reconfigure apollo enviroment setup
[buildtool] 2024-04-23 15:15:21 INFO Analyzing dependencies topological graph...
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess 3rd-grpc
[buildtool] 2024-04-23 15:15:23 INFO PostProcess 3rd-grpc
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libqhull7
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libqhull7
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess 3rd-gflags
[buildtool] 2024-04-23 15:15:23 INFO PostProcess 3rd-gflags
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libpcap0.8
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libpcap0.8
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess 3rd-glog
[buildtool] 2024-04-23 15:15:23 INFO PostProcess 3rd-glog
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libceres-dev
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libceres-dev
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libtiff5
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libtiff5
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess rsdriver
[buildtool] 2024-04-23 15:15:23 INFO PostProcess rsdriver
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libdouble-conversion1
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libdouble-conversion1
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libcurl4-openssl-dev
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libcurl4-openssl-dev
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess 3rd-yaml-cpp
[buildtool] 2024-04-23 15:15:23 INFO PostProcess 3rd-yaml-cpp
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libopenni0
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libopenni0
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libflann-dev
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libflann-dev
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess libfreetype6
[buildtool] 2024-04-23 15:15:23 INFO PostProcess libfreetype6
[buildtool] 2024-04-23 15:15:23 INFO Import depends...
[buildtool] 2024-04-23 15:15:23 INFO Preprocess 3rd-rules-python

... (skipped)

[buildtool] 2024-04-23 15:15:29 INFO PostProcess planning-scenario-traffic-light-protected
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess perception-lidar-detection-filter
[buildtool] 2024-04-23 15:15:29 INFO PostProcess perception-lidar-detection-filter
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess perception-msg-adapter
[buildtool] 2024-04-23 15:15:29 INFO PostProcess perception-msg-adapter
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess canbus-vehicle-lexus
[buildtool] 2024-04-23 15:15:29 INFO PostProcess canbus-vehicle-lexus
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess planning-scenario-emergency-stop
[buildtool] 2024-04-23 15:15:29 INFO PostProcess planning-scenario-emergency-stop
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess planning-task-pull-over-path
[buildtool] 2024-04-23 15:15:29 INFO PostProcess planning-task-pull-over-path
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess planning
[buildtool] 2024-04-23 15:15:29 INFO PostProcess planning
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess sim-obstacle
[buildtool] 2024-04-23 15:15:29 INFO PostProcess sim-obstacle
[buildtool] 2024-04-23 15:15:29 INFO Import depends...
[buildtool] 2024-04-23 15:15:29 INFO Preprocess core
[buildtool] 2024-04-23 15:15:29 INFO Using Source of core
[buildtool] 2024-04-23 15:15:30 INFO PostProcess core
[buildtool] 2024-04-23 15:15:30 INFO Compiling whole workspace...
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
Starting local Bazel server and connecting to it...
(15:15:31) INFO: Current date is 2024-04-23
(15:15:32) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (6 packages loaded, 11 targets configured).
(15:15:32) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install_src up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install_src
(15:15:32) INFO: Elapsed time: 2.761s, Critical Path: 0.02s
(15:15:32) INFO: 1 process: 1 internal.
(15:15:32) INFO: Build completed successfully, 1 total action
(15:15:32) INFO: Build completed successfully, 1 total action
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(15:15:33) INFO: Current date is 2024-04-23
(15:15:33) INFO: Analyzed target //dev/buildtool/mock:mock_install (0 packages loaded, 5 targets configured).
(15:15:33) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install
(15:15:33) INFO: Elapsed time: 0.284s, Critical Path: 0.01s
(15:15:33) INFO: 1 process: 1 internal.
(15:15:33) INFO: Build completed successfully, 1 total action
(15:15:33) INFO: Build completed successfully, 1 total action
Installing the project stripped...
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 15:15:33 INFO compilation done!

Conclution: `buildtool build` didn't fix
  [buildtool] 2024-04-23 15:19:40 ERROR hint: Could not find cyber_launch. Is cyber already installed?

# steps from apollo-edu-pre install-neo-core.sh
```
pip3 install requests -i https://mirror.baidu.com/pypi/simple/ --trusted-host mirror.baidu.com
sudo apt install -y --allow-unauthenticated uuid-dev apollo-neo-cyber-dev apollo-neo-common-dev apollo-neo-common-msgs-dev

# Output
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ sudo apt install -y --allow-unauthenticated uuid-dev apollo-neo-cyber-dev apollo-neo-common-dev apollo-neo-common-msgs-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package apollo-neo-cyber-dev
E: Unable to locate package apollo-neo-common-dev
E: Unable to locate package apollo-neo-common-msgs-dev

```

# Dreamview+ 
sudo aem bootstrap start --plus

```

[My local simulation combo xh_2024, 6 total, with parking challenge](https://apollo.baidu.com/workspace/scenario-manage/sence-preview-collection/66261ebc3d60cd7f678d919b)


[Lidar Calibration](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/Fuel%E7%A0%94%E5%8F%91%E4%BA%91%E5%B9%B3%E5%8F%B0/%E6%84%9F%E7%9F%A5%E6%A0%87%E5%AE%9A/%E6%BF%80%E5%85%89%E9%9B%B7%E8%BE%BE%E5%A4%96%E5%8F%82%E6%A0%87%E5%AE%9A)
[Camera Calibration](https://apollo.baidu.com/Apollo-Homepage-Document/Apollo_Studio/Fuel%E7%A0%94%E5%8F%91%E4%BA%91%E5%B9%B3%E5%8F%B0/%E6%84%9F%E7%9F%A5%E6%A0%87%E5%AE%9A/%E7%9B%B8%E6%9C%BA%E5%A4%96%E5%8F%82%E6%A0%87%E5%AE%9A)

Note: use 15012731636 to login, this has teacher priviledge, github also works, but it's not binded to Apollo teacher certificate training on 04202024-04212024.

#### Normal Routine
```
# 1
cd ~/workspace/apollo_9.0/application-core
sudo aem start
sudo aem enter

# pick a car
aem profile use sample

# optional, replay
wget https://apollo-system.cdn.bcebos.com/dataset/6.0_edu/demo_3.5.record -P $HOME/.apollo/resources/records/
buildtool map get sunnyvale
buildtool map list

# Dreamview+ 
sudo aem bootstrap start --plus

```

### Apollo Carla Bridge
[github](https://github.com/guardstrikelab/carla_apollo_bridge?tab=readme-ov-file)

```
sudo apt install docker-compose

```

### PNC try
[Guide](https://apollo.baidu.com/community/article/1239)
```
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/apollo_9.0/application-pnc$ sudo aem start_gpu                                                                                                        [74/148]
apollo_neo_dev_9.0.0_rc_r10_pnc_comp_apollo                                                                                                                                                                 
apollo_neo_dev_9.0.0_rc_r10_pnc_comp_opt                                                                                                                                                                    
[INFO] Determine whether host GPU is available ...                                                                                                                                                          
[INFO] USE_GPU_HOST: 1                                                                                                                                                                                      
[INFO] Start pulling docker image registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest ...                                                                                                                
9.0-latest: Pulling from apollo/apollo-env-gpu                                                                                                                                                              
Digest: sha256:a40252872d2815b0a9e8fae35487e0d04f7131d5b64e7e73c3a3640d845368cc                                                                                                                             
Status: Image is up to date for registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest                                                                                                                      
registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest                                                                                                                                                      
[INFO] Remove existing Apollo Development container ...                                                                                                                                                     
[INFO] Starting Docker container "apollo_neo_dev_9.0.0_rc_r10_pnc_comp" ...  

(... skipped)

Preparing to unpack .../apollo-neo-buildtool_9.0.0-rc1-r14_amd64.deb ...                                                                                                                                    
Unpacking apollo-neo-buildtool (9.0.0-rc1-r14) over (9.0.0-alpha3-r3) ...                                                                                                                                   
Setting up apollo-neo-buildtool (9.0.0-rc1-r14) ... 

(... skipped)

apollo_neo_dev_9.0.0_rc_r10_pnc_comp
```

```
buildtool build -p core

# Output
(... skipped)

WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:                                                    [2/1084]
/apollo_workspace/tools/bazel.rc
Extracting Bazel installation...
Starting local Bazel server and connecting to it...
(10:57:40) INFO: Current date is 2024-04-23
(10:57:56) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (6 packages loaded, 11 targets configured).
(10:57:56) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install_src up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install_src
(10:57:56) INFO: Elapsed time: 19.143s, Critical Path: 0.04s
(10:57:56) INFO: 4 processes: 4 internal.
(10:57:56) INFO: Build completed successfully, 4 total actions
(10:57:56) INFO: Build completed successfully, 4 total actions
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(10:57:56) INFO: Current date is 2024-04-23
(10:57:56) INFO: Analyzed target //dev/buildtool/mock:mock_install (0 packages loaded, 5 targets configured).
(10:57:56) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install
(10:57:56) INFO: Elapsed time: 0.346s, Critical Path: 0.02s
(10:57:56) INFO: 4 processes: 4 internal.
(10:57:56) INFO: Build completed successfully, 4 total actions
(10:57:56) INFO: Build completed successfully, 4 total actions
Installing the project stripped...
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 18:57:57 INFO compilation done!

#需要执行两次
buildtool build -p core

# Output

(... skipped)

[buildtool] 2024-04-23 19:43:48 INFO Preprocess core                                                                                                                                                [5/1574]
[buildtool] 2024-04-23 19:43:48 INFO Using Source of core
[buildtool] 2024-04-23 19:43:49 INFO PostProcess core
[buildtool] 2024-04-23 19:43:49 INFO Compiling whole workspace...
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(11:43:49) INFO: Current date is 2024-04-23
(11:43:50) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (2 packages loaded, 5 targets configured).
(11:43:50) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install_src up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install_src
(11:43:50) INFO: Elapsed time: 0.877s, Critical Path: 0.01s
(11:43:50) INFO: 1 process: 1 internal.
(11:43:50) INFO: Build completed successfully, 1 total action
(11:43:50) INFO: Build completed successfully, 1 total action
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(11:43:50) INFO: Current date is 2024-04-23
(11:43:50) INFO: Analyzed target //dev/buildtool/mock:mock_install (1 packages loaded, 6 targets configured).
(11:43:50) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install
(11:43:50) INFO: Elapsed time: 0.282s, Critical Path: 0.01s
(11:43:50) INFO: 1 process: 1 internal.
(11:43:50) INFO: Build completed successfully, 1 total action
(11:43:50) INFO: Build completed successfully, 1 total action
Installing the project stripped...
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 19:43:50 INFO compilation done!

#下载planning_base
buildtool install planning

```

```
buildtool build

#Output

(... skipped)

[buildtool] 2024-04-23 19:57:21 INFO Preprocess core                                                                                                                                               [24/1835]
[buildtool] 2024-04-23 19:57:21 INFO Using Source of core                                                                                                                                                   
[buildtool] 2024-04-23 19:57:21 INFO PostProcess core                                                                                                                                                       
[buildtool] 2024-04-23 19:57:21 INFO Requiring planning=local, Removing planning=9.0.0-rc-r10                                                                                                               
[buildtool] 2024-04-23 19:57:21 INFO Compiling whole workspace...                                                                                                                                           
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:                                                            
/apollo_workspace/tools/bazel.rc                                                                                                                                                                            
(11:57:21) INFO: Current date is 2024-04-23                                                                                                                                                                 
(11:57:22) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (3 packages loaded, 9 targets configured).                                                                                           
(11:57:22) INFO: Found 1 target...                                                                                                                                                                          
Target //dev/buildtool/mock:mock_install_src up-to-date:                                                                                                                                                    
  bazel-bin/dev/buildtool/mock/mock_install_src                                                                                                                                                             
(11:57:22) INFO: Elapsed time: 0.873s, Critical Path: 0.01s                                                                                                                                                 
(11:57:22) INFO: 4 processes: 4 internal.                                                                                                                                                                   
(11:57:22) INFO: Build completed successfully, 4 total actions                                                                                                                                              
(11:57:22) INFO: Build completed successfully, 4 total actions                                                                                                                                              
[INFO] can not calculate common prefix, install all                                                                                                                                                         
[INFO] can not calculate common prefix, install all                                                                                                                                                         
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:                                                            
/apollo_workspace/tools/bazel.rc                                                                                                                                                                            
(11:57:22) INFO: Current date is 2024-04-23                                                                                                                                                                 
(11:57:27) INFO: Analyzed target //dev/buildtool/mock:mock_install (156 packages loaded, 22048 targets configured).                                                                                         
(11:57:27) INFO: Found 1 target...                                                                                                                                                                          
Target //dev/buildtool/mock:mock_install up-to-date:                                                                                                                                                        
  bazel-bin/dev/buildtool/mock/mock_install
(11:59:44) INFO: Elapsed time: 141.680s, Critical Path: 77.34s
(11:59:44) INFO: 20653 processes: 20505 internal, 148 processwrapper-sandbox.
(11:59:44) INFO: Build completed successfully, 20653 total actions
(11:59:44) INFO: Build completed successfully, 20653 total actions
Installing the project stripped...
-- Installing: /opt/apollo/neo/lib/modules/planning/planning_component/libDO_NOT_IMPORT_planning_component.so
-- Installing: /opt/apollo/neo/lib/modules/planning/planning_component/libplanning_component.so
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/discrete_points_smoother_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/navi_planner_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/planner_open_space_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning.conf
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_navi.conf
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_semantic_map_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/public_road_planner_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/qp_spline_smoother_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/spiral_smoother_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/conf/traffic_rule_config.pb.txt
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning.dag
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning_navi.dag
-- Installing: /opt/apollo/neo/share/modules/planning/planning_component/launch/planning.launch
-- Installing: /opt/apollo/neo/share/packages/planning/cyberfile.xml
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 19:59:44 INFO compilation done!
```

#### Try to fix missing cyber_launch

```
Mine:
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ cat .workspace.json
{
    "repositories" : [
        {"name": "apollo-core", "version": "9.0.0-rc-r10"}
    ]
}
In this link: 
https://apollo.baidu.com/community/article/1159

"apollo-core", "version": "9.0.0-alpha2-r28"


sudo apt  remove apollo-neo-buildtool
Removing apollo-neo-buildtool (9.0.0-rc1-r14) ...


Get:1 https://apollo-pkg-beta.cdn.bcebos.com/apollo/core bionic/main amd64 apollo-neo-buildtool amd64 9.0.0-rc1-r14 [127 kB]                                                                                
Fetched 127 kB in 1s (200 kB/s)                                                                                                                                                                             
Selecting previously unselected package apollo-neo-buildtool.                                                                                                                                               
(Reading database ... 63625 files and directories currently installed.)                                                                                                                                     
Preparing to unpack .../apollo-neo-buildtool_9.0.0-rc1-r14_amd64.deb ...                                                                                                                                    
Unpacking apollo-neo-buildtool (9.0.0-rc1-r14) ...                                                                                                                                                          
Setting up apollo-neo-buildtool (9.0.0-rc1-r14) ... 

buildtool build -p core X 2

[buildtool] 2024-04-23 20:51:55 INFO Preprocess core                                                                                                                                              [532/1993]
[buildtool] 2024-04-23 20:51:55 INFO Using Source of core                                                                                                                                                   
[buildtool] 2024-04-23 20:51:55 INFO PostProcess core                                                                                                                                                       
[buildtool] 2024-04-23 20:51:55 INFO Compiling whole workspace...                                                                                                                                           
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:                                                            
/apollo_workspace/tools/bazel.rc                                                                                                                                                                            
(12:51:55) INFO: Current date is 2024-04-23                                                                                                                                                                 
(12:51:56) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (3 packages loaded, 9 targets configured).                                                                                           
(12:51:56) INFO: Found 1 target...                                                                                                                                                                          
Target //dev/buildtool/mock:mock_install_src up-to-date:                                                                                                                                                    
  bazel-bin/dev/buildtool/mock/mock_install_src                                                                                                                                                             
(12:51:56) INFO: Elapsed time: 1.661s, Critical Path: 0.00s                                                                                                                                                 
(12:51:56) INFO: 1 process: 1 internal.                                                                                                                                                                     
(12:51:56) INFO: Build completed successfully, 1 total action                                                                                                                                               
(12:51:57) INFO: Build completed successfully, 1 total action                                                                                                                                               
[INFO] can not calculate common prefix, install all                                                                                                                                                         
[INFO] can not calculate common prefix, install all                                                                                                                                                         
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:                                                            
/apollo_workspace/tools/bazel.rc                                                                                                                                                                            
(12:51:57) INFO: Current date is 2024-04-23                                                                                                                                                                 
(12:51:59) INFO: Analyzed target //dev/buildtool/mock:mock_install (156 packages loaded, 22048 targets configured).                                                                                         
(12:51:59) INFO: Found 1 target...                                                                                                                                                                          
Target //dev/buildtool/mock:mock_install up-to-date:                                                                                                                                                        
  bazel-bin/dev/buildtool/mock/mock_install                                                                                                                                                                 
(12:52:03) INFO: Elapsed time: 5.952s, Critical Path: 2.68s                                                                                                                                                 
(12:52:03) INFO: 6 processes: 4 internal, 2 processwrapper-sandbox.
(12:52:03) INFO: Build completed successfully, 6 total actions
(12:52:03) INFO: Build completed successfully, 6 total actions
Installing the project stripped...
-- Installing: /opt/apollo/neo/lib/modules/planning/planning_component/libDO_NOT_IMPORT_planning_component.so
-- Installing: /opt/apollo/neo/lib/modules/planning/planning_component/libplanning_component.so
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/discrete_points_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/navi_planner_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planner_open_space_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning.conf
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_navi.conf
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_semantic_map_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/public_road_planner_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/qp_spline_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/spiral_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/traffic_rule_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning.dag
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning_navi.dag
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/launch/planning.launch
-- Installing: /opt/apollo/neo/share/packages/planning/cyberfile.xml
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 20:52:03 INFO compilation done!
(apollo-9.0)[sirius@in-dev-docker:/apollo_workspace]$ buildtool build -p core

(... skipped)

[buildtool] 2024-04-23 20:52:51 INFO Preprocess core                                                                                                                                                        
[buildtool] 2024-04-23 20:52:51 INFO Using Source of core                                                                                                                                                   
[buildtool] 2024-04-23 20:52:51 INFO PostProcess core
[buildtool] 2024-04-23 20:52:51 INFO Compiling whole workspace...
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(12:52:52) INFO: Current date is 2024-04-23
(12:52:52) INFO: Analyzed target //dev/buildtool/mock:mock_install_src (3 packages loaded, 9 targets configured).
(12:52:52) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install_src up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install_src
(12:52:53) INFO: Elapsed time: 1.535s, Critical Path: 0.00s
(12:52:53) INFO: 1 process: 1 internal.
(12:52:53) INFO: Build completed successfully, 1 total action
(12:52:53) INFO: Build completed successfully, 1 total action
[INFO] can not calculate common prefix, install all
[INFO] can not calculate common prefix, install all
WARNING: The following rc files are no longer being read, please transfer their contents or import their path into one of the standard rc files:
/apollo_workspace/tools/bazel.rc
(12:52:54) INFO: Current date is 2024-04-23
(12:52:55) INFO: Analyzed target //dev/buildtool/mock:mock_install (156 packages loaded, 22048 targets configured).
(12:52:55) INFO: Found 1 target...
Target //dev/buildtool/mock:mock_install up-to-date:
  bazel-bin/dev/buildtool/mock/mock_install
(12:52:56) INFO: Elapsed time: 2.923s, Critical Path: 0.07s
(12:52:56) INFO: 1 process: 1 internal.
(12:52:56) INFO: Build completed successfully, 1 total action
(12:52:56) INFO: Build completed successfully, 1 total action
Installing the project stripped...
-- Up-to-date: /opt/apollo/neo/lib/modules/planning/planning_component/libDO_NOT_IMPORT_planning_component.so
-- Up-to-date: /opt/apollo/neo/lib/modules/planning/planning_component/libplanning_component.so
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/discrete_points_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/navi_planner_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planner_open_space_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning.conf
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_navi.conf
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/planning_semantic_map_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/public_road_planner_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/qp_spline_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/spiral_smoother_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/conf/traffic_rule_config.pb.txt
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning.dag
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/dag/planning_navi.dag
-- Up-to-date: /opt/apollo/neo/share/modules/planning/planning_component/launch/planning.launch
-- Installing: /opt/apollo/neo/share/packages/planning/cyberfile.xml
-- Installing: /opt/apollo/neo/share/packages/core/cyberfile.xml
[buildtool] 2024-04-23 20:52:57 INFO compilation done!

# Conclutions
Did remove apollo-neo-buildtool, and rebuild core X 2, same error, didn't work;
```

#### Try cpu only
application-pnc$ cat .env
change apollo-env-gpu to apollo-env-cpu
```
sudo aem start_cpu

# Output
Status: Downloaded newer image for registry.baidubce.com/apollo/apollo-env-cpu:9.0-latest
registry.baidubce.com/apollo/apollo-env-cpu:9.0-latest
[ OK ] apollo_neo_dev_9.0.0_rc_r10_pnc_comp is still running, please run the following command:
[ OK ]     aem enter
[ OK ] Enjoy!

aem list

sirius@sirius-ThinkPad-X1-Extreme:~/workspace/apollo_9.0/application-pnc$ sudo aem list
[INFO] Environment containers:
apollo_neo_dev_9.0.0_rc_r10_pnc_comp /home/sirius/workspace/apollo_9.0/application-pnc/.aem
apollo_neo_dev_9.0.0_rc_r10_core /home/sirius/workspace/apollo_9.0/application-core/.aem
apollo_neo_dev_root
[INFO] Query new version of aem...
sirius@sirius-ThinkPad-X1-Extreme:~/

seems like the GPU version got destroyed;

sudo aem enter
```

#### Solution to everything
sudo chown sirius:sirius -R /opt/apollo/neo/data/log

```
# !!! Please don't use sudo
aem bootstrap start --plus
```

#### Routine
```
sudo aem start_gpu
sudo aem enter

# 1st time only
buildtool build -p core
buildtool build -p core
buildtool map get xh_2024_contest
buildtool map list

buildtool install planning

# launch DV
sudo chown sirius:sirius -R /opt/apollo/neo/data/log
aem bootstrap start --plus

```

#### Install Profiler
[Install profiler](https://apollo.baidu.com/community/article/1031)


#### pnc gpu too short broken so fix
```
Removing apollo-neo-buildtool (9.0.0-rc1-r14) ...                                                                                                                                                           
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/pkg_maker/generator' not empty so not removed                                               
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/pkg_maker/common' not empty so not removed                                                  
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/pkg_maker/action' not empty so not removed                                                  
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/version_decide/semver' not empty so not removed                                        
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/version_decide/mixology' not empty so not removed                                      
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/version_decide/cyberfile' not empty so not removed                                     
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/task/bazel/handler' not empty so not removed                                           
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/package_identification' not empty so not removed                                       
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/pack_lib/lib' not empty so not removed                                                 
dpkg: warning: while removing apollo-neo-buildtool, directory '/opt/apollo/neo/packages/buildtool/9.0.0-rc1-r14/core/action' not empty so not removed                                                       
Reading package lists... Done                                                                                                                                                                               
Building dependency tree                                                                                                                                                                                    
Reading state information... Done                                                                                                                                                                           
The following package was automatically installed and is no longer required:                                                                                                                                
  libsqlite3-dev                                                                                                                                                                                            
Use 'sudo apt autoremove' to remove it.                                                                                                                                                                     
The following NEW packages will be installed:                                                                                                                                                               
  apollo-neo-buildtool                                                                                                                                                                                      
0 upgraded, 1 newly installed, 0 to remove and 70 not upgraded.
Need to get 127 kB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://apollo-pkg-beta.cdn.bcebos.com/apollo/core bionic/main amd64 apollo-neo-buildtool amd64 9.0.0-rc1-r14 [127 kB]
Fetched 127 kB in 0s (455 kB/s)                
Selecting previously unselected package apollo-neo-buildtool.
(Reading database ... 63625 files and directories currently installed.)
Preparing to unpack .../apollo-neo-buildtool_9.0.0-rc1-r14_amd64.deb ...
Unpacking apollo-neo-buildtool (9.0.0-rc1-r14) ...
Setting up apollo-neo-buildtool (9.0.0-rc1-r14) ...
[INFO] start to create symbolic links of buildtool
[WARN] the links of pre-version will be overwrited!
[INFO] symbolic links of buildtool created.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libSM.so.6.0.1 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libICE.so is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libXt.so.6.0.0 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libx265.so is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libXt.so.6 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libnuma.so.1 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libSM.so.6 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libqhull.so.7 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libICE.so.6.3.0 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libICE.so.6 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libqhull.so.7.2.0 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libnuma.so is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libSM.so is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libx265.so.146 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libnuma.so.1.0.0 is empty, not checked.
/sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libXt.so is empty, not checked.

(...) broken, buildtool build -p core failed, seems like files stored on disk got corrupted;

fix: remove all pnc folders, and start clean;

```

### New era application-pnc-gpu
```
sirius@sirius-ThinkPad-X1-Extreme:~/workspace/apollo_9.0/application-pnc$ sudo aem start_gpu
apollo_neo_dev_9.0.0_rc_r10_pnc_comp_apollo
apollo_neo_dev_9.0.0_rc_r10_pnc_comp_opt
[INFO] Determine whether host GPU is available ...
[INFO] USE_GPU_HOST: 1
[INFO] Start pulling docker image registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest ...
9.0-latest: Pulling from apollo/apollo-env-gpu
Digest: sha256:a40252872d2815b0a9e8fae35487e0d04f7131d5b64e7e73c3a3640d845368cc
Status: Image is up to date for registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest
registry.baidubce.com/apollo/apollo-env-gpu:9.0-latest
[INFO] Remove existing Apollo Development container ...
[INFO] Starting Docker container "apollo_neo_dev_9.0.0_rc_r10_pnc_comp" ...
```

