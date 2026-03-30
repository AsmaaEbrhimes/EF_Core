# How to make props is required?

### 1- طريقة باستخدام Fluent API:
باستخدام كلاس منفصل للإعدادات (Configuration Class) للحفاظ على نظافة الـ `DbContext`:

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

namespace EF_Test.Configurations
{
    public class BlogEntityTypeConfiguration : IEntityTypeConfiguration<Blog>
    {
        public void Configure(EntityTypeBuilder<Blog> builder)
        {
            // جعل حقل الـ Url مطلوباً (NOT NULL) في قاعدة البيانات
            builder.Property(m => m.Url).IsRequired();
        }
    }
}