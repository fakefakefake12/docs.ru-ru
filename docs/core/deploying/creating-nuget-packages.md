---
title: "Создание пакета NuGet с помощью кроссплатформенных средств"
description: "Создание пакета NuGet с помощью кроссплатформенных средств"
keywords: .NET, .NET Core, NuGet
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2f0415c1-110b-433d-87c1-ae3d543a8844
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 657981a05e831ffb849d0cd5b3ea25c079cb4fc1
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-create-a-nuget-package-with-cross-platform-tools"></a>Создание пакета NuGet с помощью кроссплатформенных средств

> [!NOTE]
> Ниже приведены примеры команд командной строки для Unix.  Показанная здесь команда `dotnet pack` точно так же работает в Windows.

Для .NET Core 1.0 библиотеки должны распространяться в виде пакетов NuGet.  Именно так распространяются и используются все библиотеки .NET Standard.  Проще всего это делать с помощью команды `dotnet pack`.

Представим, что вы только что создали полезную библиотеку, которую хотите распространить через NuGet.  Для этого можно создать пакет NuGet с помощью кроссплатформенных средств.  В приведенном ниже примере используется библиотека **SuperAwesomeLibrary**, предназначенная для `netstandard1.0`.

Если у вас есть транзитивные зависимости, то есть проекты, которые зависят от других проектов, необходимо обязательно восстановить пакеты для всего решения с помощью команды `dotnet restore`, прежде чем создавать пакет NuGet.  Если не сделать этого, команда `dotnet pack` будет работать неправильно.

Восстановив пакеты, можно перейти в каталог, где находится библиотека:

`$ cd src/SuperAwesomeLibrary`

Затем нужно выполнить всего лишь одну команду в командной строке:
    
`$ dotnet pack`

Папка `/bin/Debug` теперь будет выглядеть так:

```
$ ls bin/Debug

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

Обратите внимание на то, что при этом создается пакет, который можно отлаживать.  Если вы хотите создать пакет NuGet с двоичными файлами выпуска, вам нужно просто добавить параметр `-c`/`--configuration` и использовать `release` в качестве аргумента.

`$ dotnet pack --configuration release`

В папке `/bin` теперь будет папка `release`, содержащая пакет NuGet с двоичными файлами выпуска:

```
$ ls bin/release

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

теперь у вас есть все необходимые файлы для публикации пакета NuGet.

## <a name="dont-confuse-dotnet-pack-with-dotnet-publish"></a>Не путайте команду `dotnet pack` с командой `dotnet publish`.

Важно заметить, что команда `dotnet publish` в этом процессе не применяется.  Команда `dotnet publish` предназначена для развертывания приложений со всеми зависимостями в одном пакете, а не для создания пакета NuGet, который будет распространяться и использоваться посредством NuGet.

