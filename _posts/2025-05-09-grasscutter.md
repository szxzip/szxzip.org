---
layout: post
category: twaddle_tales
title: Genshin Impact v5.3 Grasscutter & 3dmigoto
---

--- 部署Grasscutter服务器 ---

1. 安装MongoDB、jdk17、nodejs、mitmproxy、python；

2. 启动MongoDB：
   ```
   sudo systemctl enable --now mongodb
   ```

3. 克隆<https://github.com/Kei-Luna/LunaGC_5.3.0>到本地，并按照readme进行编译；

4. 克隆<https://github.com/pmagixc/5.3-res>，重命名为 resources 并移动到 LunaGC_5.3.0 根目录；

5. 若 LunaGC_5.3.0 无 proxy.py、proxy_config.py，须自行寻找下载（<https://github.com/Grasscutters/Grasscutter>的先前提交中可找到这些文件）；

6. 启动Grasscutter：
   ```
   cd /path/to/grasscutter
   mitmdump -s proxy.py -k --set block_global=false & \
   sudo /usr/lib/jvm/java-17-openjdk/bin/java -jar grasscutter.jar
   ```

--- 本地游玩 ---

1. 安装Lutris；

2. 下载5.3数据包，并用 LunaGC_5.3.0/patch/Astrolabe.dll 覆盖5.3数据包中 GenshinImpact_Data/Plugins/Astrolabe.dll；

3. 启动Lutris，修改Wine设置，在环境变量中添加：
   ```
   http_proxy = http://localhost:8080
   https_proxy = http://localhost:8080
   ```
   
4. 添加游戏。

--- 自定义Mod ---

1. 安装ProtonPlus；

2. 使用ProtonPlus，为Lutris安装Wine-Staging-Tkg；

3. 修改Lutris设置：启用高级选项；Wine版本改为Wine-Staging-Tkg；关闭VKD3D、DXVK-NVAPI/DLSS；关闭AMD FSR、两个反作弊；启用Output debugging info；

4. 从<https://github.com/SilentNightSound/GI-Model-Importer>下载GIMI最新版本；

5. 新建launch.bat:
   ```
   cd C:\path\to\3dmigoto\
   start "" "3DMigoto Loader.exe"

   cd C:\path\to\GenshinImpact\
   start "" "GenshinImpact.exe"
   ```
   
6. 修改游戏配置文件，相关条目改为 /path/to/launch.bat ；

7. Mod统一放在 3dmigoto-gimi/Mods/ ，游戏中可按 F1 查看3dmigoto使用帮助。
