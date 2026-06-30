#### لو عاوزه اخد التعديلات من branch واحطها علي branch اخر :-
##### أول حاجه بنقف علي ال branch اللي احنا عاوزين تتحدث عليه التعديلات 
```csharp
git merge dev
```




#### طيب ولو انا عاوزه اسحب اخر التحديثات من ال main وأحها مثلا في ال dev:-
```csharp
git checkout main
```



```csharp
git merge dev
```








#### عاوزه اسحب من ال main الي branch اخر زي ال dev مثلا :-
```csharp
git checkout main
```


```csharp
git pull origin main
```
