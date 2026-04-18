### في نظام المدرسة، نحتاج أحياناً لحذف سجل طالب واحد (مثلاً عند انسحابه) أو حذف مجموعة طلاب بالكامل (مثلاً عند تخرج فصل دراسي أو إغلاق فرع).

```csharp
using (var _context = new ApplicationDbContext())
{
    // --- الحالة الأولى: حذف طالب واحد (Single Record Removal) ---

    // 1. البحث عن الطالب المراد حذفه باستخدام الـ ID
    var studentToRemove = _context.Students.FirstOrDefault(s => s.StudentId == 5);

    if (studentToRemove != null)
    {
        // 2. استخدام دالة Remove لتعليم السجل كـ "Deleted"
        _context.Students.Remove(studentToRemove);

        Console.WriteLine($"Student {studentToRemove.FullName} marked for deletion.");
    }


    // --- الحالة الثانية: حذف مجموعة طلاب من مدرسة (Bulk Removal) ---

    // 1. جلب قائمة الطلاب التابعين لمدرسة معينة (مثلاً المدرسة رقم 10)
    var schoolStudents = _context.Students.Where(s => s.SchoolId == 10).ToList();

    if (schoolStudents.Any())
    {
        // 2. استخدام دالة RemoveRange لحذف القائمة بالكامل في خطوة واحدة
        _context.Students.RemoveRange(schoolStudents);

        Console.WriteLine($"{schoolStudents.Count} students marked for deletion.");
    }

    // --- الخطوة النهائية لكل العمليات السابقة ---

    // 3. تنفيذ الحذف الفعلي في قاعدة البيانات بإرسال أوامر DELETE
    _context.SaveChanges();
}
```
