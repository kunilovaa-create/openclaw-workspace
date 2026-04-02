# RECOVERY.md — Инструкция по восстановлению

**Если ты (Старина) проснулся и ничего не помнишь — следуй этой инструкции.**

## 1. Кто ты
- Ты — **Старина**, AI-ассистент Анечки (Анна Кунилова, @annkunn, Telegram id: 401302949)
- Часовой пояс Анечки: **Красноярск UTC+7**

## 2. Восстановление из GitHub

Бэкап хранится тут: `https://github.com/kunilovaa-create/openclaw-workspace`

Токен доступа лежит в локальном файле (НЕ в git):
```
cat /root/.openclaw/GITHUB_TOKEN
```

Команды для восстановления:
```bash
# Прочитай токен
TOKEN=$(cat /root/.openclaw/GITHUB_TOKEN)

# Клонируй бэкап во временную папку
cd /tmp && git clone https://kunilovaa-create:${TOKEN}@github.com/kunilovaa-create/openclaw-workspace.git recovery

# Скопируй все файлы в workspace
cp -r /tmp/recovery/* /root/.openclaw/workspace/
cp -r /tmp/recovery/.openclaw /root/.openclaw/workspace/ 2>/dev/null

# Настрой git remote
cd /root/.openclaw/workspace
git remote remove origin 2>/dev/null
git remote add origin https://kunilovaa-create:${TOKEN}@github.com/kunilovaa-create/openclaw-workspace.git
```

## 3. Восстановление крон-задач

Файл `backup/cron-jobs.json` содержит все задачи. Пересоздай их через `openclaw cron add`.

Список актуальных задач — в `reminders.md`.

## 4. Что важно помнить
- Читай `USER.md` — там правила напоминаний
- Читай `IDENTITY.md` — там твоё имя
- Читай `MEMORY.md` — там долгосрочная память
- Читай `reminders.md` — там все напоминания
- Обращайся к ней **Анечка**
- Обычное напоминание → 1 раз
- Важное напоминание → повторять каждую минуту пока не подтвердит

## 5. После восстановления
- Напиши Анечке что восстановился
- Проверь что все крон-задачи на месте: `openclaw cron list`
- Сделай коммит и пуш
