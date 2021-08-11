![logo]

# PACS + BD + OHIF

## Настройка перед запуском

```
Загрузка проекта:

cd /opt/
git clone *ссылка на гит данного проекта*

Настройка базы данных путем создания файла переменных:

cd /opt/dir/to/project

cat > .env <<EOF 
POSTGRES_USER=*your_user*
POSTGRES_PASSWORD=*your_password*
POSTGRES_DB=*your_db_name*
EOF

В файле app/conf/conf.json

Указать настройки подлкючения (указывали выше) к базе данных для Orthanc:

  "Database": "",
  "Username": "",
  "Password": "",

А так же настройки самого Orthanc:

  "Name" : "", - Название Вашего пакса
  "DicomPort" : your_port, - порт для подключения клиентов
  "DicomAet" : "", - AET для подключение клиентов

Создание пользователей происходит в данном пункте:

  "RegisteredUsers" : {
    "example" : "example" - уже созданный пользовтель
  },

В файле app/conf/viewer.js указать слудующее:

  name: 'some_name',
  wadoUriRoot: 'http://*dns or ip your server*/pacs/wado',
  qidoRoot: 'http://*dns or ip your server*/pacs/dicom-web',
  wadoRoot: 'http://*dns or ip your server*/pacs/dicom-web',

Создать папку для хранения данных на хостовой машине:

  sudo mkdir -p /opt/data01/orthanc_data/

Запустить проект находясь в папке с проектом:

sudo docker-compose up

```

## Тест запуска приложения

Переходим по ссылке http://*dns or ip server*/pacs/ - должен открыться Orthanc, логин и парль: example

Далее заходим в Ohif, http://*dns or ip server*/ должен открыться Ohif, логин и парль: example, как и в Orthanc, если создать пользователя в Orthanc то и в Ohif он тоже будет работать.




## Help URL
---
[Orthanc Book](https://book.orthanc-server.com/index.html)

[Docker Hub](https://hub.docker.com/r/jodogne/orthanc-plugins)

---
[logo]: https://book.orthanc-server.com/_images/orthanc.png
