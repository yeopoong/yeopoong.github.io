MongoDB
=======

설치 및 실행 
-----------

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
  
