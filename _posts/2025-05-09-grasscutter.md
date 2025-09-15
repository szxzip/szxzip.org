---
layout: post
category: y
title: Genshin Impact v5.3 Grasscutter & 3DMigoto
---

---
{: data-content=" 部署本地服务器 "}

1. 安装 MongoDB、jdk17、nodejs、mitmproxy、python；

2. 启动 MongoDB：
   ```
   $ sudo systemctl enable --now mongodb
   ```

3. 克隆 [Kei-Luna/LunaGC_5.3.0](https://github.com/Kei-Luna/LunaGC_5.3.0)，并编译：
   ```
   $ chmod +x gradlew
   $ ./gradlew jar
   ```

4. 克隆 [pmagixc/5.3-res](https://github.com/pmagixc/5.3-res)，重命名为 resources，置于 LunaGC_5.3.0 根目录；

5. 获取 [MlgmXyysd/Grasscutter](https://github.com/MlgmXyysd/Grasscutter) proxy.py、proxy_config.py，置于 LunaGC_5.3.0 根目录；

6. 启动 Grasscutter：
   ```
   $ cd /path/to/LunaGC_5.3.0
   $ mitmdump -s proxy.py & \
   $ sudo /usr/lib/jvm/java-17-openjdk/bin/java -jar LunaGC-5.3.0.jar
   ```

---
{: data-content=" 本地游玩 "}

1. 安装 Lutris；

2. 下载 5.3 游戏数据，并将 GenshinImpact_Data/Plugins/Astrolabe.dll 替换为 LunaGC_5.3.0/patch/Astrolabe.dll；

3. 启动 Lutris，添加 Wine 环境变量：

   | Key | Value |
   |---|---|
   | http_proxy | http://localhost:8080 |
   | https_proxy | http://localhost:8080 |
  
4. 添加游戏。

---
{: data-content=" 自定义模组 "}

1. 安装 ProtonPlus；

2. 启动 ProtonPlus，为 Lutris 安装 Wine-Staging-Tkg；

3. 修改 Lutris 设置：开启 Advanced；启用 Wine-Staging-Tkg；关闭 VKD3D、DLSS、FSR、Anti-Cheat；

4. 由 [SilentNightSound/GI-Model-Importer](https://github.com/SilentNightSound/GI-Model-Importer) 下载 3DMigoto-GIMI；

5. 新建 launch.bat：
   ```
   cd C:\path\to\3dmigoto\
   start "" "3DMigoto Loader.exe"

   cd C:\path\to\GenshinImpact\
   start "" "GenshinImpact.exe"
   ```
   
6. Lutris 游戏主程序设为 /path/to/launch.bat；

7. 自定义模组请置于 3dmigoto-gimi/Mods/，游戏中可按 F1 查看帮助。
