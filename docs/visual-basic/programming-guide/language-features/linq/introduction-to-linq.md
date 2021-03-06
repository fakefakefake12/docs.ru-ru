---
title: "Введение в LINQ в Visual Basic | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], about LINQ in Visual Basic queries
- query execution [LINQ in Visual Basic]
- range variables
- LINQ [Visual Basic]
- LINQ [Visual Basic], about LINQ in Visual Basic
- query expressions [LINQ in Visual Basic]
- LINQ
- deferred execution
- iteration variables
ms.assetid: 3047d86e-0d49-40e2-928b-dc02e46c7984
caps.latest.revision: 28
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e1343b06089df63beb73cbb27a38de396f5cb6c8
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-linq-in-visual-basic"></a>Знакомство с LINQ в Visual Basic
Встроенные в язык запросы (LINQ) позволяют использовать запросы в [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] и предоставляют простые, но эффективные средства для работы с любыми видами данных. Технология LINQ позволяет не отправлять запросы на обработку в базу данных и не разрабатывать отдельный синтаксис запросов для каждого типа искомых данных, а вводит запросы в состав языка [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Синтаксис запросов не зависит от типа данных.  
  
 LINQ позволяет запрашивать данные из базы данных SQL Server, XML, в памяти массивов и коллекций, [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] наборы данных или любые другие данные удаленного или локального источника, поддерживаемые LINQ. Все это можно делать с помощью обычных элементов языка [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Поскольку запросы составляются на языке [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], их результаты возвращаются в виде строго типизированных объектов. Эти объекты поддерживают технологию IntelliSense, что позволяет писать код быстрее и перехватывать ошибки в запросах при компиляции, а не при выполнении. Запросы LINQ можно использовать как источник дополнительных запросов для уточнения результатов, а также связывать с элементами управления, позволяя пользователям легко просматривать и изменять результаты запросов.  
  
 Например в следующем примере кода показан запрос LINQ, возвращающий список заказчиков из коллекции и группирующий их по расположению.  
  
 [!code-vb[VbVbalrIntroToLINQ&#1;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_1.vb)]  
  
 В этом разделе содержатся сведения о следующих областях:  
  
-   [Выполнение примеров](#RunningtheExamples)  
  
-   [Поставщики LINQ](#LINQProviders)  
  
-   [Структура запроса LINQ](#StructureOfALINQQuery)  
  
-   [Операторы запросов LINQ в Visual Basic](#VisualBasicLINQQueryOperators)  
  
-   [Подключение к базе данных с помощью LINQ to SQL](#ConnectingToADatabase)  
  
-   [Возможности Visual Basic, поддерживающие LINQ](#VisualBasicFeaturesThatSupportLINQ)  
  
-   [Отложенное и немедленное выполнение запроса](#QueryExecution)  
  
-   [XML в Visual Basic](#XMLInVisualBasic)  
  
-   [Связанные ресурсы](#RelatedResources)  
  
-   [Как и пошаговые руководства](#HowToAndWalkthroughTopics)  
  
##  <a name="RunningtheExamples"></a>Выполнение примеров  
 Для выполнения примеров, приведенных во введении и в разделе «Структура запроса LINQ», используйте указанный ниже код, который возвращает список клиентов и заказов.  
  
 [!code-vb[VbVbalrIntroToLINQ&#31;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_2.vb)]  
  
##  <a name="LINQProviders"></a>Поставщики LINQ  
 Объект *поставщик LINQ* сопоставляет вашей [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] запросы LINQ для источника данных запрос. При написании запроса LINQ поставщик принимает запрос и переводит его в команды, которые источник данных будет способен выполнить. Затем поставщик преобразует данные из источника в объекты, составляющие результат запроса. И, наконец, при отправке обновлений на источник данных он преобразует объекты в данные.  
  
 В [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] входят следующие поставщики LINQ:  
  
|Поставщик|Описание|  
|---|---|  
|LINQ to Objects|Поставщик LINQ to Objects позволяет направлять запросы к коллекциям и массивам, которые находятся в памяти. Если объект поддерживает <xref:System.Collections.IEnumerable>или <xref:System.Collections.Generic.IEnumerable%601>интерфейс, поставщик LINQ to Objects позволяет запрашивать его.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable><br /><br /> Можно включить поставщик LINQ to Objects путем импорта <xref:System.Linq>имен, которое импортируется по умолчанию для всех [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] проектов.</xref:System.Linq><br /><br /> Дополнительные сведения о поставщик LINQ to Objects, в разделе [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9).|  
|LINQ to SQL|Поставщик LINQ to SQL позволяет запрашивать и изменять данные в базе данных SQL Server. Это упрощает сопоставление объектной модели приложения с таблицами и объектами в базе данных.<br /><br /> [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] упрощает работу с LINQ to SQL включением реляционного конструктора объектов (O/R-конструктора). Он используется для создания в приложении модели объекта, которая сопоставляется с объектами в базе данных. Реляционный конструктор объектов также предоставляет функциональные возможности для сопоставления хранимых процедур и функций <xref:System.Data.Linq.DataContext>объект, который управляет связью с базой данных и сохраняет состояние проверок на оптимистический параллелизм.</xref:System.Data.Linq.DataContext><br /><br /> Дополнительные сведения о поставщике LINQ to SQL см. в разделе [LINQ to SQL](https://msdn.microsoft.com/library/bb386976). Дополнительные сведения о реляционном конструкторе объектов см. в разделе [средства LINQ to SQL в Visual Studio](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).|  
|LINQ to XML|Поставщик LINQ to XML позволяет запрашивать и изменять XML. XML можно изменить в памяти, загрузить из файла и сохранить в файл.<br /><br /> Кроме того, поставщик LINQ to XML разрешает использовать литералы XML и свойств оси XML, что позволяет записывать XML непосредственно в код [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Дополнительные сведения см. в разделе [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md).|  
|LINQ to DataSet|Поставщик LINQ to DataSet позволяет запрашивать и обновлять данные в [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] набора данных. Функции LINQ можно добавить в приложения, использующие наборы данных — это позволит упростить и расширить возможности составления запросов, статистической обработки и обновления данных в наборе данных.<br /><br /> Дополнительные сведения см. в разделе [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17).|  
  
##  <a name="StructureOfALINQQuery"></a>Структура запроса LINQ  
 Запрос LINQ, часто называют *выражение запроса*, состоит из комбинации предложений запросов, определяющих источники данных и переменные итерации для запроса. Выражение запроса может также включать инструкции для сортировки, фильтрации, группировки и присоединения либо формулы для применения к исходным данным. Синтаксис выражения запроса напоминает синтаксис SQL, поэтому многие его элементы могут показаться вам знакомыми.  
  
 Выражение запроса начинается с предложения `From`. Это предложение определяет исходные данные для запроса и переменные, которые используются для обращения к каждому элементу источника данных по отдельности. Эти переменные называются *переменным диапазона* или *переменные итераций*. Предложение `From` является обязательным для запросов, кроме запросов `Aggregate`, где предложение `From` использовать необязательно. После определения области и источника запроса в предложении `From` или `Aggregate` можно добавить любую комбинацию предложений для уточнения запроса. Дополнительные сведения о предложениях запросов см. в разделе «Операторы запросов LINQ [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]» далее в этом разделе. Например, следующий запрос определяет исходную коллекцию данных клиента как переменную `customers` и как итерационную переменную `cust`.  
  
 [!code-vb[VbVbalrIntroToLINQ&#2;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_3.vb)]  
  
 Данный пример составляет допустимый запрос сам по себе, однако особенно эффективным запрос становится при добавлении нескольких предложений, уточняющих его результат. Например, предложение `Where` позволяет отфильтровать результат по одному или нескольким значениям. Каждое выражение запроса — это одна строка кода, так что предложения можно просто добавлять в конец запроса. Запрос можно разбить на несколько текстовых строк, чтобы сделать его более удобочитаемым. Для этого используется символ продолжения строки (_). В приведенном ниже примере кода показан пример запроса с предложением `Where`.  
  
 [!code-vb[VbVbalrIntroToLINQ&#3;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_4.vb)]  
  
 Другое эффективное предложение запроса — это предложение `Select`, которое позволяет возвращать из источника данных только избранные поля. Запросы LINQ возвращают перечислимые коллекции строго типизированных объектов. Запрос может вернуть коллекцию как анонимных, так и именованных типов. Предложение `Select` позволяет вернуть из источника данных отдельное поле. В этом случае типом возвращаемой коллекции является тип этого поля. Кроме того, предложение `Select` позволяет вернуть из источника данных несколько полей. В этом случае типом возвращаемой коллекции становится новый анонимный тип. Возвращенные запросом поля можно сопоставить с полями указанного именованного типа. В приведенном ниже примере кода показано выражение запроса, возвращающее коллекцию анонимных типов, члены которой заполняются данными из выбранных полей источника данных.  
  
 [!code-vb[VbVbalrIntroToLINQ&#4;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_5.vb)]  
  
 Запросы LINQ могут также использоваться для объединения нескольких источников данных и получения единого результата. Это можно сделать с помощью одного или нескольких предложений `From` или с помощью предложений `Join` или `Group Join`. В приведенном ниже примере кода показано выражение запроса, объединяющее данные клиентов и заказов и возвращающее коллекцию анонимных типов, содержащих объединенные данные.  
  
 [!code-vb[VbVbalrIntroToLINQ&#5;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_6.vb)]  
  
 Для получения иерархического результата, содержащего коллекцию объектов клиента, в запросе можно использовать предложение `Group Join`. Каждый объект клиента имеет свойство, содержащее коллекцию всех заказов этого клиента. В приведенном ниже примере кода показано выражение запроса, объединяющее данные клиентов и заказов в иерархический результат и возвращающее коллекцию анонимных типов. Запрос возвращает тип, у которого есть свойство `CustomerOrders`, содержащее коллекцию данных заказов клиента. У него также есть свойство `OrderTotal`, которое содержит общую сумму всех заказов этого клиента. (Этот запрос эквивалентен LEFT OUTER JOIN).  
  
 [!code-vb[VbVbalrIntroToLINQ №&6;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_7.vb)]  
  
 Имеется несколько дополнительных операторов запросов LINQ, которые можно использовать для создания эффективных выражений запросов. В следующем разделе описываются различные предложения запросов, которые можно использовать в выражениях запросов. Дополнительные сведения о [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] предложения запроса см. в разделе [запросов](../../../../visual-basic/language-reference/queries/queries.md).  
  
##  <a name="VisualBasicLINQQueryOperators"></a>Операторы запросов LINQ в Visual Basic  
 Классы в <xref:System.Linq>пространства имен и другие пространства имен, который поддерживает запросы LINQ включают методы, которые можно вызывать для создания и уточнения запросов на основе потребностей приложения.</xref:System.Linq> [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] содержит ключевые слова для наиболее распространенных предложений запросов, описанные в приведенной ниже таблице.  
  
|Термин|Определение|  
|---|---|  
|[Предложение From](../../../../visual-basic/language-reference/queries/from-clause.md)|Запрос должен начинаться с предложения `From` или `Aggregate`. Предложение `From` определяет коллекцию источника и переменную итерации для запроса. Например:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#7;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_8.vb)]|  
|[Предложение Select](../../../../visual-basic/language-reference/queries/select-clause.md)|Необязательный. Объявляет набор переменных итераций для запроса. Например:<br /><br /> [!code-vb[VbVbalrIntroToLINQ №&8;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_9.vb)]<br /><br /> Если предложение `Select` не указано, то переменные итераций для запроса состоят из переменных итераций, указанных предложением `From` или `Aggregate`.|  
|[Предложения Where](../../../../visual-basic/language-reference/queries/where-clause.md)|Необязательный. Определяет условие фильтрации для запроса. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ №&9;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_10.vb)]|  
|[Предложение Order By](../../../../visual-basic/language-reference/queries/order-by-clause.md)|Необязательный. Определяет порядок сортировки для столбцов в запросе. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#10;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_11.vb)]|  
|[Предложение Join](../../../../visual-basic/language-reference/queries/join-clause.md)|Необязательный. Объединяет две коллекции в одну. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&11;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_12.vb)]|  
|[Предложение Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md)|Необязательный. Группирует элементы результата запроса. Может использоваться для применения агрегатных функций к каждой группе. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#12;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_13.vb)]|  
|[Предложение Group Join](../../../../visual-basic/language-reference/queries/group-join-clause.md)|Необязательный. Объединяет две коллекции в одну иерархическую коллекцию. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#13;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_14.vb)]|  
|[Предложение Aggregate](../../../../visual-basic/language-reference/queries/aggregate-clause.md)|Запрос должен начинаться с предложения `From` или `Aggregate`. Предложение `Aggregate` применяет к коллекции одну или несколько агрегатных функций. Например, предложение `Aggregate` можно использовать для вычисления суммы всех возвращенных запросом элементов.<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#14;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_15.vb)]<br /><br /> Предложение `Aggregate` можно также использовать для изменения запроса. Например, с помощью предложения `Aggregate` можно произвести вычисление с соответствующей коллекцией запросов.<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#15;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_16.vb)]|  
|[Предложение Let](../../../../visual-basic/language-reference/queries/let-clause.md)|Необязательный. Вычисляет значение и присваивает его новой переменной в запросе. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ №&16;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_17.vb)]|  
|[Предложение Distinct](../../../../visual-basic/language-reference/queries/distinct-clause.md)|Необязательный. Ограничивает значения текущей переменной итерации, чтобы исключить повторяющиеся значения в результатах запроса. Например:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&17;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_18.vb)]|  
|[Предложение Skip](../../../../visual-basic/language-reference/queries/skip-clause.md)|Необязательный. Пропускает заданное число элементов в коллекции и возвращает остальные элементы. Например:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&18;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_19.vb)]|  
|[Предложение Skip While](../../../../visual-basic/language-reference/queries/skip-while-clause.md)|Необязательный. Пропускает элементы в коллекции, если заданное условие имеет значение `true`, и возвращает остальные элементы. Например:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&19;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_20.vb)]|  
|[Предложение Take](../../../../visual-basic/language-reference/queries/take-clause.md)|Необязательный. Возвращает указанное число идущих подряд элементов с начала коллекции. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&20;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_21.vb)]|  
|[Предложение Take While](../../../../visual-basic/language-reference/queries/take-while-clause.md)|Необязательный. Включает элементы в коллекцию, если заданное условие имеет значение `true`, и пропускает остальные элементы. Пример:<br /><br /> [!code-vb[VbVbalrIntroToLINQ&#21;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_22.vb)]|  
  
 Дополнительные сведения о [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] предложения запроса см. в разделе [запросов](../../../../visual-basic/language-reference/queries/queries.md).  
  
 Обращаясь к членам перечислимых и доступных для запроса типов, предоставляемых технологией LINQ, можно использовать дополнительные возможности запросов LINQ. Для этого на результат выражения запроса необходимо вызвать определенный оператор запроса. Например, следующий код использует пример <xref:System.Linq.Enumerable.Union%2A>метод, чтобы объединить результаты двух запросов в один результирующий.</xref:System.Linq.Enumerable.Union%2A> Он использует <xref:System.Linq.Enumerable.ToList%2A>для возврата результата запроса в виде универсального списка.</xref:System.Linq.Enumerable.ToList%2A>  
  
 [!code-vb[VbVbalrIntroToLINQ&#22;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_23.vb)]  
  
 Дополнительные сведения о дополнительных возможностях LINQ см. в разделе [Общие сведения о стандартных операторах запроса](http://msdn.microsoft.com/library/24cda21e-8af8-4632-b519-c404a839b9b2).  
  
##  <a name="ConnectingToADatabase"></a>Подключение к базе данных с помощью LINQ to SQL  
 В [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] для идентификации объектов базы данных SQL Server (таблиц, представлений и хранимых процедур), к которым необходимо получить доступ, используется файл LINQ to SQL. Файл LINQ to SQL имеет расширение DBML.  
  
 При наличии допустимое подключение к базе данных SQL Server, можно добавить **классы LINQ to SQL** шаблона элемента в проект. Это позволит отобразить реляционный конструктор объектов (O/R-конструктор). Реляционный конструктор объектов позволяет перетаскивать элементы, нужен доступ в коде, из **обозревателя**/**обозревателя базы данных** на поверхность конструктора. Добавление файла LINQ to SQL <xref:System.Data.Linq.DataContext>объект в проект.</xref:System.Data.Linq.DataContext> Этот объект включает свойства и коллекции для таблиц и представлений, к которым нужно получить доступ, а также необходимые методы для хранимых процедур. После сохранения изменений в файл LINQ to SQL (.dbml), можно использовать эти объекты в коде, ссылаясь на <xref:System.Data.Linq.DataContext>объект, который определяется реляционный конструктор объектов.</xref:System.Data.Linq.DataContext> <xref:System.Data.Linq.DataContext>Объект для проекта имя на основе имени LINQ to SQL-файл.</xref:System.Data.Linq.DataContext> Например, LINQ to SQL-файл с именем Northwind.dbml создаст <xref:System.Data.Linq.DataContext>объект с именем `NorthwindDataContext`.</xref:System.Data.Linq.DataContext>  
  
 Примеры с пошаговыми инструкциями см. в разделе [как: запросов к базе данных](../../../../visual-basic/programming-guide/language-features/linq/how-to-query-a-database-by-using-linq.md) и [Практическое руководство: вызов хранимой процедуры](../../../../visual-basic/programming-guide/language-features/linq/how-to-call-a-stored-procedure-by-using-linq.md).  
  
##  <a name="VisualBasicFeaturesThatSupportLINQ"></a>Возможности Visual Basic, поддерживающие LINQ  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] включает и другие возможности, упрощающие работу с технологией LINQ и уменьшающие размер кода, необходимый для выполнения запросов LINQ. В число этих требований входят следующие:  
  
-   **Анонимные типы**, что позволяет создать новый тип на основе результата запроса.  
  
-   **Неявно типизированные переменные**, позволяющие отложить Указание типа и позволить компилятору вывести тип на основе результатов запроса.  
  
-   **Методы расширения**, которые позволяют расширить существующий тип своими собственными методами без изменения самого типа.  
  
 Дополнительные сведения см. в разделе [Visual Basic функции, поддержка LINQ](../../../../visual-basic/programming-guide/concepts/linq/features-that-support-linq.md).  
  
##  <a name="QueryExecution"></a>Отложенное и немедленное выполнение запроса  
 Процессы выполнения и создания запросов разделены. После создания запроса его выполнение инициируется отдельным механизмом. Запрос может выполняться сразу после того, как она определена (*немедленное выполнение*), или определение может быть сохранено и запрос может быть выполнен позднее (*отложенного выполнения*).  
  
 По умолчанию вновь созданный запрос автоматически не выполняется. Вместо этого определение запроса сохраняется в переменной, которая используется для ссылки на результат этого запроса. Если впоследствии код обращается к переменной результата запроса, например в рамках цикла `For…Next`, запрос выполняется. Этот процесс называется *отложенного выполнения*.  
  
 Запросы могут также выполняться при их определении, которые называют *немедленное выполнение*. Немедленное выполнение можно инициировать с помощью метода, который требует доступа к отдельным элементам результата запроса. Это может быть результатом использования агрегатных функций, таких как `Count`, `Sum`, `Average`, `Min` или `Max`. Дополнительные сведения об агрегатных функциях см. в разделе [предложения Aggregate](../../../../visual-basic/language-reference/queries/aggregate-clause.md).  
  
 Принудительно вызвать немедленное выполнение запросов позволяют также методы `ToList` и `ToArray`. Это пригодится в том случае, если требуется выполнить запрос немедленно и кэшировать результаты. Дополнительные сведения об этих методах см. в разделе [преобразование типов данных](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md).  
  
 Дополнительные сведения о выполнении запроса см. в разделе [Your первого запроса LINQ записи](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md).  
  
##  <a name="XMLInVisualBasic"></a>XML в Visual Basic  
 Возможности XML в [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] включают литералы XML и свойства оси XML, что позволяет легко создать, использовать, запрашивать и изменять XML в коде. Литералы XML позволяют записывать XML непосредственно в код. Компилятор Visual Basic обрабатывает XML как объект данных первого класса.  
  
 В приведенном ниже примере кода показано, как создать элемент XML, получить доступ к его дочерним элементам и атрибутам и сделать запросы к содержимому элемента с помощью LINQ.  
  
 [!code-vb[VbXmlSamples №&8;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/introduction-to-linq_24.vb)]  
  
 Дополнительные сведения см. в разделе [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md).  
  
##  <a name="RelatedResources"></a>Связанные ресурсы  
  
|Раздел|Описание|  
|---|---|  
|[XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)|Описание возможностей XML в [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], к которым можно делать запросы и которые позволяют включать XML в код [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] как объекты данных первого класса.|  
|[Запросы](../../../../visual-basic/language-reference/queries/queries.md)|Содержит справочные сведения о предложениях запросов, которые доступны в [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].|  
|[LINQ (Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)|Содержит общие сведения, рекомендации по программированию и примеры для LINQ.|  
|[LINQ to SQL](https://msdn.microsoft.com/library/bb386976)|Содержит общие сведения, рекомендации по программированию и примеры для LINQ to SQL.|  
|[LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9)|Содержит общие сведения, рекомендации по программированию и примеры для LINQ to Objects.|  
|[LINQ to ADO.NET (Страница портала)](http://msdn.microsoft.com/library/dd7d3c6a-ff98-47e9-a1a7-2d4cfc42d150)|Содержит общие сведения, рекомендации по программированию и примеры для LINQ to [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)].|  
|[LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)|Содержит общие сведения, рекомендации по программированию и примеры для LINQ to XML.|  
  
##  <a name="HowToAndWalkthroughTopics"></a>Как и пошаговые руководства  
 [Практическое руководство: запросов к базе данных](how-to-query-a-database-by-using-linq.md)  
  
 [Практическое руководство: вызов хранимой процедуры](how-to-call-a-stored-procedure-by-using-linq.md)  
  
 [Практическое руководство: изменение данных в базе данных](how-to-modify-data-in-a-database-by-using-linq.md)  
  
 [Практическое руководство: объединение данных с помощью соединений](how-to-combine-data-with-linq-by-using-joins.md)  
  
 [Практическое руководство: сортировка результатов запроса](how-to-sort-query-results-by-using-linq.md)  
  
 [Практическое руководство: фильтрацию результатов запроса](how-to-filter-query-results-by-using-linq.md)  
  
 [Практическое руководство: число, суммы или среднего значения данных](how-to-count-sum-or-average-data-by-using-linq.md)  
  
 [Практическое руководство: поиск минимального или максимального значения в результатах запроса](how-to-find-the-minimum-or-maximum-value-in-a-query-result.md)  
  
 [Практическое руководство: назначение хранимых процедур для выполнения обновлений, вставок и удалений (реляционный конструктор)](http://msdn.microsoft.com/library/e88224ab-ff61-4a3a-b6b8-6f3694546cac)  
  
## <a name="featured-book-chapters"></a>Главы в популярных книгах  
 [Глава 17: LINQ](http://go.microsoft.com/fwlink/?LinkId=195277) в [программирования Visual Basic 2008](http://go.microsoft.com/fwlink/?LinkId=195383)  
  
## <a name="see-also"></a>См. также  
 [LINQ (Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [Общие сведения о LINQ to XML в Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)   
 [Обзор набора данных LINQ](http://msdn.microsoft.com/library/dc20a8fb-03f6-4b68-9c2b-7f7299e3070b)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)  
 [Средства LINQ to SQL в Visual Studio](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)   
 [Методы DataContext (реляционный конструктор)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)
