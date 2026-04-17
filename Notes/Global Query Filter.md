# مثال: الـ Soft Delete (المسح الوهمي)

### بدل ما تمسح السجل نهائياً من قاعدة البيانات، بنغير حالة عمود اسمه IsDeleted لـ true. وعشان مش كل شوية نكتب في الكود where b.IsDeleted == false بنعمل الفلتر ده.

```csharp
public class Blog
{
    public int BlogId { get; set; }
    public string Title { get; set; }
    public bool IsDeleted { get; set; } // العمود اللي هنفلتر بناء عليه
}
```

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    // الفلتر ده هيطبق على أي Query لجدول الـ Blogs
    modelBuilder.Entity<Blog>()
        .HasQueryFilter(b => !b.IsDeleted);
}
```

```csharp
// الكود بتاعك
var allBlogs = _context.Blogs.ToList();

// الـ SQL اللي هيتنفذ فعلياً في الخلفية:
// SELECT * FROM Blogs WHERE IsDeleted = 0
```
