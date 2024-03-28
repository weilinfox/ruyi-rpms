# Ruyi RPM

## 概述

这是 RUYI 包管理基于 openEuler 23.09 的 RPM 包构建。由于 RUYI 的部分 python3 依赖包版本较高，需要重新打包。

该软件源包含从 0.4.0 开始的 Release 版本。

## 软件源添加

注意该软件源只适用于 openEuler RISC-V 23.09 的独立发行版本，并不适用于 openEuler 上游发布的 RISC-V 23.09 创新版本。

暂时使用了个人 Gitee 仓库和 GitHub 仓库进行了托管

+ Gitee 仓库 <https://gitee.com/weilinfox/ruyi-rpms/>
+ GitHub 仓库 <https://github.com/weilinfox/ruyi-rpms/>

以 Gitee 仓库为例，在 ``/etc/yum.repos.d/ruyi.repo`` 添加如下内容：

```
[ruyi]
name=ruyi
baseurl=https://gitee.com/weilinfox/ruyi-rpms/raw/dev/openEuler-RISC-V/23.09/
enabled=1
gpgcheck=0
```

更新软件包：

```bash
$ sudo dnf update
```

## 安装 RUYI 包管理

由于 RUYI 包管理使用 python 编写，其包名为 python3-ruyi ：

```bash
sudo dnf install python3-ruyi
```

## 完整安装脚本

```bash
#!/usr/bin/bash

if [ $UID -gt 0 ]; then
  echo Please run as root
  exit 1
fi

cat > /etc/yum.repos.d/ruyi.repo << EOF
[ruyi]
name=ruyi
baseurl=https://gitee.com/weilinfox/ruyi-rpms/raw/dev/openEuler-RISC-V/23.09/
enabled=1
gpgcheck=0
EOF

dnf update
dnf install -y python3-ruyi
```

