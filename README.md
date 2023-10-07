После создания 3 файлов в 3 разных коммита я получил следующий лог (во всех логах пишу только коммиты, связанные с задачей, чтобы не было много инфы):

```
1e80800 (HEAD -> main) third <br/>
7ca6152 second <br/>
1669ec1 first <br/>
93e058d (origin/main, origin/HEAD) Update your-task-here.md
```

Сейчас (HEAD (Снимок последнего коммита, родитель следующего) -> main) находится на третьем коммите:

```
1e80800 (HEAD -> main) third.
```

1. **Выполним команду `git reset --soft 7ca6152` (id второго коммита) и запроса логов получаем:**

```
7ca6152 (HEAD -> main) second <br/>
1669ec1 first <br/>
93e058d (origin/main, origin/HEAD) Update your-task-here.md
685ce8d Update README.md
```

Видим, что (HEAD -> main) - переключился на один коммит назад. Третий коммит исчез из логов.

Выполняем команду с возвращением на 1e80800 (HEAD -> main) third и видим лог:

```
1e80800 (HEAD -> main) third <br/>
7ca6152 second<br/>
1669ec1 first<br/>
93e058d (origin/main, origin/HEAD) Update your-task-here.md
```

Снова вернулся наш третий коммит.

Выполняем команду `git reset --soft 1669ec1` - с id первого коммита и запрашиваем лог:

```
1669ec1 (HEAD -> main) first
93e058d (origin/main, origin/HEAD) Update your-task-here.md
685ce8d Update README.md
```

Видим, что мы переместились на самый первый коммит и 2 последующих уже не входят в логи.

2. **Выполним команду `git reset --mixed 7ca6152` (id второго коммита) и запросим лог.**

Видим ответ:

```
Непроиндексированные изменения после сброса:
M .DS_Store
D .gitignore
M one.md
M two.md
```

И лог:

```
7ca6152 (HEAD -> main) second
1669ec1 first
93e058d (origin/main, origin/HEAD) Update your-task-here.md
685ce8d Update README.md
```

Отменен последний коммит и добавление в индекс всех файлов.
Откатились назад до момента выполнения команд git add и git commit.

3. **Выполним команду `git reset --hard 1e80800` с id третьего коммита.**

Видим ответ:

```
Указатель HEAD сейчас на коммите 1e80800 third
```

И лог:

```
1e80800 (HEAD -> main) third
7ca6152 second
1669ec1 first
93e058d (origin/main, origin/HEAD) Update your-task-here.md
685ce8d Update README.md
```

Если мы не коммитили версию после `git reset --mixed`, то файл третьго коммита остается в БД и мы можем его вернуть.

**Git reset** — команда, используемая для отмены локальных изменений в репозитории Git.<br/>
**Git reset** работает с историей коммитов (HEAD ), разделом проиндексированных файлов и рабочим каталогом.

Все это позволяет работать с ветками и файлами, которые нам необходимы и возвращать различные изменения.
