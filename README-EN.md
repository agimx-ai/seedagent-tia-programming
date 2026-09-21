# SeedAgent TIA Portal Programming Agent

[中文](README.md)

Use natural language to develop, compile, archive, and—after explicit confirmation—download Siemens TIA Portal projects from a local PC or a paired engineering workstation.

SeedAgent is not a proof of concept that simply wires an LLM to TIA Portal Openness. Nor does it ask the model to discover the API by trial and error or improvise automation logic at runtime. It is ready to use after installation. Project lifecycle management, TIA version selection, workstation connectivity, file transfer, compile diagnostics, billing, confirmations, and safety boundaries are implemented as deterministic, product-grade tools. The user's AI agent can therefore focus on understanding the request, developing the PLC program, tracking project state, and moving the job forward.

Current version: **0.9.0**  
Current TIA integration component: **1.6.0**  
Currently supported AI-agent client: **Tencent WorkBuddy**  
Payment flow: **SkillPay balance; when additional authorization is required, WorkBuddy opens a WeChat Pay screen labeled “AI Exclusive Card” by Tencent**

## Built from Industrial Automation Practice

The core product is not a fork or repackaging of a third-party GitHub project. We deliver industrial automation projects for enterprise customers and have our own controls engineering team. SeedAgent began as an internal initiative and has been refined through real project requirements, day-to-day use by automation engineers, multiple TIA Portal versions, and testing with both PLC hardware and PLCSIM Advanced.

The product uses the necessary general-purpose third-party components under their applicable licenses and operates TIA Portal through Siemens' published TIA Portal Openness interface. SeedAgent's core architecture and implementation remain independently designed and developed by us.

## Core Capabilities

- **Local and remote engineering:** WorkBuddy can operate TIA Portal on the same computer or connect to other reachable, paired TIA engineering workstations, including virtual machines.
- **TIA Portal V16–V21:** SeedAgent selects from the versions actually installed and ready on each workstation; users do not need a separate conversation workflow for every TIA release.
- **Multiple workstations and TIA versions:** Different workstations and TIA major versions can maintain independent managed project sessions. To avoid acting on the wrong project, one workstation currently manages only one project per TIA major version at a time.
- **Several ways to get started:** Describe a requirement from scratch and have SeedAgent generate and compile a TIA Portal project (SCL is currently supported); restore and open a `.zapNN` archive; open an existing `.apNN` project in place on the engineering workstation; or attach to a project the user already has open in TIA Portal.
- **Iterative engineering workflow:** Read and export program blocks, compare revisions, add or modify SCL blocks, explicitly delete selected blocks, compile, inspect diagnostics, create an archive, close a project, or detach the agent while leaving both the project and TIA Portal open.
- **Project safeguards:** SeedAgent distinguishes user-owned projects, restored working copies, and generated archives. It does not silently overwrite or switch projects, close TIA Portal, or initiate a download.
- **Real compilation evidence:** Compilation runs in the actual TIA Portal installation on the selected engineering workstation and returns the real errors, warnings, and generated artifacts.
- **PLCSIM Advanced:** Supports the current, deliberately constrained workflow for deploying S7-1500 projects to PLCSIM Advanced. Standard S7-PLCSIM, online variable access, and variable forcing are not currently exposed.
- **Downloads to physical PLCs:** Every download requires explicit confirmation of the engineering workstation, project, PLC IP address, PG/PC interface, and potential impact. Once approved, SeedAgent can handle the applicable TIA download decisions and device-certificate trust prompts within that run.
- **Installation, updates, and diagnostics:** Includes controller-side and engineering-workstation packages, persistent background services, secure pairing, update checks, health checks, and maintenance utilities.

The current product primarily covers S7-1200, S7-1500, and SCL.

LAD editing, WinCC Unified engineering, servo and hardware configuration changes, and AI-driven simulation testing through OPC UA are planned for later releases.

## First Use

Start a new WorkBuddy conversation and ask:

> What can you do? How should I work with you? How is the service charged?

Then describe the engineering goal in normal language, for example:

- “Create an S7-1500 project in TIA Portal V21 on this computer, write a simple addition program, and compile it.”
- “Connect to all of my TIA Portal computers and check whether V16 is available now.”
- “Restore this `.zap20` into my Documents folder, read its program blocks, and continue modifying it.”
- “Attach to the project I already opened, compile and archive it, but do not close it.”

Before saving changes back to a user-owned project, switching away from the active project, closing a project, deleting blocks, running a simulation, or downloading to a physical PLC, the agent explains the impact and obtains the required confirmation.

## Model Guidance

SeedAgent provides the core engineering rules, deterministic tools, and real TIA Portal compilation loop needed to program S7-1200 and S7-1500 PLCs. It deliberately avoids imposing a one-size-fits-all industry template on program structure or engineering standards. Project-specific process knowledge, conventions, and best practices remain under the user's control and are interpreted with the selected model.

Based on extensive internal use, we recommend **DeepSeek V4.1 Flash or a model with comparable reasoning and coding capability**. If WorkBuddy is set to **Balanced (均衡)**, check which model was actually selected for the task. Model quality affects requirements analysis, program design, and compile-error correction, but it cannot bypass the safety boundaries enforced by the tools.

We plan to provide additional, thoroughly refined scenario capabilities through our cloud platform.

## Environment and Current Limits

- WorkBuddy is currently the only officially supported AI-agent client.
- Tencent currently does not allow WorkBuddy to be installed in a virtual machine. The SeedAgent engineering component may run on either a physical or virtual Windows machine that meets the TIA Portal, networking, and licensing requirements; WorkBuddy running on a physical machine can then connect to it. WorkBuddy and TIA Portal may also run on the same physical computer.
- Each engineering workstation needs a supported TIA Portal installation with the corresponding TIA Portal Openness access configured.
- The current user experience is Chinese-first. More Agent clients and languages will be considered as their integration capabilities mature.

## Billing

The runtime service is paid, but ordinary conversation alone is not billed:

- Basic environment, version, capability, node, and project-status queries are generally free.
- Operations that actually start or modify a TIA Portal project, compile, create an archive, download, or produce an engineering deliverable are billed individually by operation.
- Existing SkillPay balance is used first. If the balance is insufficient, WorkBuddy opens a WeChat Pay authorization screen labeled **AI Exclusive Card** by Tencent.
- Whether a failed or retried operation is billed—and the final amount charged—is determined by the server's actual settlement record and the current SkillHub listing. Prices are intentionally not hard-coded in this README.

## Installation

Find **SeedAgent TIA Portal Programming Agent** in WorkBuddy / SkillHub.

Alternatively, paste the following HTTPS link into a new WorkBuddy conversation and ask it to download, verify, and install the package:

`https://www.autohub-ai.com/downloads/seedagent/tia-programing/0.9.0/SeedAgent-TIA-Programming-Install-0.9.0-Windows-x64.zip`

At the time of publication, the version is 0.9.0. The version number in the URL will change with later updates. The 0.9.0 installer is only the starting point, and we may update the link from time to time.

Deliverables:

- Complete installer package: `SeedAgent-TIA-Programming-Install-0.9.0-Windows-x64.zip`
- Offline engineering-workstation package (WorkBuddy can provide this file during setup): `SeedAgent-TIA-Programming-Engineering-0.9.0-Windows-x64.zip`

Maintenance tools are retained under the installed product directory. Deleting the downloaded ZIP and temporary extraction folder does not remove restart and repair entry points.

The maintenance tools connect to the server to check for later versions and present them to the user, who decides whether to install an update.

## Roadmap

- LAD programming and modification.
- WinCC Unified screens, tags, alarms, and scripts.
- Reading and modifying device, industrial network, drive, and servo configuration.
- Reading and writing PLC variables through OPC UA, enabling AI to autonomously simulate and test whether program logic is correct.
- Asynchronous long-running tasks with cross-conversation recovery and result lookup.
- Additional Agent clients, English, and other languages.

Installation, pairing, programming, compilation, archiving, downloading, and recovery walkthrough videos will be published progressively.

## License and Rights

This is proprietary commercial software. This repository does not grant a source-code license. We retain the applicable rights to the software, documentation, branding, and original assets we develop. Third-party libraries and components remain subject to their respective licenses.

Siemens, SIMATIC, TIA Portal, STEP 7, S7-1200, and S7-1500 are trademarks or product names of their respective owners. This product is not affiliated with or endorsed by Siemens. These names are used solely to describe compatibility and intended use.

## Support and Feedback

Chinese-speaking users may join our official WeCom (WeChat Work) group, **SeedAgent 博途编程智能体用户群**, for product questions, feature suggestions, and regression feedback. WeCom is Tencent's enterprise messaging service and may be less accessible to users outside China.

![WeCom QR code for the SeedAgent TIA Portal Programming Agent user group](https://www.autohub-ai.com/downloads/seedagent/assets/wecom-user-group.png)

For international users, GitHub Issues is the recommended support channel. Both English- and Chinese-speaking users may use this repository's Issues for questions, suggestions, and publicly reproducible reports, or contact us through the SkillHub publisher page.

GitHub Issues are public. Do not post logs or screenshots containing customer project source code, device certificates, PLC addresses, payment credentials, personal information, or other sensitive material. For such cases, contact us first through a private official channel.
