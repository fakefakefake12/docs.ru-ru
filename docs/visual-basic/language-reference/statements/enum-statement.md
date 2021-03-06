---
title: "Оператор Enum (Visual Basic) | Документы Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Enum
dev_langs:
- VB
helpviewer_keywords:
- enumerated constants
- Enum statement
- Private keyword, Enum statements
- Public keyword, in Enum statement
- variables [Visual Basic], enumeration
- constants, enumerated
ms.assetid: a45e51f1-65ff-48e1-bf32-79130f137377
caps.latest.revision: 44
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f9d3377300d30fd045c041367a528766fa9a8ed9
ms.lasthandoff: 03/13/2017

---
# <a name="enum-statement-visual-basic"></a>Оператор Enum (Visual Basic)
Объявляет перечисление и определяет значения его членов.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
[ <attributelist> ] [ accessmodifier ]  [ Shadows ]   
Enum enumerationname [ As datatype ]   
   memberlist  
End Enum  
```  
  
## <a name="parts"></a>Части  
  
-   `attributelist`  
  
     Необязательный. Список атрибутов, применяемых для данного перечисления. Необходимо заключить [список атрибутов](../../../visual-basic/language-reference/statements/attribute-list.md) в угловые скобки («`<`«и»`>`»).  
  
     <xref:System.FlagsAttribute>Атрибут указывает, что значение экземпляра перечисления может содержать несколько членов перечисления, и что каждый элемент представляет собой битовое поле, в значение перечисления.</xref:System.FlagsAttribute>  
  
-   `accessmodifier`  
  
     Необязательный. Указывает, какой код может получить доступ к этого перечисления. Ниже указаны доступные значения.  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Закрытые](../../../visual-basic/language-reference/modifiers/private.md)  
  
     Можно указать `Protected``Friend` для доступа из кода внутри класса перечисления, производного класса или той же сборки.  
  
-   `Shadows`  
  
     Необязательный. Указывает, что данное перечисление повторно объявляет и скрывает идентично именованный программный элемент или набор перегружаемых элементов в базовом классе. Можно указать [тени](../../../visual-basic/language-reference/modifiers/shadows.md) только на самом перечислении, а не на все его члены.  
  
-   `enumerationname`  
  
     Обязательный. Имя перечисления. Сведения о допустимых именах см. в разделе [имена объявленных элементов](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   `datatype`  
  
     Необязательный. Тип данных перечисления и всех его членов.  
  
-   `memberlist`  
  
     Обязательный. Список констант элементов, объявляемых в этом операторе. Несколько элементов отображаются на отдельных строках исходного кода.  
  
     Каждый `member` имеет следующий синтаксис и компоненты:`[<attribute list>] member name [ = initializer ]`  
  
    |Отделение|Описание|  
    |---|---|  
    |`membername`|Обязательный. Имя данного элемента.|  
    |`initializer`|Необязательный. Выражение, которое вычисляется во время компиляции и присваивается этому элементу.|  
  
-   `End` `Enum`  
  
     Завершает блок `Enum`.  
  
## <a name="remarks"></a>Примечания  
 Если имеется набор неизменных значений, логически связанных друг с другом, можно определить их вместе в перечислении. Это обеспечивает значимые имена для перечисления и его членов, которые проще запомнить, чем их значения. Затем можно использовать члены перечисления во многих местах в коде.  
  
 Преимущества использования перечисления включают следующие:  
  
-   Уменьшает количество ошибок, вызванных перемещением или неправильным вводом значений.  
  
-   Позволяет легко изменять значения в будущем.  
  
-   Делает код более удобными для чтения, это означает, что маловероятно, что появилось новых ошибок.  
  
-   Обеспечение прямой совместимости. При использовании перечисления вероятность возникновения ошибок, если в будущем кто-то изменяет значения, соответствующие именам элементов кода.  
  
 Перечисления имеет имя, базовый тип данных и набор элементов. Каждый элемент представляет константу.  
  
 Перечисление, объявленное на уровне интерфейса, вне любой процедуры, модуля, класса или структуры является *член перечисления*. Она является членом класса, структуры, модуля или интерфейса, объявляющего его.  
  
 Член перечисления из может осуществляться в любом месте в пределах их класса, структуры, модуля или интерфейса. Код вне класса, структуры или модуля необходимо определять имя перечисления элементов с именем этого класса, структуры или модуля. Можно избежать необходимости использовать полные имена, добавив [импорта](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) инструкции к файлу исходного кода.  
  
 Перечисление, объявленное на уровне пространства имен, вне класса, структуры, модуля или интерфейса, является членом пространства имен, в котором он находится.  
  
 *Контекст объявления* для перечисления должен быть исходный файл, пространство имен, класс, структура, модуль или интерфейс и не может быть процедурой. Дополнительные сведения см. в разделе [Контексты объявления и уровни доступа по умолчанию](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Можно применять атрибуты к перечислению в целом, но не к его члены по отдельности. Атрибут вносит сведения для метаданных сборки.  
  
## <a name="data-type"></a>Тип данных  
 `Enum` Оператора можно объявлять тип данных перечисления. Каждый элемент принимает тип данных перечисления. You can specify `Byte`, `Integer`, `Long`, `SByte`, `Short`, `UInteger`, `ULong`, or `UShort`.  
  
 Если вы не укажете `datatype` для перечисления, каждый элемент имеет тип данных его `initializer`. Если указываются оба `datatype` и `initializer`, тип данных `initializer` должен быть преобразуемым к `datatype`. Если ни одна из `datatype` , ни `initializer` присутствует, по умолчанию для типа данных `Integer`.  
  
## <a name="initializing-members"></a>Инициализация элементов  
 `Enum` Оператор может инициализировать содержимое выбранных элементов в `memberlist`. Использовать `initializer` позволяет указать выражение для назначения члена.  
  
 Если не указать `initializer` для члена, Visual Basic инициализирует его, либо ноль (если он является первым `member` в `memberlist`), или в значение на единицу, чем непосредственно перед `member`.  
  
 Выражения, предоставленного в каждом `initializer` может быть любым сочетанием литералов, других, уже определенные константы и члены перечисления, которые уже определены, включая предыдущего члена этого перечисления. Для комбинирования этих элементов можно использовать арифметические и логические операторы.  
  
 Нельзя использовать переменные или функции в `initializer`. Однако можно использовать ключевые слова преобразования, такие как `CByte` и `CShort`. Можно также использовать `AscW` при вызове с константой `String` или `Char` аргумент, поскольку, может быть вычислено во время компиляции.  
  
 Перечисления не могут иметь значений с плавающей запятой. Если член присваивается значение с плавающей запятой и `Option Strict` имеет значение on, возникает ошибка компилятора. Если `Option Strict` выключен, то значение автоматически преобразуется в `Enum` типа.  
  
 Если значение члена превосходит верхнюю границу для базового типа данных или инициализации любого члена к допустимому значению базового типа данных, компилятор сообщает об ошибке.  
  
## <a name="modifiers"></a>Модификаторы  
 Класс, структура, модуль и интерфейс элемента перечисления по умолчанию общий доступ. Можно настроить их уровни доступа с помощью модификаторов доступа. Пространство имен элемента перечисления по умолчанию дружественный доступ. Можно настроить их уровни доступа к общедоступным, но не к закрытым или защищенным. Дополнительные сведения см. в разделе [уровни доступа в Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Все элементы перечисления имеют общий доступ, и на них нельзя использовать никакие модификаторы доступа. Однако если перечисление само имеет более ограниченный уровень доступа, указанный уровень доступа перечисления имеет приоритет.  
  
 По умолчанию все перечисления являются типами и их поля являются константами. Поэтому `Shared`, `Static`, и `ReadOnly` ключевые слова нельзя использовать при объявлении перечисления или его элементов.  
  
## <a name="assigning-multiple-values"></a>Назначение нескольких значений  
 Перечисления обычно представляют собой взаимоисключающие значения. Включив <xref:System.FlagsAttribute>атрибут `Enum` объявление, можно вместо этого назначить несколько значений экземпляра перечисления.</xref:System.FlagsAttribute> <xref:System.FlagsAttribute>Атрибут указывает, что перечисление рассматриваться как битовое поле, то есть набор флагов.</xref:System.FlagsAttribute> Это называется *побитовое* перечисления.  
  
 При объявлении перечисления с помощью <xref:System.FlagsAttribute>атрибут, рекомендуется использовать степени числа 2, который является, 1, 2, 4, 8, 16 и так далее, для значения.</xref:System.FlagsAttribute> Также рекомендуется «None» имя элемента, значение которого равно 0. Дополнительные рекомендации см. в разделе <xref:System.FlagsAttribute>и <xref:System.Enum>.</xref:System.Enum> </xref:System.FlagsAttribute>  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как использовать `Enum` инструкции. Обратите внимание, что элемент называется `EggSizeEnum.Medium`, а не как `Medium`.  
  
 [!code-vb[VbEnumsTask&#41;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_1.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере метод находится за пределами `Egg` класса. Таким образом `EggSizeEnum` которого полностью определено как `Egg.EggSizeEnum`.  
  
 [!code-vb[VbEnumsTask&#42;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_2.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере используется `Enum` инструкции для определения связанного набора именованных констант. В этом случае значения цветов, которые можно выбрать для создаваемых форм ввода данных для базы данных.  
  
 [!code-vb[VbEnumsTask&#30;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_3.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано значений, которые включают положительные и отрицательные числа.  
  
 [!code-vb[VbEnumsTask&#31;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_4.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере `As` предложение используется для указания `datatype` перечисления.  
  
 [!code-vb[VbEnumsTask №&6;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_5.vb)]  
  
## <a name="example"></a>Пример  
 Следующий пример показывает использование побитового перечисления. Несколько значений может быть присвоено экземпляру побитового перечисления. `Enum` Объявление включает в себя <xref:System.FlagsAttribute>атрибут, который указывает, что перечисление может обрабатываться как набор флагов.</xref:System.FlagsAttribute>  
  
 [!code-vb[VbEnumsTask&#61;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_6.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере выполняется итерация по перечисления. Он использует <xref:System.Enum.GetNames%2A>метод для получения массива имен членов из перечисления, и <xref:System.Enum.GetValues%2A>для извлечения массива значений членов.</xref:System.Enum.GetValues%2A> </xref:System.Enum.GetNames%2A>  
  
 [!code-vb[VbEnumsTask&#51;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enum-statement_7.vb)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.Enum></xref:System.Enum>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A></xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 [Оператор Const](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Оператор Dim](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Явные и неявные преобразования](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Функции преобразования типов](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Константы и перечисления](../../../visual-basic/language-reference/constants-and-enumerations.md)
