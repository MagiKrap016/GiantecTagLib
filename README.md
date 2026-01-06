# Giantec Tag Lib (Android) 用户手册

<p><small><span style="color:#6b7280">最后修改：2026-01-06 · 文档版本：v1.0</span></small></p>

## 🧭 简介

本库提供标签 UID 校验功能，包含以下公开 API：
- com.giantec.gtaglibrary.lib.TagVerify.Verify6699(byte[] id)
- com.giantec.gtaglibrary.lib.TagVerify.Verify5666(byte[] id)



## 📦 1.导入方式

### 1.1 方式一：通过 Maven 引入
在模块的 build.gradle 中添加依赖：
```
implementation 'com.github.MagiKrap016:GiantecTagLibAndroid:Tag'
```
[![](https://jitpack.io/v/MagiKrap016/GiantecTagLibAndroid.svg)](https://jitpack.io/#MagiKrap016/GiantecTagLibAndroid)

如需使用 JitPack，请在项目级 settings.gradle 或 build.gradle 中添加仓库源：
```groovy
repositories {
    // ... 其它仓库
    maven { url 'https://jitpack.io' }
}
```

### 1.2 方式二：本地 AAR 引入
1. 将 `closed_source_arr-1.1.aar` 复制到应用模块的 `app/libs/` 目录。
2. 在模块的 build.gradle（Groovy）中：
   ```groovy
   repositories {
       // ...existing code...
       flatDir { dirs 'libs' }
   }
   
   dependencies {
       // ...existing code...
       implementation(name: 'closed_source_arr-1.1', ext: 'aar')
   }
   ```
   若使用 Kotlin DSL：
   ```kotlin
   repositories {
       // ...existing code...
       flatDir { dirs("libs") }
   }
   
   dependencies {
       // ...existing code...
       implementation(files("libs/closed_source_arr-1.1.aar"))
   }
   ```



## 🛠️ 2.使用方法

### 2.1 API 说明
- TagVerify.Verify6699
  - 签名：`public static boolean Verify6699(byte[] id)`
  - 入参：长度为 7 的 UID 数组；若为 null 或长度不符返回 false。
  - 逻辑：校验 id[0] 是否为 0x5A，并依据异或规则验证其他字节。
  - 返回：校验通过返回 true，否则返回 false。

- TagVerify.Verify5666
  - 签名：`public static boolean Verify5666(byte[] id)`
  - 入参：长度为 8 的 UID 数组；若为 null 或长度不符返回 false。
  - 逻辑：校验 id[6] 是否为 0x5A，依据异或规则验证其他字节。
  - 返回：校验通过返回 true，否则返回 false。

### 2.2 示例代码
```java
import com.giantec.gtaglibrary.lib.TagVerify;

byte[] uid6699 = new byte[]{ (byte)0x5A, /* uid1 */ 0x00, 0x11, 0x22, 0x33, 0x44, /* uid6 */ 0x00 };
boolean ok6699 = TagVerify.Verify6699(uid6699);

byte[] uid5666 = new byte[]{ /* uid0 */ 0x00, 0x11, 0x22, 0x33, /* uid4 */ 0x44, /* uid5 */ 0x00, (byte)0x5A, /* uid7 */ 0x55 };
boolean ok5666 = TagVerify.Verify5666(uid5666);
```
注：示例仅展示调用方式，实际 UID 字节应来自设备读取；请确保长度与位置符合协议。



## ⚙️ 3.兼容性与配置

- 无需额外权限；若结合 NFC/蓝牙读取 UID，请根据实际场景在 AndroidManifest.xml 添加权限。
- 若开启混淆，建议保留库包：
```
-keep class com.giantec.gtaglibrary.** { *; }
```



## 🗂️ 4.版本信息

- AAR 版本：1.1.2
- Maven 坐标：`com.github.MagiKrap016:GiantecTagLibAndroid:Tag`
- Compile Android SDK：33
- Minimal Android SDK：26
- JDK: 11

  

## 💬 5.支持
如需问题反馈或更多文档，请联系维护者。

---

<table align="right">
  <tr>
    <td align="center" halign="middle"><img src="./logo.png" width="30" height="30" alt="logo"></td>
    <td valign="middle">Giantec Software External Doc · author: cjli, AE Team</td>
  </tr>
</table>
