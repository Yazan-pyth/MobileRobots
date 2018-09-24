Использование docker

0. Установливаем Docker по инструкции. https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#os-requirements. Настраиваем Docker для работы с ним без root доступа (без sudo) https://docs.docker.com/install/linux/linux-postinstall/
Следующие команды выполняем из папки, куда клонирован репозиторий из под обычного пользователя
1. Собираем образ (выполняется один раз, а также при изменении файла образа Dockerfile) 
``` bash
$ docker/build_docker
```
2. Запускаем контейнера (выполняется каждый раз для запуска контейнера) Также при выполнении этой команды в контейнере создается пользователь с именем текущего пользователя системы ($USER). Текущая директория (папка проекта) монтируется в докер по адресу `/home/<имя пользователя>/local/workspace`. Вся домашняя папка текущего пользователя монтируется в доке по адресу `/host`
``` bash	
$ docker/start_docker
```
3. Подсоединяем консоль к контейнеру. (можно выполнить несколько раз из разных терминалов - сколько нужно терминалов внутри докера)
``` bash
	$ docker/attach_docker
```
В результате выполнения этой команды текущий терминал оказывается подключен к докеру - оказываемся в командной строке, выполняющейся внутри докера. Все команды, выполняемые из этой консоли выполняются внутри докера (изолировано от нашей системы). Изначально мы оказываемся в ROS воркспейсе(`/home/<имя пользователя>/local/workspace/mr_ws`) нашего проекта. В первый раз необходимо собрать проект с помощью команды `catkin_make` и после сборки проинициализировать workspace 
``` bash
$ source devel/setup.bash
```
При повторных запусках консоли - инициализация workspace осуществляется автоматически.
4. Запуск проектов возможен с помощью 'roslaunch' и 'rosrun'. Также можно запустить первый проект с помощью скрпита `start.sh`. В последнем случае должно появиться окно симулятора Gazebo и окно rqt - в котором с помощью плагина publish message можно задать скорость движения робота
5. Для возврата из докера используется команда 
``` bash
$ exit
```
после этого терминал окажется в основной системе
6. Для просмотра текущих запущенных образов докера можно использовать команду:
``` bash
$docker ps
```
7. Для того, чтобы остановить докер:
``` bash
$ docker/stop_docker
```
Все изменения в докере кроме тех, что сделаны в папке проекта `/home/<имя пользователя>/local/workspace` после остановки образа будут утеряны. При выключении/перезагрузке компьютера все образы будут остановлены.

	
