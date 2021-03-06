---
title: "Была создана ссылка на внедренную сборку взаимодействия &lt;сборка_1&gt; из-за наличия неявной ссылки на эту сборки из сборки &lt;сборка_2&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40059"
  - "bc40059"
helpviewer_keywords: 
  - "BC40059"
  - "VBC40059"
ms.assetid: 520e39cb-8ab6-46f5-aa00-08afd51b4b7c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Была создана ссылка на внедренную сборку взаимодействия &lt;сборка_1&gt; из-за наличия неявной ссылки на эту сборки из сборки &lt;сборка_2&gt;
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Была создана ссылка на внедренную сборку взаимодействия \<сборка\_1\> из\-за наличия неявной ссылки на эту сборку из сборки \<сборка\_2\>.Попробуйте изменить свойство "Внедрить типы взаимодействия" любой сборки.  
  
 Была добавлена ссылка на сборку \(сборка\_1\), свойству `Embed Interop Types` которой присвоено значение `True`.  Это указывает компилятору внедрить сведения о типе сборки взаимодействия из этой сборки.  Однако компилятор не может внедрить такие сведения из этой сборки, поскольку другая сборка, на которую имеется ссылка \(сборка\_2\), также ссылается на эту сборку \(сборка\_1\), и ее свойству `Embed Interop Types` присвоено значение `False`.  
  
> [!NOTE]
>  Присвоение свойству `Embed Interop Types` для ссылки на сборку значения `True` равнозначно созданию ссылки на сборку с помощью параметра `/link` для компилятора командной строки.  
  
 **Идентификатор ошибки:** BC40059  
  
### Чтобы устранить это предупреждение, выполните следующие действия:  
  
-   Чтобы внедрить сведения о типе сборки взаимодействия для обеих сборок, присвойте свойству `Embed Interop Types` для всех ссылок на сборку \(сборка\_1\) значение `True`.  
  
-   Чтобы удалить предупреждение, свойству `Embed Interop Types` сборки \(сборка\_1\) можно присвоить значение `False`.  В этом случае сведения о типе сборки взаимодействия предоставляются основной сборкой взаимодействия.  
  
## См. также  
 [\/link](../../../visual-basic/reference/command-line-compiler/link.md)   
 [Programming with Primary Interop Assemblies](http://msdn.microsoft.com/ru-ru/306fa1d6-0703-4004-9e93-d0a57f1be81e)