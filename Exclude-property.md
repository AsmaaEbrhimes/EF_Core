# How to Exclude properties By Data Annotations & FluntApi? 

### 1- by Data Annotations:-
```csharp
    public class Blog
    {
        public int Id { get; set; }
        public string Url { get; set; }
        [NotMapped]    // exclude proprty by data Anotions
        public string PersonId { get; set; }
        public List<Posts> Posts { get; set; }
    }
```

### 2- by FluenApi:-  

```csharp
  protected override void OnModelCreating(ModelBuilder modelBuilder)
  {    
      modelBuilder.Entity<Blog>().Ignore(b => b.PersonId);  // Ignore Property FluntApi
  }
```
