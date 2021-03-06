---
title: "Оператор |= (Справочник по C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "|=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "|= - оператор (назначение ИЛИ) [C#]"
  - "оператор назначения ИЛИ (|=) [C#]"
ms.assetid: 8315b8cf-dd15-402f-92f0-c7db931696ca
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Оператор |= (Справочник по C#)
Оператор присваивания OR.  
  
## Заметки  
 Выражение, в котором используется оператор назначения `|=`, например  
  
```  
x |= y  
```  
  
 , эквивалентно выражению  
  
```  
x = x | y  
```  
  
 за исключением того, что значение `x` вычисляется только один раз.  [Оператор &#124;](../../../csharp/language-reference/operators/or-operator.md) выполняет битовую логическую операцию OR для интегральных операндов и логическую операцию OR для логических операндов.  
  
 Оператор `|=` нельзя перегрузить непосредственно, однако пользовательские типы могут перегрузить [оператор &#124;](../../../csharp/language-reference/operators/or-operator.md) \(см. [оператор](../../../csharp/language-reference/keywords/operator.md)\).  
  
## Пример  
 [!code-cs[csRefOperators#10](../../../csharp/language-reference/operators/codesnippet/CSharp/or-assignment-operator_1.cs)]  
  
## См. также  
 [Справочник по C\#](../../../csharp/language-reference/index.md)   
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Операторы C\#](../../../csharp/language-reference/operators/index.md)