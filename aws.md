AWS
=======

Amazon Linux
-----------

  * Amazon Linux는 CentOS를 기반으로 하고 있는 배포판이다.
  * CentOS 는 Red Hat Enterprise Linux를 무료로 사용할 수 있도록 만든 배포판이다.

  This is a hyperlink to [Google](http://google.com).

  Images are like hyperlinks, but with an exclamation mark in front of them:
  ![](http://placekitten.com/g/250/250)


| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

MongoDB
-------

```javascript
mongod --dbpath D:\dev\mongodb\data
mongo
```

MapReduce
---------

```javascript
db.words.save({text:'read a book'});
db.words.save({text:'write a book'});
db.words.find();

map = function() { var res = this.text.split(' '); for (var i in res) { key = {word:res[i]}; value = {count:1}; emit(key, value); } }
reduce = function(key, values) { var totalcount = 0; for (var i in values) { totalcount = values[i].count + totalcount; } return {count:totalcount}; }

db.words.mapReduce(map, reduce, "wordcount");
db.wordcount.find();
```
  
