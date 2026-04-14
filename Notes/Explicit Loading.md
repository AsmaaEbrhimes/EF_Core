## 1. تحميل "مرجع واحد" (Reference)

### إذا كان لديك كتاب (Book) وتريد تحميل المؤلف (Author) الخاص به بشكل منفصل:

```csharp
// 1. جلب الكتاب أولاً (بدون المؤلف)
var book = context.Books.Single(b => b.BookId == 2);

// 2. تحميل المؤلف بشكل صريح لاحقاً
context.Entry(book)
    .Reference(b => b.Author)
    .Load();
```

## 2. تحميل "مجموعة" (Collection):-

### إذا كان لديك مدونة (Blog) وتريد تحميل قائمة المنشورات (Posts) التابعة لها:

```csharp
// 1. جلب المدونة
var blog = context.Blogs.Single(b => b.BlogId == 5);

// 2. تحميل قائمة المنشورات التابعة لها
context.Entry(blog)
    .Collection(b => b.Posts)
    .Load();
```

## 3. عمل فلترة (Filtering) أثناء التحميل:-

### هذه ميزة قوية في الـ Explicit Loading، حيث يمكنك كتابة استعلام (Query) على البيانات المرتبطة قبل تحميلها:

```csharp
var blog = context.Blogs.Single(b => b.BlogId == 5);

// تحميل المنشورات التي معرفها (ID) أكبر من 2 فقط
context.Entry(blog)
    .Collection(b => b.Posts)
    .Query() // تتيح لك كتابة LINQ Query
    .Where(p => p.PostId > 2)
    .ToList();
```
