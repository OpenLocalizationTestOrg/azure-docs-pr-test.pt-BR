---
title: aaaTroubleshooting com o rastreamento de eventos | Microsoft Docs
description: "problemas mais comuns de saudação encontrados durante a implantação de serviços no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Solucionar problemas comuns quando você implanta serviços no Azure Service Fabric
Quando você estiver executando os serviços em seu computador de desenvolvedor, é fácil toouse [ferramentas de depuração do Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Para clusters remotos, [relatórios de integridade](service-fabric-view-entities-aggregated-health.md) sempre são um bom lugar toostart. Olá mais fácil tooaccess maneiras esses relatórios são feitas por meio do PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md). Este artigo pressupõe que você está depurando um cluster remoto e ter um entendimento básico de como toouse uma dessas ferramentas.

## <a name="application-crash"></a>Falha do aplicativo
Olá "partição está abaixo de contagem de réplica ou instância de destino" relatório é uma boa indicação de que o serviço está falhando. toofind limite em que o serviço está falhando leva investigação mais um pouco. Ao executar seu serviço em grande escala, o seu melhor amigo será um conjunto de rastreamentos bem pensados.  Sugerimos que você tente [diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) para coletar os rastreamentos e usando uma solução como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para exibir e pesquisar rastreamentos hello.

![Integridade da partição SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Durante a inicialização de ator ou serviço
Todas as exceções antes da inicialização do tipo de serviço Olá fará com que a saudação processo toocrash. Para esses tipos de falhas, log de eventos do aplicativo hello mostrará o erro de saudação do seu serviço.
Esses são hello mais comuns exceções toosee antes da inicialização do serviço de saudação.

***System.IO.FileNotFoundException***

Esse erro geralmente é devido a dependências do assembly toomissing. Verifique a propriedade de CopyLocal Olá no Visual Studio ou o cache de assembly global Olá para o nó de saudação.

***System.Runtime.InteropServices.COMException*** *em System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Isso indica que esse nome de tipo de serviço registrado Olá não coincide com o manifesto de serviço hello.

[Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) pode ser configurado tooupload Olá log de eventos para todos os seus nós automaticamente.

### <a name="runasync-or-onactivateasync"></a>RunAsync() ou OnActivateAsync()
Se ocorrer falha de saudação durante a inicialização de saudação ou execução de seu tipo de serviço registrado ou o ator, Olá exceção será identificada pela malha do serviço do Azure. Você pode exibir esses de provedores de EventSource Olá detalhadas Olá a seção "Próximas etapas".

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre diagnósticos existentes fornecidos pelo Service Fabric:

* [Diagnóstico do Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Diagnóstico do Reliable Services](service-fabric-reliable-services-diagnostics.md)

