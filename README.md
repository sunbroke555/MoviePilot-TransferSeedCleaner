# MoviePilot V2 整理后清理做种

MoviePilot V2 插件：收到整理完成事件后，延迟复核整个下载任务。确认已下载的媒体文件均已通过复制或硬链接安全入库，且下载数据没有被其他种子共用时，通过 qBittorrent 或 Transmission 删除种子任务及下载文件。

## 安装

将本仓库地址 `https://github.com/sunbroke555/MoviePilot-TransferSeedCleaner` 加入 MoviePilot 的 `PLUGIN_MARKET`（多个仓库地址用英文逗号分隔），刷新插件市场，安装并启用“整理后清理做种”。插件首次启用默认为**预览模式**；先查看插件页面里的待复核结果，再决定是否关闭预览执行删除。

等待时间和复核周期均可在插件设置中调整，默认各为 10 分钟。插件页面显示最近 20 条删除记录，插件数据保存最近 100 条。

插件只处理启用后收到整理完成事件的任务；安装前已整理的历史任务不会自动加入清理队列。软链接、未完成整理、路径不明、共享下载数据等情况会跳过。详见[插件说明](plugins.v2/transferseedcleaner/README.md)。

## 结构与验证

本仓库按 [MoviePilot V2 插件开发指南](https://github.com/jxxghp/MoviePilot-Plugins/blob/main/docs/V2_Plugin_Development.md) 提供 `package.v2.json` 索引和 `plugins.v2/transferseedcleaner/` 源码。`release: false` 表示从源码目录安装，不依赖 GitHub Release。

本地回归测试：`python -m pytest -q tests/v2/transferseedcleaner`。测试覆盖多文件种子、只整理部分剧集、下载器快照变化、软链接、硬链接和共享路径等场景。尚未在真实 MoviePilot 与下载器环境中联测。

`icons/clean.png` 来自 [MoviePilot-Plugins](https://github.com/jxxghp/MoviePilot-Plugins)，随仓库保留 GPL-3.0 许可证。
