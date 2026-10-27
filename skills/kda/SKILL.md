---
name: kda
description: 使用 NVIDIA Kernel Design Agents 工作流开发和优化 CUDA GPU kernel；在用户要求使用 KDA、自动调优算子或进行有正确性与性能证据的 kernel 迭代时使用。
---

# KDA：Codex 入口

本技能是对 [NVlabs/kda](https://github.com/NVlabs/kda) 的本地 Codex 适配，基于上游 acdd793。上游工作流文档和提示词采用 CC BY 4.0，见本仓库 LICENSE；本适配沿用该许可。它提供工作流，不包含 GPU 执行环境。

## 执行流程

1. 阅读目标项目的规则和现有实现。在目标项目或独立任务工作区内修改代码；本 KDA 仓库仅作为参考。
2. 定义任务契约：输入输出、shape、dtype、GPU 架构、精度容差、允许的实现方式、正确性命令、测速命令和接受标准。优先从项目现有配置推导，只询问影响执行的缺失条件。
3. 按需阅读本仓库 `docs/agent-flow.md` 和 `prompts/basic-flow.md`。这些路径相对于本技能所在仓库根目录，而非用户任务目录。
4. 在任务工作区写入 `docs/draft.md`，明确基线、风险、候选方案和验证方式，再整理为可执行的 `docs/plan.md`。使用 Codex 的规划能力，不依赖 Claude Code 的 humanize 插件。
5. 每次实现一个候选，先验证正确性，再在同一硬件、输入和计时协议下与基线比较。按目标仓库规则提交每次修改。
6. 按需用 `candidates.jsonl` 记录候选及父候选、接受或拒绝原因，用 `benchmark.csv` 记录性能，用 `profile/` 保存 profiling 证据。保留可复现的命令和环境信息。
7. 只有符合任务契约且有实测证据的候选才能晋级。报告已测结果、未验证项目和剩余阻碍；不从静态代码推断提速。

## 配套技能与环境

- 优化 Blackwell/Hopper kernel 时，按需读取已安装的 `KernelWiki` 技能。其知识截止日期为 2026-04-27；架构特有技巧不可直接套用到其他 GPU。
- 本机已为知识库配置独立 Python 环境。运行查询脚本时使用 `/Users/bytedance/.codex/skills/KernelWiki/.venv/bin/python`，例如：`/Users/bytedance/.codex/skills/KernelWiki/.venv/bin/python /Users/bytedance/.codex/skills/KernelWiki/scripts/query.py --tag nvfp4 --type kernel --compact`。直接调用知识库技能时也使用此解释器；其他机器使用其自己的 Python 环境。
- 分析 Nsight Compute 报告时，按需读取已安装的 `ncu-report-skill` 技能。实际 profiling 需要 NVIDIA GPU、CUDA Toolkit、`ncu` 及随其提供的 `ncu_report` Python 模块。
- Mac 可运行知识库查询。GPU 验证和测速在用户指定且已授权的 NVIDIA 主机上执行；主机不可用时，明确执行限制，不声称完成性能验证。
- 用户与目标仓库的执行限制优先。例如禁止本地运行时使用允许的静态检查，并将 GPU 正确性和性能列为未验证。
