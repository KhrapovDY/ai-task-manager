# Уровень 1 (Junior)

## Задача

Разработать веб-приложение для управления задачами.

Пользователь должен иметь возможность:

- создавать задачу;
- просматривать список задач;
- изменять статус задачи;
- удалять задачу.

# AI Task Manager

AI Task Manager — учебное веб-приложение для управления задачами. Данные сохраняются в PostgreSQL. Дополнительный Python-скрипт выгружает все задачи в CSV-файл.

## Стек технологий

- Frontend: React + JavaScript + Vite;
- Backend: Node.js + Express;
- база данных: PostgreSQL;
- дополнительно: Python;
- Docker Compose;
- Git и GitHub.

## Возможности

- создание задачи с названием и описанием;
- просмотр списка задач;
- изменение статуса через `select`;
- удаление задачи;
- отображение количества задач по статусам;
- экспорт задач в `tasks.csv`.

Статусы задач: `new`, `in_progress`, `done`.

## Описание файлов проекта

### Корень проекта

- `README.md` — описание проекта и инструкция по запуску.
- `.gitignore` — список файлов, которые не загружаются в GitHub.
- `.env.example` — пример настроек приложения и базы данных.
- `docker-compose.yml` — запуск PostgreSQL, backend и frontend в Docker.

### Backend

- `backend/Dockerfile` — сборка Docker-образа backend.
- `backend/.dockerignore` — исключения при сборке backend.
- `backend/package.json` — зависимости и команды Node.js.
- `backend/package-lock.json` — точные версии зависимостей backend.
- `backend/src/server.js` — запуск сервера.
- `backend/src/app.js` — настройка Express, маршрутов и middleware.
- `backend/src/config/db.js` — подключение к PostgreSQL.
- `backend/src/controllers/taskController.js` — получение, создание, изменение и удаление задач.
- `backend/src/routes/taskRoutes.js` — REST API-маршруты задач.
- `backend/src/middleware/asyncHandler.js` — обработка ошибок асинхронных функций.
- `backend/src/middleware/errorHandler.js` — обработка ошибок API и неизвестных маршрутов.

### База данных

- `database/init.sql` — создание таблицы `tasks` и её полей.

### Frontend

- `frontend/Dockerfile` — сборка Docker-образа frontend.
- `frontend/.dockerignore` — исключения при сборке frontend.
- `frontend/package.json` — зависимости и команды React/Vite.
- `frontend/package-lock.json` — точные версии зависимостей frontend.
- `frontend/index.html` — HTML-шаблон приложения.
- `frontend/vite.config.js` — настройки Vite.
- `frontend/src/main.jsx` — точка входа React-приложения.
- `frontend/src/App.jsx` — главный компонент и управление задачами.
- `frontend/src/api/tasks.js` — запросы frontend к backend.
- `frontend/src/components/TaskForm.jsx` — форма создания задачи.
- `frontend/src/components/TaskTable.jsx` — список задач, выбор статуса и удаление.
- `frontend/src/styles.css` — стили интерфейса.

### Python

- `scripts/export_tasks.py` — экспортирует задачи из PostgreSQL в CSV.
- `scripts/requirements.txt` — зависимости Python-скрипта.

## Запуск приложения

Для запуска должны быть установлены Git и Docker Desktop. Docker Desktop должен быть запущен.

### 1. Клонирование проекта

```powershell
git clone https://github.com/KhrapovDY/ai-task-manager.git
cd ai-task-manager
```

### 2. Создание файла настроек

```powershell
Copy-Item .env.example .env
```

### 3. Запуск Docker-контейнеров

```powershell
docker compose up -d --build
```

### 4. Проверка контейнеров

```powershell
docker compose ps
```

Контейнеры базы данных, backend и frontend должны иметь состояние `healthy`.

### 5. Открытие приложения

Откройте в браузере:

```text
http://localhost:5173
```

Backend работает по адресу `http://localhost:3000`.

## Проверка работы

1. Создайте задачу через форму.
2. Проверьте, что она появилась в списке.
3. Измените статус через выпадающий список.
4. Обновите страницу и проверьте сохранение статуса.
5. Удалите задачу.

Проверка backend:

```powershell
curl.exe http://localhost:3000/health
curl.exe http://localhost:3000/tasks
```

Просмотр логов:

```powershell
docker compose logs
```

REST API:

- `POST /tasks` — создание задачи;
- `GET /tasks` — получение списка задач;
- `PUT /tasks/:id` — изменение статуса;
- `DELETE /tasks/:id` — удаление задачи.

## Экспорт задач в CSV

Для экспорта должен быть установлен Python 3, а PostgreSQL должен быть запущен.

В корне проекта выполните:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r scripts/requirements.txt
python scripts/export_tasks.py
```

После выполнения в корне проекта появится файл `tasks.csv`.

## Остановка приложения

```powershell
docker compose down
```
