## 1. Eager Loading (التحميل المُسبق)

### المفهوم: هو إنك بتطلب من EF يجيب البيانات الأساسية والبيانات المرتبطة بيها في خبطة واحدة لقاعدة البيانات باستخدام SQL Join.

```csharp
// مثال: هات كل الشركات ومعاهم الموظفين بتوعهم في نفس الوقت
var companies = context.Companies
                       .Include(c => c.Employees)
                       .ToList();
```

## 2. Lazy Loading (التحميل الكسول)

### المفهوم: الـ EF بيجيب البيانات الأساسية بس، وأول ما تحاول "تلمس" أو تستخدم الـ Property المرتبطة في الكود، بيروح يعمل Query جديدة في اللحظة دي عشان يجيبها.

### الأداة: تحتاج تعريف الـ Property بكلمة virtual وتفعيل الـ UseLazyLoadingProxies.

```csharp
// 1. هنا جاب الشركة بس
var company = context.Companies.First();

// 2. في السطر ده، EF هيروح للقاعدة حالاً يجيب الموظفين لأنه لقاك بتستخدمهم
var count = company.Employees.Count();
```

## 3. Explicit Loading (التحميل الصريح)

### المفهوم: هو إنك بتجيب البيانات الأساسية الأول، وبعدين في وقت لاحق في الكود بتقول لـ EF "بشكل صريح" روح حمل لي البيانات المرتبطة للـ Object ده تحديداً.

```csharp
var company = context.Companies.First();

// تحميل الموظفين بتوع الشركة دي "فقط" عند الطلب
context.Entry(company)
       .Collection(c => c.Employees)
       .Load();
```
