---
title: "Не удается получить сведения о памяти из-за внутренней ошибки. | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrDiagnosticInfo_Memory"
ms.assetid: 1ba8f774-5858-438e-914e-99fddc9e5e7e
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Не удается получить сведения о памяти из-за внутренней ошибки.
Вызов одного из свойств сведений о памяти объекта `My.Computer.Info` завершился неудачно.  
  
### Исправление ошибки  
  
-   Добавьте блок `Try...Catch` вокруг вызова свойства сведений о памяти объекта `My.Computer.Info`.  
  
## См. также  
 [Объект My.Computer.Info](../../visual-basic/language-reference/objects/my-computer-info-object.md)   
 [Обработка исключений и ошибок в Visual Basic](http://msdn.microsoft.com/ru-ru/3e351e73-cf23-40ab-8b60-05794160529e)   
 [Оператор Try...Catch...Finally](../../visual-basic/language-reference/statements/try-catch-finally-statement.md)