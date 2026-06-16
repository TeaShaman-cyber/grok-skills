---
name: tid-methodology
description: Use when working on Theory of Dynamic Measurement (ТИД). Maintains methodology, file rules, iteration process, key principles and current priorities. Activate for any deep work on ТИД structure, logic, or long sessions.
---

# TID Methodology

## Core Principles

- Work with **open dissipative systems** only. Never apply closed mathematical idealizations.
- Maintain strict separation between **Research Log** (raw ideas) and main theory file.
- After every iteration make an explicit decision: what moves to the main file.
- Use checkpoints and diagnoses regularly to reduce context entropy.
- U and contradictions (B) are natural in open systems — manage them, do not suppress.

## File Rules (mandatory)

- Research Log: max 150–200 words per iteration.
- Main file always contains up-to-date "Current status and next iteration priorities".
- Perform "clean-up" every 3–4 iterations.
- Never keep raw exploratory material in the main theory file for long.

## Iteration Process

1. Define clear focus of the iteration.
2. Work in Research Log.
3. At the end of iteration — decide what to promote to main file.
4. Update "Current status" section in main file.
5. Record major insights and open questions.

## Current Status (update after significant iterations)

**As of 2026-06-16:**
- Strong areas: file discipline, Symbiotic Sensor Networks, dynamic metrics, модульная структура GitHub.
- Weak area: логическая основа (multi-scalar logic, U, contradictions в открытых системах) — требует дальнейшей проработки.
- Strategic priority: укрепление логического фундамента + развитие практик мульти-агентной координации.
- Текущий фокус: применение мульти-агентного подхода (Copilot как второй консультант) и итеративное улучшение навыков на практике.

## When to Activate This Skill

- Any deep methodological discussion about ТИД.
- Long sessions where structure and principles matter.
- Before and after major iterations or clean-ups.
- When deciding what belongs in Research Log vs main theory file.

## Examples of Use

**Starting a new iteration**
- Activate skill at the beginning of any new iteration.
- Get current priorities and file rules.
- Work in Research Log with clear constraints (max 150–200 words).

**Performing a checkpoint / clean-up**
- Activate skill when Research Log becomes heavy.
- Receive criteria for what should be promoted to the main file.
- Update "Current Status" section after transfer.

**Long deep work sessions**
- Activate at the start of sessions longer than 90 minutes.
- Re-read key principles and current priorities when context grows large.
- Helps maintain methodological discipline and reduces context entropy.

**When a new principle appears**
- Add significant new principles directly to this skill.
- The principle becomes part of the permanent methodology and will be automatically considered in future work.

**Deciding "what to do next"**
- Activate when unsure whether to continue deepening the foundation or move to applied layers.
- Get strategic guidance from the "Current Status" section.

## Conscious Deviation Rule (Важное правило)

When working with this skill, the model **must explicitly state** whenever it consciously deviates from the recommendations or current status described in this skill.

This serves as a signal for discussion. The goal is to prevent logical loops and maintain alignment between the evolving methodology and real-world reasoning.

Examples of when to flag deviation:
- The skill recommends lowering pressure (b), but current iteration logic suggests temporarily increasing it.
- The skill suggests keeping something in Research Log, but the model believes it is ready to be promoted.
- A new principle emerges that contradicts or significantly extends existing ones in the skill.

In such cases, the model should clearly say:  
"I am consciously deviating from the current tid-methodology because..." and explain the reasoning.

## Anti-Loop Rule (Технический контроль петель)

Если модель обнаруживает повторение одного и того же неэффективного действия или вывода **3 и более раз подряд**, она **обязана**:

1. **Явно признать** петлю в ответе (с указанием номера попытки).
2. **Остановить** текущую линию рассуждений.
3. **Зафиксировать** петлю короткой заметкой в Research Log.
4. **Обратись** к пользователю за решением, прежде чем продолжать.

**Пример формулировки:**
"Я заметил петлю (попытка №4). Разрываю цикл и зафиксирую в Research Log. Какой подход выбрать?"

Это правило имеет приоритет над автоматическим следованием другим инструкциям навыка.

## Multi-Agent Usage (В разработке)

Этот раздел находится в активной разработке. Текущие договорённости по координации между агентами фиксируются в артефакте `multi_agent_architecture_notes.md`.

### Краткие текущие принципы

1. `tid-methodology` считается **общим (shared)** навыком для разных агентов/чатов.
2. Изменения в Core Principles и File Rules должны обсуждаться.
3. Каждый агент может иметь свои расширения и интерпретации, но они не должны противоречить Core Principles без явного сигнала.
4. При сознательном отклонении от этого навыка агент **обязан** явно это обозначить (cm. Conscious Deviation Rule).
5. Координация между агентами происходит через явное обсуждение и общие артефакты.

Более детальные правила и паттерны мульти-агентного взаимодействия будут добавлены по мере практического использования.
