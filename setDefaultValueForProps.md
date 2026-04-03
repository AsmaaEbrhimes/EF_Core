# how to set default value for props? 

### by Data Annotations:-

```csharp
 modelBuilder.Entity<Book>().Property(b => b.Rating).HasDefaultValue(2);
```
