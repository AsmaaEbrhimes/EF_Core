# How Insert Default Data In Tabel ?

#### AplicationDBContext:-

```csharp
     public class ApplicationDbContext : DbContext
    {
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) =>
            optionsBuilder.UseSqlServer("Server=localhost;Database=EFCore;Trusted_Connection=True;TrustServerCertificate=True;");


        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {

        }

        public DbSet<Employee> Employees { get; set; }
    }
    public class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string gander { get; set; }
        public string Email { get; set; }
        public string Phone { get; set; }
    }
}
```

### Program:-
```csharp
    internal class Program
 {
     static void Main(string[] args)
     {
         SeedData();
     }

     public static void SeedData()
     {
         using (var context = new ApplicationDbContext())
         {
             var newEmployee = new List<Employee>
             {
               new Employee { Name = "أحمد محمد", gander = "Male", Email = "ahmed@example.com", Phone = "01000" },
               new Employee { Name = "سارة أحمد", gander = "Female", Email = "sara@example.com", Phone = "01111" },
               new Employee { Name = "محمود علي", gander = "Male", Email = "mahmoud@example.com", Phone = "01222" }
             };

             context.Employees.AddRange(newEmployee); //AddRange:- دي أحسن للأداء لأنها بتبعتهم للداتابيز في عملية واحدة.

             context.SaveChanges();

             Console.WriteLine(" Done Proccing!");
         }
     }
 }
```
