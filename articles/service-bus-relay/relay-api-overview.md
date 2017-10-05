---
title: "Visão geral da API de Retransmissão do Azure | Microsoft Docs"
description: "Visão geral das APIs de Retransmissão do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="ae704-103">APIs de Retransmissão disponíveis</span><span class="sxs-lookup"><span data-stu-id="ae704-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="ae704-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="ae704-104">Runtime APIs</span></span>

<span data-ttu-id="ae704-105">A tabela a seguir lista todos os clientes de tempo de execução de Retransmissão disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="ae704-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="ae704-106">A seção [informações adicionais](#additional-information) contém mais informações sobre o status de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ae704-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="ae704-107">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="ae704-107">Language/Platform</span></span> | <span data-ttu-id="ae704-108">Recurso disponível</span><span class="sxs-lookup"><span data-stu-id="ae704-108">Available feature</span></span> | <span data-ttu-id="ae704-109">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="ae704-109">Client package</span></span> | <span data-ttu-id="ae704-110">Repositório</span><span class="sxs-lookup"><span data-stu-id="ae704-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ae704-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="ae704-111">.NET Standard</span></span> | <span data-ttu-id="ae704-112">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="ae704-112">Hybrid Connections</span></span> | [<span data-ttu-id="ae704-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="ae704-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="ae704-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="ae704-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="ae704-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ae704-115">.NET Framework</span></span> | <span data-ttu-id="ae704-116">Retransmissão de WCF</span><span class="sxs-lookup"><span data-stu-id="ae704-116">WCF Relay</span></span> | [<span data-ttu-id="ae704-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="ae704-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="ae704-118">N/D</span><span class="sxs-lookup"><span data-stu-id="ae704-118">N/A</span></span> |
| <span data-ttu-id="ae704-119">Nó</span><span class="sxs-lookup"><span data-stu-id="ae704-119">Node</span></span> | <span data-ttu-id="ae704-120">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="ae704-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="ae704-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="ae704-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="ae704-122">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="ae704-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="ae704-123">.NET</span><span class="sxs-lookup"><span data-stu-id="ae704-123">.NET</span></span>
<span data-ttu-id="ae704-124">O ecossistema do .NET tem vários tempos de execução, portanto, há várias bibliotecas .NET de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ae704-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="ae704-125">A biblioteca .NET Standard pode ser executada usando o .NET Core ou o .NET Framework, enquanto a biblioteca do .NET Framework só pode ser executada em um ambiente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ae704-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="ae704-126">Para saber mais sobre o .NET Framework, veja [versões da estrutura](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="ae704-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae704-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae704-127">Next steps</span></span>
<span data-ttu-id="ae704-128">Para saber mais sobre a Retransmissão do Azure, visite estes links:</span><span class="sxs-lookup"><span data-stu-id="ae704-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="ae704-129">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="ae704-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="ae704-130">Perguntas frequentes sobre retransmissão</span><span class="sxs-lookup"><span data-stu-id="ae704-130">Relay FAQ</span></span>](relay-faq.md)