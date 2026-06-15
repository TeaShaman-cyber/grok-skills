# GitHub Actions — Модуль

Этот модуль содержит практические знания по GitHub Actions, CI/CD и автоматизации в экосистеме GitHub.

## Основные понятия

- **Workflow** — YAML-файл, описывающий автоматизированный процесс (`.github/workflows/*.yml`).
- **Job** — набор шагов, выполняющихся на одном runner'е.
- **Step** — отдельная команда или действие.
- **Action** — переиспользуемый блок (официальной, из Marketplace или свой).
- **Runner** — виртуальная машина, на которой выполняется workflow (GitHub-hosted или self-hosted).
- **Event** — событие, которое запускает workflow (push, pull_request, schedule и т.д.).

## Типичные сценарии использования

### 1. CI (Continuous Integration)

```yaml
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm test
```

### 2. CD (Continuous Deployment)

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
```

### 3. Matrix стратегия (тестирование на разных версиях/ОС)

```yaml
strategy:
  matrix:
    node-version: [18, 20, 22]
    os: [ubuntu-latest, windows-latest]
```

## Полезные практики

- Используй `actions/checkout@v4` всегда в начале.
- Кэшируй зависимости (`actions/cache` или специфичные экшены).
- Используй `secrets` для токенов и ключей.
- Разделяй большие workflows на несколько мелких job'ов.
- Используй `if` для условного выполнения шагов.
- Для сложной логики выноси код в composite actions или отдельные репозитории.

## Когда использовать GitHub Actions

**Plusy:**
- Глубокая интеграция с GitHub
- Бесплатные минуты для публичных репозиториев
- Большой Marketplace экшенов
- Хорошая поддержка self-hosted runners

**Minusy:**
- Vendor lock-in на GitHub
- Ограничения по времени выполнения на бесплатном тарифе
- Сложнее отлаживать по сравнению с некоторыми внешними CI

## Полезные ссылки

- Официальная документация: https://docs.github.com/actions
- Marketplace: https://github.com/marketplace?type=actions

---

*Модуль создан как часть экосистемного подхода к GitHub. Основной `github` skill остаётся focused на операциях.*
