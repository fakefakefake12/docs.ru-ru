---
title: "Метаданные свойства зависимости | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "API - интерфейсы, метаданные"
  - "свойства зависимостей, метаданные"
  - "метаданные, для свойств зависимостей"
  - "переопределение метаданных"
ms.assetid: d01ed009-b722-41bf-b82f-fe1a8cdc50dd
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Метаданные свойства зависимости
Система свойств [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] включает систему отчетности метаданных, содержимое которой выходит за рамки того, что можно получить из отражения или общих характеристик [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  Метаданные [свойства зависимости](GTMT) также могут быть присвоены уникальным образом с помощью класса, в котором определено [свойство зависимости](GTMT), могут быть изменены, если [свойство зависимости](GTMT) добавляется в другой класс, и могут быть переопределены специальным образом любым производным классом, наследующим [свойство зависимости](GTMT) от определяющего базового класса.  
  
   
  
<a name="prerequisites"></a>   
## Предварительные требования  
 В этом разделе предполагается знакомство с принципом работы свойств зависимостей с точки зрения потребителя существующих свойств зависимостей классов [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]; кроме того, следует прочесть раздел [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Чтобы выполнить примеры в этом подразделе, следует также понимать принципы работы [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] и знать, как создаются приложения [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="dp_metadata_contents"></a>   
## Принципы использования метаданных свойств зависимости  
 Метаданные свойств зависимости существуют в виде объекта, к которому можно обращаться для проверки характеристик свойства зависимости.  Также доступ к этим метаданным часто осуществляется с помощью системы свойств, которая обрабатывает любое заданное свойство зависимости.  Объект метаданных свойства зависимости может содержать следующие типы данных:  
  
-   Значение свойства зависимостей по умолчанию, если никакое другое значение не может быть определено для свойства зависимостей через локальное значение, стиль, наследование и т. д.  Подробное описание того, как значения по умолчанию применяются системой свойств при присвоении значений свойствам зависимостей, см. в разделе [Приоритет значения свойств зависимостей](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
-   ссылки для реализации обратного вызова, влияющего на приведение типа данных или поведение при изменении уведомления на основе собственного типа данных.  Обратите внимание, что такие обратные вызовы часто определяются с уровнем неоткрытого доступа, поэтому получение фактических ссылок из метаданных обычно невозможно, если ссылки не находятся в области разрешенного доступа.  Дополнительные сведения об обратных вызовах свойства зависимости содержатся в разделе [Проверка и обратные вызовы свойства зависимостей](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md);  
  
-   если свойство зависимости считается свойством [уровня инфраструктуры WPF](GTMT), метаданные могут содержать характеристики свойства зависимости [уровня инфраструктуры WPF](GTMT), которые содержат информацию и состояние для таких служб, как логика обработчика разметки [уровня инфраструктуры WPF](GTMT) и свойств наследования.  Дополнительные сведения об этом аспекте метаданных свойства зависимости см. в разделе [Метаданные свойств среды](../../../../docs/framework/wpf/advanced/framework-property-metadata.md).  
  
<a name="APIs"></a>   
## API\-интерфейсы метаданных  
 Типом, который сообщает большую часть сведений о метаданных, используемых системой свойств, является класс <xref:System.Windows.PropertyMetadata>.  Экземпляры метаданных указываются при необходимости, когда свойства зависимости регистрируются с помощью системы свойств, и могут быть определены снова для дополнительных типов, которые либо добавляют себя в качестве владельцев, либо переопределяют метаданные, которые они наследуют от определения свойства зависимости базового класса.  \(Для случаев, когда при регистрации свойства не указаны метаданные, создается класс <xref:System.Windows.PropertyMetadata> по умолчанию со стандартными для этого класса значениями.\) Зарегистрированные метаданные возвращаются в виде <xref:System.Windows.PropertyMetadata> при вызове перегруженных методов <xref:System.Windows.DependencyProperty.GetMetadata%2A>, которые получают метаданные из свойства зависимости экземпляра класса <xref:System.Windows.DependencyObject>.  
  
 Затем вызывается производный класс <xref:System.Windows.PropertyMetadata>, который предоставляет дополнительные метаданные для архитектурных делений, например на классы [уровня платформы WPF](GTMT).  <xref:System.Windows.UIPropertyMetadata> добавляет отчетность анимации, а <xref:System.Windows.FrameworkPropertyMetadata> предоставляет свойства [уровня платформы WPF](GTMT), упомянутые в предыдущем разделе.  При регистрации свойства зависимости могут быть зарегистрированы с производными классами <xref:System.Windows.PropertyMetadata>.  При проверке метаданных базовый тип <xref:System.Windows.PropertyMetadata> может быть потенциально приведен к производным классам, что дает возможность получить доступ к дополнительным свойствам.  
  
> [!NOTE]
>  В данной документации иногда приводятся ссылки на характеристики свойства, которые могут быть определены в классе <xref:System.Windows.FrameworkPropertyMetadata> \(«флаги»\).  При создании новых экземпляров метаданных для использования при регистрации свойства зависимости или переопределении метаданных можно задать эти значения с помощью флагового перечисления <xref:System.Windows.FrameworkPropertyMetadataOptions>, а затем указать возможные сцепления значений перечисления в конструкторе <xref:System.Windows.FrameworkPropertyMetadata>.  Однако после создания эти характеристики параметра представляются в классе <xref:System.Windows.FrameworkPropertyMetadata> как ряд логических свойств, а не как созданные значения перечисления.  Логические свойства позволяют проверить каждое условие без необходимости применять маску для значения флагового перечисления, чтобы получить требуемую информацию.  Чтобы сохранить длину сигнатуры конструктора приемлемой, конструктор использует объединенные параметры <xref:System.Windows.FrameworkPropertyMetadataOptions>, тогда как фактически построенные метаданные предоставляют дискретные свойства, чтобы сделать запрос метаданных более наглядным.  
  
<a name="override_or_subclass"></a>   
## Выбор между переопределением метаданных и созданием производного класса  
 Система свойств [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] имеет установленные возможности для изменения некоторых характеристик свойств зависимости, не требуя их полного пересоздания.  Это достигается путем создания другого экземпляра метаданных свойства для свойства зависимости, так как оно существует в качестве определенного типа.  Следует отметить, что большинство существующих свойств зависимостей не являются виртуальными свойствами, поэтому, строго говоря, их повторная реализация в наследуемых классах может быть произведена только путем переобъявления существующего члена.  
  
 Если требуемый скрипт для свойства зависимости в типе не может быть выполнен путем изменения характеристик существующих свойств зависимости, возможно, потребуется создать производный класс и затем объявить настраиваемое свойство зависимости для производного класса.  Поведение настраиваемого свойства зависимости аналогично свойствам зависимости, определенным в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)].  Дополнительные сведения о настраиваемых свойствах зависимости см. в разделе [Пользовательские свойства зависимостей](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
 Единственной важной характеристикой свойства зависимости, которая не может быть переопределена, является тип значения.  Если наследуемое свойство зависимости ведет себя приблизительно так, как ожидается, но необходим другой его тип, потребуется реализовать настраиваемое свойство зависимости и, возможно, связать свойства с помощью преобразования типов или других реализаций данного настраиваемого класса.  Кроме того, невозможно заменить существующий обратный вызов <xref:System.Windows.ValidateValueCallback>, так как он находится в поле регистрации и не входит в метаданные.  
  
<a name="scenarios"></a>   
## Сценарии для изменения существующих метаданных  
 При работе с метаданными существующего свойства зависимости одним из распространенных скриптов для изменения метаданных свойства зависимости является изменение значения по умолчанию.  Изменение или добавление обратных вызовов системы свойств является более сложным способом.  Это может потребоваться, если данная реализация производного класса имеет различные взаимосвязи между свойствами зависимости.  Одним из условий модели программирования, поддерживающей как код, так и декларативное использование, является то, что свойства должны устанавливаться в любом порядке.  Таким образом, значения всех зависимых свойств необходимо установить своевременно без контекста; нельзя полагаться на знание порядка присвоения значений, который может быть доступен в конструкторе.  Дополнительные сведения об этом аспекте системы свойств содержатся в разделе [Проверка и обратные вызовы свойства зависимостей](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  Следует отметить, что обратные вызовы проверки данных не являются частью метаданных; они являются частью идентификатора свойства зависимости.  Таким образом, обратные вызовы проверки не могут быть изменены путем переопределения метаданных.  
  
 В некоторых случаях может также потребоваться изменение параметров метаданных свойства [уровня инфраструктуры WPF](GTMT) в существующих свойствах зависимости.  Эти параметры связывают некоторые известные условия свойств [уровня инфраструктуры WPF](GTMT) и другие процессы [уровня инфраструктуры WPF](GTMT), такие как система разметки.  Настройка параметров обычно выполняется только при регистрации нового свойства зависимости, но изменить метаданные свойства [уровня инфраструктуры WPF](GTMT) можно путем вызова методов <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> или <xref:System.Windows.DependencyProperty.AddOwner%2A>.  Конкретные значения для использования и дополнительные сведения содержатся в разделе [Метаданные свойств среды](../../../../docs/framework/wpf/advanced/framework-property-metadata.md).  Дополнительные сведения о том, как должны быть заданы эти параметры для вновь зарегистрированных свойств зависимости, см. в разделе [Пользовательские свойства зависимостей](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
<a name="dp_override_metadata"></a>   
### Переопределение метаданных  
 Основной целью переопределения метаданных является то, что у разработчика появляется возможность изменить некоторые характеристики производных метаданных, которые применяются к свойству зависимости, как оно существует в данном типе.  Причины этого более подробно описаны в разделе [Метаданные](#dp_metadata_contents).  Дополнительные сведения, включая примеры кода, содержатся в разделе [Переопределение метаданных для свойств зависимостей](../../../../docs/framework/wpf/advanced/how-to-override-metadata-for-a-dependency-property.md).  
  
 Метаданные свойства могут быть предоставлены свойству зависимости во время регистрационного вызова \(<xref:System.Windows.DependencyProperty.Register%2A>\).  Однако в большинстве случаев может потребоваться предоставление метаданных определенного типа для класса, когда он наследует свойство зависимости.  Это можно сделать, вызвав метод <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>.  Рассмотрим пример из [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Класс <xref:System.Windows.FrameworkElement> является типом, который первоначально регистрирует свойство зависимостей <xref:System.Windows.UIElement.Focusable%2A>.  Но класс <xref:System.Windows.Controls.Control> переопределяет метаданные свойства зависимостей, чтобы обеспечить его собственным исходным значением по умолчанию, изменяя его с `false` на `true`, в противном случае повторно использует исходную реализацию <xref:System.Windows.UIElement.Focusable%2A>.  
  
 При переопределении метаданных различные характеристики метаданных либо объединяются, либо замещаются.  
  
-   Объект <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> объединяется.  Если добавить новый обратный вызов <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>, он сохранится в метаданных.  Если в переопределении не указан обратный вызов <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>, значение <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> переходит в качестве ссылки из ближайшего родительского объекта, указанного в метаданных.  
  
-   Фактическое поведение системы свойств <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> заключается в том, что реализации для всех владельцев метаданных в иерархии сохраняются и добавляются в таблицу в порядке выполнения системой свойств \(сначала вызывается большинство обратных вызовов производного класса\).  
  
-   Объект <xref:System.Windows.PropertyMetadata.DefaultValue%2A> заменяется.  Если в переопределении не указан обратный вызов <xref:System.Windows.PropertyMetadata.DefaultValue%2A>, значение <xref:System.Windows.PropertyMetadata.DefaultValue%2A> переходит из ближайшего родительского объекта, указанного в метаданных.  
  
-   Реализации <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> заменяются.  Если добавить новый обратный вызов <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>, он сохранится в метаданных.  Если в переопределении не указан обратный вызов <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>, значение <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> переходит в качестве ссылки из ближайшего родительского объекта, указанного в метаданных.  
  
-   Поведение системы свойств состоит в том, что только <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> вызывается непосредственно из метаданных.  Ссылки на другие реализации <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> в иерархии не сохраняются.  
  
 Такое поведение реализовано в классе <xref:System.Windows.PropertyMetadata.Merge%2A> и может быть переопределено в производных классах метаданных.  
  
#### Переопределение вложенного свойства метаданных  
 В [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [вложенные свойства](GTMT) реализуются как свойства зависимости.  Это означает, что они также имеют метаданные свойства, которые отдельные классы могут переопределить.  Проблемы видимости для вложенного свойства в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] сводятся к тому, что любой объект <xref:System.Windows.DependencyObject> может иметь свой набор присоединенных свойств.  Таким образом, любой производный класс <xref:System.Windows.DependencyObject> может переопределить метаданные любого вложенного свойства так же, как они могут быть заданы в экземпляре класса.  Переопределению подлежат значения по умолчанию, обратные вызовы или свойства сведений о характеристиках [уровня инфраструктуры WPF](GTMT).  Если вложенное свойство установлено для экземпляра класса, применяются такие переопределенные характеристики метаданных свойства.  Например, можно переопределить значение по умолчанию таким образом, что всякий раз переопределенное значение будет отображаться как значение вложенного свойства экземпляра класса, если свойство не задано иным образом.  
  
> [!NOTE]
>  Свойство <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> не относится к вложенным свойствам.  
  
<a name="dp_add_owner"></a>   
### Добавление класса в качестве владельца существующего свойства зависимости  
 Используя метод <xref:System.Windows.DependencyProperty.AddOwner%2A>, класс может сделать себя владельцем уже зарегистрированного свойства зависимости.  Это позволяет классу использовать свойство зависимости, первоначально зарегистрированное для другого типа.  Добавленный класс обычно не является производным классом того типа, который первоначально зарегистрировал свойство зависимости в качестве владельца.  Фактически, это позволяет классу и его производным классам «наследовать» реализацию [свойства зависимости](GTMT), не используя исходный класс\-владелец и добавленный класс из той же действительной иерархии классов.  Кроме того, добавляющий класс \(а также все производные классы\) может предоставлять метаданные, определяемые типом, для исходного свойства зависимости.  
  
 Также как и добавление себя в качестве владельца с помощью вспомогательных методов системы свойств, добавляющий класс должен объявить дополнительные открытые члены, чтобы сделать [свойство зависимости](GTMT) полноценным участником системы свойств с возможностью доступа к коду и разметке.  Класс, который добавляет существующее свойство зависимости, обладает теми же возможностями при предоставлении доступа к объектной модели для этого свойства зависимости, что и класс, который определяет новое пользовательское свойство зависимости.  Поле идентификатора свойства зависимости является первым таким членом.  Это поле должно быть полем `public static readonly` типа <xref:System.Windows.DependencyProperty>, которому присваивается возвращаемое значение вызова <xref:System.Windows.DependencyProperty.AddOwner%2A>.  Вторым элементом определения является свойство «оболочки» [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  Оболочка делает управление свойством зависимости в коде гораздо более удобным \(можно избежать неоднократных вызовов <xref:System.Windows.DependencyObject.SetValue%2A>: этот вызов совершается в оболочке только один раз\).  Программа\-оболочка реализуется так же, как и при регистрации пользовательского [свойства зависимостей](GTMT).  Дополнительные сведения о реализации [свойства зависимостей](GTMT) см. в разделах [Пользовательские свойства зависимостей](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) и [Добавление типа владельца для свойства зависимостей](../../../../docs/framework/wpf/advanced/how-to-add-an-owner-type-for-a-dependency-property.md).  
  
#### Метод AddOwner и вложенные свойства  
 Можно вызвать метод <xref:System.Windows.DependencyProperty.AddOwner%2A> для свойства зависимости, которое определено классом\-владельцем как вложенное свойство.  Обычно, основанием для этого является представление ранее вложенного свойства в качестве неприсоединенного свойства зависимости.  Затем будет получено возвращаемое значение метода <xref:System.Windows.DependencyProperty.AddOwner%2A> в виде поля `public static readonly` для использования в качестве идентификатора свойства зависимости и будут определены соответствующие свойства «оболочки» так, что свойство появится в таблице элементов и будет поддерживать использование невложенного свойства в классе.  
  
## См. также  
 <xref:System.Windows.PropertyMetadata>   
 <xref:System.Windows.DependencyObject>   
 <xref:System.Windows.DependencyProperty>   
 <xref:System.Windows.DependencyProperty.GetMetadata%2A>   
 [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Метаданные свойств среды](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)