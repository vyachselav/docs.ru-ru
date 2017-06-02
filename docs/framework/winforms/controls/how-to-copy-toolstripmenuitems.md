---
title: "Практическое руководство. Копирование объектов ToolStripMenuItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "пункты меню, копирование и вставка"
  - "MenuStrip — элемент управления [Windows Forms], упорядочение элементов"
  - "ToolStripMenuItems, копирование и вставка"
ms.assetid: 17ef4207-e92e-4db2-b648-27246e6517ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Практическое руководство. Копирование объектов ToolStripMenuItem
Во время разработки вы можете копировать целиком меню верхнего уровня и пункты их подменю в другое место в <xref:System.Windows.Forms.MenuStrip>. Вы также можете копировать отдельные пункты меню верхнего уровня или переупорядочивать пункты меню.  
  
### Копирование меню верхнего уровня и его подменю в другое расположение верхнего уровня  
  
1.  Щелкните левой кнопкой мыши меню, которое вы хотите скопировать, нажмите клавиши CTRL\+C или щелкните меню правой кнопкой мыши и выберите в списке команду **Копировать**.  
  
2.  Щелкните правой кнопкой мыши меню верхнего уровня, которое находится за новым предполагаемым расположением, и нажмите клавиши CTRL\+V или щелкните правой кнопкой мыши пункт меню верхнего уровня, который находится перед новым предполагаемым расположением, и выберите команду **Вставить** в контекстном меню.  
  
     Скопированное меню вставляется перед выбранным меню верхнего уровня.  
  
### Копирование меню верхнего уровня и пунктов подменю в расположение раскрывающегося списка  
  
1.  Щелкните левой кнопкой мыши меню, которое хотите переместить, и нажмите клавиши CTRL\+C или щелкните меню правой кнопкой мыши и выберите в контекстном меню команду **Копировать**.  
  
2.  В целевом меню верхнего уровня щелкните левой кнопкой мыши пункт подменю, который находится над предполагаемым новым расположением, и нажмите клавиши CTRL\+V или щелкните правой кнопкой мыши пункт подменю над предполагаемым новым расположением и выберите в контекстном меню команду **Вставить**.  
  
     Скопированное меню вставляется перед выбранным пунктом подменю.  
  
### Копирование пункта подменю в другое меню  
  
1.  Щелкните левой кнопкой пункт подменю, который вы хотите скопировать, и нажмите клавиши CTRL\+C или щелкните правой кнопкой мыши пункт подменю и выберите в контекстном меню команду **Копировать**.  
  
2.  Щелкните левой кнопкой мыши меню, которое будет содержать вырезанный пункт подменю.  
  
3.  Щелкните левой кнопкой мыши пункт подменю, который находится перед новым предполагаемым расположением, и нажмите клавиши CTRL\+V или щелкните правой кнопкой мыши пункт подменю, предшествующий предполагаемому новому расположению, и выберите в контекстном меню команду **Вставить**.  
  
     Скопированный пункт подменю вставляется перед выбранным пунктом подменю.  
  
## См. также  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Общие сведения об элементе управления MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)