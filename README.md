# 【合集】常用 VPS 脚本备忘清单｜12 类 · 60+ 条命令

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/91milk/vps-scripts?style=social)](https://github.com/91milk/vps-scripts)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Debian%20%7C%20Ubuntu%20%7C%20CentOS-green.svg)]()
[![NodeSeek](https://img.shields.io/badge/source-NodeSeek%20%7C%20Community-orange.svg)](https://www.nodeseek.com/)

> ⚠️ **先说风险（必读）**：
> 1. 本文整理收录的几乎全为第三方托管的 `curl | bash` 或 `wget | bash` 一键式自动化脚本。**执行前请务必仔细阅读对应仓库源码**。
> 2. **切勿直接在生产环境或存有重要数据的机器上运行测试脚本**！
> 3. **DD 重装脚本会彻底格式化并清空目标磁盘**，请在操作前务必做好数据异地备份。
> 4. 部分测速、网络回程和性能基准测试脚本会大量消耗 CPU 资源或网络出入站流量，流量计费型 VPS 请注意限额。

---

## 📑 目录导航（按场景速查）

- [【一】DD 重装系统脚本](#一dd-重装系统脚本)
- [【二】综合性能测试脚本](#二综合性能测试脚本)
- [【三】CPU 与算力性能测试](#三cpu-与算力性能测试)
- [【四】流媒体解锁及 IP 质量测试](#四流媒体解锁及-ip-质量测试)
- [【五】网络测速脚本](#五网络测速脚本)
- [【六】回程路由测试](#六回程路由测试)
- [【七】网络优化与系统功能脚本](#七网络优化与系统功能脚本)
- [【八】常用环境与服务一键安装](#八常用环境与服务一键安装)
- [【九】多功能综合工具箱](#九多功能综合工具箱)
- [【十】实用工具与拓展推荐](#十实用工具与拓展推荐)
- [【十一】VPS 常备实用运维命令（非脚本）](#十一vps-常备实用运维命令非脚本)
- [【十二】独立服务器（杜甫）专用检测与重装](#十二独立服务器杜甫专用检测与重装)

---

## 【一】DD 重装系统脚本

适合需要纯净 Linux 系统或官方镜像被魔改/限制时使用。**执行会抹除全盘数据！**

### 1. 史上最强 DD 脚本（LeitboGi0ro 出品）
支持自动识别网络配置、跨架构、支持 IPv4/IPv6 双栈、支持指定镜像源与自定义密码：
```bash
wget --no-check-certificate -qO InstallNET.sh 'https://raw.githubusercontent.com/leitbogioro/Tools/master/Linux_reinstall/InstallNET.sh' && chmod a+x InstallNET.sh && bash InstallNET.sh -debian 12 -pwd '你的密码'
```

### 2. 萌咖大佬的经典重装脚本（MoeClub）
支持 Debian/Ubuntu/CentOS 一键重装，自带固件支持：
```bash
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 11 -v 64 -p 你的密码 -port 22 -a -firmware
```

### 3. beta.gs 大佬一键重装脚本
全自动跨平台重装工具：
```bash
wget --no-check-certificate -O NewReinstall.sh https://raw.githubusercontent.com/fcurrk/reinstall/master/NewReinstall.sh && chmod a+x NewReinstall.sh && bash NewReinstall.sh
```

### 4. DD Windows 10（使用 LeitboGi0ro 脚本）
一键将 Linux VPS DD 为 Windows 10 中文精简版：
```bash
bash <(curl -sSL https://raw.githubusercontent.com/leitbogioro/Tools/master/Linux_reinstall/InstallNET.sh) -windows 10 -lang "cn"
```
- **默认账户**：`Administrator`
- **默认密码**：`Teddysun.com`

> **Windows 快速激活**：进入 Windows 后使用快捷键 `Win + R` 打开运行框，输入 `powershell` 回车，执行以下命令即可一键激活：
> ```powershell
> irm https://get.activated.win | iex
> ```

---

## 【二】综合测试脚本

快速获取服务器基础配置（CPU型号、核心、主频、内存、磁盘IO、三网测速等）。

### 1. bench.sh（经典秋水逸冰）
最基础、快速展示 CPU、内存、硬盘 IO 以及各节点下载速度：
```bash
wget -qO- bench.sh | bash
```

### 2. LemonBench（柠檬测试·快速模式）
包含硬件信息检测、内存与硬盘读写、宽带吞吐、国内节点多线程/单线程测速：
```bash
wget -qO- https://raw.githubusercontent.com/LemonBench/LemonBench/main/LemonBench.sh | bash -s -- --fast
```

### 3. 融合怪测评脚本（ecs.sh · 功能最全面）
集基础信息、流媒体解锁、IP 质量、三网回程、CPU 跑分（GB5/GB6）、硬盘 I/O 读写测试于一体：
```bash
bash <(wget -qO- --no-check-certificate https://gitlab.com/spiritysdx/za/-/raw/main/ecs.sh)
```

### 4. NodeBench
轻量简洁的 VPS 基准测试脚本：
```bash
bash <(curl -sL https://raw.githubusercontent.com/LloydAsp/NodeBench/main/NodeBench.sh)
```

---

## 【三】CPU 与算力性能测试

专门测试处理器性能（Geekbench 5 / Geekbench 6）与磁盘读写。

### 1. YABS（Yet Another Bench Script）完整测试
默认运行全套测试（系统信息、fio 磁盘读写、iperf3 网络测速、Geekbench 跑分）：
```bash
curl -sL yabs.sh | bash
```

### 2. YABS 跳过网络测速，测 GB5
避免由于网络测速节点失效或消耗大量流量，专注于 CPU GB5 跑分：
```bash
curl -sL yabs.sh | bash -s -- -i5
```

### 3. YABS 跳过网络和磁盘测速，测 GB5
纯测试 CPU 性能，耗时最短：
```bash
curl -sL yabs.sh | bash -s -- -if5
```

### 4. YABS 改测 GB5 不测 GB6
```bash
curl -sL yabs.sh | bash -s -- -5
```

---

## 【四】流媒体解锁及 IP 质量测试

用于评估 VPS 节点访问各大流媒体平台的连通性以及 IP 风险值（欺诈值、送中情况等）。

### 1. 流媒体解锁检测（最常用版本）
```bash
bash <(curl -L -s check.unlock.media)
```

### 2. 原生流媒体解锁检测（Media.Check.Place）
支持 IPv4/IPv6 双栈检测主流视频与音乐平台解锁：
```bash
bash <(curl -sL Media.Check.Place)
```

### 3. TQ（TcpQuality 网络与流媒体质量检测）
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/ibsgss/TcpQuality/main/runTcpQuality.sh)
```

### 4. RegionRestrictionCheck（准确度最高）
1-stream 出品的区域限制流媒体全面核验工具：
```bash
bash <(curl -L -s https://github.com/1-stream/RegionRestrictionCheck/raw/main/check.sh)
```

### 5. IP 质量体检脚本（IP.Check.Place）
检测 IP 欺诈度（Scamalytics / ipqualityscore）、原生/广播 IP 属性、邮箱黑名单、Google 是否送中等：
```bash
bash <(curl -sL IP.Check.Place)
```

### 6. 一键修改解锁 DNS（DNS-Alice-Unlock）
用于分流配置第三方解锁 DNS 服务：
```bash
wget https://raw.githubusercontent.com/Jimmyzxk/DNS-Alice-Unlock/refs/heads/main/dns-unlock.sh && bash dns-unlock.sh
```

### 7. BBR v3 一键优化脚本
安装优化别名并在系统中启用高效拥塞控制算法：
```bash
# 1. 安装别名与脚本
bash <(curl -fsSL "https://raw.githubusercontent.com/Eric86777/vps-tcp-tune/main/install-alias.sh?$(date +%s)")

# 2. 重新加载环境配置
source ~/.bashrc  # 若使用 zsh 则执行: source ~/.zshrc

# 3. 以后直接键入命令使用
bbr
```

---

## 【五】网络测速脚本

### 1. Speedtest 节点测速（bash.icu）
```bash
bash <(curl -sL bash.icu/speedtest)
```

### 2. Taier 测速
```bash
bash <(curl -sL res.yserver.ink/taier.sh)
```

### 3. hyperspeed 三网快速测速
支持电信、联通、移动多节点单线程/多线程测速：
```bash
bash <(curl -Lso- https://bench.im/hyperspeed)
```

### 4. 全球网络综合测速（nws.sh）
- **全球测速**：
  ```bash
  wget -qO- nws.sh | bash
  ```
- **指定区域速度测试**：
  ```bash
  wget -qO- nws.sh | bash -s -- -r region_name
  ```
- **Ping 和路由测试**：
  ```bash
  wget -qO- nws.sh | bash -s -- -rt [region]
  ```

---

## 【六】回程路由测试

测定数据包从 VPS 返回中国三大运营商（电信/联通/移动）网络的路径（普通163/4837/CMI，或 CN2 GIA/9929/AS58807 等）。

### 1. 直接显示四网回程（小白首选 · backtrace）
快速识别电信、联通、移动、教育网的回程路由线路：
```bash
curl https://raw.githubusercontent.com/ludashi2020/backtrace/main/install.sh -sSf | sh
```

### 2. AutoTrace 回程详细测试（推荐）
提供详尽的每一跳路由跟踪节点：
```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/Chennhaoo/Shell_Bash/master/AutoTrace.sh && chmod +x AutoTrace.sh && bash AutoTrace.sh
```

### 3. testrace 详细测试
```bash
wget https://ghproxy.com/https://raw.githubusercontent.com/vpsxb/testrace/main/testrace.sh -O testrace.sh && bash testrace.sh
```

---

## 【七】网络优化与系统功能脚本

### 1. 一键添加 SWAP 虚拟内存
防止因小内存 VPS 爆内存（OOM）导致程序崩溃：
```bash
wget https://www.moerats.com/usr/shell/swap.sh && bash swap.sh
```

### 2. 安装 Fail2ban 防暴力破解
自动封禁恶意爆破 SSH 密码的黑客 IP：
```bash
wget --no-check-certificate https://raw.githubusercontent.com/FunctionClub/Fail2ban/master/fail2ban.sh && bash fail2ban.sh 2>&1 | tee fail2ban.log
```

### 3. 系统原生开启 BBR（适用于较新的 Debian / Ubuntu）
现代 Linux 内核自带 BBR 模块，免装第三方内核即可开启：
```bash
# 写入配置
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf

# 生效并验证
sysctl -p
sysctl net.ipv4.tcp_available_congestion_control
lsmod | grep bbr
```

### 4. 多功能 BBR 安装脚本（zeruns）
```bash
wget -N --no-check-certificate "https://gist.github.com/zeruns/a0ec603f20d1b86de6a774a8ba27588f/raw/4f9957ae23f5efb2bb7c57a198ae2cffebfb1c56/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

### 5. 锐速 / BBRPLUS / BBR2 / BBR3 内核管理脚本（ylx2016）
支持更换各类针对高丢包、长延迟链路优化定制的加速内核：
```bash
wget -O tcpx.sh "https://github.com/ylx2016/Linux-NetSpeed/raw/master/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh
```

### 6. TCP 窗口调优
```bash
wget http://sh.nekoneko.cloud/tools.sh -O tools.sh && bash tools.sh
```

### 7. Cloudflare WARP 一键脚本（fscarmen）
为 IPv4-only 添加 IPv6，或为 IPv6-only 添加 IPv4 出口，或解锁奈飞等流媒体：
```bash
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh [option] [lisence/url/token]
```

### 8. 测试 VPS 是否开放 25 端口（邮件端口）
```bash
telnet smtp.aol.com 25
```
*(若能成功连接，说明 25 端口出站未被云服务商拦截)*

---

## 【八】常用环境与服务一键安装

### 1. Docker & Docker Compose 官方安装
```bash
bash <(curl -sL 'https://get.docker.com')
```

### 2. Python 多版本编译与管理
```bash
curl -O https://raw.githubusercontent.com/lx969788249/lxspacepy/master/pyinstall.sh && chmod +x pyinstall.sh && ./pyinstall.sh
```

### 3. iperf3 网络吞吐测速工具
```bash
# Debian / Ubuntu
apt update && apt install -y iperf3

# CentOS / RHEL
yum install -y epel-release && yum install -y iperf3
```

### 4. Realm 高性能端口转发
轻量、低占用的一键端口转发工具：
```bash
bash <(curl -L https://raw.githubusercontent.com/zhouh047/realm-oneclick-install/main/realm.sh) -i
```

### 5. Gost 多功能安全隧道
```bash
wget --no-check-certificate -O gost.sh https://raw.githubusercontent.com/qqrrooty/EZgost/main/gost.sh && chmod +x gost.sh && ./gost.sh
```

### 6. 极光面板（Aurora Admin Panel）
图形化端口流量与中转管理面板：
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Aurora-Admin-Panel/deploy/main/install.sh)
```

### 7. 哪吒监控（Nezha Monitoring）
- **客户端/服务端一键安装**：
  ```bash
  curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh -o nezha.sh && chmod +x nezha.sh && sudo ./nezha.sh
  ```
- **后台美化扩展自定义样式脚本**：
  ```html
  <script>
  window.ShowNetTransfer = true;
  window.FixedTopServerName = true;
  window.DisableAnimatedMan = true;
  </script>
  ```

### 8. Cloudflare WARP 菜单模式
```bash
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh
```

### 9. Aria2 多线程下载工具
```bash
wget -N git.io/aria2.sh && chmod +x aria2.sh && ./aria2.sh
```

### 10. 宝塔 Linux 面板安装（Ubuntu/Debian）
```bash
wget -O install.sh http://v7.hostcli.com/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

### 11. PVE（Proxmox VE）虚拟化环境
将独立服务器快速开小鸡/部署虚拟机：
```bash
bash <(wget -qO- --no-check-certificate https://raw.githubusercontent.com/oneclickvirt/pve/main/scripts/build_backend.sh)
```

### 12. Argox 容器平台
```bash
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/argox/main/argox.sh)
```

---

## 【九】多功能综合工具箱

集成了环境安装、系统维护、网络调优、面板管理的懒人集合工具箱。

### 1. 科技 lion 常用运维工具箱
```bash
apt update -y && apt install -y curl
bash <(curl -sL kejilion.sh)
```

### 2. SKY-BOX 综合功能工具箱（蓝天XN）
```bash
wget -O box.sh https://raw.githubusercontent.com/BlueSkyXN/SKY-BOX/main/box.sh && chmod +x box.sh && clear && ./box.sh
```

---

## 【十】实用工具与拓展推荐

### 1. Telegram 中文语言包汉化
点击一键应用官方语言包：[https://t.me/setlanguage/classic-zh-cn](https://t.me/setlanguage/classic-zh-cn)

### 2. Google IP 送中问题申诉
若 VPS 节点的原生 IP 被 Google 错误标记为中国大陆导致 Gemini、YouTube Premium 异常，可前往 Google 官方帮助中心提交 IP 归属报告申诉：
- [Google IP 问题报告中心](https://support.google.com/websearch/workflow/9308722)

### 3. Linux TCP 网络高级调优指南
- 常见参数：`tcp_tw_reuse`, `tcp_fin_timeout`, `tcp_max_syn_backlog`, `tcp_rmem`, `tcp_wmem` 等内核网络参数微调。

### 4. Awesome Docker 常用容器集合
- [awesome-docker (GitHub)](https://github.com/veggiemonk/awesome-docker)

---

## 【十一】VPS 常备实用运维命令（非脚本）

> 来源于社区交流分享：[NodeSeek 实用 VPS 命令集帖](https://www.nodeseek.com/post-424648-1)

### 1. 查看系统资源占用
```bash
# 内存占用详情（友好阅读单位）
free -h

# 磁盘剩余空间及挂载点
df -h

# 查看系统当前负载及运行时间
uptime

# 实时进程监控（推荐安装 htop）
top
```

### 2. 查看端口占用与网络连接
```bash
# 查看所有监听中的 TCP/UDP 端口
ss -tulpn

# 或使用 netstat
netstat -tunlp

# 实时查看网络流量（需安装 iftop / nload）
iftop
```

### 3. 查看公网 IP 信息
```bash
# 查看本地出口 IPv4
curl -4 ip.sb

# 查看本地出口 IPv6
curl -6 ip.sb
```

---

## 【十二】独立服务器（杜甫）专用检测与重装

独立物理服务器专属的硬件健康诊断（硬盘通电时间、通电次数、坏道、RAID 等）及针对性 DD 系统命令。

### 1. 独立服务器硬件与健康检测
```bash
# SICK 综合健康检查
curl -sL https://sick.onl | bash

# Aniverse 杜甫综合测试
wget https://github.com/Aniverse/A/raw/i/a && bash a

# nws 测速
wget -qO- nws.sh | bash

# SICK 硬件信息检测（中文输出）
curl -sL https://raw.githubusercontent.com/Yuri-NagaSaki/SICK/refs/heads/main/hardware_info.sh | bash -s -- -cn
```

### 2. 独立服务器高级 DD 重装系统（基于 LeitboGi0ro 脚本）
```bash
# 1. 提前下载安装脚本
wget --no-check-certificate -qO InstallNET.sh 'https://raw.githubusercontent.com/leitbogioro/Tools/master/Linux_reinstall/InstallNET.sh' && chmod a+x InstallNET.sh

# 2. 基础 DD 重装 Debian 12
bash InstallNET.sh -debian 12

# 3. 杜甫指定组建软 RAID 0 进行 DD
bash InstallNET.sh -debian 12 -raid "0"

# 4. 杜甫指定静态网络参数 DD（防止重装后 DHCP 失败失联）
bash InstallNET.sh -debian 12 --ip-addr 139.162.52.1 --ip-mask 24 --ip-gate 139.162.52.1 --ip6-addr 2a07:e040:2:1d3::1 --ip6-gate 2a07:e040::1 --ip6-mask 32

# 5. 指定 root 密码重装
bash InstallNET.sh -debian 12 -pwd '你的自定义密码'
```

### 3. 禁用 IPv6 / 恢复 IPv6
某些网络环境下 IPv6 连通质量较差（或为了避免优先走 IPv6 出现卡顿），可手动禁用：

- **一键禁用 IPv6**：
  ```bash
  # 向配置文件写入禁用 IPv6 的规则
  echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
  echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf
  echo "net.ipv6.conf.lo.disable_ipv6 = 1" >> /etc/sysctl.conf

  # 立即重新加载 sysctl 配置生效
  sysctl -p
  ```

- **恢复启用 IPv6**：
  ```bash
  # 从 /etc/sysctl.conf 中移除 disable_ipv6 项后执行：
  sed -i '/disable_ipv6/d' /etc/sysctl.conf
  sysctl -p
  ```

---

## ⚖️ 免责声明与许可证

1. 本项目所收录的脚本均由开源社区或第三方开发者开发维护，脚本版权归原作者所有。
2. 使用前请自行甄别脚本安全性，本项目整理者不对任何脚本造成的服务器宕机、数据丢失或网络中断承担连带责任。
3. 遵循 [MIT License](LICENSE) 开源协议。
