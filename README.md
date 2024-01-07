# GIT & GITHUB


## В этом уроке покажем, как превратить простую папку в Git-проект и проверить, что всё прошло успешно, также запишем несколько git-комманд на будущее.


### Сделать папку репозиторием — _git init_

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать Git-репозиторием (от англ. repository — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. initialize — «инициализировать»).

Например, создайте папку first-project и сделайте её Git-репозиторием: перейдите в неё с помощью команды cd и выполните git init.

```bash
$ cd ~/dev/first-project # перешли в нужную папку
$ git init # создали репозиторий 
```

Вы можете создать папку в любом месте на компьютере.


### «Разгитить» папку, если что-то пошло не так — _rm -rf .git_

Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку .git.

```bash
$ cd <папка с репозиторием> # перешли в папку
$ rm -rf .git # удалили подпапку .git 
```

Разберём подробнее, что такое -rf:
ключ -r (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;
ключ -f (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».


### Проверить состояние репозитория — _git status_

После инициализации репозитория first-project запустите команду git status (от англ. status, «статус», «состояние») — она показывает текущее состояние репозитория.

Сейчас в first-project два файла. Мы хотим отслеживать состояние обоих, поэтому можем использовать команду git add --all (от англ. add — «добавить» + от англ. all — «всё»). Ключ, или флаг, --all позволяет подготовить к сохранению все файлы в репозитории.

```bash
$ git add --all # подготовили к сохранению все файлы в репозитории
$ git status # проверили статус 
```

Добавлять файлы можно и по одному, без ключа --all.

```bash
$ git add todo.txt
$ git add readme.txt
$ git status 
```

Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (.).

```bash
$ git add . # добавить всю текущую папку
$ git status 
```

Вы можете использовать любой из этих вариантов — результат будет одинаковый.
_Команда git add не сохраняет содержимое файлов в репозитории._
_Само сохранение, или фиксацию состояния файлов, называют коммитом (от англ. commit — «совершать», «фиксировать»)._
_«Сделать коммит» значит сохранить текущую версию файла._
Если провести аналогию, команду git add можно сравнить с добавлением товаров в корзину в интернет-магазине, а коммит — с оформлением и оплатой заказа.


### Выполнить коммит — _git commit_

Сделать коммит можно командой git commit c ключом -m (от англ. message — «сообщение»), который присваивает коммиту сообщение.

Обычно в таком сообщении поясняется, в чём именно состояли изменения. Это как заметки на полях: благодаря им проще читать и понимать текст. Сообщение коммита выполняет те же функции — улучшает понимание и упрощает навигацию. Оно пишется после ключа -m в кавычках.

Например, перейдите в папку first-project и выполните коммит со следующим комментарием.

```bash
$ git commit -m 'Мой первый коммит!' 
```

После нажатия Enter текущая версия файлов будет сохранена в репозитории с сообщением Мой первый коммит!. Коммит (по названию команды git commit) — это по сути список файлов с их контентом.
Команда git commit выведет информацию о коммите.

```bash
[master (root-commit) baa3b6e] значит:
```

коммит был в ветке master;
root-commit — это самый первый, или «корневой» (англ. root), коммит в ветке, у следующих коммитов такой надписи не будет;
baa3b6e — сокращённый идентификатор коммита (подробнее об этом мы ещё расскажем).

```bash
2 files changed, 1 insertion(+) значит:
```

изменились два файла (readme.txt и todo.txt);
одна строка была добавлена (1. Пройти пару уроков по Git.).
Строки вида create mode 100644 readme.txt — это более подробная информация о новых (добавленных в Git) файлах.
create (англ. «создать») говорит, что файл был создан. Если бы файл был удалён, на этом месте было бы слово delete (англ. «удалить»).
mode 100644 сообщает, что это обычный файл. Также возможны варианты 100755 для исполняемых файлов (например, что-нибудь.exe) и 120000 для файлов-ссылок в Linux. Файлы-ссылки не содержат данных сами по себе, а только ссылаются на другие файлы — как «ярлыки» в Windows.
Если ввести git commit без флага -m, откроется редактор Vim. Чтобы выйти из него, нажмите клавишу Esc, наберите последовательность символов :q! и нажмите Enter.

Ещё раз о разнице между git add и git commit:
Сначала команда git add сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды git commit происходит само сохранение.


### Просмотреть историю коммитов — _git log_

В самостоятельном задании прошлого урока вы сделали три коммита в ваш репозиторий. Чтобы увидеть их все, введите команду git log (от англ. log — «журнал [записей]»).
В командную строку нельзя вставить текст из буфера обмена с помощью привычного сочетания Ctrl+V. На Windows (в Git Bash) и Linux для этого используется сочетание Ctrl+Shift+V, а на macOS — Cmd+V.
Также можно нажать правую кнопку мыши и выбрать пункт Paste (англ. «вставить») в выпадающем меню.


### Отправить изменения на удалённый репозиторий — _git push_

Вы уже прошли весь «цикл коммита»: подготовили файлы с помощью git add, закоммитили их с комментарием командой git commit -m. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда git push (от англ. push — «толкать»).
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории, так же и здесь нужно дополнительно связать ветки.

```bash
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master. 
```

В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push.


### Клонировать репозиторий — _git clone_

Откройте этот репозиторий. Нажмите на зелёную кнопку Code. Появится окно со ссылкой. Если вы уже настроили SSH-ключ, убедитесь что выбрана опция SSH и нажмите на кнопку с двумя квадратами справа — она скопирует ссылку в буфер обмена. Вы также можете скопировать ссылку вручную. Теперь откройте консоль, перейдите в папку, в которую хотите положить репозиторий, и выполните команду git clone (от англ. clone — «клон», «копия»). Она создаст копию удалённого репозитория на вашем компьютере. В качестве параметра команде нужно передать адрес репозитория, который вы только что скопировали на GitHub.

```bash
$ git clone https://github.com/yandex-praktikum/git-clone-lesson
# укажите адрес репозитория, который нужно склонировать 
```


### _Что такое Fork_

Fork (англ. «развилка», «ответвление»), или «форк», — это GitHub-операция; напрямую с Git она не связана. «Форк» создаёт копию репозитория в аккаунте GitHub. Такая копия будет полностью независима. Изменения, которые вы внесёте, не будут синхронизированы с исходным репозиторием. В процессе «форка» создаётся копия всех файлов, истории коммитов и веток. Эта копия сохраняется в вашей учётной записи GitHub. Вот некоторые из распространённых причин использования «форков»:
Вы хотите внести свой вклад в проект (например, open source), но не имеете прав на изменение исходного репозитория. Тогда вы можете сделать «форк», добавить нужные правки, а затем отправить запрос на включение этих изменений в оригинальный проект.
Вы хотите развивать проект независимо от исходного. Допустим, создатели проекта решили, что не будут добавлять функциональность, которая вам необходима. В таком случае вы можете сделать «форк» и добавить её самостоятельно.
Применяем «форк»
Потренируйтесь выполнять «форк». Перейдите по этой ссылке и нажмите на кнопку Fork в правом верхнем углу.
В открывшемся окне вы можете поменять название и описание репозитория. Или поставить галку, чтобы склонировать только главную ветку вместо всех сразу. Нажмите Create fork (англ. «создать копию репозитория»).
Немного подождите, пока репозиторий скопируется. После этого он будет доступен по адресу https://github.com/%USERNAME%/git-basics, где %USERNAME% — ваше имя пользователя. В результате вы получите полную копию исходного репозитория, которую можно свободно изменять и которой можно управлять. 💡 Обычно комбинация «форк» + clone используется для внесения изменений в публичные репозитории. В этом случае «форк» становится подготовительным этапом перед клонированием чужого репозитория на ваш компьютер. Если репозиторий приватный или это репозиторий вашей компании, при работе с ним достаточно clone.