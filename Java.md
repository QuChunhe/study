

[Correct way to find rowcount in Java JDBC](https://stackoverflow.com/questions/13103067/correct-way-to-find-rowcount-in-java-jdbc)

```
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
ResultSetMetaData metaData = rs.getMetaData();
rowcount = metaData.getColumnCount();
```

```
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
rowcount = rs.last() ? rs.getRow() : 0;
```
