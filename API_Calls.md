#Valid API Calls

Http get Via CometVisu-binding
------------------------------

This binding will return:

Successful
```
{"success":"1"}
```

Fail
```
{"success":"0"}
```


Turn Off
```
http://192.168.137.88:8080/services/cv/w?a=gpio_led17&v=OFF
```

Turn On
```
http://192.168.137.88:8080/services/cv/w?a=gpio_led17&v=ON
```