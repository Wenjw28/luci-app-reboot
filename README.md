# luci-app-rebootschedule

OpenWrt 25.12（apk 包管理器）用的**定时重启** LuCI 插件，带 GitHub Actions 自动打包。

- 每天定时 / 指定星期几 / 按开机时长三种触发方式
- 配置改完 20 秒内生效，不用重启服务
- 开机前 5 分钟不触发，失败后 1 小时内不重复，避免循环重启
- 附带「立即重启」按钮

## 一键打包成 .apk

25.12 的包是 apk-tools 3 的 **ADB(v3)** 二进制格式，只能用它自己的构建系统生成，
所以这里用 GitHub Actions 在云端 Linux 上编译。

1. 在 GitHub 新建一个仓库（public 免费，private 也够用）
2. 把本目录**全部内容**上传进去（网页拖拽即可，注意要带上 `.github` 目录）
3. 打开仓库的 **Actions** 标签页，等 `build-apk` 跑完（约 10–15 分钟）
4. 进入这次运行，页面底部 **Artifacts** 下载 `luci-app-rebootschedule-apk`
5. 解压得到一个 `.apk`，传到路由器安装：

```sh
scp luci-app-rebootschedule-*.apk root@192.168.1.1:/tmp/
ssh root@192.168.1.1
apk add --allow-untrusted /tmp/luci-app-rebootschedule-*.apk
/etc/init.d/rebootschedule enable
/etc/init.d/rebootschedule start
```

装完在 LuCI 里：**服务 → 定时重启**。

## 也在本地打包

有 Linux 机器的话，不用 GitHub：

```sh
cd luci-app-rebootschedule
./build-apk.sh          # 自动下 SDK → feeds → 编译 → 输出 apk
```

## 目录

```
.github/workflows/build.yml          GitHub Actions：下载 SDK 并编译
luci-app-rebootschedule/
├── Makefile                         包定义（luci.mk）
├── build-apk.sh                     本地一键编译脚本
├── htdocs/luci-static/resources/view/rebootschedule/overview.js
└── root/
    ├── etc/config/rebootschedule    UCI 配置
    ├── etc/init.d/rebootschedule    procd 服务
    ├── usr/libexec/rebootschedule/daemon
    └── usr/share/{luci/menu.d,rpcd/acl.d}/
```

## 配置项

| 选项 | 说明 | 默认 |
|---|---|---|
| `enabled` | 总开关 | `0` |
| `mode` | `daily` / `weekly` / `interval` | `daily` |
| `time` | 24 小时制 `HH:MM` | `03:30` |
| `weekdays` | 空格分隔，`0`=周日 … `6`=周六 | 全部 |
| `hours` | interval 模式的开机小时数 | `24` |
| `dry_run` | `1` 时只写日志不重启（调试） | `0` |

## License

GPL-2.0 — <https://www.gnu.org/licenses/old-licenses/gpl-2.0.html>
