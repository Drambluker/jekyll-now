---
layout: post
title: Как удалить пункт Ubuntu из UEFI (остатки ubuntu/grub)?
---

![Ubuntu - Linux for human beings](/images/Ubuntu - Linux for human beings.png)

*Источник: [florisla (Flickr)](https://www.flickr.com/photos/florisla/293231813)*

Запись [*Ubuntu*](https://www.ubuntu.com/) из *UEFI* можно удалить тремя способами:

 1. Через *BIOS*, при помощи опции *Delete Boot Option*;
 2. Через `efibootmngr`, при помощи *Live CD Ubuntu*;
 3. Через [`bcdedit`](https://technet.microsoft.com/ru-ru/library/cc709667%28v=ws.10%29.aspx) (в [*Windows*](https://www.microsoft.com/ru-ru/windows)).

Но после проделывания вышеперечисленных способов, как только вы перезагрузите компьютер, пункт [*Ubuntu*](https://www.ubuntu.com/) появится в списке доступных вариантов загрузки снова!

Для того, чтобы этого не произошло, нам необходимо удалить с системного диска *EFI* папку *ubuntu*.

Проделать это мы можем с помощью ряда действий:

 1. Загружаемся из-под [*Windows*](https://www.microsoft.com/ru-ru/windows) и запускаем командную строку от имени
    администратора;
 2. Запускаем [*DiskPart*](https://technet.microsoft.com/ru-ru/library/cc766465%28v=ws.10%29.aspx) (это можно сделать, введя команду `diskpart`);
 3. Просматриваем в [*DiskPart*](https://technet.microsoft.com/ru-ru/library/cc766465%28v=ws.10%29.aspx) список наших дисков (вводим команду `list
    disk`);
 4. Выбираем диск, на котором находится раздел *EFI* (это делается при
    помощи команды `select disk #`);
 5. Просматриваем разделы/тома жёсткого диска (команда `list volume`);
 6. Выбираем раздел с *EFI* (команда `select volume ##`);
 7. Присваиваем этому разделу букву (команда `assign`) и выходим из
    [*DiskPart*](https://technet.microsoft.com/ru-ru/library/cc766465%28v=ws.10%29.aspx) (команда `exit`).

Далее можно продолжать свои манипуляции в командной строке, либо же перейти в привычный для многих пользователей *«Проводник»*.

Если выбрали командную строку:

 1. После выхода из [*DiskPart*](https://technet.microsoft.com/ru-ru/library/cc766465%28v=ws.10%29.aspx), переходим на наш новый диск, которому мы
    до этого присвоили букву, и просматриваем директории на нём (команда
    `dir`);
 2. Переходим в директорию *boot* и удаляем в ней директорию *ubuntu*
    (команда `rmdir ubuntu`); Переходим на диск *«C»* и снова запускаем
    [*DiskPart*](https://technet.microsoft.com/ru-ru/library/cc766465%28v=ws.10%29.aspx);
 3. Выбираем раздел с *EFI*, вышеописанным способом, и отсоединяем его
    (команда `remove`); Выходим и перезагружаем компьютер.

Если выбрали *«Проводник»*, то выполняем в нём аналогичным образом 1-2 действия. Далее возвращаемся в командную строку и выполняем 3-5 действия, описанные выше.

----------
**Источник:** [**Форум русскоязычного сообщества Ubuntu**](http://forum.ubuntu.ru/index.php?topic=239344.0)
