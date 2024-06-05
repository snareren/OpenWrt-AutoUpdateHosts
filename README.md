# OpenWrt-AutoUpdateHosts  

## 脚本功能
在 OpenWrt 下实现一键合并广告拦截规则   
脚本采用的上游规则为[秋风广告规则](https://github.com/TG-Twilight/AWAvenue-Ads-Rule)


## 使用方法  
### 一键安装  
SSH 登录 OpenWrt，运行以下命令即可执行一键安装脚本（脚本下载链接已经过 GitHub Proxy 代理加速）  
```bash
curl -sSL https://mirror.ghproxy.com/https://raw.githubusercontent.com/snareren/OpenWrt-AutoUpdateHosts/main/install.sh | sh
```
一键安装脚本运行时会依次执行以下功能：  
1. 改写 dnsmasq 设置，取消忽略 hosts 的选项  
2. 下载更新脚本 autoupdatehosts.sh 至 /etc/autoupdatehosts 目录下并赋予相应的权限  
3. 在计划任务中设置每日凌晨 4:30 分运行更新脚本  
4. 运行一次更新脚本。  

更新脚本运行时会依次执行以下功能：  
1. 检查 hosts 文件中是否存在过去由此脚本添加的规则并清除  
2. 下载最新的[秋风广告规则](https://github.com/TG-Twilight/AWAvenue-Ads-Rule)并合并至 /etc/hosts 文件
3. 重启 Dnsmasq 使 hosts 文件生效  

**脚本不会破坏 hosts 文件内的原始内容以及人为手动添加的其他内容，不会重复添加内容，请放心食用**  
**如果需要人为添加其他 hosts 条目，请直接添加在 hosts 文件内容的尾部，不要添加在 start 与 end 注释之间**  

更新脚本每次运行完后，若检测到安装了 OpenClash 会自动重启 OpenClash（OpenClash 会重启 Dnsmasq），若未安装 OpenClash 则会直接重启 Dnsmasq。  

## 感谢  
- [Aethersailor/OpenWrt-AutoUpdateHosts](https://github.com/Aethersailor/OpenWrt-AutoUpdateHosts)
- [TG-Twilight/AWAvenue-Ads-Rule](https://github.com/TG-Twilight/AWAvenue-Ads-Rule)  
- [521xueweihan/GitHub520](https://github.com/521xueweihan/GitHub520)  
