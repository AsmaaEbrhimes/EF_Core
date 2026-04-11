# طرق الوصول لعنصر او لمجموعة عناصر

### 1- من خلال ال Find():-

```csharp
 static void Main(string[] args)
{
 var _context = new ApplicationDbContext();
 var stock = _context.Stocks.Find(5);
  Console.WriteLine(stock== null?"NoData" : $"This The Id {stock.Id} : {stock.Name}");  //select Item With Primarykey
}
```

### 2- من خلال ال Single():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
   var stock = _context.Stocks.Single(item => item.Id == 3);   //Single:- بنستخدمها في حاله أني متأكده مليون في الميه ان هيرجعلي item واحد فقط
   Console.WriteLine($"This The Id {stock.Id} : {stock.Name}");
}
```

### 3- من خلال ال SingleOrDefault():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
    var stock = _context.Stocks.SingleOrDefault(item => item.Id == 1001);
   Console.WriteLine(stock== null? "No Data":$"This The Id {stock.Id} : {stock.Name}");
}
```

### 4- من خلال ال First():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
    var stock = _context.Stocks.First(); // نفس الكلام انا بستخدم first في حاله انا لو متأكده مليون في الميه ان اكيد فيه عنصر علي الاقي في ال database
   Console.WriteLine($"This The Id {stock.Id} : {stock.Name}");
}
```

### 5- من خلال ال FirstOrDefault():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
    var stock = _context.Stocks.FirstOrDefault();   // عشان لو مفيش data يرجع null
   Console.WriteLine(stock== null? "No Data":$"This The Id {stock.Id} : {stock.Name}");
}
```

### 6- من خلال ال first مع تحديد criteria:-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
    var stock = _context.Stocks.First(item => item.id > 500);
   Console.WriteLine(stock== null? "No Data":$"This The Id {stock.Id} : {stock.Name}");
}
```

### \*ملحوظة هامة:-

#### single , first نقدر اننا نحدد ليهم criteria معينه ولكن مع مراعاه ان ال sinlgle يطلع عنصر واحد فقط وليس متكرر علي عكس ال first ممكن تطلع اكتر من عنصر بما يتفق مع ال criteria.

### 7- من خلال ال Last():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
   var stock = _context.Stocks.OrderBy(item => item.Id).Last();
   Console.WriteLine($"This The Id {stock.Id} : {stock.Name}");
}
```

### 8- من خلال ال LastOrDefault():-

```csharp
 static void Main(string[] args)
{
   var _context = new ApplicationDbContext();
   var stock = _context.Stocks.OrderBy(item => item.Id).LastOrDefault(item => item.Id > 2001);
 Console.WriteLine(stock == null?"NoDataInTabels":$"This The Id {stock.Id} : {stock.Name}");
}
```

### 8- من خلال ال whera():-

```csharp
  static void Main(string[] args)
 {
     var _context = new ApplicationDbContext();
     var stock = _context.Stocks.Where(item => item.Name.StartsWith("Z"));
     foreach (var item in stock)
     {
     Console.WriteLine(stock == null?"NoDataInTabels":$"This The Id {item.Id} : {item.Name}");
     }

 }
```
