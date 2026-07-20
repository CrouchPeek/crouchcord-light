# CrouchCord Light

<div align="center">

**Лёгкая, прозрачная и мощная библиотека для Discord ботов**

[![PyPI version](https://img.shields.io/pypi/v/crouchcord-light)](https://pypi.org/project/crouchcord-light/)
[![Python versions](https://img.shields.io/pypi/pyversions/crouchcord-light)](https://pypi.org/project/crouchcord-light/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/crouchpeek/crouchcord-light)](https://github.com/crouchpeek/crouchcord-light)

</div>

---

## 📦 Установка

```bash
pip install crouchcord-light
```
Или из исходников:

```bash
git clone https://github.com/crouchpeek/crouchcord-light
cd crouchcord-light
pip install .
```
🚀 Быстрый старт
```python
import crouchcordlight as crouchcord

bot = crouchcord.Bot("!")

@bot.event
async def on_ready():
    print(f"✅ Бот {bot.self_data['username']} запущен!")

@bot.command()
async def ping(ctx):
    await ctx.send("🏓 Понг!")

bot.run("ТВОЙ_ТОКЕН")
```
✨ Особенности
Фича	Описание
⚡ Префиксные команды	!ping, !ban, !help
🔄 Слеш-команды	/ping, /ban, /help
🎛️ Компоненты	Кнопки, селекты, модалки
🎤 Голос	Подключение к голосовым каналам
📦 Эмбеды	Через JSON (полный контроль)
🌐 HTTP-клиент	Прямые запросы к Discord API
🧩 Группы	Модульная структура команд
📖 Примеры
```python
#🔄 Слеш-команды
@bot.app_command(name="ping", description="Проверить пинг")
async def ping(ctx):
    await ctx.respond("🏓 Понг!")
#🎛️ Кнопки
@bot.app_command(name="button", description="Кнопка")
async def button(ctx):
    await ctx.respond(
        "Нажми кнопку!",
        components=[{
            "type": 1,
            "components": [
                {"type": 2, "style": 1, "label": "Нажми", "custom_id": "btn"}
            ]
        }]
    )

@bot.event
async def on_interaction(raw, interaction):
    if raw['data'].get('custom_id') == "btn":
        await interaction.respond("✅ Ты нажал кнопку!", ephemeral=True)
#📋 Селект
@bot.app_command(name="select", description="Выбери опцию")
async def select(ctx):
    await ctx.respond(
        "Выбери:",
        components=[{
            "type": 1,
            "components": [
                {
                    "type": 3,
                    "custom_id": "my_select",
                    "placeholder": "Выбери...",
                    "options": [
                        {"label": "Опция 1", "value": "opt1"},
                        {"label": "Опция 2", "value": "opt2"}
                    ]
                }
            ]
        }]
    )
#📝 Модалка
@bot.app_command(name="modal", description="Открыть модалку")
async def modal(ctx):
    await ctx.respond_modal({
        "title": "Модалка",
        "custom_id": "my_modal",
        "components": [
            {
                "type": 1,
                "components": [
                    {
                        "type": 4,
                        "style": 1,
                        "label": "Имя",
                        "custom_id": "name",
                        "required": True,
                        "placeholder": "Введи имя..."
                    }
                ]
            }
        ]
    })
#🎨 Эмбед
embed = {
    "title": "Заголовок",
    "description": "Описание эмбеда",
    "color": 0x00aaff,
    "fields": [
        {"name": "Поле 1", "value": "Значение", "inline": True}
    ],
    "footer": {"text": "Подвал"}
}

await ctx.send(embeds=[embed])
#🧩 Группы (модульность)
# groups/moderation.py
from crouchcord import Group, command

class ModerationGroup(Group):
    @command(name="ban", description="Забанить")
    async def ban(self, ctx, member, reason="Без причины"):
        await member.ban(reason=reason)
        await ctx.send(f"🔨 {member.display_name} забанен!")

# main.py
bot.add_group(ModerationGroup(bot))
```
🌐 HTTP-клиент
```python
# Прямой запрос к Discord API
data = await bot.http.request("GET", "guilds/123456789")

# Отправить сообщение вручную
await bot.http.send_message(
    channel_id=123456789,
    content="Привет!"
)
```
# 📊 Типы ответов
## Тип	Описание
## 4	Обычное сообщение
## 5	Отложенный ответ
## 7	Обновление сообщения
## 9	Модалка
## 12	Требуется Nitro

# 📦 Зависимости
## aiohttp >= 3.8.0 — для HTTP-запросов

## websockets >= 10.0 — для WebSocket-соединения

# 🤝 Контрибьюция
### Форкни репозиторий

### Создай ветку (git checkout -b feature/amazing-feature)

## Закоммить изменения (git commit -m 'Add amazing feature')

### Пушни ветку (git push origin feature/amazing-feature)

### Открой Pull Request

# 📄 Лицензия
## MIT License © 2026 crouchpeek

#### Сделано с ❤️ для Discord сообщества
