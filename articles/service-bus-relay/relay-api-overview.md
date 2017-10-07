---
title: "Visão geral da API de retransmissão aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="288fc-103">APIs de Retransmissão disponíveis</span><span class="sxs-lookup"><span data-stu-id="288fc-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="288fc-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="288fc-104">Runtime APIs</span></span>

<span data-ttu-id="288fc-105">Olá tabela a seguir lista todos os clientes de tempo de execução de retransmissão disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="288fc-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="288fc-106">Olá [informações adicionais](#additional-information) seção contém mais informações sobre o status de saudação de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="288fc-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="288fc-107">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="288fc-107">Language/Platform</span></span> | <span data-ttu-id="288fc-108">Recurso disponível</span><span class="sxs-lookup"><span data-stu-id="288fc-108">Available feature</span></span> | <span data-ttu-id="288fc-109">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="288fc-109">Client package</span></span> | <span data-ttu-id="288fc-110">Repositório</span><span class="sxs-lookup"><span data-stu-id="288fc-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="288fc-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="288fc-111">.NET Standard</span></span> | <span data-ttu-id="288fc-112">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="288fc-112">Hybrid Connections</span></span> | [<span data-ttu-id="288fc-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="288fc-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="288fc-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="288fc-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="288fc-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="288fc-115">.NET Framework</span></span> | <span data-ttu-id="288fc-116">Retransmissão de WCF</span><span class="sxs-lookup"><span data-stu-id="288fc-116">WCF Relay</span></span> | [<span data-ttu-id="288fc-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="288fc-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="288fc-118">N/D</span><span class="sxs-lookup"><span data-stu-id="288fc-118">N/A</span></span> |
| <span data-ttu-id="288fc-119">Nó</span><span class="sxs-lookup"><span data-stu-id="288fc-119">Node</span></span> | <span data-ttu-id="288fc-120">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="288fc-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="288fc-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="288fc-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="288fc-122">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="288fc-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="288fc-123">.NET</span><span class="sxs-lookup"><span data-stu-id="288fc-123">.NET</span></span>
<span data-ttu-id="288fc-124">ecossistema do .NET Olá tem vários tempos de execução, portanto, há várias bibliotecas .NET para Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="288fc-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="288fc-125">biblioteca .NET padrão Olá pode ser executada usando o .NET Core ou saudação do .NET Framework, enquanto a biblioteca do .NET Framework Olá só pode ser executada em um ambiente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="288fc-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="288fc-126">Para saber mais sobre o .NET Framework, veja [versões da estrutura](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="288fc-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="288fc-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="288fc-127">Next steps</span></span>
<span data-ttu-id="288fc-128">toolearn mais informações sobre a retransmissão do Azure, visite esses links:</span><span class="sxs-lookup"><span data-stu-id="288fc-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="288fc-129">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="288fc-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="288fc-130">Perguntas frequentes sobre retransmissão</span><span class="sxs-lookup"><span data-stu-id="288fc-130">Relay FAQ</span></span>](relay-faq.md)