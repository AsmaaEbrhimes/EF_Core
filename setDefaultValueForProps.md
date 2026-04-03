# how to set default value for props? 

### by Data Annotations:-

```csharp
 public class Book
 {
     public int BookKey { get; set; }
     public string Name { get; set; }
     public string Auther { get; set; }
     public int Rating { get; set; }

 }
```

```csharp
 modelBuilder.Entity<Book>().Property(b => b.Rating).HasDefaultValue(2);
```
