# SeedAgent 博途（TIA Portal）编程智能体

[English](README-EN.md) Version

<img width="600" alt="image" src="https://github.com/user-attachments/assets/99081a40-984f-43bf-b075-a1b302a0fa8b" />

通过 SeedAgent 博途（TIA Portal）编程智能体，一套面向 Siemens S7-1200、S7-1500 和 TIA Portal V16–V21 的 AI 工程 Workbuddy 扩展，让用户通过自然语言，在本机或远程工程电脑上完成西门子 TIA Portal 工程编程、编译、归档与经确认的下载。

SeedAgent 博途（TIA Portal）编程智能体，不是一个简单地把大模型接到 TIA Portal Openness 上的演示 Demo，也不依赖模型反复试错或临场拼凑 Openness 自动化逻辑，安装后即可使用。我们把项目生命周期、版本选择、工程机连接、文件传递、编译诊断、收费、确认与安全边界固化为确定性的工具级产品，让用户选择的 Agent 能够理解需求、编写西门子博途程序、管理项目状态并推进任务。

当前版本：**0.9.0**  
当前 TIA 连接器版本：**1.6.0**  
当前适配的 Agent 客户端：腾讯 **WorkBuddy**  
支付方式：**SkillPay 余额；需要追加授权时，由 WorkBuddy 调起腾讯“AI 专属卡”页面，通过微信支付完成**

本仓库用于产品介绍、安装入口、版本发布、使用文档和问题反馈。产品不开源，仓库不包含核心源代码。

## 来自真实自控工程实践

本产品的核心并非 fork 或包装某个第三方 GitHub 项目。我们长期面向企业客户提供工业自动化与控制工程服务，拥有自己的自动化控制工程团队。产品来自内部专项探索，并在真实工程需求、工程师日常使用、不同 TIA 版本以及 PLC/PLCSIM Advanced 测试中持续积累和修正。

产品按相应许可证使用必要的通用第三方组件，并通过西门子公开提供的 TIA Portal Openness 接口操作博途；SeedAgent 的核心架构与实现仍由我们独立设计和开发。

## 核心能力


- **本机与跨机器操作**：WorkBuddy 可以操作本机博途，也可以操作网络可达、已配对的其他工程电脑（含虚拟机）里的博途。
- **TIA V16～V21**：按工程电脑实际安装与就绪情况选择版本，不用为每个版本维护不同的对话方式。
 <img width="1999" height="2110" alt="image" src="https://github.com/user-attachments/assets/e49ce33b-eb15-4ba1-8ab5-0af648ca7102" />
 
- **多工程机、多版本会话**：多台工程电脑和不同 TIA 主版本可以分别保持独立的受控项目会话；当前同一工程电脑的同一 TIA 主版本一次只控制一个项目，避免误操作错误工程。
- **多种项目接入方式**：从零开始描述需求，生成并编译博途工程（目前支持 SCL）；恢复并打开 `.zapNN`；打开工程电脑上的 `.apNN` 原工程；或挂载用户已在博途中打开的项目。
- **连续协作**：读取和导出程序块、比较变更、新增或修改 SCL 块、在明确确认后删除指定块、编译、查看诊断、归档、关闭项目，或仅断开 Agent 控制而保留项目和博途窗口。
- **项目保护**：内置项目保护机制，能够区分用户原工程、恢复后的工作副本和归档产物；不会静默覆盖、切换、关闭或下载。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/61f15458-85a7-4ffd-9aa4-97ddc247dcea" />

- **真实编译结果**：由目标工程电脑上的真实 TIA Portal 执行编译，并返回实际的错误、警告和编译产物。
- **PLCSIM Advanced**：当前支持在既定安全边界内将 S7-1500 项目下载到 PLCSIM Advanced。普通 S7-PLCSIM、在线变量读写和强制变量当前未开放。
- **真实 PLC 下载**：每次都要明确确认工程电脑、项目、PLC IP、PG/PC 接口和可能影响；用户确认后，可在本次下载过程中继续处理已经授权的下载选项和设备证书信任提示。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7bbf334d-28c2-4169-8fd0-8770e6e9b4c8" />

- **安装、更新与诊断**：提供控制端、工程端、持久化服务、配对、更新检查、状态检查和维护入口。

当前主要覆盖 S7-1200、S7-1500 与 SCL。梯形图编写与修改、WinCC Unified、伺服和硬件组态修改，以及通过 OPC UA 自主仿真调试等能力，将在后续版本中逐步支持。

## 第一次使用

建议在 WorkBuddy 新会话中先问：

> 你能做什么？我要怎么操作你？怎么收费？

之后直接用自然语言描述目标，例如：

- “在这台电脑的 TIA V21 里创建一个 1500 项目，写一个简单的加法程序并编译。”
- “连接我的所有博途机，看看 V16 现在能不能用。”
- “把这个 `.zap20` 恢复到我的文档文件夹，读取程序块并继续修改。”
- “挂载我已经打开的项目，编译并归档；先不要关闭项目。”

涉及保存原工程、替换当前项目、关闭、删除块、仿真或真实 PLC 下载时，智能体会在真正执行前说明影响并取得相应确认。

<img width="2046" height="3357" alt="image" src="https://github.com/user-attachments/assets/26e4ef46-2f9d-4bf3-8a19-9b8bf0e3b928" />

<br>

<img width="3034" height="1814" alt="image" src="https://github.com/user-attachments/assets/48a1c8de-03c3-4276-9f3e-cc543cb22705" />


## 模型建议

本产品提供 S7-1200/S7-1500 编程所需的基础工程规则、确定性工具和真实编译闭环，但不会用统一的行业模板替用户决定程序风格和工程标准。具体工艺、企业规范和最佳实践，仍由用户结合所选模型确定。

根据我们大量的内部使用与对比结果，建议使用 **DeepSeek V4.1 Flash 或具备相近推理和代码能力的模型**。如果在 WorkBuddy 中选择“均衡”，请留意该次任务实际路由到的模型；模型能力会影响需求理解、程序设计和编译错误修正质量，但不会改变底层工具的安全边界。

后续我们计划通过云平台开放更多经过真实项目反复迭代的行业场景能力。

## 运行环境与当前限制

- 控制端目前只正式适配 WorkBuddy。
- 按 WorkBuddy 之前的环境限制，WorkBuddy 不能安装在虚拟机环境；产品的工程端可以部署在满足 Windows、TIA Portal、网络和授权条件的实体机或虚拟机中，再由实体机上的 WorkBuddy 连接。WorkBuddy 和博途安装在同一台电脑也是可以的。
- 执行工程操作的电脑需要安装受支持版本的 TIA Portal，并启用对应的 Openness 环境。
- 产品当前以中文使用体验为主，后续会根据其他 Agent 平台的开放程度扩展客户端和语言。

## 收费方式

运行服务需要收费，但不会仅因普通对话收费：

- 环境、版本、能力、节点和项目状态等基础查询原则上免费。
- 实际修改工程、导入或导出完整程序内容、编译、归档、下载或产生工程交付物的操作，按实际执行的单项能力计费。
- 余额充足时直接从 SkillPay 余额扣除；余额不足时，WorkBuddy 会调起腾讯“AI 专属卡”授权页面，由用户通过微信支付完成。
- 重试、失败是否扣费以及最终金额，以服务端返回的实际结算记录和 SkillHub 当期页面为准；README 不写死单价。

## 安装

可在 WorkBuddy / SkillHub 搜索 **SeedAgent 博途（TIA Portal）编程智能体**。

也可以把下面的链接粘贴到 WorkBuddy 新会话，请它下载、校验并安装：

`https://www.autohub-ai.com/downloads/seedagent/tia-programing/0.9.0/SeedAgent-TIA-Programming-Install-0.9.0-Windows-x64.zip`

> SHA-256: 97BD1661503BFFEBEA87F2D53AC99B8A3A5F15B420AA37BA0318318E38A565F1

当前发布版本为 0.9.0。后续版本号和下载地址会随发布更新，请以 SkillHub 或官方发布信息为准。

交付包：

- 完整安装包：`SeedAgent-TIA-Programming-Install-0.9.0-Windows-x64.zip`
- 工程端离线包（可在 WorkBuddy 对话中自动获取）：`SeedAgent-TIA-Programming-Engineering-0.9.0-Windows-x64.zip`

完整安装后，维护工具保存在安装目录中；删除下载 ZIP 和临时解压目录不会丢失重启与修复入口。

维护工具会定期（每6小时）连接服务器检查更新并提示后续新版本，由用户自行决定是否安装。

## 即将陆续上线

- LAD 梯形图的编写与修改能力。
- WinCC Unified 画面编辑、变量、报警和脚本能力。
- 设备、网络、驱动与伺服组态的读取和修改。
- OPC UA 读写 PLC 变量，使 AI 能自主仿真测试程序逻辑是否正确。
- 长任务异步进度、跨对话恢复和结果查询。
- 适配更多 Agent 客户端，并完善英文及其他语言体验。

我们也会逐步上线安装、配对、编程、编译、归档、下载和故障恢复的操作示例视频。

## 许可与权利

本产品为闭源商业软件，不通过本仓库提供源代码许可。由我们独立开发的程序、文档、品牌与原创资产，其相关权利由我方依法享有；第三方库及组件继续遵守各自许可证。

Siemens、SIMATIC、TIA Portal、STEP 7、S7-1200 和 S7-1500 是其各自权利人的商标或产品名称。本产品与 Siemens 无隶属或背书关系，对这些名称的使用仅用于说明兼容性和用途。

## 支持与反馈

企业微信用户群：**SeedAgent 博途编程智能体用户群**。欢迎中文用户入群交流使用问题、功能建议和回归结果。

![SeedAgent 博途编程智能体用户群企业微信二维码](https://www.autohub-ai.com/downloads/seedagent/assets/wecom-user-group.png)

中英文用户也都可以通过本仓库的 GitHub Issues 提交问题、建议和可公开复现的信息，或通过 SkillHub 发布者页面反馈。

GitHub Issues 是公开页面。请勿提交包含客户项目源码、设备证书、PLC 地址、支付凭证、个人信息或其他敏感内容的日志与截图；此类问题请先通过非公开官方渠道联系我们。
