---
title: "Неявно типизированные лямбда-выражения"
description: "Неявно типизированные лямбда-выражения"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a3851da9-e018-4389-9922-233db7d0f841
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c3621f6feb29929d3681b6ed66cc12c5d8018ba1
ms.lasthandoff: 03/13/2017

---

# <a name="implicitly-typed-lambda-expressions"></a>Неявно типизированные лямбда-выражения

Для объявления этого дерева выражения не используется `var`. Объявление неявно типизированной переменной нельзя использовать для объявления лямбда-выражения.
В этом случае компилятор сталкивается с проблемой замкнутого цикла. Объявление `var` предписывает компилятору определить тип переменной на основе типа выражения в правой части оператора присваивания. Лямбда-выражение не имеет типа во время компиляции, но может быть преобразовано в любой соответствующий тип делегата или выражения. Когда вы присваиваете лямбда-выражение переменной, имеющей тип делегата или выражения, вы предписываете компилятору выполнить попытку преобразовать лямбда-выражение в выражение или делегат, которые соответствуют сигнатуре этой переменной. Компилятор должен попытаться сделать так, чтобы правая часть присваивания соответствовала типу левой части. 

Обе части оператора присваивания не могут одновременно предписывать компилятору выполнить проверку объекта в другой части на предмет соответствия типа.

Чтобы получить дополнительные сведения о том, почему в языке C# принято такое поведение, прочитайте [эту статью](http://download.microsoft.com/download/5/4/B/54B83DFE-D7AA-4155-9687-B0CF58FF65D7/type-inference.pdf) (скачиваемый PDF-файл).



