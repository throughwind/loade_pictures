# Публикация фотографий космической тематики (Spase-x, NASA) через телеграмм бота

## Как установить

Python3 должен быть уже установлен.
Для удобства работы и изоляции зависимостей от системы - создайте виртуальное окружение (например с помощью venv).
````
python3 -m venv venv
````
Активируйте виртуальное окружение.
````
source venv/bin/activate
````

Затем используйте pip (или pip3, есть конфликт с Python2) для установки зависимостей:
```
pip install -r requirements.txt
```
Для скрытия токена используйте файл `.env` и библиотеку `python_dotenv`.

Python3 должен быть уже установлен. 
Затем используйте `pip` (или `pip3`, если есть конфликт с Python2) для установки зависимостей:
```
pip install -r requirements.txt
```
## Модуль fetch_spacex.py

Модуль предназначен для скачивания картинок космоса с сайта проекта [space-x](https://documenter.getpostman.com/view/2025350/RWaEzAiG#bc65ba60-decf-4289-bb04-4ca9df01b9c1).

Для использования API SPASE-X нет необходимости получать токены.

URL адрес для запроса `https://api.spacexdata.com/v3/launches/latest`
```
Бывает, что фотографий на запуске не делали. 
В такой ситуации придётся работать не с первым запуском. Уберите latest из ссылки и вы получите все вылеты. 
Выберите из них какой-нибудь и работайте с ним.

Ответом на запрос будет огромный объект. 
Чтобы найти нужное поле, воспользуйтесь примером ответа на запрос из документации. 
Там тот же ответ, только выведен красиво.
```

## Модуль fetch_nasa.py

Для использования API сервера NASA необходимо получить токен на [сайте](https://api.nasa.gov).

Токен выглядит как строка наподобие следующей: `B9TVgrRWFcUNo9dVwj45z74CTw5fzuDqE1vChd7a`.

Модуль предназначен для скачивания картинок космоса с сайта проекта [NASA](https://api.nasa.gov).

API использует для запросов два адреса:
- URL для скачивания основных фотографий `https://api.nasa.gov/planetary/apod`;
- URL для скачивания снимков Земли с космоса `https://api.nasa.gov/EPIC/api/natural/images/`;

## Модуль filename_extension.py

В связи с тем, что фотографии могут быть разного расширения, данный модуль парсит ссылку и получает нужное
расширение файлов картинок. Используя данный модуль мы всегда можем получить точное расширение файла и сохранить его 
на диск корректно.

## Модуль send_photo_tg_bot.py

Данный модуль отправляет скаченные картинки в телеграмм-группу с помощью бота
Для работы с модулем необходимо создать телеграмм бота и получить токен. Как полуить токен и настроить телеграмм бота
можно узнать по [ссылке](https://smmplanner.com/blog/otlozhennyj-posting-v-telegram/).

Так же необходимо в файл `.env` добавить  параметр `TIME_SLEEP` равный переодичностью публикации фотографий (задается в секундах, `24 часа это 86400 секунд`).

# Как использовать

Для начала активируем виртуальное окружение
```
% source env/bin/activate   
```
По результату получим вывод терминала похожий на:
```
(venv) loade_pictures %
```
## Качаем картинки с NASA

Введем команду для скачивания картинок c сайта NASA
```
(venv) loade_pictures % python fetch_nasa.py
```
В итоге в папке проекта появится каталог `images` со скачанными картинками.

## Качаем картинки SPACE-X

Таким же образом можно скачать картинки SPACE-X
```
(venv) loade_pictures % python fetch_spacex.py
```

## Запускаем телеграмм бота и публикуем картинки в телеграмм

```
(venv) loade_pictures % python send_photo_tg_bot.py
```

Have fun!

# Цель проекта

Код написан в образовательных целях на онлайн-курсе для python-разработчиков [dvmn.org](https://dvmn.org/).
