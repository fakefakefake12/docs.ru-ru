---
title: "Производные классы не могут вызывать события базового класса | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30029"
  - "bc30029"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30029"
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Производные классы не могут вызывать события базового класса
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Событие может возникнуть только из пространства объявления, в котором оно было объявлено.  Следовательно, класс не может вызвать событие из другого класса, даже из того, от которого он является производным.  
  
 **Идентификатор ошибки:** BC30029  
  
### Чтобы исправить эту ошибку  
  
-   Переместите оператор `Event` или `RaiseEvent` в тот же класс, в котором имеется соответствующий ему оператор.  
  
## См. также  
 [Оператор Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Оператор RaiseEvent](../../../visual-basic/language-reference/statements/raiseevent-statement.md)