# Data Integrity with Unique Indexes ?
#### * دي وظيفتها تضمن إن القيمة مكررة ممنوعة في العمود ده.
#### * في المثال بتاعك: أنت عملت Index على الـ Url وخليته IsUnique. ده معناه لو حاولت تضيف رابط مدونة (Url) موجود قبل كده، قاعدة البيانات هتطلع Error وتمنع العملية.

#### * الهدف: الحفاظ على سلامة البيانات (Data Integrity). مستحيل يكون فيه 2 Blog ليهم نفس الرابط.





#### by Data Annotations:-
```csharp
[Index(nameof(Url), IsUnique =true)]
    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }
        public List<Post> Posts { get; set; }
    }
```

### by Data FluentApi:-
```csharp
   {
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) =>
            optionsBuilder.UseSqlServer("Server=localhost;Database=EFCore;Trusted_Connection=True;TrustServerCertificate=True;");

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
             modelBuilder.Entity<Blog>()
             .HasIndex(b => new { b.Url , b.BlogId });
             .IsUnique();
        }
        public DbSet <Blog> Blogs { get; set; }
    }
```
