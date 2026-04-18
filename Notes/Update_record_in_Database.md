# How To Update Record In Database:-
### تخيلي عندك سيستم مدرسة، وفيه طالب نقل من سكنه، ومحتاجين نحدث عنوانه ونغير اسمه لأنه كان مكتوب غلط.

```csharp
public class School
{
    public int SchoolId { get; set; }
    public string SchoolName { get; set; }
    
    // المدرسة الواحدة فيها طلاب كتير
    public List<Student> Students { get; set; } = new List<Student>();
}

public class Student
{
    public int StudentId { get; set; }
    public string FullName { get; set; }     // اسم الطالب (ثابت منطقياً)
    public string Address { get; set; }      // عنوان الطالب (بيتغير لو نقل سكنه)
    public DateTime BirthDate { get; set; }  // تاريخ الميلاد (مستحيل يتغير)

    // Foreign Key: الطالب يتبع مدرسة حالياً
    public int SchoolId { get; set; }
    public School School { get; set; }
}
```

```csharp
using (var _context = new ApplicationDbContext())
{
    // 1. استلمنا بيانات الطالب الجديدة من الـ UI
    var updatedStudent = new Student
    {
        StudentId = 5,              // الـ ID الأساسي عشان نوصل للسجل
        FullName = "Yassin Ahmed",  // الاسم (باعتينه بس مش هنغيره)
        Address = "Cairo, Zayed",   // العنوان الجديد (محتاجين نحدثه)
        SchoolId = 102,             // رقم المدرسة الجديدة (محتاجين نحدثه)
        BirthDate = new DateTime(2015, 5, 12) // تاريخ الميلاد (باعتينه بس "قفلناه")
    };

    // 2. بنعلم على الـ Object كله إنه "تعدل"
    _context.Update(updatedStudent);

    // 3. --- حماية البيانات التي لا يجب تغييرها ---
    
    // اسم الطالب مش مسموح يتغير في العملية دي
    _context.Entry(updatedStudent).Property(s => s.FullName).IsModified = false;

    // تاريخ الميلاد ده "خط أحمر" مستحيل يتغير برمجياً هنا
    _context.Entry(updatedStudent).Property(s => s.BirthDate).IsModified = false;

    // 4. الحفظ النهائي
    // الـ EF هيحدث فقط: Address و SchoolId
    _context.SaveChanges();
}
```




### نحتاج لتحديث بيانات مجموعة من الطلاب (مثل تغيير العناوين أو المدرسة التابعين لها) مع ضمان عدم تغيير البيانات الأساسية التي لا يجب تعديلها برمجياً في هذه العملية (مثل الاسم وتاريخ الميلاد)، حتى لو كانت القيم الجديدة موجودة في القائمة المرسلة.

```csharp
using (var _context = new ApplicationDbContext())
{
    // 1. قائمة الطلاب اللي جاية ببيانات معدلة (مثلاً من Web API أو Form)
    var updatedStudents = new List<Student>
    {
        new Student { StudentId = 1, Address = "Giza", SchoolId = 10, FullName = "Ahmed", BirthDate = new DateTime(2010,1,1) },
        new Student { StudentId = 2, Address = "Cairo", SchoolId = 10, FullName = "Sara", BirthDate = new DateTime(2011,2,2) },
        new Student { StudentId = 3, Address = "Alex", SchoolId = 10, FullName = "Mona", BirthDate = new DateTime(2012,3,3) }
    };

    // 2. بنستخدم UpdateRange عشان نعلم عليهم كلهم مرة واحدة إنهم "Modified"
    _context.Students.UpdateRange(updatedStudents);

    // 3. --- هنا بقى نطبق الحماية اللي اتعلمناها لو عاوزين ---
    foreach (var student in updatedStudents)
    {
        // بنمنع تعديل الاسم وتاريخ الميلاد لكل طالب في القائمة
        _context.Entry(student).Property(s => s.FullName).IsModified = false;
        _context.Entry(student).Property(s => s.BirthDate).IsModified = false;
    }

    // 4. الحفظ
    // الـ EF Core هيبعت أوامر Update لكل طالب في القائمة دي
    _context.SaveChanges();
}
```