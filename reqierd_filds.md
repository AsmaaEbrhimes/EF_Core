# How to make props is required?

### 1- طريقة باستخدام Fluent API:

```csharp
    public class BlogEntityTypeConfiguration : IEntityTypeConfiguration<Blog>
    {
        public void Configure(EntityTypeBuilder<Blog> builder)
        {
            builder.Property(m => m.Url).IsRequired();
        }
    }

* وفي ملف ال DBContext :-
 protected override void OnModelCreating(ModelBuilder modelBuilder)
 {
    new BlogEntityTypeConfiguration().Configure(modelBuilder.Entity<Blog>());
 }
```

### 2- طريقة باستخدام Data Annotations:

```csharp
public class Blog
{
    public int Id { get; set; }
    [Required]   // Data Annotations
    public string Url { get; set; }
    public List<Posts> Posts { get; set; }
}
```
