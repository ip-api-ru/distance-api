# Distance API - расчет дистанции между точками a и b.

###### Версия API

- 4.0 (от 04 июля 2019 года).

###### HTTPS/HTTP

- Поддержка HTTPS осуществляется через адрес https://ssl.ip-api.ru/;
- Поддержка HTTP осуществляется через адрес http://nossl.ip-api.ru/.

###### Ключи

- Обязательным ключем является apiKey - Ваш уникальный API-ключ для доступа к сервису;
- Distance API поддерживает следующие ключи, с которыми необходимо делать запросы: a (откуда), b (куда);
- Дополнительные ключи: litersPer100, pricePerLiter и project;
- Ключи a и b могут содержать страну, город, улицу, шоссе, проспект, переулок, тупик, проезд, номер дома, строение, корпус, литер и владение. Кроме того, значениями ключей могут быть и названия аэропортов, торговых центров и других объектов массового притяжения людей.
- Ключ litersPer100 должен иметь значение расхода топлива на 100 км;
- Ключ pricePerLiter должен иметь значение стоимости топлива за 1 литр.

    Используйте в запросе ключ project со значением названия проекта, чтобы статистика запросов отображала количество запросов по Вашему конкретному проекту (если название проекта будет содержать не только латинские буквы, не забудьте делать кодировку при запросе).
    
###### Пример и описание данных из ответа

    Пример URL на отправку запроса на получение информации с учетом расхода топлива и ответ:
    https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=Россия, Москва, шоссе Энтузиастов 36&b=Россия, Санкт-Петербург, Невский проспект 20&litersPer100=11&pricePerLiter=48.29
```json
{
"status":"success",
"trackDistanceKilometers":"727",
"distanceTime":"10:34:00",
"trackDistanceMiles":"452",
"lineDistanceKilometers":"639",
"a":"Россия, Москва, шоссе Энтузиастов 36",
"b":"Россия, Санкт-Петербург, Невский проспект 20",
	"fuelInfo": {
		"litersPer100":"11",
		"pricePerLiter":"48.29",
		"trackDistanceLiters":"79.97",
		"trackDistanceFuelPrice":"3861.75"
	}
}
```

В данном ответе Вы получаете дистанцию от точки a и b в километрах (trackDistanceKilometers), милях (trackDistanceMiles), по прямой в километрах (lineDistanceKilometers), примерное время в пути (distanceTime) без учета пробок, расчет расхода топлива на 100 км (trackDistanceLiters) и его стоимость (trackDistanceFuelPrice) в рублях РФ.
```
Для удобства расчета дистанции на Вашем сайте у нас есть приложение-виджет distanceWidget. distanceWidget - это готовое решение, которое встраивается на Ваш сайт через html-тег iframe.
```

###### Все возможные данные из ответа IP API:

|Название|Описание|Пример|Тип|
| --- | --- | --- | --- |
|status||Статус запроса (fail - отклонен или success - выполнен)|success|String|
|trackDistanceKilometers|Дистанция в километрах|727|String|
|distanceTime|Время преодоления дистанции (без учета пробок)|10:34:00|String|
|trackDistanceMiles|Дистанция в милях|452|String|
|lineDistanceKilometers|Дистанция в километрах по прямой|639|String|
|a|Откуда|Россия, Москва, шоссе Энтузиастов 36|String|
|b|Куда|Россия, Санкт-Петербург, Невский проспект 20|String|
|fuelInfo|Массив данных по при ключах litersPer100 и pricePerLiter|		
|litersPer100|Расход топлива на 100 км|11|String|
|pricePerLiter|Стоимость топлива за 1 литр|48.29|String|
|trackDistanceLiters|Расход топлива на всю дистанцию|79.9|String|
|trackDistanceFuelPrice|Полная стоимость топлива на всю дистанцию|3858.37|String|

###### Использование API
jQuery
```js
$.ajax({
  	url: 'https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда',
  	/*HTTP url: 'http://nossl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда', */   
  	dataType: 'json',
    success: function(data) {
        alert(data.a + ' - ' + data.b + '\n' + data.trackDistanceKilometers + '\n' + data.trackDistanceMiles);
    }
});
```
Node.js
```js
const request = require('request-promise')
request('https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда')
/* HTTP request('http://nossl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда') */

  .then(response => console.log(JSON.parse(response)))
  .catch(err => console.log(err))
```
php
```php
$data = json_decode(file_get_contents('https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда'));
/* HTTP $data = json_decode(file_get_contents('http://nossl.ip-api.ru/distance-api.json?apiKey=apiKey=ваш-api-ключ&a=откуда&b=куда')); */
var_dump($data);
```
Python
```python
requests.get('https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда')
/* HTTP requests.get('http://nossl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда') */
```
Ruby
```ruby
require 'json'
require 'open-uri'

JSON.parse(open('https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда').read)
/* HTTP JSON.parse(open('http://nossl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда').read) */
```
Kotlin
```kotlin
val result = URL("https://ssl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда").readText()
/* HTTP val result = URL("http://nossl.ip-api.ru/distance-api.json?apiKey=ваш-api-ключ&a=откуда&b=куда").readText() */

Официальный сайт сервиса IP-API: https://ip-api.ru/. Документация по всем API: https://ip-api.ru/documentation/ или https://github.com/ip-api-ru/
