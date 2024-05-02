# Магазин Marzban

Marzban Shop - это магазин ботов Telegram, построенный на основе aiogram, который позволяет продавать VPN через Telegram.

## Содержание

Автор: 
- [Gunship](https://github.com/gunsh1p/)

### Особенности

- Тестовые подписки
- Поддержка платежей: [Cryptomus](https://cryptomus.com/) и [YooKassa](https://yookassa.ru/)
- Русский и английский интерфейс 

### Зависимости

- [Docker](https://www.docker.com/)

### Инструкция по установке

#### Настройка

```bash
git clone https://github.com/gunsh1p/marzban-shop.git
cd marzban-shop
docker compose build
```

После этого отредактируйте файл goods.examples.json

##### Пример товара

```json
{
        "title": <ваш_заголовок_здесь>,
        "price": {
            "en": <цена_для_крипто_платежей>,
            "ru": <цена_для_платежей_через_YooKassa>
        },
        "traffic": <трафик_в_байтах>,
        "callback": <уникальный_идентификатор_товара>,
        "months": <количество_месяцев>
    }
```

И отредактируйте файл .env.example (см. [конфигурацию](#Конфигурация))

После этого выполните этот код

```bash
mv goods.example.json goods.json
mv .env.example .env
```

### Вебхуки

Для корректной работы платежей нам нужен вебхук.

Как его настроить?

```bash
apt install python3-pip nginx
```
Подробные инструкции скоро будут доступны. 

#### Запуск

```bash
docker compose up -d
```

### Конфигурация

> Нижеуказанные параметры можно установить с помощью переменных среды или поместив их в файл `.env`.

| Переменная      | Описание |
|-|-|
| BOT_TOKEN | Токен бота. Для его получения введите команду /newbot в t.me/BOTFATHER|
| SHOP_NAME | Название вашего магазина VPN|
| TEST_PERIOD | Наличие тестового периода (true или false) |
| PERIOD_LIMIT | Лимит тестового периода.|
| ABOUT | Описание вашего сервиса|
| RULES_LINK | Правила вашего магазина (по умолчанию nometa.xyz)|
| SUPPORT_LINK | Ссылка на поддержку|
| YOOKASSA_TOKEN | Токен YooKassa |
| YOOKASSA_SHOPID | shopId YooKassa |
| EMAIL | Email для квитанций |
| CRYPTO_TOKEN | Токен Cryptomus |
| MERCHANT_UUID | Merchant UUID Cryptomus |
| DB_NAME | Имя базы данных |
| DB_USER | Имя пользователя базы данных |
| DB_PASS | Пароль базы данных |
| DB_URL | URL (например, postgresql+psycopg://user:password@server/db), где пользователь - DB_USER, пароль - DB_PASS, сервер - IP базы данных (по умолчанию localhost), а db - DB_NAME |
| PANEL_HOST | URL для подключения к панели marzban (если установлено на том же сервере, что и marzban-shop, укажите localhost и порт панели) |
| PANEL_GLOBAL | URL для выдачи подписок (этот параметр может отличаться от PANEL_HOST, подробнее [здесь](#Разница-между-хостом-и-глобальным)) |
| PANEL_USER | Имя пользователя панели |
| PANEL_PASS | Пароль панели |
| WEBHOOK_URL | Адрес вебхука (URL) (подробнее [здесь](#О-вебхуке)) |
| WEBHOOK_PORT | Порт вебхука |

#### Разница между хостом и глобальным

Есть две переменные окружения PANEL_HOST и PANEL_GLOBAL.

PANEL_HOST - адрес панели для взаимодействия с API. Если панель установлена на том же сервере, что и marzban-shop, то в качестве адреса следует указать localhost. Например, <http://localhost:8080>

PANEL_GLOBAL - адрес для выдачи подписок. Он используется для замены ссылки на подписку. Он должен быть доступен не только в локальной сети, но и вне её.

!ПРЕДУПРЕЖДЕНИЕ! Если переменная XRAY_SUBSCRIPTION_LINK в вашей панели marzban установлена, оставьте переменную PANEL_GLOBAL пустой

#### О вебхуке

Для получения ответов от сервера Telegram и серверов платежных систем используется вебхук. Это должен быть адрес, по которому все эти серверы будут обращаться. Он должен быть доменом с поддержкой TLS 1.2 или выше. Запросы должны быть направлены на порт, указанный в .env в переменной WEBHOOK_PORT.
Кроме того, для правильной работы YooKassa вам нужно будет указать адрес вебхука в вашем личном кабинете со значением /yookassa_payment в конце (например, <https://my-awesome-webhook.example.com/yookassa_payment>) и выбрать все значения, которые начинаются с payment.

### Дальнейшие шаги

- [ ] Хранение товаров в базе данных
- [ ] Веб-панель для администраторов
- [ ] Рефакторинг кода

## Вклад

Вклад вносит открытое сообщ

ество, делая его удивительным местом для обучения, вдохновления и творчества. Любой вклад, который вы вносите, **очень ценится**.

Если у вас есть предложение, которое сделает проект лучше, пожалуйста, форкните репозиторий и создайте pull request. Вы также можете просто открыть issue с тегом "enhancement".
Не забудьте поставить звезду проекту! Спасибо еще раз!

1. Форкните проект
2. Создайте свою ветку с функцией (`git checkout -b feature/AmazingFeature`)
3. Зафиксируйте ваши изменения (`git commit -m 'Add some AmazingFeature'`)
4. Запушьте ветку (`git push origin feature/AmazingFeature`)
5. Откройте Pull Request

### Пожертвования

- BTC: `bc1qmrwu6uv00xcvsjvjkwnaw2ky6aenhjgqewg0w4`
- LTC: `ltc1qrl3fp7cwwxsun2fsk60zxgncuutkrydwgju6a2`
- USDT (TRC-20): `TJUUhJpeaZBBXpG6yUtzLsQmT3XQjViowV`
- ETH: `0x052D18812fA247Ce6853a6D95213CEbdb45c6277`
- TON: `UQBtG5NZECAH7wc2MrHnoVTv1mRzC9z-vqB-5cUpUaMJbptZ`

### Лицензия

Проект лицензирован по [GPL-3.0](https://github.com/gunsh1p/marzban-shop/blob/main/LICENSE)

### Контакты

Email: <bertollo@gunship.su>

Telegram: [@blackbloodredkiss](https://t.me/blackbloodredkiss)
