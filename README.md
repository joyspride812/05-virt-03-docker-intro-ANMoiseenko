Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»
Выполнил Моисеенко Алексе  й Николаевич группа SHDEVOPS-17

Задача 1

Сценарий выполнения задачи:

Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.21.1;
Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

Ответ.

https://hub.docker.com/repository/docker/anmoiseenko/custom-nginx/general

Задача 2

1.Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
2.Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3.Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
4.Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

Ответ.

1.![image](https://github.com/user-attachments/assets/4f283712-db93-4543-9bbd-3220b3111a51)
2.![image](https://github.com/user-attachments/assets/8a96bbfb-5010-42f9-84fc-d409f8a5df0f)
3.![image](https://github.com/user-attachments/assets/28145e93-b2c4-4d3c-85b7-4a61d13c7f32)
4.![image](https://github.com/user-attachments/assets/cc72e83b-5911-4cee-b78c-5e073acd9504)
![image](https://github.com/user-attachments/assets/ec305e58-9f9f-4e50-891e-298bfeca5b73)


Задача 3

1.Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2.Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3.Выполните docker ps -a и объясните своими словами почему контейнер остановился.
4.Перезапустите контейнер
5.Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6.Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7.Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8.Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
9.Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
10.Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
11.Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно.
12.Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Ответ.

1.![image](https://github.com/user-attachments/assets/8f61617b-137a-463f-b096-47a3f8b56672)

2.![image](https://github.com/user-attachments/assets/f6dc8348-c8be-4796-a7d7-5ec5714adc2d)

3.Потому что был отправлен  сигнал SIGINT(сигнал остановки процесса) оосновному процессу контейнера custom-nginx-t2.

![image](https://github.com/user-attachments/assets/211f5ad5-1b51-4b87-910d-be6f7c3e787d)

4.![image](https://github.com/user-attachments/assets/b874673d-a9ff-487f-a94d-c9557682ca77)

5.![image](https://github.com/user-attachments/assets/a6d384a0-5952-4ad5-99be-5a2babed29ce)

6.![image](https://github.com/user-attachments/assets/72d161e8-efb5-4256-81ca-35c7a85c34e7)

7.![image](https://github.com/user-attachments/assets/d8db2212-a5a9-41be-8d48-98b47f6df82a)

8.![image](https://github.com/user-attachments/assets/6f1d01b4-52ca-4e8a-a8ec-cca9dcb5b73d)

9.![image](https://github.com/user-attachments/assets/99f3b18b-9ec8-49f4-9141-f08c1e1cef98)

10.Проблема в том, что nginx в контейнере слушает 81 порт, а внутрь контейнера настроен проброс 8080:80

![image](https://github.com/user-attachments/assets/4fdb1254-01ca-4ef7-9279-2607f654bdeb)

11.![image](https://github.com/user-attachments/assets/736c110e-d1e0-4022-94fa-34df6ef0d94d)
![image](https://github.com/user-attachments/assets/e1fab547-3cd3-4a78-a79f-5f163c0732f9)
12.![image](https://github.com/user-attachments/assets/bd477895-efe9-47d2-a59a-b7c1280eabc4)

