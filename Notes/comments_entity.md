# اهم ال comments اللي موجوده في ال entity? 

### 1- لو محتاجه اضيف migration:-
```csharp
add-migration InitialCreate
 ```



### 2- لو محتاجه أمسح migration:-
```csharp
Remove-Migration
```

### 3- عشان نرفع التعديلات اللي احنا عملناها دي في ال sql:-
```csharp
update-database
```


### 4- تصفير قاعدة البيانات:-
```csharp
Update-Database -Migration 0
Remove-Migration
```

### 5- عندي مجموعة Migrations وعاوزه أمسح Migration معينه من ال Database:-
```csharp
Update-Database 20260408182835_removecolumn
```

### 6- عاوزه بناءا علي ال connection بتاع database موجوده أجيب الجداول اللي موجوده فيها وأحطها عندي في الكود:-
```csharp
scaffold-dbcontext 'Server=localhost;Database=EFCore;Trusted_Connection=True' Microsoft.EntityFrameworkCore.SqlServer
```

### 7- طيب عاوزه اقوله يعرض جدول معين من ال database ب ال migration بتاعته وليس كل الجداول
```csharp
scaffold-dbcontext 'Server=localhost;Database=EFCore;Trusted_Connection=True' Microsoft.EntityFrameworkCore.SqlServer -Tables Blogs
```

### 8-طيب عاوزه أحط ال جداول ال models اللي موجوده في ال Database في  ملفات الفيجوال ولكن بداخل ملف أسمه model عشان مش يبقا في ال root بشكل عشوائي
```csharp
scaffold-dbcontext 'Server=localhost;Database=EFCore;Trusted_Connection=True' Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models // أسم الملف Models
```

### 9- طيب عشان أقدر أفصل ال dbcontext عن ال models:-
```csharp
scaffold-dbcontext 'Server=localhost;Database=EFCore;Trusted_Connection=True' Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -ContextDir Data
```

### 10- طيب عشان اقدر ال model تتعمل ب Data Annotations ومش fluentApi لان ال هي ال Default:-
```csharp
scaffold-dbcontext 'Server=localhost;Database=EFCore;Trusted_Connection=True' Microsoft.EntityFrameworkCore.SqlServer DataAnnotations
```



