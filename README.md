# fetchdata

Another way to consume a REST API in Dart Flutter

## Create an Stateful widget

> stful

## import async and convert

```
import 'dart:convert';
import 'dart:async';

```

## Install http package

> dependencies
>>   http: ^0.12.0+4
>
> flutter pub get
>
```
import 'package:http/http.dart' as http;
```

## Create variables

```
  final String url = "https://swapi.co/api/people";
  List data;
```

## Create initState

```
  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    this.getJsonData();
  }
```

## Create method inside class

```

  Future<String> getJsonData() async {
    var response = await http.get(
      // Encode URL
      Uri.encodeFull(url),
      // only accept json response
      headers: {"Accept": "application/json"},
    );

    print(response.body);

    setState(() {
      var convertDataToJson = json.decode(response.body);
      data = convertDataToJson['results'];
    });
    return "Success";
  }
```

## Finally use it in a ListView builder

```
ListView.builder(
        itemCount: data == null ? 0 : data.length,
        itemBuilder: (BuildContext context, int index) {
          return Container(
            child: Center(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: <Widget>[
                  Card(
                    child: Container(
                      child: Text(data[index]['name']),
                      padding: EdgeInsets.all(
                        20.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          );
        },
      ),
        
```