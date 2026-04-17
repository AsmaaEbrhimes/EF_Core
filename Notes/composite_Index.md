# * make  Composite Index ?

#### by Data Annotations:-
```csharp
 [Index (nameof(Url) , nameof(Posts))]
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
        }
        public DbSet <Blog> Blogs { get; set; }  
    }
```
