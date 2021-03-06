---
title: "Практическое руководство. Создание неподписанных дружественных сборок (C#) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 78cbc4f0-b021-4141-a4ff-eb4edbd814ca
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c7d2924f0a619c234871232e155bb6f23e43aee4
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-unsigned-friend-assemblies-c"></a>Практическое руководство. Создание неподписанных дружественных сборок (C#)
В этом примере показано использование дружественных сборок с неподписанными сборками.  
  
### <a name="to-create-an-assembly-and-a-friend-assembly"></a>Создание сборки и дружественной сборки  
  
1.  Откройте окно командной строки.  
  
2.  Создайте файл C# с именем `friend_signed_A.`, содержащий приведенный ниже код. Код использует атрибут <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> для объявления friend_signed_B в качестве дружественной сборки.  
  
    ```csharp  
    // friend_unsigned_A.cs  
    // Compile with:   
    // csc /target:library friend_unsigned_A.cs  
    using System.Runtime.CompilerServices;  
    using System;  
  
    [assembly: InternalsVisibleTo("friend_unsigned_B")]  
  
    // Type is internal by default.  
    class Class1  
    {  
        public void Test()  
        {  
            Console.WriteLine("Class1.Test");  
        }  
    }  
  
    // Public type with internal member.  
    public class Class2  
    {  
        internal void Test()  
        {  
            Console.WriteLine("Class2.Test");  
        }  
    }  
    ```  
  
3.  Скомпилируйте и подпишите сборку friend_signed_A с помощью приведенной ниже команды.  
  
    ```csharp  
    csc /target:library friend_unsigned_A.cs  
    ```  
  
4.  Создайте файл C# с именем `friend_unsigned_B`, содержащий приведенный ниже код. Так как файл friend_unsigned_A задает friend_unsigned_B в качестве дружественной сборки, код friend_unsigned_B может обращаться к типам и членам `internal` из friend_unsigned_A.  
  
    ```csharp  
    // friend_unsigned_B.cs  
    // Compile with:   
    // csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    public class Program  
    {  
        static void Main()  
        {  
            // Access an internal type.  
            Class1 inst1 = new Class1();  
            inst1.Test();  
  
            Class2 inst2 = new Class2();  
            // Access an internal member of a public type.  
            inst2.Test();  
  
            System.Console.ReadLine();  
        }  
    }  
    ```  
  
5.  Скомпилируйте сборку friend_signed_B с помощью приведенной ниже команды.  
  
    ```csharp  
    csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    ```  
  
     Имя сборки, созданной компилятором, должно соответствовать имени дружественной сборки, передаваемой атрибуту <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. Необходимо явно указать имя выходной сборки (EXE или DLL) с помощью параметра компилятора `/out`. Дополнительные сведения см. в разделе [/out (параметры компилятора C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md).  
  
6.  Запустите файл friend_signed_B.exe.  
  
     Программа выведет две строки: "Class1.Test" и "Class2.Test".  
  
## <a name="net-framework-security"></a>Безопасность платформы .NET Framework  
 Существует сходство между атрибутом <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> и классом <xref:System.Security.Permissions.StrongNameIdentityPermission>. Основное различие заключается в том, что <xref:System.Security.Permissions.StrongNameIdentityPermission> могут требоваться разрешения безопасности для выполнения определенного раздела кода, тогда как атрибут <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> контролирует видимость типов и членов `internal`.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Сборки и глобальный кэш сборок (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [Дружественные сборки (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [Практическое руководство. Создание подписанных дружественных сборок (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [Руководство по программированию на C#](../../../../csharp/programming-guide/index.md)
