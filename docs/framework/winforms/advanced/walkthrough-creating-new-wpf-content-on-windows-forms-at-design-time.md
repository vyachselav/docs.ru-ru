---
title: "Пошаговое руководство. Создание нового содержимого WPF для формы Windows Forms во время разработки | Microsoft Docs"
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
  - "ElementHost - элемент управления"
  - "размещение содержимого WPF в Windows Forms"
  - "взаимодействие, WPF и Windows Forms"
  - "содержимое WPF, размещение в Windows Forms"
  - "пользовательский элемент управления WPF, размещение в Windows Forms"
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Пошаговое руководство. Создание нового содержимого WPF для формы Windows Forms во время разработки
В этом разделе показано, как создать элемент управления Windows Presentation Foundation \(WPF\) для использования в приложениях на основе Windows Forms.  
  
 В этом пошаговом руководстве выполняются следующие задачи:  
  
-   создание проекта;  
  
-   создание элемента управления WPF;  
  
-   добавление нового элемента управления WPF в форму Windows Forms.  Элемент управления WPF размещается в элементе управления <xref:System.Windows.Forms.Integration.ElementHost>.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска.  Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров**.  Дополнительные сведения см. в разделе [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/ru-ru/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Обязательные компоненты  
 Ниже приведены компоненты, необходимые для выполнения данного пошагового руководства.  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## Создание проекта  
 Первым шагом является создание проекта Windows Forms.  
  
> [!NOTE]
>  При размещении содержимого WPF поддерживаются только проекты C\# и Visual Basic.  
  
#### Создание проекта  
  
-   Создайте проект приложения Windows Forms в Visual Basic или Visual C\# с именем `HostingWpf`.  
  
## Создание элемента управления WPF  
 Создать элемент управления WPF и добавить его в проект можно так же легко, как добавить в проект любой другой элемент.  Конструктор Windows Forms работает с элементами управления особого типа, которые называются *составными* или *пользовательскими элементами управления*.  Подробнее о пользовательских элементах управления WPF см. в разделе <xref:System.Windows.Controls.UserControl>.  
  
> [!NOTE]
>  Тип <xref:System.Windows.Controls.UserControl?displayProperty=fullName> для элементов управления WPF отличается от типа пользовательских элементов управления, предоставляемого Windows Forms, который также называется <xref:System.Windows.Forms.UserControl?displayProperty=fullName>.  
  
#### Создание элемента управления WPF  
  
1.  В **обозревателе решений** добавьте в решение новый проект **Библиотека пользовательских элементов управления WPF**.  Используйте имя по умолчанию для библиотеки элементов управления \(`WpfControlLibrary1`\).  Имя элемента управления по умолчанию — `UserControl1.xaml`.  
  
     В результате добавления нового элемента управления происходит следующее:  
  
    -   Добавляется файл UserControl1.xaml.  
  
    -   Добавляется файл UserControl1.xaml.cs или UserControl1.xaml.vb.  Этот файл содержит код программной части для обработчиков событий и иных реализованных компонентов.  
  
    -   Добавляются ссылки на сборки WPF.  
  
    -   Файл UserControl1.xaml открывается в [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)].  
  
2.  Убедитесь в том, что элемент `UserControl1` выбран в представлении конструирования.  Подробнее см. в разделе [Практическое руководство. Выбор и перемещение элементов в область конструктора](http://msdn.microsoft.com/ru-ru/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  В окне **Свойства** присвойте свойствам <xref:System.Windows.FrameworkElement.Width%2A> и <xref:System.Windows.FrameworkElement.Height%2A> значение `200`.  
  
4.  Перетащите элемент управления <xref:System.Windows.Controls.TextBox?displayProperty=fullName> из **панели элементов** в рабочую область конструирования.  
  
5.  В окне **Свойства** присвойте свойству <xref:System.Windows.Controls.TextBox.Text%2A> значение Hosted Content.  
  
    > [!NOTE]
    >  Обычно размещается более сложное содержимое WPF.  Элемент управления <xref:System.Windows.Controls.TextBox?displayProperty=fullName> используется здесь в целях наглядности.  
  
6.  Выполните построение проекта.  
  
## Добавление элемента управления WPF в форму Windows Forms  
 Новый элемент управления WPF готов к использованию в форме.  Элемент управления <xref:System.Windows.Forms.Integration.ElementHost> используется в формах Windows Forms для размещения содержимого WPF.  
  
#### Добавление элемента управления WPF в форму Windows Forms  
  
1.  Откройте `Form1` в конструкторе Windows Forms.  
  
2.  В области **Панель элементов** найдите вкладку **WPFUserControlLibrary элементы управления WPF**.  
  
3.  Перетащите экземпляр `UserControl1` в форму.  
  
    -   Для размещения элемента управления WPF на форме будет автоматически создан элемент управления <xref:System.Windows.Forms.Integration.ElementHost>.  
  
    -   Элемент управления <xref:System.Windows.Forms.Integration.ElementHost> получает имя `elementHost1`, а как видно в окне **Свойства**, его свойство <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> получает значение **UserControl1**.  
  
    -   В проект добавляются ссылки на сборки WPF.  
  
    -   Элемент управления `elementHost1` имеет панель смарт\-тегов, на которой приводятся имеющиеся параметры размещения.  
  
4.  На панели смарт\-тегов **Задачи ElementHost** выберите пункт **Закрепить в родительском контейнере**.  
  
5.  Нажмите клавишу F5, чтобы выполнить сборку приложения и запустить его.  
  
## Следующие действия  
 Windows Forms и WPF — это разные технологии, но они предназначены для тесного взаимодействия.  Следующие приемы расширяют возможности по настройке внешнего вида и поведения приложений:  
  
-   Размещение элемента управления Windows Forms на странице WPF.  Подробнее см. в разделе [Пошаговое руководство. Размещение элемента управления Windows Forms в приложении WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md).  
  
-   Применение стилей оформления Windows Forms к содержимому WPF.  Подробнее см. в разделе [Практическое руководство. Включение визуальных стилей в гибридном приложении](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md).  
  
-   Изменение стиля оформления содержимого WPF.  Подробнее см. в разделе [Пошаговое руководство. Применение стилей к содержимому WPF](../../../../docs/framework/winforms/advanced/walkthrough-styling-wpf-content.md).  
  
## См. также  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Миграция и взаимодействие систем](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Использование элементов управления WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [Конструктор WPF](http://msdn.microsoft.com/ru-ru/c6c65214-8411-4e16-b254-163ed4099c26)