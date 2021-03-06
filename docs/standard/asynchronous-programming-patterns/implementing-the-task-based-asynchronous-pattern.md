---
title: "Implementing the Task-based Asynchronous Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework, and TAP"
  - "asynchronous design patterns, .NET Framework"
  - "TAP, .NET Framework support for"
  - "Task-based Asynchronous Pattern, .NET Framework support for"
  - ".NET Framework, asynchronous design patterns"
ms.assetid: fab6bd41-91bd-44ad-86f9-d8319988aa78
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Implementing the Task-based Asynchronous Pattern
Можно реализовать асинхронную модель на основе задач \(TAP\) тремя способами: с помощью компиляторов C\# и Visual Basic в Visual Studio, вручную или путем сочетания этих методов.  Каждый метод подробно обсуждается в следующих разделах.  Шаблон TAP можно использовать для реализации асинхронных операций, привязанных к ограничениям по скорости вычислений и вводу\-выводу. В разделе [рабочие нагрузки](#workloads) рассматриваются операции каждого типа.  
  
## Создание методов TAP  
  
### С помощью компиляторов  
 В [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] и [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], любой метод, который помечен c помощью атрибута ключевым словом `async` \(`Async` в Visual Basic\) считается асинхронным методом, а компиляторы C\# и Visual Basic выполняют необходимые преобразования для реализации метода асинхронно с помощью шаблона TAP.  Асинхронный метод должен возвращать объект  <xref:System.Threading.Tasks.Task?displayProperty=fullName> или <xref:System.Threading.Tasks.Task%601?displayProperty=fullName>.  В последнем случае тело функции должны возвращать `TResult`, и компилятор гарантирует доступность этого результата через объект результирующей задачи.  Аналогичным образом любые исключения, которые не обрабатываться в теле метода маршалируются в выходную задачу и вызывают окончание результирующей задачи в состоянии <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>.  Исключение возникает, когда <xref:System.OperationCanceledException> \(или производный тип\) остаются необработанными. В этом случае результирующая задача заканчивается в состоянии <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>.  
  
### Создание методов TAP вручную  
 Можно реализовать шаблон TAP для улучшения контроля над реализацией вручную.  Компилятор использует общую контактную зону, предоставленную из пространства имен <xref:System.Threading.Tasks?displayProperty=fullName>, и вспомогательные типы в пространстве имен <xref:System.Runtime.CompilerServices?displayProperty=fullName>.  Чтобы реализовать шаблон TAP самостоятельно, необходимо создать объект <xref:System.Threading.Tasks.TaskCompletionSource%601>, выполнить асинхронную операцию и после ее завершения вызвать метод <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A> или <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A>, или версии одного из этих методов `Try`.  При реализации метода TAP вручную необходимо выполнить результирующую задачу после завершения представленной асинхронной операции.  Например:  
  
 [!code-csharp[Conceptual.TAP_Patterns#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#1)]
 [!code-vb[Conceptual.TAP_Patterns#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#1)]  
  
### Гибридный подход  
 Может оказаться полезным реализовать шаблон TAР вручную, но делегировать основную логику для реализации компилятору.  Например, может использовать гибридный подход, когда требуется проверить аргументы за пределами асинхронного метода, созданного компилятором, для того, чтобы исключения могли переходить к непосредственному вызывающему объекту метода, а не предоставлялись через объект <xref:System.Threading.Tasks.Task?displayProperty=fullName>:  
  
 [!code-csharp[Conceptual.TAP_Patterns#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#2)]
 [!code-vb[Conceptual.TAP_Patterns#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#2)]  
  
 Другой случай, когда такое делегирование полезно, связан с реализацией оптимизации быстрого перехода при необходимости вернуть кэшированную задачу.  
  
<a name="workloads"></a>   
## Рабочие нагрузки  
 Реализацию асинхронных операций, связанных с вводом\-выводом и ограниченных по скорости вычислений, можно выполнить как методы TAP.  Тем не менее, когда методы TAP предоставляются открыто из библиотеки, они должны быть предоставлены только для рабочих нагрузок, связанных с операциями ввода\-вывода \(они также могут включать в себя вычисления, но не должны быть исключительно вычислительными\).  Если метод является ограниченным исключительно по скорости вычислений, он должен быть предоставлен только как синхронная реализация; код, который его использует, может определять, следует ли создать оболочку для вызова этого асинхронного метода в задачу для выгрузки работы в другой поток или для достижения параллелизма.  
  
### Задачи, ограниченные по скорости вычислений  
 Класс <xref:System.Threading.Tasks.Task?displayProperty=fullName> идеально подходит для представления ресурсоемких вычислительных операций.  По умолчанию он использует специальную поддержку в классе <xref:System.Threading.ThreadPool>, чтобы обеспечить эффективное выполнение, а также обеспечивает значительный контроль над тем, когда, где и как выполнять асинхронные вычисления.  
  
 Задачи ограниченных по скорости вычислений можно создать одним из следующих способов:  
  
-   В платформе .NET Framework 4 используйте метод <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName>, который принимает делегат \(обыкновенно <xref:System.Action%601> или <xref:System.Func%601>\) для асинхронного выполнения.  Если предоставить делегат <xref:System.Action%601>, этот метод возвращает объект <xref:System.Threading.Tasks.Task?displayProperty=fullName>, представляющий асинхронное выполнение этого делегата.  Если предоставить делегат <xref:System.Func%601>, этот метод возвращает объект <xref:System.Threading.Tasks.Task%601?displayProperty=fullName>.  Перегрузки метода <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> принимают маркер отмены \(<xref:System.Threading.CancellationToken>\), параметры создания задач \(<xref:System.Threading.Tasks.TaskCreationOptions>\) и планировщик заданий \(<xref:System.Threading.Tasks.TaskScheduler>\), которые обеспечивают точное управление планированием и выполнением задачи.  Экземпляр фабрики, предназначенный для текущего планировщика заданий доступен как статическое свойство \(<xref:System.Threading.Tasks.Task.Factory%2A>\) из класса <xref:System.Threading.Tasks.Task>; Например: `Task.Factory.StartNew(…)`.  
  
-   В [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] используйте статический метод <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> как ярлык для <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName>.  Вы можете использовать <xref:System.Threading.Tasks.Task.Run%2A> для простого запуска ограниченных по скорости вычислений задач, предназначенных для пула потоков.  В [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] это предпочтительный механизм для запуска задачи, ограниченной по скорости вычислений.  Используйте `StartNew` непосредственно, только когда требуется обеспечить более точный контроль над задачей.  
  
-   Используйте конструкторы типа `Task` типа или метод `Start`, если требуется создать и запланировать задание отдельно.  Открытые методы должны возвращать только задачи, которые уже были начаты.  
  
-   Можно использовать перегрузки метода <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=fullName>.  Этот метод создает новую задачу, которая запланирована после завершения другой задачи.  Некоторые перегрузки <xref:System.Threading.Tasks.Task.ContinueWith%2A> принимают токен отмены, параметры продолжения и планировщик задач для улучшения контроля над планированием и выполнением задачи продолжения.  
  
-   Используйте методы <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=fullName> и <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A?displayProperty=fullName>.  Эти методы создают новую задачу, которая планируется по завершении всех или какой\-либо из предоставленного набора задач.  Эти методы также предоставляют перегрузки для управления планированием и исполнением этих задач.  
  
 В задачах, ограниченных по скорости вычислений, система может предотвратить выполнение запланированной задачи при получении запроса отмены до запуска задачи.  Таким образом, если предоставить токен отмены \(объект<xref:System.Threading.CancellationToken>\), можно передать его асинхронному коду, который следит за токеном.  Можно также предоставить токен для одного из вышеупомянутых методов таких, как `StartNew` или `Run` для того, чтобы среда выполнения , `Task` могла также осуществлять его мониторинг.  
  
 Например, рассмотрим асинхронный метод, который выводит изображение на экран.  Тело задачи может выполнять опрос токена отмены для того, чтобы код мог завершиться раньше при получении запроса отмены во время отрисовки.  Кроме того, если перед началом отрисовки поступает запрос на отмену, можно запретить операцию визуализации:  
  
 [!code-csharp[Conceptual.TAP_Patterns#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#3)]
 [!code-vb[Conceptual.TAP_Patterns#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#3)]  
  
 Задача, ограниченная по скорости вычислений, завершается в состоянии <xref:System.Threading.Tasks.TaskStatus>, если хотя бы одно из следующих условий верно:  
  
-   запрос отмены поступает через объект <xref:System.Threading.CancellationToken>, который предоставляется как аргумент метода создания \(например, `StartNew` или `Run`\) до того, как задача переходит в состояние <xref:System.Threading.Tasks.TaskStatus>.  
  
-   исключение <xref:System.OperationCanceledException> остается необработанным в теле такой задачи, исключение содержит тот же токен отмены <xref:System.Threading.CancellationToken>, который передается задаче, а токен указывает на наличие запроса отмены.  
  
 Если другое исключение останется необработанным в теле задачи, задача завершается в состояние <xref:System.Threading.Tasks.TaskStatus>, и любые попытки ожидания для задачи или доступа к ее результату вызывает исключение.  
  
### Задачи ввода вывода  
 Чтобы создать задание, которое не должно непосредственно поддерживаться потоком во время всего его выполнения, используйте тип <xref:System.Threading.Tasks.TaskCompletionSource%601>.  Этот тип предоставляет свойство <xref:System.Threading.Tasks.TaskCompletionSource%601.Task%2A>, которое возвращает связанный экземпляр <xref:System.Threading.Tasks.Task%601>.  Жизненный цикл этой задачи управляется методами <xref:System.Threading.Tasks.TaskCompletionSource%601>, такими как <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A>, и их вариантами `TrySet`.  
  
 Предположим, что вы хотите создать задачу, которая будет завершена после указанного периода времени.  Например, можно отложить выполнение в пользовательском интерфейсе.  Класс <xref:System.Threading.Timer?displayProperty=fullName> обеспечивает возможность асинхронного вызова делегат после определенного периода времени, а используя <xref:System.Threading.Tasks.TaskCompletionSource%601>, можно установить начало <xref:System.Threading.Tasks.Task%601> на таймере, например:  
  
 [!code-csharp[Conceptual.TAP_Patterns#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#4)]
 [!code-vb[Conceptual.TAP_Patterns#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#4)]  
  
 Начиная с [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], метод <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=fullName> предоставляется для этой цели, и можно использовать его внутри другого асинхронного метода, например, для реализации асинхронного цикла опроса:  
  
 [!code-csharp[Conceptual.TAP_Patterns#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#5)]
 [!code-vb[Conceptual.TAP_Patterns#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#5)]  
  
 Класс <xref:System.Threading.Tasks.TaskCompletionSource%601> не имеет неуниверсального эквивалента.  Теме не менее, <xref:System.Threading.Tasks.Task%601> является производным от <xref:System.Threading.Tasks.Task> и это дает возможность использовать универсальный объект <xref:System.Threading.Tasks.TaskCompletionSource%601> для связанных с вводом\-выводом методов, которые просто возвращают задачу.  Чтобы это сделать, можно использовать источник с фиктивным `TResult` \(<xref:System.Boolean> — неплохой выбор по умолчанию, однако, если вас беспокоит пользователь <xref:System.Threading.Tasks.Task>, приводящие его к <xref:System.Threading.Tasks.Task%601>, можно вместо этого использовать частный тип `TResult`\).  Например, метод `Delay` в предыдущем примере возвращает текущее значение времени и конечного смещения \(`Task<DateTimeOffset>`\).  Если значение результата не нужно, метод можно вместо этого построить следующим образом \(Обратите внимание на изменение типа возвращаемого значения и изменения аргумент для <xref:System.Threading.Tasks.TaskCompletionSource%601.TrySetResult%2A>\):  
  
 [!code-csharp[Conceptual.TAP_Patterns#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#6)]
 [!code-vb[Conceptual.TAP_Patterns#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#6)]  
  
### Смешанные задачи, связанные с вводом\-выводом и ограниченные по скорости вычислений  
 Асинхронные методы не ограничиваются только операциями, связанными с вводом\-выводом или ограниченными по скорости вычислений, а могут представлять собой их комбинацию.  На практике несколько асинхронных операций часто объединяются в большие по размеру смешанные операции.  Например, метод `RenderAsync` в предыдущем примере выполнил операцию с большим количеством вычислений, чтобы отобразить изображение, зависящее от некоторых входных данных `imageData`.  Это изображение `imageData` могло бы быть получено из веб\-службы, к которой осуществляется асинхронный доступ:  
  
 [!code-csharp[Conceptual.TAP_Patterns#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#7)]
 [!code-vb[Conceptual.TAP_Patterns#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#7)]  
  
 Этот пример также демонстрирует, как один токен отмены может направляться через несколько асинхронных операций.  Дополнительные сведения см. в разделе «Использование отмены» в [Consuming the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md).  
  
## См. также  
 [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)   
 [Consuming the Task\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)   
 [Interop with Other Asynchronous Patterns and Types](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)