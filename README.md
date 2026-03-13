# Liquid Market — мини Avito

Современный стеклянный веб‑сайт объявлений: React (Vite) + Node.js/Express + MongoDB + JWT, хранение фото локально через Multer.

## Структура

- `backend/` — API, авторизация, CRUD объявлений, загрузка фото.
- `frontend/` — React SPA с iOS‑style “Liquid Glass” UI.

## Запуск локально

1. Установите Node.js 18+.
   - MongoDB не обязательно: если `MONGO_URI` недоступен или Mongo не запущена, API автоматически запустит встроенную in-memory MongoDB (данные пропадут после перезапуска). Для постоянной базы поставьте MongoDB и пропишите `MONGO_URI` в `.env`.
2. Backend:
   - `cd backend`
   - `cp .env.example .env` и при необходимости обновите `MONGO_URI`, `JWT_SECRET`, `CLIENT_ORIGIN`.
   - `npm install`
   - `npm run dev` (порт по умолчанию `5000`)
3. Frontend:
   - В новом терминале `cd frontend`
   - `cp .env.example .env` (при необходимости укажите `VITE_API_URL=http://localhost:5000`)
   - `npm install`
   - `npm run dev` (Vite на `5173`)
4. Откройте http://localhost:5173 — UI общается с API.

## Деплой

- **Backend**: задеплойте на любой Node‑хостинг (Render/Heroku/Railway/Vercel functions). Установите переменные `PORT`, `MONGO_URI`, `JWT_SECRET`, `UPLOAD_DIR`, `CLIENT_ORIGIN`. Обеспечьте постоянное хранилище для папки `uploads` (volume или cloud storage). Включите HTTPS.
- **Frontend**: `cd frontend && npm run build`, затем раздайте содержимое `dist/` через любой static hosting (Vercel/Netlify/S3+CloudFront). Установите `VITE_API_URL` указывая публичный адрес API до сборки.
- Если API и UI на разных доменах — не забудьте настроить `CLIENT_ORIGIN` на API и CORS (уже включено).

## Основные возможности

- Регистрация/вход (JWT), пароли хешированы (bcrypt).
- Создание, редактирование, удаление объявлений только автором.
- Загрузка до 8 фотографий, локальное хранение (`/uploads`).
- Поиск и фильтр по цене, профиль с объявлениями пользователя.
- Стиль iOS‑26: стеклянные карточки, мягкие тени, адаптивная сетка.
