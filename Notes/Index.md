# * Database Indexing: Performance vs. Storage Trade-off"
#### * سرعة البحث (Fast Retrieval): لو عندك مليون "Blog" في قاعدة البيانات، وعملت Query عشان تجيب بلوج معين بالـ Url بتاعه، قاعدة البيانات هتروح تجيبه في أجزاء من الثانية بدل ما تلف على المليون سجل سجل.

#### * كل Index هو نسخة إضافية مرتبة؛ الإفراط فيه قد يضاعف حجم قاعدة البيانات من 1GB إلى 3GB، ويُبطئ عمليات الإضافة والتعديل بسبب اضطرار الداتابيز لتحديث كل الفهارس مع كل تغيير. اذا يكفي column فقط للبحث


#### by Data Annotations:-
```csharp
 [Index (nameof(Url))]
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
                .HasIndex(b => b.Url);
        }
   
        public DbSet <Blog> Blogs { get; set; }  
    }
```
