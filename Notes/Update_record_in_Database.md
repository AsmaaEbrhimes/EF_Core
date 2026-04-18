# How To Update Record In Database:-

```csharp
public class School
{
    public int SchoolId { get; set; }
    public string SchoolName { get; set; }
    public string Location { get; set; }

    // Navigation Property: المدرسة الواحدة عندها قائمة مدرسين
    public List<Teacher> Teachers { get; set; } = new List<Teacher>();
}

public class Teacher
{
    public int TeacherId { get; set; }
    public string Name { get; set; }
    public DateTime HireDate { get; set; } // تاريخ التعيين (ثابت منطقياً)

    // Foreign Key: المدرس بيتبع مدرسة واحدة
    public int SchoolId { get; set; }

    // Navigation Property
    public School School { get; set; }
}
```

```csharp
using (var _context = new ApplicationDbContext())
{
    // استلمنا بيانات المدرس من السيستم (كأنه Object جديد)
    var teacherTransfer = new Teacher
    {
        TeacherId = 1,       // نفس المدرس
        Name = "Ahmed",      // اسمه ثابت مش هيتغير
        SchoolId = 20,       // دي القيمة الوحيدة اللي "منطقياً" عايزين نحدثها
        HireDate = DateTime.Parse("2020-01-01") // تاريخ تعيينه القديم مش عايزينه يتلمس
    };

    // بنعلم على المدرس كله إنه Modified
    _context.Update(teacherTransfer);

    // --- هنا المنطق والذكاء ---
    // بنقول للـ EF: "ماتغيرش الاسم في الداتابيز حتى لو بعتهولك"
    _context.Entry(teacherTransfer).Property(t => t.Name).IsModified = false;

    // وبنقول له: "كمان تاريخ التعيين ده خط أحمر، سيبه زي ما هو في الداتابيز"
    _context.Entry(teacherTransfer).Property(t => t.HireDate).IsModified = false;

    // النتيجة: الـ EF هيعمل Update لـ SchoolId فقط
    _context.SaveChanges();
}
```
