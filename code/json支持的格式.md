## JSON格式的特殊格式

```java
var json1 = '{}';
var json2 = '{"myCount": null}';
var json3 = '{"myCount": 0}';
var json4 = '{"myString": ""}';
var json5 = '{"myString": "null"}';
var json6 = '{"myArray": []}';

console.log(JSON.parse(json1)); // {}
console.log(JSON.parse(json2)); // {myCount: null}
console.log(JSON.parse(json3)); // {myCount: 0}
console.log(JSON.parse(json4)); // {myString: ""}
console.log(JSON.parse(json5)); // {myString: "null"}
console.log(JSON.parse(json6)); // {myArray: []}
```

* JSON不支持`Decimal`格式的参数。