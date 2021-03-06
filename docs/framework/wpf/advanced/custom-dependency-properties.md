---
title: "Пользовательские свойства зависимостей | Microsoft Docs"
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
  - "пользовательские свойства зависимостей"
  - "свойства зависимостей, пользовательский"
  - "реализация, оболочки"
  - "метаданные, для свойств"
  - "свойства, метаданные"
  - "свойства, регистрация"
  - "регистрация свойств"
  - "оболочки, реализация"
ms.assetid: e6bfcfac-b10d-4f58-9f77-a864c2a2938f
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Пользовательские свойства зависимостей
В этом разделе описываются причины, по которым разработчики приложения [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] и авторы компонента могут создавать пользовательские [свойства зависимостей](GTMT), а также этапы и параметры реализации, которые могут повысить производительность, удобство использования и универсальность свойства.  
  
   
  
<a name="prerequisites"></a>   
## Предварительные требования  
 В этом разделе предполагается, что вы понимаете свойства зависимостей с точки зрения потребителя существующих свойств зависимостей классов [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] и ознакомлены с разделом [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Чтобы выполнить примеры в этом подразделе, следует также понимать принципы работы [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] и знать, как создаются приложения [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="whatis"></a>   
## Что такое свойство зависимостей?  
 То, что в противном случае будет свойством [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] можно настроить для поддержки стилизации, привязки данных, наследования, анимаций и значений по умолчанию, посредством реализации в качестве [свойства зависимостей](GTMT).  Свойства зависимостей являются свойствами, которые зарегистрированы системой свойств [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] посредством вызова метода <xref:System.Windows.DependencyProperty.Register%2A> \(или <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A>\) и зарезервированы полем идентификатора <xref:System.Windows.DependencyProperty>.  Свойства зависимостей могут использоваться только типами <xref:System.Windows.DependencyObject>, но <xref:System.Windows.DependencyObject> расположен довольно высоко в иерархии классов [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], поэтому большинство классов, доступных в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], могут поддерживать свойства зависимостей.  Дополнительные сведения о свойствах зависимостей и некоторых терминах и соглашениях, используемых для их описания в этом [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)], см. в разделе [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
<a name="example_dp"></a>   
## Примеры свойств зависимостей  
 Примерами свойств зависимостей, реализуемых в классах [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], являются, например, свойство <xref:System.Windows.Controls.Control.Background%2A>, свойство <xref:System.Windows.FrameworkElement.Width%2A>, и свойство <xref:System.Windows.Controls.TextBox.Text%2A>.  Каждое свойство зависимостей, предоставляемое классом, содержит соответствующее открытое статическое поле типа <xref:System.Windows.DependencyProperty>, предоставляемое для этого же класса. Это поле является идентификатором свойства зависимостей.  Идентификатор именуется в соответствии со следующим соглашением: к имени [свойства зависимостей](GTMT) добавляется строка `Property`.  Например, соответствующим полем идентификатора <xref:System.Windows.DependencyProperty> для свойства <xref:System.Windows.Controls.Control.Background%2A> является <xref:System.Windows.Controls.Control.BackgroundProperty>.  После регистрации идентификатор хранит информацию о [свойстве зависимостей](GTMT), а затем используется для других операций, включающих [свойство зависимостей](GTMT), например при вызове <xref:System.Windows.DependencyObject.SetValue%2A>.  
  
 Как отмечалось в разделе [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md), все свойства зависимостей в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(за исключением большинства [вложенных свойств](GTMT)\) также являются свойствами [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] из\-за реализации программы\-оболочки.  Следовательно из кода можно получить или установить свойства зависимости путем вызова методов доступа [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], определяющих программы\-оболочки таким же образом, что и использование других свойств [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Как потребители установленных свойств зависимостей, разработчики обычно не используют методы <xref:System.Windows.DependencyObject.GetValue%2A> и <xref:System.Windows.DependencyObject.SetValue%2A> объекта <xref:System.Windows.DependencyObject>, являющиеся точкой подключения для основной системы свойств.  Существующая реализация свойств [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] уже вызывает <xref:System.Windows.DependencyObject.GetValue%2A> и <xref:System.Windows.DependencyObject.SetValue%2A> в реализациях программы\-оболочки `get` и `set` свойства, надлежащим образом используя поле идентификатора.  Если разработчик самостоятельно реализует пользовательское свойство зависимости, программа\-оболочка будет определяться аналогичным образом.  
  
<a name="backing_with_dp"></a>   
## Когда следует реализовывать свойство зависимостей?  
 При реализации свойства в классе \(если класс является производным от <xref:System.Windows.DependencyObject>\) разработчик может зарезервировать свое свойство с идентификатором <xref:System.Windows.DependencyProperty>, таким образом сделав это свойство свойством зависимости.  Свойство не всегда удобно делать свойством зависимости, это будет зависеть от потребностей скрипта.  Иногда подходят обычные способы резервирования свойства с закрытым полем.  Однако свойство всегда следует реализовывать как [свойство зависимостей](GTMT) в том случае, когда свойство должно поддерживать одну или несколько следующих возможностей [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Свойство должно устанавливаться в стиле.  Дополнительные сведения см. в разделе [Стилизация и использование шаблонов](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
-   Свойство должно поддерживать привязку данных.  Дополнительные сведения о привязке данных свойств зависимостей содержатся в разделе [Привязка свойств двух элементов управления](../../../../docs/framework/wpf/data/how-to-bind-the-properties-of-two-controls.md).  
  
-   Свойство должно устанавливаться ссылкой на динамический ресурс.  Дополнительные сведения см. в разделе [Ресурсы XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
-   Необходимо автоматическое наследование значения свойства из родительского элемента в дереве элементов.  В этом случае следует зарегистрировать с помощью метода <xref:System.Windows.DependencyProperty.RegisterAttached%2A>, даже при создании программы\-оболочки свойства для доступа к [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Дополнительные сведения см. в разделе [Наследование значения свойства](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
-   Свойство должно быть анимируемым.  Дополнительные сведения см. в разделе [Общие сведения об эффектах анимации](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
-   Система свойств должна уведомлять разработчика, когда предыдущее значение свойства изменяется в результате действий, производимых системой свойств, средой или пользователем, а также в результате чтения и использования стилей.  Используя метаданные свойства, свойство сможет задать метод обратного вызова, который будет вызываться каждый раз, когда система свойств определит, что значение свойства было окончательно изменено.  Связанным понятием является приведение значения свойства.  Дополнительные сведения см. в разделе [Проверка и обратные вызовы свойства зависимостей](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  
  
-   Необходимо использование установленных соглашений о метаданных, которые также используются процессами [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], например, уведомлением о том, должно ли изменение значения свойства удовлетворять системе макета, чтобы представлять визуализации элемента.  Также в том случае, если необходима возможность использования переопределений метаданных таким образом, чтобы производные классы могли изменять основанные на метаданных характеристики, такие как значение по умолчанию.  
  
-   Свойства пользовательского элемента управления должны получать поддержку [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)], например редактирование окна **Свойства**.  Дополнительные сведения см. в разделе [Общие сведения о разработке управления](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 При рассмотрении этих скриптов также следует учитывать, можно ли выполнить скрипт, переопределяя метаданные существующего [свойства зависимостей](GTMT), вместо реализации совершенно нового свойства.  Практичность переопределения метаданных зависит от скрипта и от того, насколько точно он совпадает с реализацией существующих свойств зависимостей и классов [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Дополнительные сведения о переопределении метаданных в существующих свойствах см. в разделе [Метаданные свойства зависимости](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="checklist"></a>   
## Контрольный список для определения свойства зависимостей  
 Определение свойства зависимости состоит из четырех различных понятий.  Эти понятия не обязательно являются строгими процедурными этапами, так как некоторые из объединяются в одну строку кода в реализации:  
  
-   \(Необязательно\) Создание метаданных свойства для свойства зависимости.  
  
-   Регистрация имени свойства с помощью системы свойства, путем задания типа владельца и типа значения свойства.  Также необходимо задать метаданные свойства \(при их использовании\).  
  
-   Определение идентификатора <xref:System.Windows.DependencyProperty> как поле `public` `static` `readonly` в типе владельца.  
  
-   Определите свойство программы\-оболочки [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], имя которого соответствует имени свойства зависимостей.  Реализуйте методы доступа `get` и `set` свойства программы\-оболочки [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] для соединения со свойством зависимостей, которое резервирует его.  
  
<a name="registering"></a>   
### Регистрация свойства с помощью системы свойств  
 Чтобы свойство было [свойством зависимостей](GTMT), необходимо зарегистрировать это свойство в таблице, поддерживаемой системой свойств, и предоставить ему уникальный идентификатор, используемый в качестве квалификатора для последующих операций системы свойств.  Эти операции могут быть внутренними операциями или системой свойств [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)], обращающейся к собственному коду.  Чтобы зарегистрировать свойство, нужно вызвать метод <xref:System.Windows.DependencyProperty.Register%2A> в теле класса \(внутри класса, но вне определений любого из членов\).  Вызов метода <xref:System.Windows.DependencyProperty.Register%2A> также предоставляет поле идентификатора в качестве возвращаемого значения.  Причина того, что вызов <xref:System.Windows.DependencyProperty.Register%2A> выполняется вне определений других членов, заключается в том, что это возвращаемое значение используется для назначения и создания поля `public` `static` `readonly` типа <xref:System.Windows.DependencyProperty> как части класса.  Это поле становится идентификатором для данного свойства зависимостей.  
  
 [!code-csharp[WPFAquariumSln#RegisterAG](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerag)]
 [!code-vb[WPFAquariumSln#RegisterAG](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerag)]  
  
<a name="nameconventions"></a>   
### Соглашения об имени свойств зависимостей  
 Существуют установленные соглашения об именах, касающиеся свойств зависимостей. Эти соглашения необходимо соблюдать во всех случаях за редким исключением.  
  
 Само свойство зависимости будет иметь базовое имя — в следующем примере "AquariumGraphic". Это имя предоставляется в качестве первого параметра <xref:System.Windows.DependencyProperty.Register%2A>.  Это имя должно быть уникальным внутри каждого регистрирующего типа.  Считается, что свойства зависимости, наследуемые через базовые типы, уже являются частью регистрирующего типа; имена наследуемых свойств не могут быть зарегистрированы повторно.  Однако, существует метод для добавления класса как владельца свойства зависимостей, даже если свойство зависимостей не наследуется. Подробные сведения содержатся в разделе [Метаданные свойства зависимости](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
 При создании поля идентификатора назовите это поле по имени зарегистрированного свойства, прибавив суффикс `Property`.  Это поле является идентификатором для свойства зависимостей, и позднее будет использовано как ввод для вызовов методов <xref:System.Windows.DependencyObject.SetValue%2A> и <xref:System.Windows.DependencyObject.GetValue%2A>, которые будут осуществляться в программах\-оболочках, посредством любого другого доступа к коду в свойстве через собственный код, посредством любого внешнего разрешенного доступа к коду, посредством системы свойств или потенциально с помощью процессоров [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
> [!NOTE]
>  Определение свойства зависимости в теле класса является обычной реализацией, но также возможно определить свойство зависимости в статическом конструкторе класса.  Этот подход может пригодиться в том случае, если для инициализации свойства зависимостей понадобится несколько строк кода.  
  
<a name="wrapper1"></a>   
### Реализация "программы\-оболочки"  
 Реализация программы\-оболочки должна вызывать <xref:System.Windows.DependencyObject.GetValue%2A> в реализации `get`, и <xref:System.Windows.DependencyObject.SetValue%2A> в реализации `set` \(исходный вызов регистрации и поле также показаны здесь для ясности\).  
  
 Во всех случаях, за редким исключением, реализации программы\-оболочки должны выполнять только действия <xref:System.Windows.DependencyObject.GetValue%2A> и <xref:System.Windows.DependencyObject.SetValue%2A>, соответственно.  Причина этого обсуждается в разделе [Загрузка кода XAML и свойства зависимостей](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md).  
  
 Все существующие открытые свойства зависимости, предоставляемые на классах [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], используют эту простую модель реализации программы\-оболочки. Основная трудность того, как работают свойства зависимости, заключается либо в поведении системы свойств, либо в реализации других основных понятий, таких как приведение типа данных или обратный вызов свойства через метаданные свойства.  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
 Согласно правилам, имя упаковщика свойства должно совпадать с именем, выбранным и заданным как первый параметр вызова <xref:System.Windows.DependencyProperty.Register%2A>, регистрирующего свойство.  Если свойство не следует правилу, это не обязательно отключает все возможные применения, но приведет к следующим существенным проблемам:  
  
-   Не будут работать определенные аспекты стилей и шаблонов.  
  
-   Большинство инструментов и конструкторов должны полагаться на соглашения об именах для правильной сериализации [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] или для предоставления помощи среды конструктора на уровне каждого свойства.  
  
-   Текущая реализация загрузчика [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] полностью обходит программы\-оболочки и основывается на соглашении об именах при обработке значений атрибута.  Дополнительные сведения см. в разделе [Загрузка кода XAML и свойства зависимостей](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md).  
  
<a name="metadata"></a>   
### Метаданные свойства для нового свойства зависимости  
 При регистрации свойства зависимости регистрация с помощью системы свойств создает объект метаданных, который хранит характеристики свойства.  Большинство этих характеристик имеют значения по умолчанию, которые установлены, если свойство зарегистрированно с простыми сигнатурами <xref:System.Windows.DependencyProperty.Register%2A>.  Другие подписи <xref:System.Windows.DependencyProperty.Register%2A> позволяют указывать метаданные, требуемые при регистрации свойства.  Наиболее общие метаданные, заданные для свойств зависимости, можно получить, задав им значение по умолчанию, применяемое на новых экземплярах, которые использует свойство.  
  
 Если создается свойство зависимостей, размещающееся на производном классе <xref:System.Windows.FrameworkElement>, то можно использовать более специализированный класс метаданных <xref:System.Windows.FrameworkPropertyMetadata> вместо базового класса <xref:System.Windows.PropertyMetadata>.  Конструктор для класса <xref:System.Windows.FrameworkPropertyMetadata> имеет несколько сигнатур, где можно указать различные сочетания характеристик метаданных.  Если требуется указать только значение по умолчанию, следует использовать подпись, принимающую один параметр типа <xref:System.Object>.  Передайте этот параметр объекта в качестве типоспецифического значения по умолчанию для свойства \(предоставленное значение по умолчанию должно быть типом, предоставленным как параметр `propertyType` в вызове <xref:System.Windows.DependencyProperty.Register%2A>\).  
  
 Для <xref:System.Windows.FrameworkPropertyMetadata> можно также указать флаги параметра метаданных для свойства.  После регистрации эти флаги преобразуются в дискретные свойства в метаданных свойства и используются для связи определенных условных операторов с другими процессами, такими как обработчик макета.  
  
#### Задание соответствующих флагов метаданных  
  
-   Если свойство \(или изменения в его значении\) влияет на [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] и, в частности, влияет на то, как система макета будет изменять размер или визуализировать элемент на странице, задайте один или несколько следующих флагов: <xref:System.Windows.FrameworkPropertyMetadataOptions>, <xref:System.Windows.FrameworkPropertyMetadataOptions> и <xref:System.Windows.FrameworkPropertyMetadataOptions>.  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> показывает, что изменение этого свойства требует изменения для отрисовки [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], где содержащийся объект может потребовать большего или меньшего пространства внутри родителя.  Например, этот флаг должен быть установлен у свойства Width.  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> показывает, что изменение этого свойства требует изменения отрисовки [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], обычно не требующей изменения в назначенном пространстве, но не указывает на изменение положения в пространстве.  Например, этот флаг должен быть установлен у свойства Alignment.  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> показывает, что произошли некоторые другие изменения, которые не повлияют на макет и масштаб, но требуют повторной визуализации.  Примером будет свойство, изменяющее цвет существующего элемента, такое как Background.  
  
    -   Эти флаги часто используются в метаданных в качестве протокола для собственных реализаций переопределения системы свойств или обратных вызовов макета.  Например, можно иметь обратный вызов <xref:System.Windows.DependencyObject.OnPropertyChanged%2A>, который будет вызывать <xref:System.Windows.UIElement.InvalidateArrange%2A>, если любое свойство экземпляра уведомляет об изменении значения и имеет <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> в качестве `true` в своих метаданных.  
  
-   Некоторые свойства могут влиять на характеристики отрисовки включенного родительского элемента \(т.е. уменьшать или увеличивать требуемый размер\) различными способами, упомянутыми ранее.  Примером этого является свойство <xref:System.Windows.Documents.Paragraph.MinOrphanLines%2A>, используемое в модели потокового документа, где изменения этого свойства могут изменять общую отрисовку документа нефиксированного формата, содержащего абзац.  Используйте <xref:System.Windows.FrameworkPropertyMetadataOptions> или <xref:System.Windows.FrameworkPropertyMetadataOptions> для определения похожих случаев в своих свойствах.  
  
-   По умолчанию свойства зависимостей поддерживают привязку данных.  Можно специально отключить привязку данных для случаев, когда реалистичного скрипта для привязки данных не существует или когда быстродействие в привязке данных для больших объектов становится проблемой.  
  
-   Привязка данных <xref:System.Windows.Data.Binding.Mode%2A> для свойств зависимости по умолчанию устанавливается равной <xref:System.Windows.Data.BindingMode>.  Всегда можно изменить привязку так, что она будет равна <xref:System.Windows.Data.BindingMode> для каждого экземпляра привязки. Дополнительные сведения см. в разделе [Указание направления привязки](../../../../docs/framework/wpf/data/how-to-specify-the-direction-of-the-binding.md).  Как автор свойства зависимости, вы можете выбирать вариант, когда свойство использует по умолчанию режим привязки <xref:System.Windows.Data.BindingMode>.  Примером существующего свойства зависимостей является <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A?displayProperty=fullName>; скрипт для этого свойства заключается в том, что логика установки <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> и компоновка из <xref:System.Windows.Controls.MenuItem> взаимодействуют со стилями темы по умолчанию.  Логика свойства <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> изначально использует привязку данных для поддержания состояния свойства в соответствии с другими свойствами состояния и вызовами методов.  Другим примером свойства, которое по умолчанию связывает <xref:System.Windows.Data.BindingMode>, является <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName>.  
  
-   Можно также включить наследование свойства в пользовательском свойстве зависимости, установив флаг <xref:System.Windows.FrameworkPropertyMetadataOptions>.  Наследование свойства полезно для скрипта, в котором родительские и дочерние элементы одновременно имеют одно свойство, что может помешать дочерним элементам установить то же значение данного свойства, что и значение родительского элемента.  Примером наследуемого свойства является <xref:System.Windows.FrameworkElement.DataContext%2A>, которое используется для привязки операций, чтобы включить важный скрипт "основной\/подробности" для представления данных.  Если сделано <xref:System.Windows.FrameworkElement.DataContext%2A> наследуемым, то любые дочерние элементы также наследуют контекст данных.  По причине наследования значения свойства можно указать контекст данных на странице или в корне приложения, что освобождает от необходимости повторного указания наследования для привязки во всех возможных дочерних элементах.  Свойство <xref:System.Windows.FrameworkElement.DataContext%2A> также представляет собой хороший пример для демонстрации того, что наследование переопределяет значение по умолчанию, но может всегда быть локально установлено для любого конкретного дочернего элемента. Дополнительные сведения см. в разделе [Использование шаблона "главный\-подчиненный" с иерархическими данными](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md).  Наследование значения свойства снижает быстродействие, а, следовательно, должно использоваться минимально. Дополнительные сведения см. в разделе [Наследование значения свойства](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
-   Установленный флаг <xref:System.Windows.FrameworkPropertyMetadataOptions> показывает, что свойство зависимостей определено или используется службами навигации по журналированию.  Примером является свойство <xref:System.Windows.Controls.Primitives.Selector.SelectedIndex%2A>. любой элемент, выбранный в элементе управления выбора, должен сохраняться при навигации по истории журналирования.  
  
<a name="RODP"></a>   
## Свойства зависимости "только для чтения"  
 Можно определить свойство зависимости, которое является свойством "только для чтения".  Однако, ситуации, в которых свойство может задаваться как свойство "только для чтения", немного отличаются, как и процедура их регистрации системой свойств и предоставление идентификатора.  Дополнительные сведения см. в разделе [Свойства зависимости "только для чтения"](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md).  
  
<a name="CTDP"></a>   
## Свойства зависимостей типа коллекции  
 Следует учитывать некоторые дополнительные проблемы при реализации свойства зависимостей типа коллекции.  Дополнительные сведения см. в разделе [Свойства зависимостей типа коллекция](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md).  
  
<a name="SecurityC"></a>   
## Вопросы безопасности свойств зависимостей  
 Свойства зависимостей должны объявляться как открытые свойства.  Поля идентификатора свойства зависимостей должны объявляться как открытые статические поля.  Даже при попытке объявить другие уровни доступа \(например, защищенный\), свойство зависимости всегда может быть доступно через идентификатор в сочетании с системой свойств [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)].  Даже защищенное поле идентификатора потенциально доступно из\-за метаданных, уведомляющих об определении значений [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)], являющихся частью системы свойств, например, <xref:System.Windows.LocalValueEnumerator>.  Дополнительные сведения см. в разделе [Безопасность свойства зависимости](../../../../docs/framework/wpf/advanced/dependency-property-security.md).  
  
<a name="DPCtor"></a>   
## Свойства зависимостей и конструкторы класса  
 Общий принцип в программировании управляемого кода \(который часто применяется с помощью инструментов анализа кода, таких как FxCop\) заключается в том, что конструкторы класса не должны вызывать виртуальные методы.  Это вызвано тем, что конструкторы могут быть вызваны в качестве основной инициализации конструктора производного класса, а ввод виртуального метода в конструктор может произойти на незавершенной стадии инициализации конструируемого экземпляра объекта.  При наследовании из любого класса, который уже является производным от <xref:System.Windows.DependencyObject>, следует помнить, что сама система свойств вызывает методы и предоставляют виртуальные методы для внутренних целей.  Эти виртуальные методы являются частью служб системы свойств [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Переопределение методов позволяет производным классам участвовать в определении значения.  Чтобы избежать возможных проблем с инициализацией времени выполнения, не следует устанавливать значения свойства зависимостей в конструкторах классов за исключениям того случая, когда используется очень специфичный шаблон конструктора.  Дополнительные сведения см. в разделе [Шаблоны безопасного конструктора для DependencyObjects](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md).  
  
## См. также  
 [Общие сведения о свойствах зависимости](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Метаданные свойства зависимости](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [Общие сведения о разработке управления](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [Свойства зависимостей типа коллекция](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)   
 [Безопасность свойства зависимости](../../../../docs/framework/wpf/advanced/dependency-property-security.md)   
 [Загрузка кода XAML и свойства зависимостей](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)   
 [Шаблоны безопасного конструктора для DependencyObjects](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)