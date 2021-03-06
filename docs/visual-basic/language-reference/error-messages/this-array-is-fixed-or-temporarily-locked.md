---
title: "Массив имеет фиксированный размер или временно заблокирован (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID10"
dev_langs: 
  - "VB"
ms.assetid: de6713a6-51d7-4edb-8515-d5fb544e2091
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Массив имеет фиксированный размер или временно заблокирован (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Причиной возникновения данной ошибки может быть:  
  
-   Использование `ReDim` для изменения числа элементов массива фиксированного размера.  
  
-   Изменение размерности динамического массива на уровне модуля, в котором один элемент был передан процедуре в качестве аргумента.  Если элемент уже был передан, массив заблокирован, чтобы предотвратить освобождение памяти для параметра ссылки в пределах процедуры.  
  
-   Попытка присвоения значения для переменной `Variant`, содержащей массив, но `Variant` заблокирована.  
  
### Чтобы исправить эту ошибку  
  
1.  Сделайте исходный массив динамическим, а не фиксированным, объявив его с помощью `ReDim` \(если массив объявляется в пределах процедуры\) или объявив его без указания числа элементов \(если массив объявляется на уровне модуля\).  
  
2.  Определите, необходима ли передача элемента, если он видим всем процедурам модуля.  
  
3.  Определите, почему заблокирована переменная `Variant` и разблокируйте ее.  
  
## См. также  
 [Массивы](../../../visual-basic/programming-guide/language-features/arrays/index.md)