MongoDB
=======

Install MongoDB for Windows. 
----------------------------

MongoDB 사이트에서 바이너리 버전을 다운로드 받고 압축을 푼다.
* http://downloads.mongodb.org/win32/mongodb-win32-x86_64-2008plus-ssl-3.4.1.zip


```
D:\dev\mongodb
```

Set up the MongoDB environment.
------------------------------

데이터 디렉토리를 생성한다.

```
cd D:\dev\mongodb
mkdir data\db
```

Start MongoDB
-------------

```
mongod --dbpath D:\dev\mongodb\data --rest
```

Connect to MongoDB
------------------

```
mongo
```

Connect to Monitoring Web 
-------------------------

```
http://localhost:28017/
```

MapReduce
---------

```javascript
db.words.save({text:'read a book'});
db.words.save({text:'write a book'});
db.words.find();

map = function() { 
  var res = this.text.split(' '); 
  for (var i in res) { 
    key = {word:res[i]}; 
    value = {count:1}; 
    emit(key, value); 
  } 
}

reduce = function(key, values) { 
  var totalcount = 0; 
  for (var i in values) { 
    totalcount = values[i].count + totalcount; 
  } 
  return {count:totalcount}; 
}

db.words.mapReduce(map, reduce, "wordcount");
db.wordcount.find();
```
  
