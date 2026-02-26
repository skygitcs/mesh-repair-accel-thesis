# mesh-repair-accel-thesis

本仓库为毕业设计总工作区，用于组织与复现“网格修复加速”相关的代码、实验脚本与结果。
核心思路是在保持修复输出拓扑正确性约束的前提下，将快速求交与结构化拆分模块集成到修复流水线的关键瓶颈环节，实现端到端吞吐提升。

> 说明：本仓库使用 Git submodule 管理两个上游代码库（修复框架 A 与求交框架 B），主仓库仅记录并锁定子模块的具体版本，便于复现与回滚。

---

## 目录结构
```txt
├── repos/
│ ├── A_visual_repair/ # 子模块：网格修复框架（A）
│ └── B_fast_arrangement/ # 子模块：网格求交/排列框架（B）
├── .gitmodules # submodule 配置
└── README.md
```

后续建议逐步补齐以下目录（用于工程化与论文复现）：

```txt
scripts/ # 批处理、计时剖析、验证、统计等脚本
data/ # 数据子集（建议只存清单与少量样例；大数据放外部路径）
outputs/ # baseline/ 与 accel/ 的输出、日志、统计表
docs/ # 设计文档、实验日志、里程碑记录
```

---

## 快速开始

### 方式一：首次克隆（推荐）
在 Git Bash（或任意终端）中执行：

```bash
git clone --recurse-submodules https://github.com/<your-username>/mesh-repair-accel-thesis.git
cd mesh-repair-accel-thesis
```

### 方式二：已克隆但未拉取 submodule
```bash
git submodule update --init --recursive
```

---

## 子模块版本锁定与更新原则
- 主仓库记录的是子模块的“提交指针”，因此任何一次实验都可以精确复现使用的 A/B 版本。
- 当你在 A 或 B 中提交了新改动，需要在主仓库“推进子模块指针”，否则主仓库不会反映子模块更新。

## 在子模块内开发（示例：修改 A）
```bash
cd repos/A_visual_repair
git checkout -b accel-integration
# 修改代码...
git add .
git commit -m "Integrate arrangement module (WIP)"
git push -u origin accel-integration
```

回到主仓库记录子模块新指针：
```bash
cd ../../
git add repos/A_visual_repair
git commit -m "Bump A submodule pointer"
git push
```

> 修改 B 的流程相同。

---

## 构建与运行（占位说明，后续补齐）
- A_visual_repair 与 B_fast_arrangement 的编译方式、依赖与运行入口请优先参考各自子模块仓库内的说明文档（README / docs）。
- 本毕业设计后续将在 `scripts/` 中提供：
  - 基线运行脚本（baseline）
  - 加速版本运行脚本（accel）
  - 分阶段计时剖析（profiling）
  - 拓扑正确性验证（validation）
  - 统计汇总与出图（reporting）

---

## 常见问题
1. **子模块目录为空或缺少内容**
通常是未初始化 submodule。执行：
```bash
git submodule update --init --recursive
```

2. **提示 “LF will be replaced by CRLF”**
这是 Windows 下 Git 的行尾转换提示，不影响 submodule 正常使用。
如需减少提示，可在本机设置（按你的习惯选择其一）：
- 推荐保持默认（不必处理）
- 或者设置为自动转换：
```bash
git config --global core.autocrlf true
```
- 或者不自动转换：
```bash
git config --global core.autocrlf false
```

---

## 许可与引用
- 子模块各自遵循其原仓库许可证与引用要求。
- 本仓库仅作为毕业设计工程化组织与复现入口。


