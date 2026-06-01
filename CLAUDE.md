# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

# AI 编程心法约束

写代码时严格遵循以下 4 条：

## 1. YAGNI(用不到不要做)
- 用最简单的实现满足当前需求
- 不要为未来可能的扩展提前设计抽象层
- 不留 TODO/未来扩展位
- 1 种实现就别造工厂模式

## 2. KISS(保持简单)
- 能用普通函数解决的，不要用类
- 能用 if-else 解决的，不要用 Strategy 模式
- 优先可读性，不优先"看起来专业"
- 5 行能写完的，不要用 50 行

## 3. 命名是设计
- 变量名/函数名要精确说明它装的是什么/做什么
- 不要用 data / temp / helper / util / manager 这种通用名
- 函数名里不要用 do / process / handle 这种空动词
- 如果需要注释解释命名，先改名字

## 4. Fail Fast(快速失败)
- 不要 catch 你不知道怎么处理的异常
- 在数据边界(API 输入、DB 输出)校验输入，出错立即抛具体异常
- 报错信息要包含"是什么值导致的"
- 绝不允许 silent fail / try： ... except： pass
