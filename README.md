# Обрезка ссылок с помощью Битли #

Использует сервисы VK для сокращения ссылок и получения информации о количестве переходов пользователей по ним.

---

### Как установить

Для получения API ключа,вам необходмо зарегестрироваться в VK подробнее про получение API ключа [здесь](https://dev.vk.com/ru/api/access-token/getting-started)

Пример API ключа: 82a02da882a02da882a02da8a981b7f3cc882a082a02da8e4af9c41e8551329276dde72

---

### Переменные окружения

Переменная окружения называется token

Взять её можно [здесь](https://dev.vk.com/ru/api/access-token/getting-started)

Служит для передачи вашего токена из VK в скрипт,без токена работа скрипта невозможна! 

---

### Код

```
SHORTEN_LINK_URL = 'https://api.vk.com/method/utils.getShortLink'
LINK_STATS_URL = 'https://api.vk.com/method/utils.getLinkStats'


def shorten_link(token, url):
    payload = {
        "access_token": token,
        "v": "5.199",
        "url": url,
        "private": "0"
    }
    response = requests.get(SHORTEN_LINK_URL, params=payload)
    response.raise_for_status()
    request_response = response.json()
    return request_response['response']['short_url']
```
Сокращает ссылку

```
def count_clicks(token, short_url):
    parsed = urlparse(short_url)
    path = parsed.path.strip('/')
    payload = {
        "access_token": token,
        "v": "5.199",
        "url": short_url,
        "interval": 'forever',
        "private": "0",
        "key": path
    }
    response = requests.get(LINK_STATS_URL, params=payload)
    response.raise_for_status()
    stats = response.json()
    return stats['response']['stats'][0]['views']
```
Выводит количество переходов пользователей по ссылке

```
def is_short_link(url):
    parsed_url = urlparse(url)
    return parsed_url.netloc == 'vk.cc'
```

Проверяет,сокращена ссылка или нет

```
     parser = argparse.ArgumentParser(description='Сокращение ссылок и получение статистики по просмотрам.')
    parser.add_argument('-u', '--url', type=str, required=True,
                        help='Введите ссылку для сокращения или получения статистики.')
    args = parser.parse_args()
    url_input = args.url

    load_dotenv()
    token = os.environ["VK_TOKEN"]

    try:
        if is_short_link(url_input):
            clicks = count_clicks(token, url_input)
            print('Количество просмотров:', clicks)
        else:
            short_link = shorten_link(token, url_input)
            print('Сокращенная ссылка:', short_link)
    except requests.exceptions.HTTPError as e:
        print("Ошибка при запросе:", str(e))
```

Ожидает ссылку,которую надо ввести, в зависимости от ссылки выводит количество просмотров или сокращает ссылку

[Пример работы](https://imgur.com/a/5AG0OhT):

---

Python3 должен быть уже установлен. 
Затем используйте `pip` (или `pip3`, есть конфликт с Python2) для установки зависимостей:
```
pip install -r requirements.txt
```

### Цель проекта

Код написан в образовательных целях на онлайн-курсе для веб-разработчиков [dvmn.org](https://dvmn.org/).
