# MaxBy , MinBy :-

### 1- الطالب المتفوق: اللي جايب أعلى درجات (Top Performer).

### 2- الطالب المتعثر: اللي جايب أقل درجات عشان يساعدوه (Needs Support).

```csharp
var students = new List<Student>
{
    new Student { StudentId = 1, FullName = "أحمد علي", Grade = 85, BirthDate = new DateTime(2010, 5, 12) },
    new Student { StudentId = 2, FullName = "سارة محمود", Grade = 98, BirthDate = new DateTime(2011, 3, 20) }, // أشطر واحدة
    new Student { StudentId = 3, FullName = "ياسين محمد", Grade = 70, BirthDate = new DateTime(2012, 8, 15) }, // أصغر واحد
    new Student { StudentId = 4, FullName = "منى يوسف", Grade = 92, BirthDate = new DateTime(2009, 11, 2) }   // أكبر واحدة سنًا
};



// أشطر طالب (صاحب أعلى درجة) في كلمة واحدة
var topStudent = students.MaxBy(s => s.Grade);

// أصغر طالب (أحدث تاريخ ميلاد) في كلمة واحدة
var youngest = students.MaxBy(s => s.BirthDate);

// النتيجة:
Console.WriteLine(topStudent.FullName); // طبع اسم الطالب فوراً
```
