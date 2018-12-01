# Процесс развертывания сервера
-------------------------------
Для начала необходимо скачать, установить и настроить следующий список программ:
  - Виртуальную машину (VirtualBox, образ Ubuntu 16.04);
  - Git;
  - Vagrant

Далее потребуется создать конфигурацию для запуска сервера. Для этого воспользуемся приложением **PuPHPet**. Данный сервис позволит нам создать собственный конфигурационный архив для запуска сервера. В начале необходимо перейти по [ссылке](https://puphpet.com/) и нажать кнопку "Get started right away".

## Выбор виртуальной машины и настройка ее параметров 
---------------------------
После нажатия кнопки "Get started right away", сервис предложит выбрать, на какой виртаульной машине необходимо запустить сервис. В данном находятся 2 пункта - *Provider* и _Distro_. В пункте *Provider* нам необходимо выбрать опцию **VirtualBox**, во втором же пункте нужно выбрать дистрибутив **Ubuntu Xenial 16.04 LTS x64**. Далее система предлагает нам дать название создаваемой виртуальной машине и выбрать имя хоста. В пункте *Iternal Identifier* и *Hostname* пишем **bott/**. В графах *IP Address*, *Memory* и *CPUs* оставляем значения, **заданные по умолчанию**. Параметры в разделе *Forwarded ports* тоже оставляем **по умолчанию**. Затем нам предлагается указать каталоги, где будет находиться виртуальная машина, и каталоги, которые будут являться __общими__ как для хоста, так и для виртуальной машины. В пункте *Foulder Source* указываем путь **C://bott/www** - сюда будет помещена виртуальная машина, а в пункте *Folder Target* указываем **/var/www/bott/** - это каталог в нашей создаваемой виртуальной машине. Пункт *Shared Folder Type* оставляем по умолчанию, т.е. **Default**. *Enable Proxy* отключаем.

## Пакеты создаваемой системы
-----------------------------
В данном пункте можно увидеть, что PuPHPet по умолчанию добавил следующие компоненты:
  - bash-completion;
  - htop;
  - vim
Данный раздел необходимо **оставить без изменений** и перейти к следующим параметрам. Разделы **Пользователи и группы**, **Время** и **Фаервол** также пропускаем, настройка параметров в данных разделах не требуется.

## Настройка конфигурационного файла Resolv.conf
------------------------------------------------
В данном разделе PuPHPet предлагает пользователю настроить файл, который предоставляет виртуальной машине системе доступ к DNS. По умолчанию в пункт *Name Server IP Address* забиты следующие IP-адреса:
  - 8.8.8.8
  - 8.8.4.4

Данные IP-адреса пользователю необходимо **удалить**, так как их присутствие в конфигурационном архиве вызывет проблемы при настройке сети виртуальной машины. Поле *Name Server IP Address* следует оставить пустым, как и поля *Search List for Host-Name Lookup* и *Local Domain Name*. Далее пользователю необходимо оставить настройки **по умолчанию** в разделах **Cron Jobs** и **Custom Files**.

## Выбор и настройка веб-сервера для проекта
-------------------------------------
В качестве веб-сервера для проекта была выбран Apache. Пользователю необходимо дойти до раздела под названием **Nginx**. В верхней части данного раздела будет по умолчанию включена опция *Install Nginx*. Данную опцию нужно **отключить** и перейти в следующий раздел под названием **Apache** и активировать опцию *Install Apache*. Пункт *Apache Modules* необходимо оставить **без изменений**. В графе *Server Name* указываем **bott**, в поле *Document Root* вносим следующий путь **/var/www/bott**. Далее необходимо перейти к пункту *Path* и там прописать путь **/var/www/bott**. Остальные пункты данного раздела следует оставить **без изменений**.

## Версия PHP и выбор СУБД для проекта
--------------------------------------
В разделе **Install PHP** пользователю предлагается выбрать версию языка PHP для разработки. В пункте *PHP Version* выбираем **7.2**, остальные пункты оставляем **по умолчанию**. Далее переходим в раздел **MySQL**. Так как именно *MySQL* была выбрана в качестве СУБД для проекта, необходимо активировать пункт *Install MySQL*. В пункте *Root Password* необходимо задать пароль и запомнить его. На этом настройка конфигурационного архива завершена и пользователю остается лишь скачать его.

## Запуск сконфигурированной виртуальной машины
-----------------------------------------------
Для того, чтобы запустить установку сконфигурированной виртуальной машины, необходимо распаковать скачанный архив в папку **C://bott**. Далее необходимо открыть консоль *Windows Power Shell* и с перейти в каталог с распакованным архивом.
```
cd C:/bott/*название архива*
```
После перехода в данный каталог необходимо запустить процесс установки
```
vagrant up
```
После завершения процесса установки все файлы, находящиеся в папке **C://bott/www** будут доступны на виртуальной машине.