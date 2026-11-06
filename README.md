# RootFirst

**5Why × First Principles — fused at the exact point where drilling stops working.**

一个把「5Why 追问」和「第一性原理」真正接在一起的 Agent Skill。
接口是追问卡住的那一刻，出口是一条有实测证据支撑的结论。

[English](#english) · [中文](#中文)

---

## English

### Why not just use them separately

**5Why alone** drills down until it hits a wall — "that's just how it's done", "everyone does it this way", "it's the convention". A drill cannot argue with a convention. So you fix a habit, call it a root cause, and the problem comes back wearing a different face.

**First principles alone** can break through any wall, but it doesn't know where to start. A complex problem decomposes in ten directions; decomposing all ten is unbounded work, and you end up reinventing the wheel without ever touching the original pain.

Each one's weakness is exactly what the other fixes.

### The fusion: the stall point is the handoff point

Ask why until the answer hardens into an unexamined assumption. **That sentence is the target.** Split it in two:

- **Real constraints** — physics, math, genuine cost/time/headcount ceilings, law, safety, compatibility. Each one must state what concretely goes wrong if violated.
- **Inherited habits** — someone's temporary choice back then, "industry convention" nobody can justify, a shortcut taken to ship fast. These are **void** and can be re-chosen.

Anything that cannot state a concrete consequence of violation goes in the habits pile.

Then rebuild from the constraints only, walk back up the chain, and verify the load-bearing assumption.

### The two steps that make it close

**Walking back up** catches half-fixes. Every worked example here shows the same failure: do only half the changes and some layer stays unexplained. Add a verification gate but no routing, and "the agent can't find the skill" is still unsolved — the skill being correct doesn't help if nothing surfaces it.

**Verifying the load-bearing assumption** catches false ground. Logical coherence is not factual truth. Skip this and the whole method is just issuing itself a certificate.

| | Load-bearing | Peripheral |
|---|---|---|
| Test | "If this is false, does the solution still work?" **No** → load-bearing | Works, just less well → peripheral |
| Action | **Verify now**, cheapest available method | Note it, watch while doing |
| If it fails | Solution is void — go back and re-split the target | Adjust details, keep the skeleton |
| Count | Usually one or two | Everything else |

> Load-bearing verification should always be cheap. If it's expensive, you probably picked the wrong assumption.

Until a load-bearing assumption has real evidence, the output is marked **pending** and must not be treated as an established conclusion for anything consequential.

### Flow

```
1 Pin down the symptom
2 Ask why ──reached something actionable──→ 5 Walk back up → 6 List assumptions → 7 Verify ground → Close
   │                                                ↑                        │
   └─hit "everyone does it this way"→ 3 Split → 4 Rebuild ┘                  │
                                                              assumption falsified
                                                                    ↓
                                                          back to step 3, re-split
```

**Closing condition**: every load-bearing assumption has measured evidence, or the target has been re-split and the new ground verified. Peripheral assumptions may stay open — demanding all of them be verified means the analysis never closes.

### Install

Flat layout, so one clone is the whole install:

```bash
# Qoder
git clone https://github.com/<your-username>/rootfirst ~/.qoder-cn/skills/rootfirst

# Claude Code
git clone https://github.com/<your-username>/rootfirst ~/.claude/skills/rootfirst

# Any agent that reads SKILL.md
git clone https://github.com/<your-username>/rootfirst <your-skills-dir>/rootfirst
```

Restart the agent so it reloads skills.

### Usage

```
/rootfirst 我们的技能库攒了几百条，但实际被用上的没几条
```

Prefer the explicit command. Without it, the skill only activates in three situations: a requirement too vague to act on, a design tradeoff needing defensible justification, or the same problem returning after it was supposedly fixed. It stays out of everything else.

Natural-language triggers: 5why, first principles, root cause, 根因分析, 第一性原理, 从根本上想想, 为什么总是.

**Not for** single reproducible crashes or test failures — those belong in a debugging workflow with evidence and reproduction.

### Output

Two tiers, chosen by whether the drilling hit a wall:

- **Light** — reached an actionable cause, no wall: symptom → chain → fix → walk-back → ground check. Around a dozen lines.
- **Full** — hit a wall: adds target decomposition (constraints vs. habits), rebuild rationale, and why existing solutions can't be reused. About a page.

Both tiers always include the walk-back and the ground check.

### Files

| File | Contents |
|---|---|
| [SKILL.md](SKILL.md) | The method: 7 steps, closing condition, tiered output format, 8 anti-patterns |
| [examples.md](examples.md) | Five fully worked examples — one light tier, four full tier |

The four full-tier examples cover skill libraries, stock investing, recurring bug classes, and ML experiment design.

### Anti-patterns

Eight are listed in [SKILL.md](SKILL.md#反模式出现即为失败). The three that bite hardest:

1. **Padding to five whys** — layers four and five are usually filler. Stop at three if three is enough.
2. **Treating a habit as a constraint** — "everyone uses X" is not a constraint.
3. **Listing assumptions and moving on** — the judge is on paper but never seated on the bench.

---

## 中文

### 为什么不能分开用

**只用 5Why**：往下钻，钻到某一层会突然钻不动——「当初就是这么设计的」「大家都这么做」「这是规范」。钻头没法反驳一句惯例，于是你修掉一个习惯，把它叫根因，问题过阵子换个样子又回来。

**只用第一性原理**：它能砸穿任何墙，但不知道该从哪儿开始拆。一个复杂问题能拆十个方向，全拆就是无限扩张，最后轮子重新发明了一遍，原来那个痛根本没碰。

两者的短板正好是对方能补的。

### 融合点：卡住的那一层就是切换点

往下追问，直到答案变成一句没被检验过的假设。**那句话就是靶子。** 拆成两堆：

- **硬约束** —— 物理、数学、成本/时间/人力的真实上限、法规、安全、兼容性。每条必须说得出「违反它会发生什么具体的坏事」。
- **历史习惯** —— 前人当时的临时选择、说不出理由的「业界惯例」、当初图快走的捷径。这些**全部作废**，可以重选。

说不出违反后果的，一律归入习惯堆。

然后只用硬约束重建方案，倒回追问链逐层交代，最后验掉承重的那条假设。

### 让它真闭环的两步

**反向校验**抓的是「只做一半」。这里的每个完整档例子都演示了同一个失败：只改一半，某一层就交代不掉。只加验证闸门不加路由，「Agent 找不到技能」这层照样没解决——技能再合格，没人把它推到面前也白搭。

**验地基假设**抓的是「地基本身是假的」。逻辑自洽不等于事实为真。少了这步，整套方法就是自己给自己发合格证。

| | 地基假设 | 边角假设 |
|---|---|---|
| 判定 | 问「这条不成立，方案还能用吗？」不能用 → 地基 | 能用、只是效果差些 → 边角 |
| 处理 | **当场就验**，用最省事的验法 | 记下来，边做边看 |
| 验不过 | **方案作废，退回重拆靶子** | 调细节，不动骨架 |
| 数量 | 通常一两条 | 剩下全归这儿 |

> 地基验证应该总是很便宜。如果它很贵，通常说明你挑的地基不对。

地基假设拿到实测证据之前，输出必须标成**待验证**，不得当成已成立的结论去做大动作。

### 流程

```
1 锁定现象
2 往下追问 ──追到能动手──→ 5 反向校验 → 6 列假设 → 7 验地基 → 关闭
   │                                      ↑                  │
   └─撞到「大家都这样」→ 3 拆靶子 → 4 重建 ┘                  │
                                                     地基假设被证伪
                                                          ↓
                                                    退回第 3 步重拆
```

**关闭条件**：地基假设全部有实测证据，或已回炉重拆、新地基已验。边角假设可以挂着——要求全验完，分析就永远关不掉。

### 安装

扁平结构，一条 clone 就是完整安装：

```bash
# Qoder
git clone https://github.com/<your-username>/rootfirst ~/.qoder-cn/skills/rootfirst

# Claude Code
git clone https://github.com/<your-username>/rootfirst ~/.claude/skills/rootfirst

# 任何读 SKILL.md 的 agent
git clone https://github.com/<your-username>/rootfirst <你的-skills-目录>/rootfirst
```

装完重启 agent 让它重新加载。

### 用法

```
/rootfirst 我们的技能库攒了几百条，但实际被用上的没几条
```

优先用显式命令。没有命令时只在三种情况自动启用：需求模糊到没法动手、方案取舍需要站得住的依据、同一个问题「修好了」又回来。其余情况不主动插进来。

自然语言触发词：5why、第一性原理、根因分析、从根本上想想、为什么总是。

**不适用**：单次可复现的报错、测试失败、崩溃——那属于要有证据链和复现步骤的调试流程。

### 输出

分两档，由追问有没有撞墙决定：

- **轻量档** —— 追到可动手的原因，没撞墙：现象 → 追问链 → 方案 → 反向校验 → 地基验证。十几行。
- **完整档** —— 撞墙了：多出靶子拆解（硬约束 vs 历史习惯）、重建理由、以及为什么现成方案不能复用。一页左右。

**两档都必须有反向校验和地基验证。**

### 文件

| 文件 | 内容 |
|---|---|
| [SKILL.md](SKILL.md) | 方法本体：7 步、关闭条件、分级输出格式、8 条反模式 |
| [examples.md](examples.md) | 五个走完流程的实例——一个轻量档，四个完整档 |

四个完整档分别覆盖：技能库、股票投资、反复出现的同类 bug、算法实验设计。

### 反模式

完整 8 条见 [SKILL.md](SKILL.md#反模式出现即为失败)。最容易犯的三条：

1. **硬凑五轮** —— 第 4、5 轮多半是废话，三层能收工就三层。
2. **把习惯当约束** —— 「大家都用 X」不是硬约束。
3. **列了假设不验就当结论用** —— 裁判写在纸上，却没请上审判席。

---

## License

MIT © 2026 h4444433333
