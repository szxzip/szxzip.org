---
layout: post
category: y
title: Genshin Impact v5.3 Grasscutter & 3DMigoto
---

---
{: data-content=" 部署本地服务器 "}

1. 安装MongoDB、jdk17、nodejs、mitmproxy、python；

2. 启动MongoDB：
   ```
   $ sudo systemctl enable --now mongodb
   ```

3. 克隆[Kei-Luna/LunaGC_5.3.0](https://github.com/Kei-Luna/LunaGC_5.3.0)到本地，并编译：
   ```
   $ chmod +x gradlew
   $ ./gradlew jar
   ```

4. 克隆[pmagixc/5.3-res](https://github.com/pmagixc/5.3-res)，重命名为 resources 并移动到LunaGC_5.3.0根目录；

5. 若LunaGC_5.3.0根目录无 proxy.py、proxy_config.py ，须自行寻找下载（[Grasscutters/Grasscutter](https://github.com/Grasscutters/Grasscutter)的先前提交中可找到这些文件）；

6. 启动Grasscutter：
   ```
   $ cd /path/to/LunaGC_5.3.0
   $ mitmdump -s proxy.py -k --set block_global=false & \
   $ sudo /usr/lib/jvm/java-17-openjdk/bin/java -jar LunaGC-5.3.0.jar
   ```

---
{: data-content=" 本地游玩 "}

1. 安装Lutris；

2. 下载5.3游戏数据，并用 LunaGC_5.3.0/patch/Astrolabe.dll 覆盖 GenshinImpact_Data/Plugins/Astrolabe.dll ；

3. 启动Lutris，添加Wine环境变量：

   | Key | Value |
   |---|---|
   | http_proxy | http://localhost:8080 |
   | https_proxy | http://localhost:8080 |
  
4. 添加游戏。

---
{: data-content=" 自定义模组 "}

1. 安装ProtonPlus；

2. 启动ProtonPlus，为Lutris安装Wine-Staging-Tkg；

3. 修改Lutris设置：开启高级选项；Wine版本改为Wine-Staging-Tkg；关闭VKD3D、DXVK-NVAPI/DLSS、AMD FSR、2个反作弊；

4. 从[SilentNightSound/GI-Model-Importer](https://github.com/SilentNightSound/GI-Model-Importer)下载3DMigoto-GIMI；

5. 新建launch.bat:
   ```
   cd C:\path\to\3dmigoto\
   start "" "3DMigoto Loader.exe"

   cd C:\path\to\GenshinImpact\
   start "" "GenshinImpact.exe"
   ```
   
6. Lutris相关设置修改为 /path/to/launch.bat ；

7. 自定义模组请置于 3dmigoto-gimi/Mods/ ，游戏中可按 F1 查看帮助。
