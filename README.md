# IP地址计算器（Android）

输入一个 IPv4 地址或网段，算出网段各项关键信息；也可以把网段继续切成更小的子网。纯本地计算，不联网、不上传任何数据。

## 功能
- 三种输入写法：`192.168.1.10/24`、`192.168.1.10 255.255.255.0`、`192.168.1.10`
- 输出：IP、CIDR、子网掩码、通配符、网络地址、广播地址、可用地址范围、可用主机数、地址类型、地址类别、主机位、二进制（网络位/主机位分界）
- 点任意一行即复制
- 子网切分：按新前缀列出子网段与地址范围
- 应用内在线更新：读取签名清单 → 校验 sha256 → 自动安装

## 目录
```
ipcalc/                     Android 工程
  src/com/example/ipcalculator/  MainActivity、OtaManager
  build.sh                 手工构建脚本（release 密钥库在 ../secrets，不进仓库）
dist/                      OTA 分发目录
  update.json             单文件自包含签名清单 {"payload","sig"}
  app-<版本>.apk          每版独立文件名，避免缓存拿到旧包
```

## 构建
```
cd ipcalc && ./build.sh
```
链路：`aapt2 compile/link → javac → d8 → zipalign → apksigner`（不使用 Gradle）。

## 规格
- 包名：`com.example.ipcalculator`
- minSdk 24 / targetSdk 34
- 当前版本：v1.0.1（versionCode 2）
