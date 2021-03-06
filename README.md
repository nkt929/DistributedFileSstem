# Distributed File System

![Interface](https://i.imgur.com/EByMnnR.png)

## Authors

-   Bogdanova Alina
-   Dubina Nikita
-   Sirgalina Rufina

## NS API

| API                                                                     | HowTo Implement implement?                                                                                                                                                                                                                                                    |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** `/refresh`                                                      | client-> nameserver                                                                                                                                                                                                                                                           |
| **GET** `/copy?from=...&to=...` (`from` and `to` - pathes to the files) | [PythonImpl](https://stackoverflow.com/questions/123198/how-do-i-copy-a-file-in-python)                                                                                                                                                                                       |
| **GET** `/move?from=...&to=...` (`from` and `to` - pathes to the files) | [PythonImpl](https://stackoverflow.com/questions/8858008/how-to-move-a-file)                                                                                                                                                                                                  |
| **GET** `/mkdir?path=...`                                               | [PythonImpl](https://thispointer.com/how-to-create-a-directory-in-python/)                                                                                                                                                                                                    |
| **GET** `/rmdir?path=...`                                               | [Here use os.rmdir](https://stackoverflow.com/questions/6996603/how-to-delete-a-file-or-folder)                                                                                                                                                                               |
| **GET** `/touch?path=...`()                                             | [If you don't remember](https://stackoverflow.com/questions/12654772/create-empty-file-using-python)                                                                                                                                                                          |
| **GET** `/rm_file?path=...`                                             | [Here use os.remove](https://stackoverflow.com/questions/6996603/how-to-delete-a-file-or-folder)                                                                                                                                                                              |
| **GET** `/download?path=...`                                            | ???                                                                                                                                                                                                                                                                           |
| **POST** (upload) ????                                                  | ???                                                                                                                                                                                                                                                                           |
| **GET** `/info?name=...`                                                | REMOVED (data passed with fs)[Get file size](https://stackoverflow.com/questions/6591931/getting-file-size-in-python) <br>[Date and time of creation and modification](https://stackoverflow.com/questions/237079/how-to-get-file-creation-modification-date-times-in-python) |
| **rm_rf** `/clear_all`                                                  | [HOWTO rm non-empty dir](https://stackoverflow.com/questions/303200/how-do-i-remove-delete-a-folder-that-is-not-empty)                                                                                                                                                        |

## Docker

### front

```
cd ./front
docker build -t front .
docker run -it -p 8080:8080 --rm --name dockerize-front front
```

### stupid way of testing storages

To start Storage Server
```
cd ./storage_server
docker build -t storage .
docker run -p 5000:5000 storage
```

To start Name Server
```
cd ./name_server
export FLASK_APP=main.py
flask run --host 0.0.0.0 --port 5001
```

Use it to avoid collisions between ports. Also check that /front/src/requests should contain this setup:
```
	baseURL: "http://0.0.0.0:5001",
```