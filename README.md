<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="">
    <meta name="author" content="">
    <title>json</title>
  </head>
<body>
  <h1>JSON 是存储和交换文本信息的语法。类似XML。JSON比XML更小、更快、更易解析。JSON 指的是javascript对象表示法。</h1>
  <h2>在Javascript 中创建 JSON 对象</h2>
  <p>
    name:<span id="jname"></span><br />
    Age:<span id="jage"></span><br />
    Address:<span id="jstreet"></span><br />
    Phone:<span id="jphone"></span><br />
  </p>
  <hr />
  <h2>通过JSON 字符串来创建对象</h2>
  <p>First Name:<span id="fname"></span></p>
  <hr />
  <h2></h2>
  <p>
    First Name:<span id="fname1"></span><br />
    last Name:<span id="lname1"></span><br />
  </p>

<script>
  var JSONObject = {"name":"Bill Gates", "street":"Fifth Avenue New York 666", "age":56, "phone":"555 1234567"};
  document.getElementById("jname").innerHTML = JSONObject.name;
  document.getElementById("jage").innerHTML = JSONObject.age;
  document.getElementById("jphone").innerHTML = JSONObject.phone;
  document.getElementById("jstreet").innerHTML = JSONObject.street;

  var employees = [
    {"firstName": "Bill", "lastName": "Gates"},
    {"firstName": "George", "lastName": "Bush"},
    {"firstName": "Thomas", "lastName": "Carter"}
  ];
  employees[1].firstName = "Jobs";
  document.getElementById("fname").innerHTML = employees[1].firstName;
  document.getElementById("fname").innerHTML = employees[0].lastName;

  var txt = '{"exployees2":['+
            '{"firstName":"Bill", "lastName": "Gates"},'+
            '{"firstName": "George", "lastName":"Bush"},'+
            '{"firstName":"Thomas", "lastName":"Carter"}]}';
  var obj = eval("(" + txt + ")");
  document.getElementById("fname1").innerHTML = obj.exployees2[0].firstName;
  document.getElementById("lname1").innerHTML = obj.exployees2[2].lastName;


  /*
    在 JS 中将 JSON 的字符串解析成 JSON 数据格式，一般有两种方式：
    1、一种为使用 eval() 函数
    2、另外一种就是使用 Function 对象来进行返回解析
  */

  /*
  JSON 的语法可以表示为三种类型的值：
  1，简单值
  2，对象
  3，数组

  JSON 和javascript的语法相同，可以在JSON中表示字符串，数值，布尔值和NULL。JSON不支持javascript中的特 殊值undefined。
  早期 JSON 解析器基本上用的是javascript的 eval()函数。eval()函数可以解析、解释并返回javascript对象和数组。
  但是使用 evail() 对 JSON 数据结构求值存在风险，可能会执行一些恶意代码。 对于不能支持原生 JSON 解析的浏览器，使用shim。

  JSON 对象有两个方法：
  1,stringify() 将 javascript 对象序列化为 JSON 字符串
  2,parse() 将 JSON 字符串解析为原生 javascript 值

  */

  var book = {
    title: "Professional JavaScript",
    authors: [
      "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
  };
  var jsonText = JSON.stringify(book);
  // {"title": "Professional JavaScript", "authors": ["Nicholas C. Zakas"], "edition": 3, "Year": 2011}

  var bookCopy = JSON.parse(jsonText);

  //一、序列化选项
  var book = {
    title: "Professional JavaScript",
    authors: [
      "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
  };
  //1、过滤结果
  var jsonText = JSON.stringify(book, ["title", "edition"]); // {"title": "Professional JavaScript", "edition": 3}

  //2、字符串缩进
  var jsonText = JSON.stringify(book, null, 4);
  var jsonText = JSON.stringify(book, null, " - -");

  //3、toJSON()方法
  var book = {
    "title": "Professional JavaScript",
    "authors": [
      "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011,
    toJSON:function() {
      return this.title;
    }
  };
  var jsonText = JSON.stringify(book);

  // 二、解析选项
  var book = {
    "title": "Professional JavaScript",
    "authors": [
      "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011,
    releaseDate: new Date(2011, 11, 1)
  };
  var jsonText = JSON.stringify(book);

  var bookCopy = JSON.parse(jsonText, function(key, value) {
    if(key == "releaseDate") {
      return new Date(value);
    } else {
      return value;
    }
  });
  alert(bookCopy.releaseDate.getFullYear());

</script>

</body>
</html>
