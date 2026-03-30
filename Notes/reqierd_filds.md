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