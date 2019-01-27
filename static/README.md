Arch-Project
=============================

Итоговый проект по первому блоку курса "Архитектура информационных систем". Вариант 9

Директории
------------
Пожалуйста, удостоверьтесь, что все файлы, представленные ниже, имеются в вашем источнике

      static/               
            css/           стили
            js/            файлы Javasctipt, настройки страницы, JQuery и селектбокса
            /img           изображения
            /templastes    html страница
      README.md            описание
      app.py               файл инициации
      parser.py            компонента сбора и обработки данных



Описание
------------
Проект представляет собой веб - сервис, который состоит из серверной и клиентской части.
Серверная часть отвечает за сборку, обработку и передачу данных на клиент.
Клиентская часть отвечает за динамическое отображение данных.
 
Серверная часть
-----------
Сервер использует Flask для сбора и обработки информации. Логически серверную часть сервиса можно поделить
на две компоненты. Первая компонента отвечает за непосредственно за сбор данных и его обраотку.

Процесс сбора данных 30 текстовых файлов занимает в среднем 10 секунд, соответсвенно
было бы неразумнынм каждый раз направлять пользовательский запрос на сервер, чтобы
отобразить данные. В связи с этим необходимо прописать правило перезапуска функции любым способом, чтобы перезапускать функцию парсера данных и избавить пользователя от лишнего ожидания. Интервал обновления функции составляет 25 минут, так как было замечено, что самый часто обновляемый элемент текстового файла - время, через каждые полчаса.
Данные собираются при помощи библиотеки requests и передаются в функцию обработки в формате JSON в связи с техническим ограничением
Flask принимать и отдавать глобальные переменные list. 

Вторая серверная компонента отвечает за обработку забранной информации в формат, удобный для отображения на html странице.
Исходный формат имеет вид строки в формате JSON, декодируется в список, состоящий из строк. В исходнымх файлах не хватает тегов (Name:), 
поэтому они были добавлены при помощи инструмента работы с регулярными выражениями re. Далее создается словарь, клюоч к которым
является METAR код, а значеним - список из строк. Так же при помощи регулярных выражений
были так же вычленены значения температуры, ветра, атм. давления (Вариант 9). 

Вычлененные значения сопостоавляются с условием и по запросу с клиента при помощи REST API отпраляются
на клиент в JSON массиве, состоящим из строк. Данные отображаются на html странице, которая генерируется при помощи
маршрутов Flask

Клиентская часть
----------- 
Клиент представляет собой селектбокс, в котором указаны все предложенные варианты METAR кодов.
При нажатии на элемент селектбокса, гугловский JQuery отправляет POST запрос на сервер с информацией о порядковом номере элемента,
который был кликнут пользователем. Селектбокс может может управляться при помощи стрелок, запрошенная информация, а так же 
выводы по ней отображается в правой части страницы в виде текста. Исходный код селектбокса был взят с портала W3C на правах открытого исходного кода.



Что дальше и небольшие выводы
-----------

Удалось разработать веб сервис со относительно сложной структурой и динамически отображающимся контентом.
Далее планируется подтянуть дизайн клиентской части, а так же добавлять новый функционал.

Версии
----------

1.0 - учебная, стабильная
1.1 - исправлены критические ошибки

Кропотин Вадим
kropvad@gmail.com
https://github.com/supahero