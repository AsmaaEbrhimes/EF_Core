# اهم ال comments اللي موجوده في ال entity? 

### 1- لو محتاجه اضيف migration:-
```csharp
 * add-migration InitialCreate
 ```



### 2- لو محتاجه أمسح migration:-
```csharp
* Remove-Migration
```

### 3- عشان نرفع التعديلات اللي احنا عملناها دي في ال sql:-
```csharp
* update-database
```


### 4- تصفير قاعدة البيانات:-
```csharp
* Update-Database -Migration 0
* Remove-Migration
```



