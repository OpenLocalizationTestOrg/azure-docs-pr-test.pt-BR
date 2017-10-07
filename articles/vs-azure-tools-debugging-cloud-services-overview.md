---
title: "Serviços de nuvem aaaOptions para depuração do Azure | Microsoft Docs"
description: "Depurando serviços de nuvem do Azure"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Olá várias maneiras de aprender toodebug um serviço de nuvem do Azure
Este artigo fornece links toohello várias maneiras toodebug um serviço de nuvem do Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Depurando um serviço de nuvem do Azure no Visual Studio
Você pode economizar tempo e dinheiro usando toodebug de emulador de computação do Azure Olá seu serviço de nuvem em um computador local. Ao depurar um serviço localmente antes de implantá-lo, você pode aprimorar a confiabilidade e o desempenho sem pagar pelo tempo de computação. No entanto, alguns erros podem ocorrer somente quando um serviço de nuvem é executado no Azure. Erros que ocorrem apenas quando você executa um serviço de nuvem no Azure podem ser depurados habilitando a depuração remota quando você publicar seu serviço e, em seguida, anexando a instância de função hello depurador tooa. Para saber mais, consulte [Depurar o serviço de nuvem no computador local](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)

## <a name="using-azure-diagnostics"></a>Usando o Diagnóstico do Azure 
Você pode usar o diagnóstico do Azure toolog obter informações de execução de código em funções, quer funções hello estejam em execução no ambiente de desenvolvimento de saudação ou no Azure. Para saber mais, confira [Habilitando o Diagnóstico do Azure nos Serviços de Nuvem do Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Usando o IntelliTrace 
Se você estiver usando funções do Visual Studio Enterprise toowrite direcionada .NET Framework 4.5, você pode habilitar o IntelliTrace no tempo de saudação que você implantar um serviço de nuvem do Azure do Visual Studio. IntelliTrace fornece um log que você pode usar com o Visual Studio toodebug seu aplicativo como se ele estivesse sendo executado no Azure. Para saber mais, consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Depuração remota 
Você pode habilitar a depuração remota dos serviços de nuvem em tempo de hello quando você implanta o serviço de nuvem de saudação do Visual Studio. Se você escolher tooenable remota de depuração para uma implantação, os serviços de depuração remota são instalados em máquinas virtuais de saudação que são executados a cada instância de função. Esses serviços – como `msvsmon.exe` – não afetam o desempenho nem resultam em custos extras. Para saber mais, consulte [Depurar o serviço de nuvem no Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)

## <a name="next-steps"></a>Próximas etapas
- [Depuração de um serviço de nuvem do Azure ou a VM no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -obter Olá detalhes de como serviços em nuvem toodebug do Azure.
