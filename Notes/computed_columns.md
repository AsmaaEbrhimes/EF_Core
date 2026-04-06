# أزاي ممكن اربط بين اتنين columns عشان يكون ال result يكون هو ال value بتاع ال column جديد 

### by FluenApi:
```csharp
 public class Auther
 {
     public int Id { get; set; }
     public string FirstName { get; set; }
     public string LastName { get; set; }
    [Required , MaxLength(150)] 
     public string DisblayName { get; set; }
 }
```


```csharp
public class ApplicationDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) =>
      optionsBuilder.UseSqlServer("Server=localhost;Database=EFCore;Trusted_Connection=True;TrustServerCertificate=True;");

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Auther>()
            .Property(p => p.DisblayName)
            .HasComputedColumnSql("[FirstName] + ',' + [LastName]");
    }
    public DbSet<Auther> Authers { get; set; }
}
```