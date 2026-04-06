# لو افترضنا إن عندك كلاس Book (الأب) وكلاس Review (الابن)، وبدل ما تسمي الـ FK في الـ Review باسم BookId سميته MyBookLink:
                                              
### * OneToOne * 
#### by Data Annotations:-
```csharp
 public class Blog
 {
     public int Id { get; set; }
     public string person { get; set; }
     public string Url { get; set; }
     public BlogImage BlogImage { get; set; }
 }


 public class BlogImage
 {
     public int Id { get; set; }
     public string imge { get; set; }
     public string Caption { get; set; }
     public int ForeignKeyBlog { get; set; }
     [ForeignKey("ForeignKeyBlog")]   // data Annotaions    
     public Blog Blog { get; set; }
 }
```



### by Data FluentApi:-

```csharp
modelBuilder.Entity<Citizen>()          // 1. يا مواطن
    .HasOne(c => c.Passport)            // 2. إنت ليك باسوورد واحد
    .WithOne(p => p.Citizen)            // 3. ويا باسوورد، إنت بتاع مواطن واحد
    .HasForeignKey<Passport>(p => p.CitizenId); //  4. والـ FK هيكون "جوه" شنطة الباسوورد or هيكون في ال child فيه حاجه لازم اربطها ب ال parent
```
