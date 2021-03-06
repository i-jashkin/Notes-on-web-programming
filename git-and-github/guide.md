Данный мануал является кратким конспектом из источника https://git-scm.com/book/ru/v2
и некоторых других ресурсов

Открываем командную строку
С помощью команды cd переходим в нужную нам директорию проекта

Команда | Описание
--------|---------
$ git init | инициализирует Git-репозиторий (создается поддиректория .git)
$ git add as.js | добавляет (индексирует) файл as.js для следующего коммита
$ git add . | добавляет в индекс все файлы. 
$ git add -u  | добавляет в индекс все измененные файлы. 
$ git commit -m "first commit" | фиксирует изменения с коментарием в кавычках (параметр -m указывает на коментарий)
$ git commit -a -m "added new" | параметра -a заставляет Git автоматически индексировать каждый уже отслеживаемый на момент коммита файл, позволяя вам обойтись без git add
$ git reset -- path/file.cpp | удаляет из индекса файл path/file.cpp.
$ git status | показывает состояние файлов
							
## Ветвление

https://git-scm.com/book/ru/v1/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-%D0%B2%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B8-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD%D0%B8%D1%8F

Команда | Описание
-----------|---------
$ git branch |                       выводит список имеющихся веток (символ * указывает ветку, на которую указывает HEAD т.е. ветку, на которой вы находитесь в настоящий момент)
$ git branch dev |                   создает ветку с именем dev (но не переключает вас на нее!)
$ git branch -d dev |                удаляет ветку с именем dev
$ git checkout dev |                 переключает на ветку dev
$ git checkout -b dev |              создает ветку dev и сразу переключается на нее
$ git branch -v |                    показывает последний коммит в каждой ветке
$ git branch -m old new |            переименоввает локальную ветку с old на new


## Слияние

Обратите внимание                   Перед тем как слить ветки, нужно с помощью команды $ git checkout <name_branch> перейти в ту ветку, в которую будет производится слияние 

Команда             | Описание
-----------------|---------
$ git merge dev |                    вливает ветку dev в текущую ветку
$ git mergetool |                    открывает графический инструмент для разрешения конфликтов
$ git branch --merged |              показывает список веток, которые вы уже слили с текущей. Те ветки из этого списка, перед которыми нет символа *, можно смело удалять командой git branch -d; наработки из этих веток уже включены в другую ветку, так что ничего не потеряется.
$ git branch --no-merged |           показывает список веток, содержащие наработки, которые вы пока ещё не слили в текущую ветку. Эти ветки невозможно удалить командой git branch -d

## Удаленные репозитории

Каждый удаленный репозиторий имеет URL адрес и сокращенное имя

Команда | Описание
-----------|---------
$ git remote |                       Отображает сокращенные имена (мемы) удалённых репозиториев
$ git remote -v |                    Отображает сокращенные имена (мемы) удалённых репозиториев и соответствующие им URL
$ git remote show og |               Отображает информацию об удалённом репозитории og
$ git remote add og url |            Добавляет новый удалённый репозиторий по адресу url, которому дается сокращенное имя og. Это позволит в дальнейшем обращатся к удаленному репозиторию по имени (вместо url)
$ git clone url |                    Клонирует репозиторий из указанного адреса url
$ git clone url asd |                Клонирует репозиторий из указанного адреса url и переименовывает в asd
$ git push og dev |                  Отправляет ветку dev на удаленный репозиторий og (og - это либо полный путь к удаленному репозиторию, либо его сокращенный мем). Эта команда срабатывает только в случае, если вы клонировали с сервера, на котором у вас есть права на запись, и если никто другой с тех пор не выполнял команду push. Если вы и кто-то ещё одновременно клонируете, затем он выполняет команду push, а затем команду push выполняете вы, то ваш push точно будет отклонён. Вам придётся сначала вытянуть (pull) их изменения и объединить с вашими. Только после этого вам будет позволено выполнить push. 
$ git push -u og dev |               Отправляет ветку dev на удаленный сервер og и связывает локальную ветку dev и ветку dev в удаленном репозитарии. То есть, после такой команды (которая выполняется единожды), можно будет отправлять/принимать изменения лишь выполняя git push из ветки без указания всяких алиасов для сервера и удалённых веток.
$ git fetch og |                     Извлекает из удаленного репозитория og все изменения, которых нет в вашем локальном репозитории, но не сливает их с вашими наработками и не модифицирует то, над чем вы работаете в данный момент. Вам необходимо вручную слить эти данные с вашими, когда вы будете готовы с посощью команды merge.
$ git push og --delete ser |         Удаляет ветку ser на сервере og. На самом деле, удаляется указатель на сервере. Как правило, Git-сервер оставит данные, пока не запустится сборщик мусора. Т. е., если ветка случайно была удалена, чаще всего ее легко восстановить.
$ git remote rename kt oleg |        Переименовывает удаленный репозиторий kt в oleg
$ git remote rm paul |               Удаляет ссылку на удаленный репозиторий. Это бывает нужно, например, если вы сменили сервер или больше не используете определённое зеркало, или, возможно, контрибьютор перестал быть активным
                                
https://git-scm.com/book/ru/v1/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8

