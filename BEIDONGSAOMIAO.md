网络空间测绘引擎与子域名收集学习
 一、和 ZoomEye（钟馗之眼）功能类似的网络空间搜索引擎
ZoomEye（钟馗之眼，知道创宇）属于网络空间测绘搜索引擎，用来扫描全网联网设备、Web站点、开放端口、服务指纹、IoT设备等资产。同类主流引擎如下：

1. *OFA（白帽汇，国内最常用）
国内网络资产测绘引擎，对国内IP、工控设备、Web指纹识别能力很强，语法和ZoomEye接近，适合国内资产测绘。
2. Shodan（国外老牌）
全球最早的空间测绘引擎，侧重主机banner、端口、设备信息，全球IoT、路由、摄像头资产收录量大。
3. Censys
擅长证书检索、TLS证书关联资产，适合通过SSL证书关联域名、主机，证书情报是它的特色。
4. Netlas
新兴测绘引擎，扫描速度快，协议覆盖广，免费额度友好。
5. Criminal IP
韩国的测绘+威胁情报结合平台，除资产检索外附带恶意IP情报。

简单对比：
ZoomEye / FOFA 更适合国内资产；Shodan、Censys适合海外资产、证书情报。

二、ZoomEye 搜索实操说明
ZoomEye 支持自定义语法检索资产，示例检索语句：
domain:"(edu.cn)"
含义：检索后缀为edu.cn的教育网域名相关联网资产。
平台返回资产IP、域名、开放端口、协议、地理位置、HTTP头、证书、哈希等测绘信息。

![ZoomEye搜索edu.cn结果](./img/zoomeye-search-edu.png)

三、子域名收集方法
方式1：ZoomEye EASM攻击面管理平台收集
1. 进入 ZoomEye EASM：https://easm.zoomeye.org/
2. 左侧菜单【资产管理】→【子域名】
3. 点击【添加资产】，填入目标主域名
4. 平台自动通过DNS记录、CT证书、公开情报被动挖掘子域名
5. 任务完成后展示子域名、解析IP、ICP备案、地理位置，支持导出资产

特点：自动化被动测绘，不需要本地发包；仅针对你添加的指定域名持续监控。

方式2：其他被动收集手段
1. crt.sh：查询SSL证书透明度日志，提取证书绑定的全部子域名
2. VirusTotal / SecurityTrails：查询历史DNS解析记录
3. 搜索引擎语法：`site:xxx.edu.cn -www`

方式3：本地工具收集（Kali）
Subfinder：被动子域名枚举，速度快
bash
subfinder -d example.com
Amass：OWASP 官方工具，被动 + 验证
OneForAll：集成多数据源，国内使用广泛
Gobuster：DNS 字典爆破（⚠️ 爆破必须获得目标授权）
网络空间测绘引擎可以快速获取互联网暴露资产信息；子域名收集属于渗透测试信息收集阶段，优先选择被动收集方案，在不主动向目标发包的前提下获取资产，规避风险。未经授权不得对任意目标进行主动扫描、爆破
[ZoomEye搜索edu.cn结果](./picture1.png)

