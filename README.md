### Using CSV data

The other way to provide your data is using CSV document format.
You can enter a publicly accessible URL (not behind any authentication) of a CSV file into the input field on the first page.
For example, a [raw URL](https://raw.githubusercontent.com/thoughtworks/build-your-own-radar/master/spec/end_to_end_tests/resources/sheet.csv) for a CSV file hosted publicly on GitHub can be used.
The format is just the same as that of the Google Sheet, the example is as follows:

```
name,ring,quadrant,isNew,description
Composer,adopt,tools,TRUE,"Although the idea of dependency management ..."
Canary builds,trial,techniques,FALSE,"Many projects have external code dependencies ..."
Apache Kylin,assess,platforms,TRUE,"Apache Kylin is an open source analytics solution ..."
JSF,hold,languages & frameworks,FALSE,"We continue to see teams run into trouble using JSF ..."
```

If you do not want to host the CSV file publicly, you can follow [these steps](#advanced-option---docker-image-with-a-csvjson-file-from-the-host-machine) to host the file locally on your BYOR docker instance itself.

**_Note:_** The CSV file parsing is using D3 library, so consult the [D3 documentation](https://github.com/d3/d3-request/blob/master/README.md#csv) for the data format details.

### Using JSON data

Another other way to provide your data is using a JSON array.
You can enter a publicly accessible URL (not behind any authentication) of a JSON file into the input field on the first page.
For example, a [raw URL](https://raw.githubusercontent.com/thoughtworks/build-your-own-radar/master/spec/end_to_end_tests/resources/data.json) for a JSON file hosted publicly on GitHub can be used.
The format of the JSON is an array of objects with the the fields: `name`, `ring`, `quadrant`, `isNew`, and `description`.

An example:

```json
[
  {
    "name": "Composer",
    "ring": "adopt",
    "quadrant": "tools",
    "isNew": "TRUE",
    "description": "Although the idea of dependency management ..."
  },
  {
    "name": "Canary builds",
    "ring": "trial",
    "quadrant": "techniques",
    "isNew": "FALSE",
    "description": "Many projects have external code dependencies ..."
  },
  {
    "name": "Apache Kylin",
    "ring": "assess",
    "quadrant": "platforms",
    "isNew": "TRUE",
    "description": "Apache Kylin is an open source analytics solution ..."
  },
  {
    "name": "JSF",
    "ring": "hold",
    "quadrant": "languages & frameworks",
    "isNew": "FALSE",
    "description": "We continue to see teams run into trouble using JSF ..."
  }
]
```

If you do not want to host the JSON file publicly, you can follow [these steps](#advanced-option---docker-image-with-a-csvjson-file-from-the-host-machine) to host the file locally on your BYOR docker instance itself.

**_Note:_** The JSON file parsing is using D3 library, so consult the [D3 documentation](https://github.com/d3/d3-request/blob/master/README.md#json) for the data format details.

### Building the radar

```
docker build -t wwwthoughtworks/build-your-own-radar
```

### Running the radar
```
docker run --rm -p $PORT:80  wwwthoughtworks/build-your-own-radar1
```

$PORT - внешний порт.

### Csv данные

Сервер ищет в локальной папке файл index.csv, если он его не находит, то производится
попытка открыть index.json. Если этих файлов нет, то отображается стартовая страница.

Данные для радара добавляются/хранятся в папки src/localfiles.

Напрмер, производится запрос localhost:80/android/. Тогда в папке src/localfiles/android/ ищется
файл index.csv или index.json. Если запрос на localhost:80/backend/- то в каталоге
src/localfiles/backend/.
