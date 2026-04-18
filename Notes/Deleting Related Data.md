### تخيلي إن عندك مدرسة فيها طلاب متميزين جداً، والسيستم معمول بحيث يمنع مسح أي مدرسة بالخطأ إلا لو تم نقل الطلاب لمدرسة تانية الأول. لو جربتِ تمسحي المدرسة وهي لسه فيها طلاب، السيستم هيرفض ويطلع Error.

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<School>()
        .HasMany(s => s.Students)
        .WithOne(st => st.School)
        .OnDelete(DeleteBehavior.Restrict); // "ممنوع المسح"
}
```

```csharp
using (var _context = new ApplicationDbContext())
{
    try
    {
        // 1. بنجيب مدرسة موجودة وجواها طلاب فعلاً
        var school = _context.Schools.FirstOrDefault(s => s.SchoolId == 2);

        if (school != null)
        {
            // 2. بنحاول نمسح المدرسة (وهي لسه شايلة طلاب)
            _context.Schools.Remove(school);

            // 3. هنا هيحصل الـ Crash أو الـ Error
            // الـ SQL Server هيرفض لأن فيه Foreign Key مربوط بطلاب
            _context.SaveChanges();
        }
    }
    catch (Exception ex)
    {
        // الرسالة اللي هتظهر لك هنا هتكون:
        // "The DELETE statement conflicted with the REFERENCE constraint..."
        Console.WriteLine("عفواً! لا يمكن مسح المدرسة لأنها تحتوي على طلاب مرتبطة بها.");
    }
}
```
