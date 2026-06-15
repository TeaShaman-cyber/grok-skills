# Git Flow и стратегии ветвления — Модуль

Этот модуль содержит практические рекомендации по организации ветвления (branching strategy) в Git и работе с GitHub.

## Основные стратегии ветвления

### 1. Git Flow (классика)

**Vetvi:**
- `main` / `master` — стабильная продакшн-версия
- `develop` — основная ветка разработки
- `feature/*` — новые фичи
- `release/*` — подготовка релизов
- `hotfix/*` — срочные исправления в продакшене

**Plusy:**
- Чёткая структура
- Хорошо подходит для проектов с долгим циклом релизов
- Понятна командам, привыкшим к waterfall-подходу

**Minusy:**
- Сложная для маленьких команд и быстрых итераций
- Много долгоживущих веток
- Сложнее с continuous delivery

### 2. Trunk-Based Development (рекомендуется для большинства современных команд)

**Osnovnaya ideya:**
- Есть одна основная ветка (`main` / `trunk`)
- Все разработчики регулярно мёржат в неё (минимум 1 раз в день)
- Фичи разрабатываются через короткоживущие ветки или feature flags
- CI/CD запускается на каждое изменение в `main`

**Plusy:**
- Фысокая скорость поставки
- Меньше конфликтов
- Лучше continuous integration
- Проще с feature flags

**Minusy:**
- Требует хорошей культуры code review и автоматизированного тестирования
- Не всегда подходит для очень больших команд без feature flags

### 3. GitHub Flow (упрощённый)

**Osnovnaya ideya:**
- `main` всегда deployable
- Все изменения идут через Pull Request в `main`
- Короткоживущие ветки
- CI проверяет каждый PR

**Kogda ispolzovat:**
- Небольшие и средние команды
- Веб-приложения и SaaS с частыми деплоями
- Когда важна простота

## Рекомендации

### Для большинства команд (Текущий 2026 год):

**Trunk-Based Development + Pull Requests + Feature Flags** — лучший баланс скорости, качества и простоты.

### Практические правила:

1. **Main всегда зелёный**
   - В `main` должен быть только код, который проходит все проверки и может быть задеплоен.

2. **Короткоживущие ветки**
   - Идеально — до 1–2 дней жизни ветки.
   - Длинные ветки = большие конфликты и риск.

3. **Регулярные мёржи в main**
   - Лучше маленькие частые PR, чем один большой в конце спринта.

4. **Защищённые ветки**
   - Включи branch protection rules на `main`:
     - Требовать PR
     - Требовать прохождение CI
     - Требовать approval (опционально)

5. **Feature Flags вместо длинных веток**
   - Если фича большая — прячь её за feature flag, а не за долгоживущей веткой.

## Типичные сценарии

### Маленькая команда / стартап
→ Trunk-Based Development + GitHub Flow

### Средняя команда с частыми релизами
→ Trunk-Based + Feature Flags + CI/CD на каждый коммит

### Большая команда / enterprise с долгим циклом QA
→ Git Flow или его модификации

### Open Source проект
→ GitHub Flow (максимальная простота и прозрачность)

## Полезные практики в GitHub

- Используй **Draft PR** для WIP (work in progress)
- Включи **auto-merge** для маленьких безопасных изменений
- Используй **CODEOWNERS** файл для автоматического назначения ревьюеров
- Настрой **branch protection rules** на `main`

## Примеры команд Git (Git Flow)

### Инициализация Git Flow в репозитории

```bash
git flow init
```

### Работа с feature-ветками

```bash
# Начать новую фичу
git flow feature start my-new-feature

# Закончить фичу (мёрж в develop + удаление ветки)
git flow feature finish my-new-feature

# Опубликовать фичу на удалённый репозиторий
git flow feature publish my-new-feature

# Получить чужую опубликованную фичу
git flow feature pull origin my-new-feature
```

### Работа с release-ветками

```bash
# Начать подготовку релиза
git flow release start 1.2.0

# Закончить релиз (мёрж в main и develop, создание тега)
git flow release finish 1.2.0

# Опубликовать релиз
git flow release publish 1.2.0
```

### Работа с hotfix-ветками

```bash
# Начать hotfix (от main)
git flow hotfix start 1.2.1

# Закончить hotfix
git flow hotfix finish 1.2.1
```

### Полезные алиасы (добавить в `~/.gitconfig`)

```ini
[alias]
    # Git Flow shortcuts
    fs = "!git flow feature start"
    ff = "!git flow feature finish"
    rs = "!git flow release start"
    rf = "!git flow release finish"
    hs = "!git flow hotfix start"
    hf = "!git flow hotfix finish"
```

---

*Модуль создан как часть экосистемного подхода к GitHub. Основной `github` skill остаётся focused на операциях.*
