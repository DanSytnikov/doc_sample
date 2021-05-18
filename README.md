# Работа с гитом

Перед каждым рабочим днём необходимо смёрджить свои локальные ветки с изменениями, которые лежат на гите. У каждого репозитория есть главная (или основная рабочая ветка `<mainbranch>`: `main`/`master`/`develop`), в которую делаются PR с других веток. После того, как рабочий день закончен, ваши изменения перепушиваются и/или мёрджатся в основную ветку. В ОБОИХ случаях необходимо эти изменения подтянуть. Иначе ваши локальные изменения не сопоставляются с опубликованными => коммиты дублируются => ветка ломается. Два сценария:

## Для работы в новой ветке после успешного закрытия ПР или для работы над новым функционалом:

> <sup>Переключиться на основную ветку, чтобы подтянуть изменения:</sup>
```
git checkout <mainbranch>
```
> <sup>Убрать последние локальные изменения из основной ветки (на случай, если в прошлый раз забыли переключиться на рабочую ветку. Убедитесь, что у вас не осталось не запушенных изменений, иначе они удалятся).</sup>
```
git reset --hard HEAD~1
```
> <sup>Подтянуть все актуальные изменения основной ветки.</sup>
```
git pull origin <mainbranch> --rebase
```
Теперь у вас актуальная версия проекта. Если знаете над чем точно будете работать, создавайте новую "фича"-ветку. Рекомендации по неймингу будут ниже. Если вы не создавали новую ветку, можете закоммитить изменения (НО не пушить), после чего переключиться на новую ветку.
```
git checkout -b <branchname>
```
и запушить ваши локальные коммиты. Все действия по ребейзу, переносу изменений на новую ветку и прочее должны происходить, когда весь код закоммичен и нет неиндексированных локальных изменений!
#### Нейминг веток (Рекомендации):
`<changes_type>/<commit_message>`

**changes_type** — тип изменений (например `feature/`, `bugfix/`, `style/`).

**commit_message** — краткое описание проделанных в ветке изменений, должно соответствовать типу изменений (например `feature/login-logic`, `style/hero-section`, `bugfix/401-error`).  


## Для продолжения работы в той же опубликованной ветке, если функционал не был закончен:

> <sup>Подтянуть изменения, которые были запушены в рабочую ветку, чтобы смёрджить их с локальными (не важно, если там тот же код).</sup> 
```
git pull origin <workbranch> --rebase
```
> <sup>Подятнуть изменения, которые были добавлены другими разработчиками или ваши изменения, которые были смёрджены из ПР в основную ветку `<mainbranch>`.</sup>
```
git pull origin <mainbranch> --rebase
```
Если всё сделано правильно, конфликтов быть не должно. Если конфликты возникли из-за изменений другого разработчика, аккуратно исправляем их, стараясь не удалить чужую работу. Проверяем работу функционала, которого задели конфликты. После внесенных изменений гит может потребовать запушить изменения с тегом `--force`, потому что локальная версия ветки (с исправленными конфликтами) не может засинхрониться с опубликованной веткой:
```
git push --force
```
<sup><sup>В других случаях `--force` не следует использовать.</sup></sup>

Вы всегда должны следить за тем, чтобы в рабочей ветке не оставалось неподтянутых изменений с основной (иначе вашу работу нельзя смёрджить => заказчик остается без деливери). Это можно легко проверить, зайдя на свою ветку на гите. 

**Не используйте `git pull ` без тега `--rebase`! Иначе вы создаете merge request, что также засоряет ветку.**


Если вы внесли много мелких правок — объедините ваши коммиты в один или несколько более сгруппированных. 
```
git rebase -i HEAD~<n>
```
Меняем коммиты в соответствие с инструкцией. Детальнее можно почитать здесь https://htmlacademy.ru/blog/boost/tools/how-to-squash-commits-and-why-it-is-needed или где-кгодно еще, но лучше всего описано, что за что отвечает в самом редакторе. 
```
git push --force
```

**Вы должны знать и понимать, что делает каждая из перечисленных команд.**


| New branch       | Continue Workbranch                | Rebase |
| ------------- |------------------| :----------|
| `git checkout <mainbranch>`    | `git pull origin <workbranch> --rebase`    | `git rebase ih HEAD~<n>`
| `git reset --hard HEAD~1`     | `git pull origin <mainbranch> --rebase` | <... changes>
| `git pull origin <mainbranch> --rebase`  | <... changes>         | `git push --force` |
| `git checkout -b <branchname>` | `git push --force`
