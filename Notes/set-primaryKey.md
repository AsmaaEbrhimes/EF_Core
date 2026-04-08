#### ببساطة، لما تغير الاسم من id لأي اسم تاني زي BookKey الـ Entity بيفقد القدرة إنه يتعرف عليه لوحده. عشان كدة لازم "تعرفه يدوي" بواحدة من الطريقتين دول:

### by Data Annotations:-

```csharp
 public class Book
 {
     [Key]
     public int BookKey { get; set; }
     public string Name { get; set; }
     public string Auther { get; set; }
 }
```

### by Data FluenApi:-

```csharp
  public class ApplicationDbContext : DbContext
  {
     protected override void OnModelCreating(ModelBuilder modelBuilder)
     {
       modelBuilder.Entity<Book>().HasKey(b => b.BookKey);
     }
  }
```
