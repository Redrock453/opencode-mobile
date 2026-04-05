# Установка OpenCode на телефон (Termux / Android)

Полная пошаговая инструкция для установки OpenCode на Android-телефон через Termux.

---

## Шаг 1: Установи Termux

Скачай Termux **только** из F-Droid (версия из Google Play устарела):
- https://f-droid.org/packages/com.termux/

Или напрямую APK:
- https://github.com/termux/termux-app/releases

## Шаг 2: Обнови пакеты и установи зависимости

Открой Termux и выполни по очереди:

```bash
# Обновляем всё
pkg update && pkg upgrade -y

# Устанавливаем необходимые пакеты
pkg install -y git nodejs curl wget
```

## Шаг 3: Установи Bun (менеджер пакетов для opencode)

```bash
# Устанавливаем bun
curl -fsSL https://bun.sh/install | bash

# Перезагружаем окружение
source ~/.bashrc
```

Проверь что bun установился:
```bash
bun --version
```

## Шаг 4: Установи OpenCode

### Вариант A — Через npm (самый простой, рекомендуется)

```bash
npm i -g opencode-ai@latest
```

### Вариант B — Через install-скрипт

```bash
curl -fsSL https://opencode.ai/install | bash
```

### Вариант C — Из моего репозитория (полный исходник с плагинами)

```bash
# Клонируем репозиторий
git clone https://github.com/Redrock453/opencode-mobile.git
cd opencode-mobile

# Устанавливаем зависимости
bun install

# Запускаем в режиме разработки
bun dev
```

## Шаг 5: Настрой API-ключ

OpenCode поддерживает множество провайдеров. Выбери один:

### OpenAI
```bash
export OPENAI_API_KEY="твой-ключ"
```

### Anthropic (Claude)
```bash
export ANTHROPIC_API_KEY="твой-ключ"
```

### Google (Gemini)
```bash
export GOOGLE_API_KEY="твой-ключ"
```

### Или настрой интерактивно при первом запуске — opencode сам спросит.

## Шаг 6: Запусти!

```bash
# В любой папке просто набери:
opencode

# Или укажи конкретную папку:
opencode /путь/к/проекту
```

---

## Основные команды

| Команда | Что делает |
|---------|-----------|
| `opencode` | Запустить TUI в текущей папке |
| `opencode /путь/к/проекту` | Запустить в конкретной папке |
| `opencode serve` | Запустить как сервер (порт 4096) |
| `opencode web` | Сервер + веб-интерфейс |
| `opencode --help` | Все доступные команды |

## Горячие клавиши в TUI

| Клавиша | Действие |
|---------|----------|
| `Tab` | Переключить агента (build / plan) |
| `Ctrl+C` | Выход |
| `@general` | Вызвать суб-агент для сложных задач |

---

## Обновление

```bash
# Если ставил через npm:
npm update -g opencode-ai

# Если клонировал репо:
cd opencode-mobile
git pull
bun install
```

---

## Если что-то не работает

1. **Ошибка при установке bun** — убедись что `curl` установлен: `pkg install curl`
2. **`opencode: command not found`** — проверь PATH: `echo $PATH`, если нужно добавь `~/.opencode/bin` в PATH
3. **Нехватка памяти** — Termux на телефоне может ограничивать память, попробуй закрыть другие приложения
4. **Проблемы с node** — обнови: `pkg upgrade nodejs`

---

## Полезные ссылки

- Документация: https://opencode.ai/docs
- Discord: https://opencode.ai/discord
- GitHub оригинал: https://github.com/anomalyco/opencode
- Мой репозиторий: https://github.com/Redrock453/opencode-mobile
