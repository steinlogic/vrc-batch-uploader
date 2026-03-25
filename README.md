# VRChat Batch Uploader (VRC 批量上传工具)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Unity](https://img.shields.io/badge/Unity-2022.3%20LTS+-black.svg?logo=unity)](https://unity.com/)

VRChat Batch Uploader 是一款专为 VRChat 创作者打造的免费 Unity 编辑器插件。它允许你将多个 Avatar 加入队列，实现真正的全自动、无人值守（AFK）挂机批量上传。

### 💡 开发初衷

作为作者，我非常推崇“极致性能优化”的理念。
目前很多创作者喜欢把所有的衣服、道具全部塞进一个 Avatar 里做成“大衣柜”（通过 Toggle 切换），这会导致极其严重的性能开销（多余的骨骼、材质和网格数据）。
我个人更喜欢将不同穿搭拆分成独立的 Prefab 来保持模型处于最高的性能评级。但这种做法有一个痛点：每次修改完母模型，所有的子模型/穿搭变体都需要手动点击重新上传一遍，非常折磨。

为了解决这个痛点，我开发了这款完全免费的批量上传插件。你可以把所有变体一次性丢进队列，去喝杯咖啡，回来就全部上传好了！

## ✨ 核心特性

- **🚀 真正的无人值守**：针对最新的 VRChat SDK 进行了底层优化，全自动拦截并绕过 SDK 弹出的“版权确认 (I Agree)”和“商品化提醒”模态框，中途绝不卡进度。
- **🌐 多语言原生支持**：内置 简体中文 / 日本語 / English 三语界面，可在设置中随时切换并自动保存偏好。
- **⏱️ 实时独立计时器**：队列面板实时显示每个 Avatar 的单次上传耗时（动态跳动，成功后定格），上传进度与耗时一目了然。
- **🚀 深度性能护航**：针对长队列上传进行了底层内存优化（引入强制 GC 序列、释放 Shader 变体缓存、主线程让步机制），彻底解决了连续上传时“越传越慢”的性能衰减问题。
- **⏳ 可控的任务缓冲**：任务之间提供倒计时缓冲期（可在设置中自定义等待秒数），提供视觉进度条，允许中途安全打断或点击“立即开始”一键跳过等待。
- **📦 极简队列管理**：支持从 Hierarchy 拖入对象，也支持从 Project 直接拖入 Prefab（甚至支持未激活的隐藏对象）。
- **🔍 一键扫描场景**：点击“扫描场景”按钮，一键抓取场景内所有带有 `VRCAvatarDescriptor` 的模型。
- **♻️ 失败自动重试**：遇到网络波动导致上传失败？插件会自动重置计时并进行重试（最多3次）。如果你手动跳过，则会安全中断，避免死循环。
- **🔔 任务完成通知**：整个队列上传完毕后，系统将播放提示音（可在设置面板中自由开启或关闭）。

## 🛠 使用环境

- Unity 版本：`2022.3 LTS` 及以上（推荐使用 VCC 默认的 Unity 版本）。
- VRChat SDK：`VRCSDK 3.x` (兼容最新的 UI Toolkit 面板，测试环境为 3.7.1+)。
- 仅支持 Avatar 批量上传。

## 📥 安装方法

本插件开箱即用，提供两种安装方式：

**方式一：使用 UnityPackage (推荐)**
1. 在 Release 页面下载最新的 `.unitypackage` 文件。
2. 双击文件或在 Unity 中选择 `Assets > Import Package > Custom Package` 直接导入到你的工程中。

**方式二：使用源码文件**
1. 下载本项目的源码。
2. 找到项目中的 `VRCBatchUploader` 文件夹（或相关的 `.cs` 文件）。
3. 将文件放置到你 Unity 工程的 `Assets/Editor/VRCBatchUploader/` 目录下。
   *(注意：必须存放在名为 `Editor` 的特殊文件夹层级内，如果没有请手动创建)*
4. 等待 Unity 编译完成。

编译完成后，在顶部菜单栏中即可看到 `Tools > VRC Batch Uploader`。

## 📖 使用指南

1. **打开面板**：在 Unity 顶部菜单栏点击 `Tools -> VRC Batch Uploader` (或使用快捷键 `Ctrl + Shift + U`)。
2. **添加任务**：
   - 将你需要上传的 Avatar 从左侧 Hierarchy 或下方 Project 直接拖入插件的绿色拖放区。
   - 或者直接点击工具栏的 [扫描场景]。
3. **调整队列**：你可以通过点击行尾的 `▲` `▼` 调整上传顺序，或点击 `↑` 将某个模型设为紧急优先。
4. **个性化设置**：在设置页面 (Settings) 中，你可以切换语言、调整任务间的倒计时时长，以及开关完成后的声音提示。
5. **开始上传**：点击右上角的 [▶ 开始上传]，然后你就可以离开电脑了！

## ⚠️ 版权与使用条款 (非常重要)

本插件内置了对 VRChat SDK 版权确认弹窗的自动化同意机制（用于实现无人值守）。
使用本插件进行上传，即代表您完全理解并同意以下条款：

1. 您确认拥有您所上传的所有 Avatar / 素材的完全版权，或已获得原作者的合法授权。
2. 您的上传行为完全遵守 [VRChat 官方服务条款 (Terms of Service)](https://hello.vrchat.com/legal) 以及相关的社区准则。
3. **责任自负**：本插件仅作为自动化点击和队列管理的效率工具。对于因盗用模型、侵犯版权、上传违规内容而导致的 VRChat 账号封禁或其他法律纠纷，作者（逻辑XR）概不负责。

如果您没有相关模型的合法使用权，请立即停止使用本插件进行上传。

## 📄 协议与开源

- 作者：[逻辑XR](https://github.com/steinlogic)
- 项目地址：[https://github.com/steinlogic/vrc-batch-uploader](https://github.com/steinlogic/vrc-batch-uploader)
- 开源协议：本项目遵循 [MIT License](LICENSE) 协议，完全免费开源。欢迎提交 Issue 或 Pull Request 来帮助改进此项目！
