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
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="957ba-103">Solucionar problemas comuns quando você implanta serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="957ba-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="957ba-104">Quando você estiver executando os serviços em seu computador de desenvolvedor, é fácil toouse [ferramentas de depuração do Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="957ba-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="957ba-105">Para clusters remotos, [relatórios de integridade](service-fabric-view-entities-aggregated-health.md) sempre são um bom lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="957ba-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="957ba-106">Olá mais fácil tooaccess maneiras esses relatórios são feitas por meio do PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="957ba-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="957ba-107">Este artigo pressupõe que você está depurando um cluster remoto e ter um entendimento básico de como toouse uma dessas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="957ba-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="957ba-108">Falha do aplicativo</span><span class="sxs-lookup"><span data-stu-id="957ba-108">Application crash</span></span>
<span data-ttu-id="957ba-109">Olá "partição está abaixo de contagem de réplica ou instância de destino" relatório é uma boa indicação de que o serviço está falhando.</span><span class="sxs-lookup"><span data-stu-id="957ba-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="957ba-110">toofind limite em que o serviço está falhando leva investigação mais um pouco.</span><span class="sxs-lookup"><span data-stu-id="957ba-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="957ba-111">Ao executar seu serviço em grande escala, o seu melhor amigo será um conjunto de rastreamentos bem pensados.</span><span class="sxs-lookup"><span data-stu-id="957ba-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="957ba-112">Sugerimos que você tente [diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) para coletar os rastreamentos e usando uma solução como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para exibir e pesquisar rastreamentos hello.</span><span class="sxs-lookup"><span data-stu-id="957ba-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![Integridade da partição SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="957ba-114">Durante a inicialização de ator ou serviço</span><span class="sxs-lookup"><span data-stu-id="957ba-114">During service or actor initialization</span></span>
<span data-ttu-id="957ba-115">Todas as exceções antes da inicialização do tipo de serviço Olá fará com que a saudação processo toocrash.</span><span class="sxs-lookup"><span data-stu-id="957ba-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="957ba-116">Para esses tipos de falhas, log de eventos do aplicativo hello mostrará o erro de saudação do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="957ba-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="957ba-117">Esses são hello mais comuns exceções toosee antes da inicialização do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="957ba-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="957ba-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="957ba-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="957ba-119">Esse erro geralmente é devido a dependências do assembly toomissing.</span><span class="sxs-lookup"><span data-stu-id="957ba-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="957ba-120">Verifique a propriedade de CopyLocal Olá no Visual Studio ou o cache de assembly global Olá para o nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="957ba-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="957ba-121">***System.Runtime.InteropServices.COMException*** *em System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="957ba-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="957ba-122">Isso indica que esse nome de tipo de serviço registrado Olá não coincide com o manifesto de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="957ba-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="957ba-123">[Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) pode ser configurado tooupload Olá log de eventos para todos os seus nós automaticamente.</span><span class="sxs-lookup"><span data-stu-id="957ba-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="957ba-124">RunAsync() ou OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="957ba-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="957ba-125">Se ocorrer falha de saudação durante a inicialização de saudação ou execução de seu tipo de serviço registrado ou o ator, Olá exceção será identificada pela malha do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="957ba-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="957ba-126">Você pode exibir esses de provedores de EventSource Olá detalhadas Olá a seção "Próximas etapas".</span><span class="sxs-lookup"><span data-stu-id="957ba-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="957ba-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="957ba-127">Next steps</span></span>
<span data-ttu-id="957ba-128">Saiba mais sobre diagnósticos existentes fornecidos pelo Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="957ba-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="957ba-129">Diagnóstico do Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="957ba-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="957ba-130">Diagnóstico do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="957ba-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

