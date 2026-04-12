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

### 9- من خلال ال whera():-

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

### 10- من خلال ال Any():-

```csharp
   internal class Program
 {
     static void Main(string[] args)
     {
         var _context = new ApplicationDbContext();
         var stock = _context.Stocks.Any();  // في حاله لو فيه data هيرجع true والعكس لو مش موجود data هيرجع false
         Console.WriteLine(stock);
     }
 }
```

### \*ملحوظة هامة:-

#### Any :- ممكن اننا نضفلها criteria وممكن نسبها كما في المثال.

### 11- من خلال ال All():-

```csharp
  var _context = new ApplicationDbContext();
 var stock = _context.Stocks.All(item => item.Id>0);
 Console.WriteLine(stock);
```

### \*ملحوظة هامة:-

#### // .All() تعيد true فقط إذا كانت جميع العناصر تحقق الشرط، وإذا خالف عنصر واحد الشرط تعيد false

### 12- من خلال ال Append():-

```csharp
 static void Main(string[] args)
 {
     var _context = new ApplicationDbContext();
     var stock = _context.Stocks.Where(item => item.Id > 500).ToList().Prepend(new Stock { Id =1001 , Name ="testAsmaa"}); //  arrayهنا بيضيف العنصر نهايه ال
     foreach (var item in stock)
     {
         Console.WriteLine(item.Name);
     }
 }
```

### 13- من خلال ال Prepend():-

```csharp
    static void Main(string[] args)
    {
        var _context = new ApplicationDbContext();
        var stock = _context.Stocks.Where(item => item.Id > 500).ToList().Prepend(new Stock { Id =1001 , Name ="testAsmaa"}); //  arrayهنا بيضيف العنصر أول ال
        foreach (var item in stock)
        {
            Console.WriteLine(item.Name);
        }
    }
```

### 14- من خلال Mix():-

```csharp
    static void Main(string[] args)
    {
         var _context = new ApplicationDbContext();
          var stock = _context.Stocks.Max(item => item.Id);  // اكبر قيمه
          Console.WriteLine(stock);
    }
```

### 15- من خلال Mix():-

```csharp
    static void Main(string[] args)
    {
          var _context = new ApplicationDbContext();
          var stock = _context.Stocks.Min(item => item.Id);  // أقل قيمه
          Console.WriteLine(stock);
    }
```

### 16- من خلال OrderBy():-

```csharp
     static void Main(string[] args)
 {
     var _context = new ApplicationDbContext();
     var stock = _context.Stocks.OrderBy(item => item.Id).ToList(); ;
     foreach (var item in stock)
     {
     Console.WriteLine(item.Id);
     }
 }
```

### 17- من خلال Select():-

```csharp
      static void Main(string[] args)
   {
       var _context = new ApplicationDbContext();
       var stock = _context.Stocks.Select(item => new {item.Id , item .Name}).ToList();
       foreach (var item in stock)
       {
       Console.WriteLine($"{item.Id} => {item.Name}");// استخدام Select بيعمل حاجة بنسميها Projection، وده فعلاً بيحسن الـ Performance لأنك مش بتسحب كل الداتا (زي الصور أو النصوص الطويلة) من قاعدة البيانات، أنت بتطلب بس اللي محتاجه.
       }
   }
```

### 18- من خلال Distinct():-

```csharp
     static void Main(string[] args)
 {
     var _context = new ApplicationDbContext();
     var stock = _context.Stocks.Select(item => new {item.Industry}).Distinct().ToList();
     foreach (var item in stock)
     {
         Console.WriteLine(item.Industry); //Distinct:- هي فايدتها اني برجع ال value اللي مش متكررة مثلا لو عندي tabel وفيه ارقام متكرره وانا عاوزه بس ال uinq
     }
 }
```

### 19- من خلال Take() , Skip():-

```csharp
  internal class Program
 {
     static void Main(string[] args)
     {
         var _context = new ApplicationDbContext();
         var stock = GetDataByPagnation(2, 10);
         foreach (var item in stock)
         {
             Console.WriteLine(item.Id);
         }
     }

     public static List<Stock> GetDataByPagnation(int currentPage , int pageSize)
     {
         var _context = new ApplicationDbContext();
         return _context.Stocks.Skip((currentPage - 1) * pageSize).Take(pageSize).ToList();   // Skip:- اول عشره , Take:- هياخد اللي بعد العشره
     }

 }
```
