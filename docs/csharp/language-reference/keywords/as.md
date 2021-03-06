---
title: "as (Справочник по C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- as_CSharpKeyword
- as
dev_langs:
- CSharp
helpviewer_keywords:
- type conversion [C#], as keyword
- as keyword [C#]
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
caps.latest.revision: 24
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7a55c696ac295eee8d5d35ed56038f3c4a90b215
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="as-c-reference"></a>as (Справочник по C#)
Оператор `as` можно использовать для выполнения определенных типов преобразований между совместимыми ссылочными типами или [типами, допускающими значение NULL](../../../csharp/programming-guide/nullable-types/index.md). Вот пример кода:  
  
 [!code-cs[csrefKeywordsOperator#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_1.cs)]  
  
## <a name="remarks"></a>Примечания  
 Оператор `as` аналогичен операции приведения. Однако, если преобразование невозможно, `as` возвращает `null`, а не вызывает исключение. Рассмотрим следующий пример.  
  
```  
expression as type  
```  
  
 Этот код является эквивалентом следующего выражения, за исключением того, что переменная `expression` вычисляется только один раз.  
  
```  
expression is type ? (type)expression : (type)null  
```  
  
 Обратите внимание, что оператор `as` выполняет только преобразования ссылок, преобразования типов, допускающих значение NULL, и преобразования-упаковки. Оператор `as` не может выполнять другие преобразования, например пользовательские преобразования, которые следует выполнять с помощью выражения приведения.  
  
## <a name="example"></a>Пример  
 [!code-cs[csrefKeywordsOperator#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_2.cs)]  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)   
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)   
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Оператор ?:](../../../csharp/language-reference/operators/conditional-operator.md)   
 [Ключевые слова операторов](../../../csharp/language-reference/keywords/operator-keywords.md)

