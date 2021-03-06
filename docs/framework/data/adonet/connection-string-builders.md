---
title: "Построители строк подключения | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Построители строк подключения
В более ранних версиях [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] проверка строк подключения с объединенными строковыми значениями во время компиляции не проводилась, поэтому во время выполнения неверное ключевое слово приводило к формированию исключения <xref:System.ArgumentException>.  Каждый из поставщиков данных платформы [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] поддерживал различный синтаксис ключевых слов строк соединения, что делало ручное построение допустимых строк соединения затруднительным.  Для решения этой проблемы в [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 появились новые построители строк подключения для каждого поставщика данных платформы [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Каждый поставщик данных включает класс построителя строк соединения со строгой типизацией, наследованный от класса <xref:System.Data.Common.DbConnectionStringBuilder>.  В следующей таблице перечислены поставщики данных платформы [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] и связанные с ними классы построителей строк соединения.  
  
|Поставщик|Класс ConnectionStringBuilder|  
|---------------|-----------------------------------|  
|<xref:System.Data.SqlClient>|<xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OleDb>|<xref:System.Data.OleDb.OleDbConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.Odbc>|<xref:System.Data.Odbc.OdbcConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OracleClient>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=fullName>|  
  
## Атаки путем внедрения данных в строку подключения  
 Атака путем внедрения данных в строку соединения может произойти при использовании динамического объединения строк для построения строк соединения, основанных на входных данных пользователя.  Если строка не проверяется, а вредоносный текст или символы не экранируются, злоумышленник может получить потенциальный доступ к конфиденциальным данным или другим ресурсам сервера.  Например, злоумышленник может осуществить атаку, установив точку с запятой и добавив дополнительное значение.  Строка соединения анализируется с помощью алгоритма «по последнему значению», и допустимое значение заменяется вредоносными данными.  
  
 Классы построителей строк соединения созданы для устранения предположений и защиты от синтаксических ошибок и уязвимостей системы безопасности.  Они предоставляют методы и свойства, соответствующие известным парам «ключ\-значение», разрешенным каждым поставщиком данных.  Каждый класс поддерживает фиксированную коллекцию синонимов и может переводить синоним в соответствующее общеизвестное ключевое имя.  Выполняются проверки на допустимые пары «ключ\-значение», и недопустимая пара вызывает исключение.  Кроме того, внедренные значения обрабатываются безопасным образом.  
  
 В следующем примере демонстрируется обработка с помощью объекта <xref:System.Data.SqlClient.SqlConnectionStringBuilder> дополнительного значения для параметра `Initial Catalog`.  
  
```vb  
Dim builder As New System.Data.SqlClient.SqlConnectionStringBuilder  
builder("Data Source") = "(local)"  
builder("Integrated Security") = True  
builder("Initial Catalog") = "AdventureWorks;NewValue=Bad"  
Console.WriteLine(builder.ConnectionString)  
```  
  
```csharp  
System.Data.SqlClient.SqlConnectionStringBuilder builder =  
  new System.Data.SqlClient.SqlConnectionStringBuilder();  
builder["Data Source"] = "(local)";  
builder["integrated Security"] = true;  
builder["Initial Catalog"] = "AdventureWorks;NewValue=Bad";  
Console.WriteLine(builder.ConnectionString);  
```  
  
 Выход показывает, что объект <xref:System.Data.SqlClient.SqlConnectionStringBuilder> правильно выполняет обработку параметра путем экранирования дополнительного значения, заключенного в двойные кавычки, вместо того чтобы добавить его в строку соединения в качестве новой пары «ключ\-значение».  
  
```  
data source=(local);Integrated Security=True;  
initial catalog="AdventureWorks;NewValue=Bad"  
```  
  
## Построение строк соединения из файлов конфигурации  
 Если некоторые элементы строки соединения известны заранее, их можно сохранить в файле конфигурации и во время выполнения получить для построения полной строки соединения.  Например, в отличие от имени сервера, имя базы данных может быть известно заранее.  Также можно принудительно задать ввод пользователем имени и пароля во время выполнения, чтобы исключить возможность внедрения других значений в строку соединения.  
  
 Один из перегруженных конструкторов для построителя строки соединения принимает в качестве аргумента значение типа <xref:System.String>, что позволяет использовать частичную строку соединения, которую впоследствии пользователь может дополнить.  Частичную строку соединения можно сохранить в файле конфигурации и получить во время выполнения.  
  
> [!NOTE]
>  Пространство имен <xref:System.Configuration> обеспечивает программный доступ к файлам конфигурации, предоставляя класс <xref:System.Web.Configuration.WebConfigurationManager> для веб\-приложений и класс <xref:System.Configuration.ConfigurationManager> для приложений Windows.  Дополнительные сведения о работе со строками соединения и файлами конфигурации см. в разделе [Строки соединения и файлы конфигурации](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md).  
  
### Пример  
 В этом примере демонстрируется получение частичной строки соединения из файла конфигурации и ее завершение путем установки свойств <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>, <xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> и <xref:System.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> для объекта <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  Файл конфигурации определяется следующим образом.  
  
```  
<connectionStrings>  
  <clear/>  
  <add name="partialConnectString"   
    connectionString="Initial Catalog=Northwind;"  
    providerName="System.Data.SqlClient" />  
</connectionStrings>  
```  
  
> [!NOTE]
>  Для запуска кода необходимо задать в проекте ссылку на библиотеку `System.Configuration.dll`.  
  
 [!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/CS/source.cs#1)]
 [!code-vb[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/VB/source.vb#1)]  
  
## См. также  
 [Строки подключения](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Конфиденциальность и безопасность данных](../../../../docs/framework/data/adonet/privacy-and-data-security.md)   
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)