---
layout: article
---
Для этих целей мы можем использовать команду `docker container exec`. Это исполнит заданную команду в контейнере. 

```
docker container exec 3df3eff8d66c hostname
```

В данном случае она покажет имя хоста, т.е. напечатает уникальный идентификатор, который устанавливается в качестве имени хоста для контейнера.

Это одна команда, а если нам требуется выполнить их несколько? Нам было бы удобно просто поработать в оболочке этого контейнера. Для этого мы вновь запускаем команду `docker container exec`, но на этот раз с терминалом и в интерактивном режиме. 

```
docker container exec -it 3df3eff8d66c /bin/bash
```

Далее укажем команду, которая требуется. Нам нужна оболочка, в образе ubuntu на находится по пути `/bin/bash`.

Как видишь, приглашение консоли изменилось. Мы попали в оболочку контейнера и можем запускать в нем другие команды, т.е. сейчас мы работаем внутри контейнера. Мы можем запускать команды, смотреть вывод, что-то менять и проверять. Эта техника особенно полезна в целях устранения неполадок.

```
root@3df3eff8d66c:/# ps aux
```

Допустим у нас веб-приложение, работающее в контейнере, но с ним что-то не так. Мы бы хотели попасть внутрь этого контейнера, чтобы проверить логи сервера, конфигурационные файлы приложения или ещё что-то. В этом нам поможет команда `container exec`. Чтобы выйти из этой оболочки, я напишу `exit`.

```
root@3df3eff8d66c:/# exit
```

У нас есть альтернатива `exec` - это `attach`. С его помощью мы можем снова подключиться к контейнеру. Как ты помнишь, у нас сейчас два работающих контейнера из образа ubuntu. Я делаю:

```
docker container attach 3d
```

После этого я попадаю в уже запущенный шелл, где могу запускать команды. На первый взгляд механизмы `attach` и `exec` похожи, но это совсем не так. Давай в этом убедимся. Я запускаю команду:
