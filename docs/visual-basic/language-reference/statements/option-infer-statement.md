---
title: "Оператор Option Infer | Документы Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.OptionInfer
- vb.Infer
dev_langs:
- VB
helpviewer_keywords:
- variables [Visual Basic], declaring
- Option Infer statement
- Infer keyword
- declaring variables, inferred
- inferred variable declaration
ms.assetid: 4ad3e6e9-8f5b-4209-a248-de22ef6e4652
caps.latest.revision: 72
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
ms.openlocfilehash: e6074ad44b94c80f275af562edef2dcd1173c0c3
ms.lasthandoff: 03/13/2017

---
# <a name="option-infer-statement"></a>Option Infer - оператор
Включает использование локального определения типов при объявлении переменных.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
Option Infer { On | Off }  
```  
  
## <a name="parts"></a>Части  
  
|Термин|Определение|  
|---|---|  
|`On`|Необязательно. Включает локальное определение типов.|  
|`Off`|Необязательно. Отключает локальное определение типов.|  
  
## <a name="remarks"></a>Примечания  
 Чтобы задать `Option Infer` в файле, введите `Option Infer On` или `Option Infer Off` в начале файла перед всем остальным исходным кодом. Если значение, заданное для `Option Infer` в файле, конфликтует со значением, заданным в среде разработки или в командной строке, приоритет имеет значение в файле.  
  
 Если задать для `Option Infer` значение `On`, можно объявлять локальные переменные, не задавая явным образом тип данных. Компилятор определяет тип переменной по типу ее выражения инициализации.  
  
 На следующей иллюстрации `Option Infer` включен. Переменная в объявлении `Dim someVar = 2` объявляется как целочисленная определением типов.  
  
 ![IntelliSense-просмотров объявления.](../../../visual-basic/language-reference/statements/media/optioninferasinteger.png "optionInferAsInteger")  
IntelliSense при включенном параметре Option Infer  
  
 На следующей иллюстрации `Option Infer` отключен. Переменная в объявлении `Dim someVar = 2` объявляется как `Object` определением типов. В этом примере **Option Strict** установлено значение **отключение** на [компиляция, конструктор проектов (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic).  
  
 ![IntelliSense-просмотров объявления.](../../../visual-basic/language-reference/statements/media/optioninferasobject.png "optionInferAsObject")  
IntelliSense при отключенном параметре Option Infer  
  
> [!NOTE]
>  Если переменная объявлена как `Object`, тип времени выполнения может измениться в ходе работы программы. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]выполняет операции *упаковки* и *распаковки* для преобразования между `Object` и тип значения, что замедляет выполнение. Сведения об упаковке и распаковке см. в разделе [спецификация языка Visual Basic](../../../visual-basic/reference/language-specification.md).  
  
 Определение типов применяется на уровне процедур и не применяется вне процедур в классах, структурах, модулях и интерфейсах.  
  
 Дополнительные сведения см. в разделе [вывод локального типа](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
## <a name="when-an-option-infer-statement-is-not-present"></a>Если оператор Option Infer отсутствует  
 Если исходный код не содержит `Option Infer` инструкции, **Option Infer** на [компиляция, конструктор проектов (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) используется. Если используется компилятор командной строки, [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) используется параметр компилятора.  
  
#### <a name="to-set-option-infer-in-the-ide"></a>Чтобы включить Option Infer в среде разработки  
  
1.  В **обозревателе**, выберите проект. На **проекта** меню, щелкните **свойства**. Дополнительные сведения см. в разделе [NIB: управление свойства проекта с помощью конструктора проектов](http://msdn.microsoft.com/en-us/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Откройте вкладку **Компиляция**.  
  
3.  Задайте значение в **Option infer** поле.  
  
 При создании нового проекта, **Option Infer** на **компиляции** задано значение **Option Infer** в **VB по умолчанию** диалоговое окно. Для доступа к **VB по умолчанию** в диалоговом **средства** меню, щелкните **параметры**. В **параметры** диалогового окна разверните **проекты и решения**и нажмите кнопку **VB по умолчанию**. Начальный параметр по умолчанию в **VB значения по умолчанию** — `On`.  
  
#### <a name="to-set-option-infer-on-the-command-line"></a>Чтобы включить Option Infer в командной строке  
  
-   Включить [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) параметра компилятора в **vbc** команды.  
  
## <a name="default-data-types-and-values"></a>Типы данных и значения по умолчанию  
 В следующей таблице перечислены результаты различных сочетаний заданных типов данных и инициализаторов в операторе `Dim`.  
  
|Указан тип данных?|Указан инициализатор?|Пример|Результат|  
|---|---|---|---|  
|Нет|Нет|`Dim qty`|Если `Option Strict` отключен (по умолчанию), для переменной устанавливается значение `Nothing`.<br /><br /> Если параметр `Option Strict` включен, при компиляции возникает ошибка.|  
|Нет|Да|`Dim qty = 5`|Если параметр `Option Infer` включен (по умолчанию), переменная получает тип данных инициализатора. В разделе [вывод локального типа](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Если параметры `Option Infer` и `Option Strict` отключены, переменная получает тип данных `Object`.<br /><br /> Если параметр `Option Infer` отключен, а параметр `Option Strict` включен, при компиляции возникает ошибка.|  
|Да|Нет|`Dim qty As Integer`|Переменная инициализируется со значением по умолчанию для типа данных. Дополнительные сведения см. в разделе [оператора Dim](../../../visual-basic/language-reference/statements/dim-statement.md).|  
|Да|Да|`Dim qty  As Integer = 5`|Если тип данных инициализатора нельзя преобразовать в указанный тип данных, возникает ошибка времени компиляции.|  
  
## <a name="example"></a>Пример  
 В следующих примерах показано, как оператор `Option Infer` включает локальное определение типов.  
  
 [!code-vb[VbVbalrTypeInference №&6;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_1.vb)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано, что тип времени выполнения может различаться, когда переменная указана как `Object`.  
  
 [!code-vb[VbVbalrTypeInference&11;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_2.vb)]  
  
## <a name="see-also"></a>См. также  
 [Оператор Dim](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Вывод локального типа](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Оператор Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Оператор Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Оператор Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Диалоговое окно параметров значения по умолчанию, проекты, Visual Basic](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)   
 [/ optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Упаковка-преобразование и распаковка-преобразование](../../../csharp/programming-guide/types/boxing-and-unboxing.md)
