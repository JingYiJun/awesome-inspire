# Awesome Inspire

一个面向启智平台（Inspire）的 awesome list，收集 GitHub 上和 CLI、MCP、SSH、隧道、自动化脚本及相关依赖生态有关的项目。

最后检索日期：`2026-03-27`

## 收录范围

- 直接相关：仓库明确面向启智平台，直接提供 notebook、job、workspace、compute group、SSH、资源查询等能力。
- 间接相关：仓库本身不是启智专用，但被启智工具链直接依赖，用来补齐 SSH、MCP、隧道或无头环境适配。
- fork 生态：只要 fork 已经表现出独立维护、功能试验或团队定制价值，就保留索引。

## 目录

- [CLI 与一站式工作流](#cli-与一站式工作流)
- [任务管理、MCP 与批量调度](#任务管理mcp-与批量调度)
- [SSH、隧道与远程访问](#ssh隧道与远程访问)
- [无头环境工具链](#无头环境工具链)
- [Fork 生态](#fork-生态)
- [维护信号速览](#维护信号速览)
- [选型建议](#选型建议)

## CLI 与一站式工作流

- [EmbodiedForge/Inspire-cli](https://github.com/EmbodiedForge/Inspire-cli)  
当前公开可见中产品化程度最高的一类启智平台 CLI，目标不是单点脚本，而是把配置发现、资源查询、notebook 管理、job 提交、SSH 隧道、代码同步、镜像管理和 Bridge 操作统一起来。  
功能：`init --discover`、`job`、`notebook`、`image`、`project`、`resources`、`bridge exec/ssh/scp`、`sync`。  
亮点：把“平台 API + notebook 隧道 + 本地开发工作流”串成一条完整链路。  
关系：直接相关，适合作为总入口项目。  
- [realZillionX/Inspire-cli](https://github.com/realZillionX/Inspire-cli)  
`Inspire-cli` 的中文化发行分支，公开文档明显更偏实验室落地与首次接入说明。  
功能：继承上游的一站式 CLI 能力，覆盖 notebook、分布式训练、高性能计算、SSH 隧道、镜像与同步。  
亮点：更强调中文用户场景、真实入口地址和一次性配置流程。  
关系：直接相关，`EmbodiedForge/Inspire-cli` 的 fork。  
- [JingYiJun/Inspire-cli](https://github.com/JingYiJun/Inspire-cli)  
一个已经表现出独立功能方向的 fork，重点强化 HPC / Slurm 风格任务、workspace-aware 镜像与更实操的运维文档。  
功能：GPU job、HPC job、notebook 管理、镜像浏览、SSH/Bridge、代码同步。  
亮点：把启智里的 HPC 任务做成一级命令，而不是边角能力。  
关系：直接相关，`EmbodiedForge/Inspire-cli` 的 fork。

## 任务管理、MCP 与批量调度

- [tianyilt/qzcli_tool](https://github.com/tianyilt/qzcli_tool)  
更偏“平台黑客工具”的启智 CLI，重心在登录、资源发现、空闲节点查询、任务创建、批量提交和状态监控。最大的特点是仓库内直接提供 `qzcli-mcp`。  
功能：`login`、`res -u`、`avail`、`ls`、`create`、`hpc`、`batch`、`ws`、`qzcli-mcp`。  
亮点：既能做人类高频运维，也能直接接进 Codex / Claude Code 的 MCP 工具链。  
关系：直接相关，是启智任务管理工具生态的核心仓库之一。  
- [ppolariss/qzcli_tool](https://github.com/ppolariss/qzcli_tool)  
一个结构性重构 fork，不只是同步上游，而是在重新整理命令接口与资源解析模型。  
功能：`catalog` 资源目录、`avail` 资源查询、`create` / `create-hpc`、`batch`、`qzcli-mcp`。  
亮点：把 `res` 明确重命名为 `catalog`，并加强 workspace alias 与资源唯一解析策略。  
关系：直接相关，`tianyilt/qzcli_tool` 的高价值 fork。

## SSH、隧道与远程访问

- [JingYiJun/qz_ssh_starter](https://github.com/JingYiJun/qz_ssh_starter)  
一个非常典型的“补齐平台原生缺口”的脚本项目，核心目标是让启智里的 notebook / 容器快速具备稳定 SSH 能力。  
功能：自动安装 `openssh-server` 与 `rtunnel`、写入公钥、输出 SSH 命令与 `~/.ssh/config` 片段、支持 `stop` / `stop-all`。  
亮点：显式适配启智不同资源空间的 `VC_BASE_HOST`，并对 GitHub 镜像下载做测速与持久化选择。  
关系：直接相关，适合需要本地 IDE / 终端接管启智容器的人。  
- [Sarfflow/rtunnel](https://github.com/Sarfflow/rtunnel)  
虽然不是启智专用仓库，但它是启智 SSH 生态里最关键的基础设施之一。  
功能：WebSocket / WSS 下的 TCP 隧道、客户端/服务端双模式、TLS、ACK/重传、窗口控制、心跳与自动重连。  
亮点：不是只求“能通”，而是把可靠传输做到应用层，适合长连接 SSH / SCP / ProxyCommand。  
关系：间接相关，属于启智远程访问方案的核心依赖。

## 无头环境工具链

- [ShacklesLay/setup-lark-mcp](https://github.com/ShacklesLay/setup-lark-mcp)  
一个专门解决“在启智这种无头远程服务器上稳定使用飞书 MCP”问题的脚本仓库。  
功能：安装 `gnome-keyring` / `libsecret`，通过 `dbus-run-session` 包裹 `lark-mcp`，并附带飞书官方 skills。  
亮点：直接针对 OpenI / AIStation / 启智这类 headless 环境处理 token 持久化问题。  
关系：间接相关，是启智远程 agent 工具链的增强项目。

## Fork 生态

### `Inspire-cli`

- [y-tarl/Inspire-cli](https://github.com/y-tarl/Inspire-cli)  
接近上游阶段性快照，保留了 `personal-visible` 镜像源、平台感知 `rtunnel` 下载 URL 等改动。  
关系：直接相关。  
状态：更像近上游镜像，不像独立路线。  
- [ADIOCLASSMATE/Inspire-cli](https://github.com/ADIOCLASSMATE/Inspire-cli)  
在 notebook 交互流之外额外补了一批 `tools/gpu-*` 脚本，更偏实验室内部运维工具箱。  
关系：直接相关。  
状态：有独立脚本化倾向。  
- [YangW796/Inspire-cli](https://github.com/YangW796/Inspire-cli)  
最近维护集中在 Playwright / web session 兼容性修补。  
关系：直接相关。  
状态：技术性补丁分支。  
- [kaysonyu/Inspire-cli](https://github.com/kaysonyu/Inspire-cli)  
改动集中在 job 逻辑、GitHub 下载辅助与实验汇总 workflow。  
关系：直接相关。  
状态：偏团队工作流定制。

### `qzcli_tool`

- [qiyuangong/qzcli_tool](https://github.com/qiyuangong/qzcli_tool)  
目前公开 diff 很轻，主要是 `cli.py` 微调。  
关系：直接相关。  
状态：轻量个人分支。  
- [BraveDrXuTF/qzcli_tool](https://github.com/BraveDrXuTF/qzcli_tool)  
代表性改动是登录流程中 RSA 密文前导零修复。  
关系：直接相关。  
状态：稳定性修补分支。  
- [hairuoliu1/qzcli_tool](https://github.com/hairuoliu1/qzcli_tool)  
承接过 MCP 支持功能的集成，再由其他分支回流。  
关系：直接相关。  
状态：短期功能中转分支。  
- [kevin-wen1/qzcli_tool](https://github.com/kevin-wen1/qzcli_tool)  
重点补了 HPC `logs` 与 `perf` 两个高价值子命令。  
关系：直接相关。  
状态：功能孵化分支，且已向上游输送特性。  
- [Hashmapw/qzcli_tool](https://github.com/Hashmapw/qzcli_tool)  
早期承担登录修复与 MCP 打样。  
关系：直接相关。  
状态：问题修复 / 功能试验台。  
- [ashun989/qzcli_tool](https://github.com/ashun989/qzcli_tool)  
补了 `prune` 命令，用于清理归档任务历史。  
关系：直接相关。  
状态：日常运维能力增强分支。  
- [ekonwang/qzcli_tool](https://github.com/ekonwang/qzcli_tool)  
重点扩展了交互式建模列表与基于 Jupyter API 的远程执行。  
关系：直接相关。  
状态：高价值功能孵化分支，已被上游吸收一部分。  
- [Stepuuu/qzcli_tool](https://github.com/Stepuuu/qzcli_tool)  
修复了关键的 RSA 前导零兼容性 bug，并补了测试。  
关系：直接相关。  
状态：小而关键的补丁分支。

### `qz_ssh_starter`

- [dest1n1s/qz_ssh_starter](https://github.com/dest1n1s/qz_ssh_starter)  
主要改动集中在 `install_rtunnel.sh` 的 shell 检测与 PATH 处理。  
关系：直接相关。  
状态：做过本地安装体验修复，但目前已落后于上游。

## 维护信号速览

- `EmbodiedForge/Inspire-cli`：主线仓库，持续维护。
- `realZillionX/Inspire-cli`：活跃，偏发行整理与中文落地。
- `JingYiJun/Inspire-cli`：活跃，偏 HPC 独立功能线。
- `tianyilt/qzcli_tool`：活跃，上游会吸收 fork 特性。
- `ppolariss/qzcli_tool`：活跃，偏结构重构。
- `kevin-wen1/qzcli_tool`：活跃，偏 HPC 运维增强。
- `ekonwang/qzcli_tool`：活跃，偏 notebook / dev machine 运维增强。
- `JingYiJun/qz_ssh_starter`：活跃，仍在跟进资源空间信息。
- `Sarfflow/rtunnel`：仓库规模较小，但对启智生态价值高。

## 选型建议

- 如果你想找“总入口 CLI”，先看 [EmbodiedForge/Inspire-cli](https://github.com/EmbodiedForge/Inspire-cli)。
- 如果你更关心“资源查询 + 批量起任务 + MCP”，先看 [tianyilt/qzcli_tool](https://github.com/tianyilt/qzcli_tool)。
- 如果你最痛的是“怎么稳定 SSH 进启智容器”，先看 [JingYiJun/qz_ssh_starter](https://github.com/JingYiJun/qz_ssh_starter) 和 [Sarfflow/rtunnel](https://github.com/Sarfflow/rtunnel)。
- 如果你在启智上跑 Claude Code / agent，想补飞书能力，看 [ShacklesLay/setup-lark-mcp](https://github.com/ShacklesLay/setup-lark-mcp)。

## License

[MIT](./LICENSE)
