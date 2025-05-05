Habit Tracker — это современный сервис, разработанный на Django REST Framework, предназначенный для удобного управления ежедневными привычками пользователей. Сервис предлагает аутентификацию через JWT-токены, интеграцию с Telegram для отправки уведомлений и подробную документацию API с помощью инструментов Swagger и ReDoc.

## Локальное использование

Чтобы начать работу с проектом на локальном компьютере, необходимы:

- Docker и Docker Compose
- Python 3.10
- Git

### Инструкция по установке:

1. Убедитесь, что Docker установлен и работает:
   ```bash
   docker --version
   ```
   
2. Скопируйте репозиторий проекта:
   ```bash
   git clone https://github.com/your-username/habit-tracker.git && cd habit-tracker
   ```

3. Создайте конфигурационный файл `.env`:
   ```bash
   SECRET_KEY=your-secret-key
   DEBUG=True
   POSTGRES_DB=habit_tracker_db
   POSTGRES_USER=habit_user
   POSTGRES_PASSWORD=habit_password
   POSTGRES_HOST=db
   POSTGRES_PORT=5432
   REDIS_URL=redis://:default_redis_pass@redis:6379/0
   TELEGRAM_TOKEN=your-telegram-bot-token
   ```

4. Запустите проект с помощью Docker Compose:
   ```bash
   docker-compose up -d
   ```

5. Проверьте состояние сервисов:
   ```bash
   docker-compose ps
   ```

6. Примените миграции баз данных:
   ```bash
   docker-compose run backend python manage.py migrate
   ```

## Запуск на сервере

Развёртывание сервиса требует следующего:

- Сервер с Ubuntu 24.04
- Docker и Docker Compose
- SSH доступ

### Настройка сервера:

1. Подключитесь к серверу через SSH:
   ```bash
   ssh user@your-server-ip
   ```

2. Обновите систему и установите Docker:
   ```bash
   sudo apt update && sudo apt install -y docker.io docker-compose
   sudo systemctl start docker && sudo systemctl enable docker
   ```

3. Настройте SSH-ключи для безопасного соединения:
   ```bash
   ssh-keygen -t rsa -b 4096
   ssh-copy-id user@your-server-ip
   ```

## Автоматическая сборка и развёртывание (CI/CD)

Настройке CI/CD-процесса можно следовать следующим образом:

- Добавьте секреты в GitHub:  
  В разделе настроек репозитория введите значения:
  - SSH_USER: имя пользователя сервера
  - SSH_KEY: приватный SSH-ключ
  - SERVER_IP: IP-адрес сервера
  - DEPLOY_DIR: директория проекта
  - TELEGRAM_TOKEN: токен Telegram-бота

- Файл `.github/workflows/ci.yml` настроен для автоматического запуска тестов и развёртывания проекта.

## Доступность API

Адреса API доступны по следующему пути:
```
http://158.160.87.62:8000/api/
```

## Тестирование

Для запуска тестов выполните:
```bash
docker-compose run backend python manage.py test
```

## Документирование API

Подробная документация представлена в двух вариантах:

- **Swagger UI**: `http://localhost:8000/swagger/`
- **ReDoc**: `http://localhost:8000/redoc/`
