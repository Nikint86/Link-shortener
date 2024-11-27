Обрезка ссылок с помощью Битли

Использует сервисы VK для сокращения ссылок и получения информации о количестве переходов пользователей по ним.

---

### Как установить

Для получения API ключа,вам необходмо зарегестрироваться в VK подробнее про получение API ключа [здесь](https://dev.vk.com/ru/api/access-token/getting-started)

Пример API ключа: 82a02da882a02da882a02da8a981b7f3cc882a082a02da8e4af9c41e8551329276dde72

---

### Переменные окружения

token = os.environ["VK_TOKEN"]

---

[Пример работы](https://imgur.com/a/5AG0OhT):

---

Служит для передачи токена из VK в скрипт,без токена работа скрипта невозможна! 

Python3 должен быть уже установлен. 
Затем используйте `pip` (или `pip3`, есть конфликт с Python2) для установки зависимостей:
```
pip install -r requirements.txt
```

### Цель проекта

Код написан в образовательных целях на онлайн-курсе для веб-разработчиков [dvmn.org](https://dvmn.org/).
