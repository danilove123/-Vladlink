# Vladlink
Тестовое задание Vladlink, php разработчик

## Условия
- Задание должно быть выполнено на PHP
- Нельзя использовать фреймверĸи (Symfony, Laravel, Lumen, Yii и т.д.)
- Можно использовать библиотеĸи и ĸомпоненты (Doctrine2, Twig и т.д.)
- Можно использовать composer
- В ĸачестве БД можно использовать MySQL, PostgreSQL
**Решение должно содержать:**
- README.md инструĸцию по развертыванию проеĸта на другой машине
- Сĸрипты или ĸоманды по импорту/эĸспорту данных
- Сгенерированные приложением файлы
- SQL сĸрипт для генерации струĸтуры БД
## Задача
- Реализовать фунĸционал для хранения/обработĸи/вывода списĸа меню.
- Графичесĸий интерфейс - не требуется.
## Решение
**1. Развёртывание:** Для решения был использован Open Server, который предоставляет программы Php Adminer, Sublime_text, а также активирует сервер по локальному хосту (в данной задаче). Php Adminer - для настройки БД, Sublime_text - для редактирования кода.
- **Для запуска:**
- Главный файл list_menu.php
- В yourFiles содержатся все файлы
- yourPath - то, куда установили Open Server
```
yourPath\OSPanel\domains\localhost\ --yourFiles--
```
- Проверяем страничку по локальному хосту localhost или 127.0.0.1
- **Для подключения к БД:**
- Используем Php Adminer с MySql
- В zip будет файл categories.sql, нужно будет заимпортировать

> Есть небольшой нюанс, я не понял, как сделать в БД столбец Children списком и потом с ним работать. (Можно ли это было сразу с json залить так и не понял). 
Сделал немного подругому, посмотрел json, вручную забил столбцы (добавил родительский для прохода рекурсией), что структура получилась такой: id; url_name; alias; name; parent_id.

**2. Код:** В папке functions приведён файл functions.php: функция **db** - осуществляет подключение к БД, **get_array** - делает запрос к БД и возвращет результат в массиве, **view_write** - отображает на странице и записывает в файл **type_a.txt**.

Основная функция **view_write** имеет параметры: ```$array - массив из get_array,  $parent_id - родительский id, $str - костыль (всегда "" не трогать), $num_1 - костыль (всегда 0 не трогать),$num_2 - показывает уровень вложенности, $mode - показывает включен ли уровень вложенности (True - открываем все ветки).```

**Пример**: запрос ```view_write($result,0,"",0,2,False);```
**Результат**:
- Пользователи /users
  - Создание /users/create
  - Список /users/list
  - Поиск /users/search
- Заявки /requests
  - Подключение /requests/connecting
  - Восстановление /requests/repairs
  - Обход /requests/round
- Жалобы /reports
  - Маркетинг /reports/marketing
  - Контроль /reports/control

**Пример**: запроса ```view_write($result,0,"",0,3,False);```
**Результат**:
- Пользователи /users
  - Создание /users/create
  - Список /users/list
    - Активные /users/list/active
    - Удалённые /users/list/deleted
  - Поиск /users/search
- Заявки /requests
  - Подключение /requests/connecting
  - Восстановление /requests/repairs
  - Обход /requests/round
- Жалобы /reports
  - Маркетинг /reports/marketing
    - Списания /reports/marketing/write-offs
    - Цены /reports/marketing/costs
    - Год /reports/marketing/year
  - Контроль /reports/control
    - Эффективность /reports/control/efficiency
    - Подключение /reports/control/connecting
    - 
**Пример**: запроса ```view_write($result,0,"",0,1,True);```
**Результат**:
- Пользователи /users
  - Создание /users/create
  - Список /users/list
    - Активные /users/list/active
    - Удалённые /users/list/deleted
  - Поиск /users/search
- Заявки /requests
  - Подключение /requests/connecting
  - Восстановление /requests/repairs
  - Обход /requests/round
- Жалобы /reports
  - Маркетинг /reports/marketing
    - Списания /reports/marketing/write-offs
    - Цены /reports/marketing/costs
    - Год /reports/marketing/year
  - Контроль /reports/control
    - Эффективность /reports/control/efficiency
    - Подключение /reports/control/connecting
