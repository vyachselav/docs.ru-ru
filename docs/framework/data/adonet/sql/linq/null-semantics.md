---
title: "Семантика NULL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a97017ae-d634-4cf3-bbaf-054a528fd683
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Семантика NULL
В следующей таблице приведены ссылки на различные части документации [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], в которых обсуждаются проблемы, связанные со значением `null` \(`Nothing` в [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\).  
  
|Раздел|Описание|  
|------------|--------------|  
|[Несоответствия типов SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mismatches.md)|В подразделе "Семантика со значениями NULL" данного раздела сравнивается тип значений SQL "Boolean", принимающий три состояния, с типом значения среды CLR <xref:System.Boolean>, принимающим два состояния, литералом `Nothing` \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) и `null` \(C\#\) и рассматриваются другие аналогичные проблемы.|  
|[Преобразование стандартных операторов запросов](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)|В подразделе "Семантика со значениями NULL" данного раздела описывается семантика сравнений со значением NULL в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].|  
|[Методы System.String](../../../../../../docs/framework/data/adonet/sql/linq/system-string-methods.md)|В подразделе "Отличия от платформы .NET" данного раздела описывается, каким образом значение 0, возвращенное методом <xref:System.String.LastIndexOf%2A>, может означать, что строка равна значению NULL либо найденная позиция равна 0.|  
|[Вычисление суммы значений числовой последовательности](../../../../../../docs/framework/data/adonet/sql/linq/compute-the-sum-of-values-in-a-numeric-sequence.md)|Описывается, как оператор <xref:System.Linq.Enumerable.Sum%2A> выполняет сравнение со значением `null` \(`Nothing` в [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) вместо 0 для последовательности, содержащей только значения NULL, или пустой последовательности.|  
  
## См. также  
 [Типы данных и функции](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)