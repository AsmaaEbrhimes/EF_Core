how to make props is requierd ?
1-  طريقه باستخدام Fluent API:
***
    public class BlogEntityTypeConfiguration : IEntityTypeConfiguration<Blog>
    {
        public void Configure(EntityTypeBuilder<Blog> builder)
        {
            builder.Property(m => m.Url).IsRequired();
        }
    }
 
 وفي ملف ال DbContext:
  public class ApplicationDbContext : DbContext
 {
     protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) =>

   //  optionsBuilder.UseSqlServer("Data Source=(localdb)\\MSSQLLocalDB;Initial Catalog=EFCore;Integrated Security=True;TrustServerCertificate=True");
       optionsBuilder.UseSqlServer("Server=localhost;Database=EFCore;Trusted_Connection=True;TrustServerCertificate=True;");

     protected override void OnModelCreating(ModelBuilder modelBuilder)
     {
        new BlogEntityTypeConfiguration().Configure(modelBuilder.Entity<Blog>());
     }
     public DbSet<Blog> Blogs { get; set; }
 }

