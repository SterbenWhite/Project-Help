# **Инструкция по работе с Git**
----
## 1. **Загрузка и установка Git**

1) Скачать по [ссылке](https://git-scm.com/downloads/win) локальную версию Git и GitBrash нужной разрядности.
2) Установить Git по инструкции, оставляя все параметры по умолчанию.

## 2. **Создание локального репозитория**

1) Зайти в нужную папку с проектом. Кликнув ПКМ нажать "Open Git Bash here", чобы открыть терминал Git

2) Чтобы создать локальный репозиторий, использовать следующую команду:
```
git init
``` 

3) Чтобы подготовить все файлы в репозитории к сохранению, ввести следующую команду:
```
git add --all
```
Или использовать следующую команду для подготовить конкретный файл:
```
git add [Path]
```

4) Проверить статус репозитория, ввести следующую команду:
```
git status
```
Статусы файлов:
```
untracked //Неотслеживаемый (новый файл) файл
tracked //Отслеживаемый файл, который уже был однажды закоммичен
staged //Файлы, подготовленные для коммита, командой git add
modified //Изменённые файлы
```
5) Для создания коммита (сохранения файлов в новую версию), написать следующую команду
```
git commit -m "Название коммита"
```

## 3. **Создание удалённого репозитория на GitHub**

1) Перейти на сайт [GitHub](https://github.com), и зарегистрироваться нажам на "SignUp" в углу экрана;

2) Нажать на иконку своего профиля в углу экрана, в выпадающем меню выбрать "Your repositories". 
В появившейся странице нажать кнопку "New", для создания новго репозитория. Настроив название и приватность - нажать кнопку "Create repository"

## 4. **Создание SSH-ключа**

1) перейти в домашнюю папку командой:
```
cd ~
```

2) Проверить, есть-ли уже существующуе ключи, командой:
```
ls -la .ssh/
```
если папка пуста или её нет, то всё в порядке.

3) Сгенерировать новый ключ одной из двух команд:

```
1) ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
2) ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
```
4) После ввода команды, программа предложит выбрать путь для расположения папки с ключами, затем кодовую фразу. Чтобы оставить путь по умолчанию (домашняя папка) и отказаться от кодовой фразы - просто нажимать Enter.

5)Проверить созданные ключи, можно командой:
```
ls -a ~/.ssh 
```
Должно быть 2 файла.
Файл с расширением .pub - публичный ключ, а файл без расширения - приватный.
Приватный ключ никому не передавать и не копировать.

## 5. **Подключение SSH-ключа к GitHub**

1) Перейти в домашнюю папку, открыть папку ".ssh", и скопировать содержимое файла-ключа с рисширением ".pub".

2) Нажав на иконку профиля, выбрать пункту "Settings".

3) В меню "Settings", выбрать пункт "SSH and GPG keys".

4) В открывшейся вкладке нажать кнопку "New SSH key"
В поле Title - напишите название ключа.
В поле Key type - должно быть Authentication Key.
В поле Key вставьте, ранее скопированное содержимое файла-ключа с расширением ".pub".

5) Нажать на кнопку "Add SSH key ".

6) Проверить правильность ключа, можно командой:
```
ssh -T git@github.com 
```
## 6. **Подключение локального репозитория к удалённому**

1) После создания удалённого репозитория на GitHub, появится инструкция по подкючению репозитория. 
Инструкция находится под строкой "…or push an existing repository from the command line", и выглядит примерно так:
```
git remote add origin https://github.com/"USER_NAME"/"REPOSITORY_NAME".git
git branch -M main
git push -u origin main
```
Нужно ввести все команды по указанному порядку, после чего удалённый репозиторий, получит данные локального и они станут идентичны.

2) Далее, для добавления нового коммита, последоватеьность команд будет следующей:
```
git add --all
git commit -m "Название коммита"
git push
```
## 7. **Состав лога коммитов**

Что-бы получить лог всех коммитов, используется комманда:
```
git log
```
Состав лога:

```
commit e83c5163316f89bfbde7d9ab23ca2e25604af290 //Хеш - главный идентификатор коммита
Author: Linus Torvalds <torvalds@linux-foundation.org> //Имя автора и его электронная почта
Date:   Thu Apr 7 15:13:13 2005 -0700 //Дата и время создания коммита

    Initial revision of "git", the information manager from hell //Сообщение коммита
```

Получить сокращённый лог, можно следующей командой:
```
git log --oneline
```
Сокращённый лог, выдаёт только первые несоклько символов хеша и сообщение коммита.
HEAD - это один из служебных файлов папки ".git", он указывает на последний созданный коммит (самый новый).
Файл, ссылку на который хранит файл HEAD, хранит хеш последнего коммита

Многие команды Git, в качестве параметра, принимают хеш коммита, но вместе коммита можно использовать указатель HEAD.
При выводе сообщения через git log ```git log --oneline```, умещается максимум 72 символа сообщения коммита.
Сообщение коммита, нужно составлять коротким и информативным.

## 8. **Исправление коммитов**

Для того, что-бы дополнить HEAD-коммит, используется команда:
```
git commit --amend --no-edit
```

Изменить сообщение HEAD-коммита, можно командой:
```
git commit --amend -m "Новое_сообщение"
```

Удалить файл из списка "staged", можно командой:
```
git restore --staged <file>
```

Откатить репозиторий до указанного коммита, можно командой:
```
git reset --hard <commit hash>
```

Если коммиты сильно отличаются от удалённого и после ```git push``` выдаёт ошибку, то пишем команду:
```
git push --force # В таком случае, будет совершена перезапись, и некоторые коммиты могут быть утеряны
```
Откатить файл до последнего сделанного коммита или ```git add```, можно командой:
```
git restore <file>
```
## 9. **Просмотр изменений**

Чтобы вывести лог, и видеть изменения в каждом коммите, используется команда:
```
git log -p
```

Что-бы проверить, какие изменения внесены в файлы, используется команда:
```
git diff <file>
```
Команда ```git diff```, может быть использована с флагом ```--staged```, чтобы посмотреть изменения в staged файлах:
```
git diff --staged <file>
```
Узнать какие изменения произошли в коммите, по сравнению с другим коммитом, можно командой:
```
git diff <commit_hash_1> <commit_hash_2>
```

## 10. **Игнорирование файлов**

Игнорируемые файлы, записываются в файл ".gitignore", если его нет, то его нужно создать.
Игнорирование работает, только для untracked-файлов
Каждое правило записывается в отдельную строку.

1) Символ ```#``` - обозначает коментарий, текст после него не будет считываться Git.

2) Можно указать название файла:
```
FileName # Будут игнорироваться все файлы с названием "FileName"
```

3) Символ ```*``` - обозначает любую строку, даже пустую.
```
*.txt # будет проигнорирован любой файл, который заканчивается на ".txt"
```

4) Символ ```?``` - обозначает любой символ.
```
FileName? # Любой файл с названием "FileName" и любым символом на конце, будет проигнорирован
```

5) Символ ```[...]``` - обозначает перечисление символов, или задание диапозона чисел ```[0-9]``` или букв ```[a-z]```

```
FileName[0-2] # Любой с названием "FileName" и числом от 0 до 2, будет проигнорирован
FileName[a-c] # Любой файл с с названием "FileName" и буквой от a до c, будет проигнорирован 
FileName[1,2,3] #Любой файл с названием "FileName" и цифрами 1,2 или 3, будет проигнорирован
```

6) Символ ```/``` - указывает на каталог
```
/*.txt #Любой файл, который заканчивается на ".txt", находящийся в корне репозитория, будет проигнорирован
Folder_1/Folder_2/* # любой файл, находящийся в папке "Folder_2", будет проигнорирован
Folder_1/ # папка "Folder_1", будет проигнорирована
```

7) Символ ```**``` - обозначает любое количество папок (даже нулю)
```
docs/**/tmp # Игнорировать все файлы, находящиеся по пути, который начинается с "docs" и находятся в папке tmp
```

8) Символ ```!``` - обозначает исключение
```
*.txt # Любой файл, который заканчивается на ".txt", будет проигнорирован
!File_A.txt # Но только не файл "File_A.txt"
```

Отобразить все файлы включая игнорируемые
```
git status --ignored
```

## 11. **Клонирование репотизиториев**

1) На странице репозитория, нажать зелёноу кнопку "<> Code", затем выбрать "SSH" и скопировать ссылку.

2) Перейти в нужную папку, затем использовать следующую команду:
```
git clone [URL] # Где "URL" - Скопированная ранее SSH-ссылка
```
После этого, будет создана папка с репозиторием. 
Локальный репозиторий будет автоматически связан с удалённым.

## 11. **Работа с ветками**

Для просмотра локальных веток репозитория, используется команда:
```
git branch
```

Для создания ветки, используется команда:
```
git branch [Название]
```
Название ветки, должно отражать суть её содержимого.

Для перемещения в другую ветку, используется команда:
```
git checkout [Название_ветки]
```

Создать ветку и сразу переключиться на неё, можно командой:
```
git checkout -b [Название_ветки]
```

Для просмотра всех веток проекта, в том числе и на GitHub, используется команда:
```
git branch -a
```
Будет указан отдельный список удалённых веток с прификсом ```remotes/origin```

Для сравнения изменений в файлах веток, можно исполльзовать команду:
```
git diff [Название_ветки_1] [Название_ветки_2ы]
``` 
Можно сравнить ветку с хегом другой ветки, командой:
```
git diff [Название_ветки_1] [Хеш_ветки_2]
```
Для получении ссылки на коммит, определённого номера в списке, используется команда:
```
[Коммит]~[N] # Где N - номер коммита следующего за указанным.
HEAD~0 # Указывает сам на себя
HEAD~1 # Предыдущий коммит
```

Выполнить слияние веток, можно командой:
```
git merge [branch_1] # Нужно находиться в ветке, с которой будет сливаться "branch_1". После слияния "branch_1", останется. 
```

Для удаления ветки, используется команда:
```
git branch -D [название_ветки] 
```

Для более безопасного удаления веток, используется команда:
```
git branch -d [название_ветки] # Удаляет ветку, только если она уже слилась с другой
```

Чтобы отправить новую ветку в удалённый репозиторий, используется команда:
```
git push -u origin [название_ветки]
```

Загрузить изменения из удалённого репозитория на локальный, можно, перейдя в нужную ветку (обычно это main или master), и введя команду:
```
git pull
```

Перед созданием нового pull-request
считается хорошей практикой перейти в главную ветку, 
«подтянуть» в неё изменения, а затем добавить эти изменения в вашу ветку с помощью git merge main.

Отключить режим fast-forward, можно командой:
```
git merge --no-ff [название_ветки] # Выполнить слияние без fast-forward
```