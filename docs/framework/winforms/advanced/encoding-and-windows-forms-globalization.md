---
title: "Encoding and Windows Forms Globalization | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ListView control [Windows Forms], lack of Unicode support"
  - "DateTimePicker control [Windows Forms], lack of Unicode support"
  - "TrackBar control [Windows Forms], lack of Unicode support"
  - "ImageList component [Windows Forms], lack of Unicode support"
  - "Unicode [Windows Forms]"
  - "ToolBar control [Windows Forms], lack of Unicode support"
  - "international applications [Windows Forms], character display"
  - "StatusBar control [Windows Forms], lack of Unicode support"
  - "MonthCalendar control [Windows Forms], lack of Unicode support"
  - "international characters"
  - "TabControl control [Windows Forms], lack of Unicode support"
  - "Windows Forms, encoding"
  - "TreeView control [Windows Forms], lack of Unicode support"
  - "ProgressBar control [Windows Forms], Unicode-enabled forms"
  - "localization [Windows Forms], character sets"
  - "globalization [Windows Forms], character sets"
ms.assetid: 22e8965d-a712-42b3-8167-3ee346bd70f9
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Encoding and Windows Forms Globalization
Приложения Windows Forms полностью поддерживают Юникод, т. е. каждый символ представлен уникальным числом независимо от платформы, программы или языка.  Для получения дополнительных сведений о Юникоде посетите [веб\-сайт консорциума Юникода](http://www.unicode.org).  
  
## Преимущества Юникода  
 В число преимуществ форм с поддержкой Юникода входит возможность работать с языками, поддерживаемыми только Юникодом, например хинди.  Кроме того, можно работать с несколькими языками в одной форме.  В Юникоде все символы занимают два байта, поэтому для представления двухбайтовых символов не требуется специальных усилий.  Также можно написать единый код, который будет работать на всех платформах.  Этим ситуация отличается от предыдущих версий [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], где требовалось писать разный код для разных платформ, например для Windows NT и [!INCLUDE[win98](../../../../includes/win98-md.md)].  
  
 Однако некоторые элементы управления в [!INCLUDE[win98](../../../../includes/win98-md.md)] и Windows Millennium Edition не поддерживают Юникод.  Эти элементы управления, которые все без исключения являются наследниками типового элемента управления, обрабатывают данные с использованием кодовых страниц Windows, таких как [!INCLUDE[vcpransi](../../../../includes/vcpransi-md.md)].  Это такие элементы управления, как <xref:System.Windows.Forms.TabControl>, <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.DateTimePicker>, <xref:System.Windows.Forms.MonthCalendar>, <xref:System.Windows.Forms.TrackBar>, <xref:System.Windows.Forms.ProgressBar>, <xref:System.Windows.Forms.ImageList>, <xref:System.Windows.Forms.ToolBar> и <xref:System.Windows.Forms.StatusBar>.  Таким образом, невозможно отображать данные Юникода в этих элементах управления на перечисленных платформах.  Например, нельзя отобразить японские символы в английской версии операционной системы [!INCLUDE[win98](../../../../includes/win98-md.md)].  
  
 В качестве альтернативы элементам управления <xref:System.Windows.Forms.ToolBar> и <xref:System.Windows.Forms.StatusBar> можно использовать элементы управления <xref:System.Windows.Forms.ToolStrip> и <xref:System.Windows.Forms.StatusStrip>, поддерживающие Юникод.  Чтобы добиться схожего внешнего вида элементов в приложении, используйте для отрисовки меню элемент управления <xref:System.Windows.Forms.MenuStrip> вместо <xref:System.Windows.Forms.MainMenu>.  Подобно элементам <xref:System.Windows.Forms.ToolStrip> и <xref:System.Windows.Forms.StatusStrip>, элемент <xref:System.Windows.Forms.MenuStrip> также может обрабатывать и отображать символы Юникода.  
  
## См. также  
 [Globalizing Windows Forms](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)