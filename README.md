# 4ch_recording

苏州烟草四通道音频采集与录音项目。工程基于 LabVIEW 开发，用于通过声卡/音频采集设备进行 4 路同步采集、录音保存、日志记录，并配套频谱/瀑布图显示相关 VI。

## 功能概览

- 4 通道音频同步采集与 WAV 录音
- 采集过程日志写入
- STFT/频谱瀑布图相关显示与示例 VI
- WaveIO 动态库和 LabVIEW LLB 依赖随工程保存
- 提供 LabVIEW Application Builder 生成规格，可构建 Windows 可执行程序

## 项目结构

```text
.
├── 苏州烟草.lvproj                  # LabVIEW 工程文件
├── 苏州烟草.aliases / 苏州烟草.lvlps # LabVIEW 工程辅助文件
├── VIs/                            # 主程序与核心子 VI
│   ├── main.vi                     # 顶层主 VI
│   ├── recording-audio-queued].vi   # 录音采集相关 VI
│   ├── stft.vi                     # 时频分析相关 VI
│   ├── stimulus.vi                 # 激励/信号相关 VI
│   ├── WriteLog.vi                 # 日志写入
│   └── YMD.vi                      # 日期时间辅助 VI
├── waveio_108/                     # WaveIO 运行依赖
│   ├── WaveIO.dll
│   ├── WaveIO_x64.dll
│   ├── WaveIO.llb
│   └── lvsound2.dll
├── Log/                            # 历史运行日志
├── path.txt                        # 默认录音保存目录配置
├── thermal_colormap_u32_utf16.txt  # 频谱/瀑布图颜色映射数据
└── Generate Waterfall Plot.vi 等    # 频谱瀑布图示例/辅助 VI
```

## 开发环境

- Windows
- LabVIEW 2021 或兼容版本（工程文件版本为 `LVVersion="21008000"`）
- NI Sound and Vibration / Analysis 相关组件
- 支持 4 通道输入的声卡或音频采集设备

工程中已包含 `waveio_108` 目录下的 WaveIO 相关 DLL/LLB。首次打开工程时，如果 LabVIEW 提示依赖丢失，请优先检查该目录、NI 自带 `vi.lib` 依赖以及本机声卡驱动。

## 运行方式

1. 使用 LabVIEW 打开 `苏州烟草.lvproj`。
2. 在 `My Computer > VIs` 下打开并运行 `main.vi`。
3. 检查 `path.txt` 中的录音保存路径，默认指向本机 `TEST_WAV` 目录。
4. 确认 4 通道音频输入设备连接正常，再开始采集。

## 构建可执行程序

工程内置 Build Specification：

- 名称：`Dongyuan4ch_record_0908B`
- 目标程序：`Dongyuan.exe`
- 默认输出目录：`builds/NI_AB_PROJECTNAME/Dongyuan4ch_record_0908B/`
- 顶层 VI：`VIs/main.vi`

在 LabVIEW 项目中右键 `Build Specifications > Dongyuan4ch_record_0908B`，选择 `Build` 即可生成可执行程序。

## 数据与版本控制说明

- `TEST_WAV/` 中的录音样本属于运行数据，体积较大，不建议直接提交到普通 GitHub 仓库。
- 新增日志、构建输出、录音数据和本地下载的辅助资源包已通过 `.gitignore` 排除。
- 如果确实需要长期保存大体积 WAV 数据，建议使用 Git LFS、网盘、NAS 或单独的数据归档仓库。

## 仓库地址

GitHub: <https://github.com/addddou/4ch_recording.git>
