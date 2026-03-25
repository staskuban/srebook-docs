---
title: "guide_to_setting_up_runbookai_telegram_bot_integration_via_docker"
runbook_type: instruction
published_at: "2026-03-25"
layout: default
---

## Развертывание Telegram-бота RunbookAI в Docker

Пошаговая инструкция по деплою и настройке интеграции Telegram-бота с платформой SREBook в собственной инфраструктуре.

---

**Аудитория:** Специалисты с базовыми знаниями Docker (системные администраторы, разработчики, DevOps-инженеры), которые могут самостоятельно подготовить среду для запуска контейнеров.

**Уровень сложности:** Начальный

### Цель

Развертывание и настройка Telegram-бота RunbookAI в собственной инфраструктуре с использованием Docker-образа ghcr.io/staskuban/runbookai/telegram-bot:latest для интеграции с платформой srebook.tech.

### Предварительные требования

**Обязательные:**
- **Docker Engine:** Установленная актуальная версия Docker на сервере.
- **Сетевой доступ:** Исходящий доступ к api.telegram.org и api.srebook.tech (порт 443).
- **Telegram Bot Token:** Токен, полученный у @BotFather в Telegram.
- **SREBook Auth Token:** Токен API из личного кабинета https://portal.srebook.tech/dashboard/tokens.

**Опциональные:**
- Docker Compose

### Шаги выполнения

#### Шаг 1: Подготовка переменных окружения

Создайте файл .env в рабочей директории для хранения конфигурации бота.

```
cat <<EOF > .env
TELEGRAM_BOT_TOKEN=ваш_токен_от_BotFather
API_URL=https://api.srebook.tech
AUTH_TOKEN=ваш_токен_из_srebook_portal
ANSWER_LIMIT=5
EOF
```

> 💡 **Заметка:** Не используйте кавычки для значений токенов. ANSWER_LIMIT по умолчанию равен 5.

#### Шаг 2: Развертывание контейнера

Запустите бота через Docker CLI или Docker Compose.

```
docker run -d --name runbookai-bot --env-file .env --restart unless-stopped ghcr.io/staskuban/runbookai/telegram-bot:latest
```

*Пример:* Альтернатива через docker-compose.yml:
services:
  telegram-bot:
    image: ghcr.io/staskuban/runbookai/telegram-bot:latest
    container_name: runbookai-bot
    restart: unless-stopped
    env_file:
      - .env

> 💡 **Заметка:** Для запуска через Compose используйте команду `docker compose up -d`.

### Проверка результата

1. **Проверка статуса контейнера**
   - Ожидаемый результат: Команда `docker ps` показывает контейнер runbookai-bot со статусом Up.

2. **Отправка сообщения /start в Telegram**
   - Ожидаемый результат: Бот присылает приветственное сообщение или отвечает на поисковый запрос.

### Решение проблем

**Проблема:** 401 Unauthorized в логах
**Решение:** Убедитесь, что AUTH_TOKEN скопирован верно и он активен в панели SREBook.

**Проблема:** Polling error
**Решение:** Проверьте TELEGRAM_BOT_TOKEN и наличие исходящего доступа к api.telegram.org.

**Проблема:** 403 Forbidden / Not enough tokens
**Решение:** Проверьте баланс токенов в личном кабинете SREBook.

### Примеры

#### Безопасное хранение секретов (Docker Secrets)

Пример подключения токенов через файлы секретов в Docker Compose.

```
secrets:
  bot_token:
    file: ./bot_token.txt
  api_auth_token:
    file: ./auth_token.txt
```

### Лучшие практики

- Используйте политику перезапуска --restart unless-stopped.
- Для повышения безопасности используйте Docker Secrets вместо переменных в открытом .env.
- Ограничивайте ANSWER_LIMIT для экономии токенов и читаемости ответов в мессенджере.

---

### Сводка по задачам

- **goal:** Развертывание и настройка Telegram-бота RunbookAI в собственной инфраструктуре с использованием Docker-образа ghcr.io/staskuban/runbookai/telegram-bot:latest для интеграции с платформой srebook.tech.
- **audience:** Специалисты с базовыми знаниями Docker (системные администраторы, разработчики, DevOps-инженера), которые могут самостоятельно подготовить среду для запуска контейнеров.
- **prerequisites:** Установленный Docker, токены от BotFather и SREBook Portal, исходящий доступ в интернет по HTTPS.
- **steps:** Подготовка .env файла, запуск контейнера через Docker CLI или Docker Compose, проверка статуса через docker ps.
- **validation:** Бот отвечает в Telegram на команду /start, в логах отсутствуют ошибки подключения (Polling error, 401, 403).
- **troubleshooting:** Матрица ошибок (401, 403, 404, ECONNREFUSED) и способы их решения через проверку токенов и сетевых настроек.
- **examples:** Использование Docker Secrets для безопасного хранения токенов и настройка политики перезапуска.
