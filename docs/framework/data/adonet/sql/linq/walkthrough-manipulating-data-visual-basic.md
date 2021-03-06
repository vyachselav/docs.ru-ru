---
title: "Пошаговое руководство. Обработка данных (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f6a54f6-ec33-452a-a37d-48122207bf14
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Пошаговое руководство. Обработка данных (Visual Basic)
В данном руководстве представлен основной и полный сценарий [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] по добавлению, изменению и удалению данных в базе данных.  Для добавления клиента, изменения его имени и удаления заказа следует использовать копию учебной базы данных Northwind.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Это пошаговое руководство было написано с помощью параметров разработки Visual Basic.  
  
## Обязательные компоненты  
 Необходимо выполнить следующие требования.  
  
-   Для хранения файлов используется выделенная папка \("c:\\linqtest2"\).  Прежде чем приступить к выполнению задач, создайте такую папку.  
  
-   Наличие учебной базы данных Northwind.  
  
     Если база данных не установлена на компьютере разработчика, загрузите ее с веб\-узла Центра загрузки Майкрософт.  Дополнительные сведения см. в разделе [Загрузка образцов баз данных](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  После загрузки базы данных скопируйте файл northwnd.mdf в папку c:\\linqtest2.  
  
-   Наличие файла кода Visual Basic, созданного из базы данных "Борей".  
  
     Его можно создать либо помощью оператора [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)], либо с помощью средства SQLMetal.  Данное пошаговое руководство было написано с использованием средства SQLMetal со следующей командной строкой:  
  
     **sqlmetal \/code:"c:\\linqtest2\\northwind.vb" \/language:vb "C:\\linqtest2\\northwnd.mdf" \/pluralize**  
  
     Для получения дополнительной информации см. [SqlMetal.exe \(средство создания кода\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Обзор  
 Данное пошаговое руководство состоит из шести основных задач.  
  
-   Создание решения [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] в [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Добавление файла кода базы данных в проект.  
  
-   Создание нового объекта клиента.  
  
-   Изменение контактного имени клиента.  
  
-   Удаление заказа.  
  
-   Отправка внесенных изменений в базу данных Northwind.  
  
## Создание решения LINQ to SQL  
 В первой задаче создается решение [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], которое содержит ссылки, необходимые для построения и выполнения проекта [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
#### Создание решения LINQ to SQL  
  
1.  В меню **Файл** [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] выберите пункт **Создать проект**.  
  
2.  В диалоговом окне **Создание проекта** в области **Тип проекта** выберите **Visual Basic**.  
  
3.  В области **Шаблоны** щелкните **Консольное приложение**.  
  
4.  В поле **Имя** введите LinqDataManipulationApp.  
  
5.  Нажмите кнопку **ОК**.  
  
## Добавление ссылок и директив LINQ  
 В этом пошаговом руководстве используются сборки, которые могут быть не установлены по умолчанию в проект.  Если `System.Data.Linq` не входит в список ссылок проекта \(щелкните **Показать все файлы** в **обозревателе решений** и разверните узел **Ссылки**\), добавьте ее, как описано в следующих действиях.  
  
#### Добавление сборки System.Data.Linq  
  
1.  В **Обозревателе решений** щелкните правой кнопкой мыши узел **Ссылки** и выберите команду **Добавить ссылку**.  
  
2.  В диалоговом окне **Добавление ссылки** щелкните **.NET**, выберите сборку System.Data.Linq, а затем нажмите кнопку **ОК**.  
  
     Сборка будет добавлена в проект.  
  
3.  В редакторе кода добавьте следующую директиву перед **Module1**.  
  
     [!code-vb[DLinqWalk3VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#1)]  
  
## Добавление файла кода Northwind в проект  
 При выполнении этих действий подразумевается, что для создания файла кода из учебной базы данных Northwind использовалось средство SQLMetal.  Дополнительные сведения см. в разделе "Предварительные требования" ранее в этом руководстве.  
  
#### Добавление файла кода northwind в проект  
  
1.  В меню **Проект** выберите команду **Добавить существующий элемент**.  
  
2.  В диалоговом окне **Добавление существующего элемента** перейдите к файлу c:\\linqtest2\\northwind.vb и нажмите кнопку **Добавить**.  
  
     Файл northwind.vb будет добавлен в проект.  
  
## Настройка подключения к базе данных  
 Сначала проверьте подключение к базе данных.  Обратите особое внимание, что в имени базы данных \- Northwnd \- отсутствует буква "i".  Если при выполнении следующих действий возникают ошибки, просмотрите файл northwind.vb, чтобы определить написание разделяемого класса Northwind.  
  
#### Настройка и проверка подключения к базе данных  
  
1.  Введите или вставьте следующий код в `Sub Main`.  
  
     [!code-vb[DLinqWalk3VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#2)]  
  
2.  Чтобы проверить приложение на этом этапе, нажмите клавишу F5.  
  
     Откроется окно **Консоль**.  
  
     Закройте приложение. Для этого в окне **Консоль** нажмите клавишу ВВОД либо в [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] в меню **Отладка** выберите команду **Остановить отладку**.  
  
## Создание новой сущности  
 Создание новой сущности не представляет особых проблем.  Для создания объектов \(например, `Customer`\) можно использовать ключевое слово `New`.  
  
 В этом и следующих разделах выполняются изменения только локального кэша.  Изменения не будут отправлены в базу данных до тех пор, пока ближе к концу данного руководства не будет вызван <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
#### Добавление нового объекта сущностей Customer  
  
1.  Создайте новый `Customer`, добавив перед `Console.ReadLine` в `Sub Main` следующий код.  
  
     [!code-vb[DLinqWalk3VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#3)]  
  
2.  Нажмите клавишу F5 для отладки решения.  
  
     В окне консоли отображаются следующие результаты.  
  
     `Customers matching CA before insert:`  
  
     `Customer ID: CACTU`  
  
     `Customer ID: RICAR`  
  
     Обратите внимание, что в выходных данных новая строка не отображается.  Новые данные еще не были переданы в базу данных.  
  
3.  Чтобы остановить отладку, в окне **Консоль** нажмите клавишу ВВОД.  
  
## Обновление сущности  
 При выполнении следующих действий будет извлечен объект `Customer` и изменено одно из его свойств.  
  
#### Изменение имени клиента  
  
-   Добавьте следующий код перед `Console.ReadLine()`:  
  
     [!code-vb[DLinqWalk3VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#4)]  
  
## Удаление сущности  
 Используя тот же самый объект клиента, можно удалить первый заказ.  
  
 В следующем коде показано, как разорвать связь между строками и удалить строку из базы данных.  
  
#### Удаление строки  
  
-   Добавьте следующий код перед `Console.ReadLine()`.  
  
     [!code-vb[DLinqWalk3VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#5)]  
  
## Отправка изменений в базу данных  
 Последнее действие, необходимое для создания, обновления и удаления объектов, заключается в фактической отправке изменений в базу данных.  Без него изменения останутся на локальном уровне и не появятся в результатах запроса.  
  
#### Отправка изменений в базу данных  
  
1.  Вставьте следующий код перед `Console.ReadLine`.  
  
     [!code-vb[DLinqWalk3VB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#6)]  
  
2.  Вставьте следующий код \(после `SubmitChanges`\), чтобы показать результаты до и после отправки изменений.  
  
     [!code-vb[DLinqWalk3VB#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#7)]  
  
3.  Нажмите клавишу F5 для отладки решения.  
  
     Появится окно консоли со следующими данными.  
  
    ```  
    Customers matching CA before update:  
    Customer ID: CACTU  
    Customer ID: RICAR  
  
    The Order Detail to be deleted is: OrderID = 10643  
  
    Customers matching CA after update:  
    Customer ID: A3VCA  
    Customer ID: CACTU  
    Customer ID: RICAR  
    ```  
  
4.  Чтобы остановить отладку, в окне **Консоль** нажмите клавишу ВВОД.  
  
> [!NOTE]
>  После добавления нового клиента путем отправки изменений это решение нельзя повторно выполнить в исходном виде, поскольку этот же клиент не может быть добавлен без изменений.  Для повторного выполнения решения измените значение идентификатора добавляемого клиента.  
  
## См. также  
 [Обучение с помощью пошаговых руководств](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)