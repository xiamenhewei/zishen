# 自审 · zishen

[![skills.sh](https://skills.sh/b/xiamenhewei/zishen)](https://skills.sh/xiamenhewei/zishen)

[中文](#中文) ｜ [English](#english)

---

## 中文

一个给 Claude Code（及兼容 Agent）用的**自审 Skill**：在动手改代码/落地方案之前，用一套 **14 条框架**系统地把方案或代码改动审一遍，逐条给出结论（通过 / 不通过 / 需补充），把问题挡在施工之前。

### 为什么需要它

AI 写代码最容易犯的错不是"写不出"，而是"没想全就动手"：漏了边界条件、改了数据字段没同步所有读取点、在错误的入口打补丁、重复造轮子……这个 Skill 把这些"踩过的坑"沉淀成 14 条 checklist，每次施工前强制过一遍。

### 核心铁规则

- **自审发现不通过，必须停下等用户确认**，禁止自审完自己改自己上。
- **自审通过 ≠ 开工许可**。通过只是汇报结论，必须等用户明确说"去做"才能动代码。

### 14 条框架

1. **需求符合性** —— 有没有多做、少做、歪曲
2. **第一性原理** —— 从根本出发，不过度设计
3. **遗漏和错误** —— 边界条件、异常、环境差异
4. **客观事实依据** —— 看代码/数据确认，禁止凭记忆猜
5. **复用已有模块** —— 含「参照物逐项对比」铁规则
6. **长期最优解** —— 考虑数据规模，不临时凑合
7. **根本问题** —— 治本不治标
8. **验证方法** —— 每个改动点同步想验证，且必须实跑
9. **影响范围** —— 含 DOM 操作、显示类漏点、数据字段语义三条子规则
10. **方案对齐** —— 验收时逐条对照批准方案
11. **共用路径** —— 多模式共发的 bug 必须改在共用代码
12. **多入口规则收敛** —— 同一动作多入口，规则收敛到统一函数
13. **优先用现成算法/库** —— 经典问题禁止重复造轮子
14. **运行时分支假设验证** —— 方案假设走某分支必须真跑验证，禁止凭代码阅读推断（代码里有分支 ≠ 运行时真走它）

每条都配「反面教材 / 正面教材」，告诉 AI 不该怎么做、应该怎么做。

### 安装

**Claude Code / 兼容 Agent：**

```bash
# 方式一：npx skills（会进 skills.sh 目录）
npx skills add xiamenhewei/zishen@自审

# 方式二：手动克隆到 skills 目录
git clone https://github.com/xiamenhewei/zishen.git ~/.claude/skills/自审
```

### 使用

安装后，对 AI 说：

- "自审一下这个方案"
- "把刚才的改动再审一遍"
- "过一遍清单"
- "审查这个代码改动"

AI 会按 14 条逐条给结论，最后汇总，等你指示。

### 文件结构

```
zishen/
├── SKILL.md      # Skill 主体（14 条框架 + 铁规则）
└── README.md     # 本文件
```

### License

MIT

---

## English

> **zishen (自审)** means "self-review" in Chinese — review your plan or code change *before* you build.

A **self-review Skill** for Claude Code (and compatible agents): before touching code or executing a plan, run it through a **14-point framework** that systematically audits the proposal or code change, giving a verdict per point (Pass / Fail / Needs-more), so problems are caught *before* implementation.

### Why

The most common AI coding mistake isn't "can't write it" — it's "acting before thinking it through": missing edge cases, changing a data field without syncing every read site, patching the wrong entry point, reinventing the wheel... This Skill distills those hard-won lessons into a 14-point checklist enforced before every build.

### Core rules

- **If any point fails, stop and wait for the user.** Never self-correct and proceed.
- **Passing review ≠ permission to build.** A pass only means "report the verdict"; you must wait for an explicit "go" before changing code.

### The 14 points

1. **Requirements fit** — nothing extra, missing, or distorted
2. **First principles** — root cause, no over-engineering
3. **Gaps & errors** — edge cases, exceptions, env differences
4. **Factual basis** — verify against real code/data, no guessing from memory
5. **Reuse existing modules** — includes the "item-by-item comparison" rule
6. **Long-term optimum** — plan for scale, no band-aids
7. **Root cause** — fix the disease, not the symptom
8. **Verification method** — think verification per change, and actually run it
9. **Blast radius** — includes DOM-order, display-field-leak, and data-field-semantics sub-rules
10. **Plan alignment** — check final result against the approved plan, point by point
11. **Shared code path** — bugs affecting multiple modes must be fixed in shared code
12. **Multi-entry convergence** — one action with many entries: rules converge to one handler
13. **Prefer existing libraries** — never reinvent the wheel for solved problems
14. **Runtime branch verification** — if the plan assumes code takes a branch, verify by actually running it; reading code/grep can't tell which branch executes at runtime

Each point ships with a counter-example and a positive example, telling the AI what *not* to do and what to do instead.

### Install

**Claude Code / compatible agents:**

```bash
# Option 1: npx skills (lists on skills.sh)
npx skills add xiamenhewei/zishen@自审

# Option 2: clone into your skills dir
git clone https://github.com/xiamenhewei/zishen.git ~/.claude/skills/自审
```

### Usage

After installing, tell the AI:

- "self-review this plan"
- "run the checklist on that change again"
- "audit this code change"

The AI walks the 14 points, gives a verdict per point, summarizes, and waits.

### License

MIT
