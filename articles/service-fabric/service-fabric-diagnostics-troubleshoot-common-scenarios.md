---
title: "Solução de problemas com o rastreamento de eventos | Microsoft Docs"
description: "Os problemas mais comuns encontrados durante a implantação de serviços no Service Fabric do Microsoft Azure."
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
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="3e8a0-103">Solucionar problemas comuns quando você implanta serviços no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3e8a0-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="3e8a0-104">Ao executar serviços em seu computador de desenvolvedor, é fácil usar as [ferramentas de depuração do Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="3e8a0-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="3e8a0-105">Para clusters remotos, [relatórios de integridade](service-fabric-view-entities-aggregated-health.md) sempre são um bom lugar para começar.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="3e8a0-106">As maneiras mais fáceis de acessar esses relatórios são por meio do PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3e8a0-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="3e8a0-107">Este artigo pressupõe que você está depurando um cluster remoto e tem um entendimento básico de como usar essas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="3e8a0-108">Falha do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e8a0-108">Application crash</span></span>
<span data-ttu-id="3e8a0-109">O relatório “Partição está abaixo da contagem de réplicas ou instâncias de destino” é uma boa indicação de que o serviço está falhando.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="3e8a0-110">Para descobrir onde o serviço está falhando, é necessário um pouco mais de investigação.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="3e8a0-111">Ao executar seu serviço em grande escala, o seu melhor amigo será um conjunto de rastreamentos bem pensados.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="3e8a0-112">Sugerimos que você experimente o [Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) para coletar esses rastreamentos e use uma solução como [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) para exibir e pesquisar os rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![Integridade da partição SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="3e8a0-114">Durante a inicialização de ator ou serviço</span><span class="sxs-lookup"><span data-stu-id="3e8a0-114">During service or actor initialization</span></span>
<span data-ttu-id="3e8a0-115">Todas as exceções antes que o tipo de serviço seja inicializado farão com que o processo falhe.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="3e8a0-116">Para esses tipos de falhas, o log de eventos do aplicativo mostrará o erro de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="3e8a0-117">Estas são as exceções mais comuns vistas antes que o serviço seja inicializado.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="3e8a0-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="3e8a0-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="3e8a0-119">Esse erro, frequentemente, é devido à ausência de dependências do assembly.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="3e8a0-120">Verifique a propriedade CopyLocal no Visual Studio ou no cache de assembly global para o nó.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="3e8a0-121">***System.Runtime.InteropServices.COMException*** *em System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="3e8a0-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="3e8a0-122">Isso indica que o nome do tipo de serviço registrado não coincide com o manifesto de serviço.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="3e8a0-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) pode ser configurado para carregar o log de eventos do aplicativo para todos os seus nós automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="3e8a0-124">RunAsync() ou OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="3e8a0-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="3e8a0-125">Se a falha ocorre durante a inicialização ou a execução do seu tipo de serviço registrado ou um ator, a exceção será capturada pelo Service Fabric do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="3e8a0-126">Você pode exibi-las nos provedores EventSource detalhados na seção “Próximas etapas”.</span><span class="sxs-lookup"><span data-stu-id="3e8a0-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e8a0-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e8a0-127">Next steps</span></span>
<span data-ttu-id="3e8a0-128">Saiba mais sobre diagnósticos existentes fornecidos pelo Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="3e8a0-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="3e8a0-129">Diagnóstico do Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="3e8a0-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="3e8a0-130">Diagnóstico do Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3e8a0-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

