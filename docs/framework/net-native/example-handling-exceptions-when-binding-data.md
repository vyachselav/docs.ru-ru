---
title: "Пример: Обработка исключений при привязке данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bd63ed96-9853-46dc-ade5-7bd1b0f39110
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Пример: Обработка исключений при привязке данных
> [!NOTE]
>  В этом разделе рассматривается предварительная версия программного обеспечения для разработчиков машинного кода .NET.  Предварительную версию можно загрузить на [веб\-сайте Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=394611) \(требуется регистрация\).  
  
 Следующий пример показывает, как для разрешения исключения [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), которое возникает при компиляции приложения с [!INCLUDE[net_native](../../../includes/net-native-md.md)], цепочка инструментов пытается привязать данные.  Сведения об исключении:  
  
```  
  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:   
App.ViewModels.MainPageVM  
  
```  
  
 Ниже приведен связанный стек вызова:  
  
```  
  
Reflection::Execution::ReflectionDomainSetupImplementation.CreateNonInvokabilityException+0x238  
Reflection::Core::ReflectionDomain.CreateNonInvokabilityException+0x2e  
Reflection::Core::Execution::ExecutionEnvironment.+0x316  
System::Reflection::Runtime::PropertyInfos::RuntimePropertyInfo.GetValue+0x1cb  
System::Reflection::PropertyInfo.GetValue+0x22  
System::Runtime::InteropServices::WindowsRuntime::CustomPropertyImpl.GetValue+0x42  
App!$66_Interop::McgNative.Func_IInspectable_IInspectable+0x158  
App!$66_Interop::McgNative::__vtable_Windows_UI_Xaml_Data__ICustomProperty.GetValue__STUB+0x46  
Windows_UI_Xaml!DirectUI::PropertyProviderPropertyAccess::GetValue+0x3f   
Windows_UI_Xaml!DirectUI::PropertyAccessPathStep::GetValue+0x31   
Windows_UI_Xaml!DirectUI::PropertyPathListener::ConnectPathStep+0x113  
  
```  
  
## Что делало это приложение?  
 В основе стека, кадры из пространства имен [Windows.UI.Xaml](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.aspx) указывают, что запущен механизм отрисовки XAML.  Использование метода <xref:System.Reflection.PropertyInfo.GetValue%2A?displayProperty=fullName>указывает на поиск на основе отражения значения свойства типа, метаданные которого были удалены.  
  
 На первом шаге предоставления директивы метаданных следовало бы добавить метаданные `serialize` для типа, чтобы его свойства стали доступны:  
  
```  
<Type Name="App.ViewModels.MainPageVM" Serialize="Required Public" />  
```  
  
## Это изолированный случай?  
 В этом сценарии, если привязка данных имеет неполные метаданные для одной модели `ViewModel`, это может быть справедливо и для других.  Если код структурирован таким образом, что все модели просмотра приложения находятся в пространстве имен `App.ViewModels`, можно использовать более общую директиву среды выполнения:  
  
```  
<Namespace Name="App.ViewModels " Serialize="Required Public" />  
```  
  
## Можно переписать код, чтобы не использовать отражение?  
 Так как привязки данных интенсивно использует отражение, изменение кода, чтобы избежать отражения невозможно.  
  
 Однако, существуют способы задания `ViewModel` странице XAML таким образом, чтобы цепочка инструментов могла связать привязки свойства с нужным типом во время компиляции и сохранить метаданные без использования директивы среды выполнения.  Например, можно применить атрибут [Windows.UI.Xaml.Data.BindableAttribute](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.data.bindableattribute.aspx) для свойств.  Это вынуждает компилятор XAML создать необходимые таблицы подстановок и избежать использования директивы среды выполнения в файле Default.rd.xml.  
  
## См. также  
 [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [Пример: Устранение неполадок динамического программирования](../../../docs/framework/net-native/example-troubleshooting-dynamic-programming.md)