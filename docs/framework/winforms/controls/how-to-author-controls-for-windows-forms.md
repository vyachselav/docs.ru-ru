---
title: "Практическое руководство. Создание элементов управления для форм Windows Forms | Microsoft Docs"
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
  - "элементы управления [Windows Forms], создание"
  - "пользовательские элементы управления [Windows Forms], создание"
  - "UserControl - класс, Windows Forms"
ms.assetid: 7570e982-545b-4c3a-a7c7-55581d313400
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Практическое руководство. Создание элементов управления для форм Windows Forms
Элемент управления играет роль графической связи между пользователем и программой.  Элемент управления может предоставлять или обрабатывать данные, принимать данные, введенные пользователем, реагировать на события, а также выполнять любые другие функции, связывающие пользователя и приложение.  Поскольку элемент управления по существу является компонентом с графическим интерфейсом, он может обрабатывать любую функцию, которую выполняет компонент, а также обеспечивать взаимодействие с пользователем.  Элементы управления создаются для конкретных целей; их разработка — это лишь одна из разновидностей задач программирования.  С учетом этого в следующих разделах представлены общие сведения о процессе разработки элементов управления.  Приводятся также ссылки на дополнительные сведения об отдельных шагах описываемых процедур.  
  
> [!NOTE]
>  Если необходимо создать пользовательский элемент управления для использования в конструкторе Web Forms, см. раздел [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md).  
>   
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих настроек или выпуска.  Чтобы изменить параметры, в меню **Сервис** выберите команду **Импорт и экспорт параметров**.  Дополнительные сведения см. в разделе [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/ru-ru/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Чтобы разработать элемент управления, выполните следующие действия:  
  
1.  Определите действия, которые должен выполнять элемент управления, или роль, которую он будет играть в приложении.  Необходимо рассмотреть следующие факторы:  
  
    -   Какой вид должен иметь графический интерфейс?  
  
    -   Какие особые виды взаимодействия с пользователем будет обрабатывать элемент управления?  
  
    -   Существуют ли элементы управления, выполняющие нужные функции?  
  
    -   Можно ли получить нужные функции путем объединения нескольких элементов управления Windows Forms?  
  
2.  Если для элемента управления необходима объектная модель, определите способ распределения функций в этой модели и разделите их между элементом управления и вложенными объектами.  Объектная модель может быть полезна при планировании сложного элемента управления или при необходимости объединения нескольких функций.  
  
3.  Определите необходимый тип элемента управления \(например, пользовательский элемент управления, нестандартный элемент управления, унаследованный элемент управления Windows Forms\).  Дополнительные сведения см. в разделах [Рекомендации относительно типов элементов управления](../../../../docs/framework/winforms/controls/control-type-recommendations.md) и [Создание собственных элементов управления](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md).  
  
4.  Представьте функции в качестве свойств, методов и событий элемента управления и его вложенных объектов или вспомогательных структур, а затем назначьте соответствующие уровни доступа \(например, открытый, защищенный и т. д.\).  
  
5.  Если для элемента управления необходимо пользовательское оформление, добавьте соответствующий код.  Дополнительные сведения см. в разделе [Рисование и отрисовка пользовательского элемента управления](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md).  
  
6.  Если элемент управления наследует от класса <xref:System.Windows.Forms.UserControl>, можно проверить его поведение во время выполнения, построив управляющий проект и запустив его в **тестовом контейнере пользовательских элементов управления**.  Дополнительные сведения см. в разделе [Практическое руководство. Тестирование поведения элемента UserControl во время выполнения](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
7.  Можно также выполнить тестирование и отладку элемента управления путем создания нового проекта, например приложения Windows, и помещения его в контейнер.  Этот процесс описан в разделе [Пример. Создание составного элемента управления с помощью Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md).  
  
8.  Включите в тестовый проект поочередно каждую функцию элемента управления для проверки.  
  
9. Повторите этот шаг, каждый раз внося уточнения в структуру элемента.  
  
10. Выполните упаковку и развертывание элемента управления.  Дополнительные сведения см. в разделе [Развертывание приложений, служб и компонентов](../Topic/Deploying%20Applications,%20Services,%20and%20Components.md).  
  
## См. также  
 [Пример. Создание составного элемента управления с помощью Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [Пример. Наследование элементов управления форм Windows Forms с помощью Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [Практическое руководство. Наследование класса UserControl.](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [Практическое руководство. Наследование класса Control.](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [Практическое руководство. Наследование существующих элементов управления Windows Forms](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [Практическое руководство. Тестирование поведения элемента UserControl во время выполнения](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)   
 [Создание собственных элементов управления](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)