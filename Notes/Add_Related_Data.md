# Add Related Data:-

### خيلي إن عندك تطبيق "مدرسة"، وعندنا جدول للمدرسين (Teachers) وجدول للكورسات (Courses). العلاقة هنا إن المدرس الواحد يقدر يدرس أكتر من كورس (One-to-Many).

### بدل ما تروحي تضيفي المدرس الأول وتعملي SaveChanges عشان تاخدي الـ ID بتاعه، وبعدين تضيفي الكورسات.. EF Core بيسمح لك تعملي كدة:

```csharp
public class Teacher
{
    public int TeacherId { get; set; }
    public string Name { get; set; }

    // الرابط: المدرس عنده قائمة من الكورسات
    public List<Course> Courses { get; set; } = new List<Course>();
}

public class Course
{
    public int CourseId { get; set; }
    public string Title { get; set; }

    // الرابط: الكورس يتبع مدرس معين
    public int TeacherId { get; set; }
    public Teacher Teacher { get; set; }
}
```

```csharp
using (var context = new SchoolContext())
{
    // بنجهز البيانات في الـ Memory الأول
    var newTeacher = new Teacher
    {
        Name = "Ahmed",
        Courses = new List<Course>
        {
            new Course { Title = "Entity Framework Core" },
            new Course { Title = "C# Advanced" }
        }
    };

    // بنقول للـ EF: "خد المدرس ده عندك"
    // الـ EF ذكي، هيشوف إن المدرس جواه كورسات، فهيعتبرهم كلهم "سجل جديد"
    context.Teachers.Add(newTeacher);

    // هنا السحر بيحصل!
    // 1. هيعمل Insert للمدرس في جدول Teachers.
    // 2. هياخد الـ Id اللي طلع للمدرس (مثلاً رقم 1).
    // 3. هيروح لجدول Courses ويعمل Insert للكورسين ويحط TeacherId = 1 أوتوماتيك.
    context.SaveChanges();
}
```
