---
title: "Компонент BindingSource | Microsoft Docs"
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
  - "BindingSource - компонент [Windows Forms]"
  - "привязка данных, Windows Forms"
  - "Windows Forms, элемент управления связывания данных"
ms.assetid: 3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Компонент BindingSource
Encapsulates a data source for binding to controls.  
  
 Компонент <xref:System.Windows.Forms.BindingSource> служит двум целям.  Во\-первых, он обеспечивает уровень косвенного обращения при выполнении привязки элементов управления в форме к данным.  Это достигается путем привязки компонента <xref:System.Windows.Forms.BindingSource> к источнику данных и последующей привязки элементов управления в форме к компоненту <xref:System.Windows.Forms.BindingSource>.  Все последующие взаимодействия с данными, включая перемещение, сортировку, фильтрацию и обновление, осуществляются с помощью вызовов компонента <xref:System.Windows.Forms.BindingSource>.  
  
 Во\-вторых, компонент <xref:System.Windows.Forms.BindingSource> может действовать как строго типизированный источник данных.  Добавление типа в компонент <xref:System.Windows.Forms.BindingSource> с методом <xref:System.Windows.Forms.BindingSource.Add%2A> создает список этого типа.  
  
## В этом подразделе  
 [Общие сведения о компоненте BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)  
 Основные понятия, связанные с компонентом <xref:System.Windows.Forms.BindingSource>, позволяющим привязывать источник данных к элементу управления.  
  
 [Практическое руководство. Специальная обработка значений DBNull при связывании элементов управления с данными в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-windows-forms-controls-to-dbnull-database-values.md)  
 Показан процесс обработки значения <xref:System.DBNull> из источника данных с помощью компонента <xref:System.Windows.Forms.BindingSource>.  
  
 [Практическое руководство. Сортировка и фильтрация данных ADO.NET с помощью компонента BindingSource в Windows Forms](../../../../docs/framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для сортировки и фильтрации отображаемых данных.  
  
 [Практическое руководство. Связывание с веб\-службой с помощью компонента BindingSource в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-to-a-web-service-using-the-windows-forms-bindingsource.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для привязки к веб\-службе.  
  
 [Практическое руководство. Обработка ошибок и исключений, происходящих при связывании элементов управления с данными](../../../../docs/framework/winforms/controls/how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для правильной обработки ошибок, возникающих при операциях привязки к данным.  
  
 [Практическое руководство. Связывание элемента управления с типом в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для привязки к типу.  
  
 [Практическое руководство. Связывание элемента управления с объектом\-фабрикой в Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-factory-object.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для привязки к объекту\-фабрике или методу.  
  
 [Практическое руководство. Настройка дополнений к элементам с помощью элемента управления BindingSource в Windows Forms](../../../../docs/framework/winforms/controls/how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для создания элементов и добавления их в источник данных.  
  
 [Практическое руководство. Уведомление об изменении данных с использованием метода ResetItem компонента BindingSource](../../../../docs/framework/winforms/controls/how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для инициирования событий уведомления об изменениях для источников данных, не поддерживающих уведомление об изменениях.  
  
 [Практическое руководство. Получение уведомления об изменении данных с использованием компонента BindingSource и интерфейса INotifyPropertyChanged](../../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md)  
 Демонстрируется использование типа, наследуемого от <xref:System.ComponentModel.INotifyPropertyChanged>, с элементом управления <xref:System.Windows.Forms.BindingSource>.  
  
 [Практическое руководство. Отражение в элементе управления данных, которые обновились в источнике, с использованием компонента BindingSource в Windows Forms](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)  
 Показано, как обеспечить реакцию на изменения в источнике данных с помощью компонента <xref:System.Windows.Forms.BindingSource>.  
  
 [Практическое руководство. Совместное использование одних и тех же данных в нескольких формах посредством компонента BindingSource](../../../../docs/framework/winforms/controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)  
 Демонстрируется использование компонента <xref:System.Windows.Forms.BindingSource> для привязки нескольких форм к одному и тому же источнику данных.  
  
## Ссылка  
 <xref:System.Windows.Forms.BindingSource>  
 Содержит справочную документацию по компоненту <xref:System.Windows.Forms.BindingSource>.  
  
 <xref:System.Windows.Forms.BindingNavigator>  
 Содержит справочную документацию по элементу управления <xref:System.Windows.Forms.BindingNavigator>.  
  
## Связанные подразделы  
 [Связывание элементов управления Windows Forms с данными](../../../../docs/framework/winforms/windows-forms-data-binding.md)  
 Содержит ссылки на разделы, в которых описывается архитектура привязки к данным в Windows Forms.  
  
 См. также [Привязка элементов управления к данным в Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md).