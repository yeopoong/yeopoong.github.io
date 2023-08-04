---
layout: post
published: true
title: "2408. Design SQL"
categories: interview
tags: medium design 
---

> 배열 이름과 열로 표시되는 n개의 테이블이 주어질 때 각 연산을 구현하라.  
> : names[i]는 i번째 테이블의 이름이고 columns[i]는 i번째 테이블의 열 수


[2408. Design SQL](https://leetcode.com/problems/design-sql/)

```java
class SQL {

    Storage storage;
    
    public SQL(List<String> names, List<Integer> columns) {
        storage = new Storage(names, columns);
    }
    
    public void insertRow(String name, List<String> row) {
        Table table = storage.getTable(name);
        table.insert(row);
    }
    
    public void deleteRow(String name, int rowId) {
        Table table = storage.getTable(name);
        table.delete(rowId);       
    }
    
    public String selectCell(String name, int rowId, int columnId) {
        Table table = storage.getTable(name);
        List<String> row = table.getRow(rowId);
        return row.get(columnId - 1);
    }

    class Table {
        int nextRowId = 1;
        Map<Integer, List<String>> contents;
        String tableName;

        Table(String tableName) {
            contents = new HashMap<>();
            tableName = tableName;
        }

        int getNextRowId() {
            return nextRowId++;
        }

        void insert(List<String> row) {
            contents.put(getNextRowId(), row);
        }

        void delete(int rowId) {
            contents.remove(rowId);
        }

        List<String> getRow(int rowId) {
            return contents.get(rowId);
        }
    }

    class Storage {
        Map<String, Table> tableCollection;
        List<Integer> columns;
        List<String> names;

        Storage(List<String> names, List<Integer> columns) {
            tableCollection = new HashMap<>();
            columns = columns;
            names = names;
            for (String name : names) {
                tableCollection.put(name, new Table(name));
            }
        }

        Table getTable(String tableName) {
            return tableCollection.get(tableName);
        }
    }
}

/**
 * Your SQL object will be instantiated and called as such:
 * SQL obj = new SQL(names, columns);
 * obj.insertRow(name,row);
 * obj.deleteRow(name,rowId);
 * String param_3 = obj.selectCell(name,rowId,columnId);
 */
```