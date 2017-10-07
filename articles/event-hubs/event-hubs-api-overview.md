---
title: "Visão geral da API de Hubs de evento aaaAzure | Microsoft Docs"
description: "Visão geral das APIs de Hubs de Eventos do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="124d1-103">APIs de Hubs de Eventos disponíveis</span><span class="sxs-lookup"><span data-stu-id="124d1-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="124d1-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="124d1-104">Runtime APIs</span></span>

<span data-ttu-id="124d1-105">a seguir Olá é uma descrição de todos os clientes de tempo de execução de Hubs de eventos do Azure disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="124d1-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="124d1-106">Embora algumas dessas bibliotecas também incluem a funcionalidade de gerenciamento limitado, também há [bibliotecas específicas](#management-apis) dedicado toomanagement operações.</span><span class="sxs-lookup"><span data-stu-id="124d1-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="124d1-107">foco principal Olá essas bibliotecas é toosend e receber mensagens de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="124d1-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="124d1-108">Consulte [informações adicionais](#additional-information) para obter mais detalhes sobre o status atual de saudação de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="124d1-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="124d1-109">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="124d1-109">Language/Platform</span></span> | <span data-ttu-id="124d1-110">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="124d1-110">Client package</span></span> | <span data-ttu-id="124d1-111">Pacote EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="124d1-111">EventProcessorHost package</span></span> | <span data-ttu-id="124d1-112">Repositório</span><span class="sxs-lookup"><span data-stu-id="124d1-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="124d1-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="124d1-113">.NET Standard</span></span> | [<span data-ttu-id="124d1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="124d1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="124d1-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="124d1-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="124d1-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="124d1-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="124d1-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="124d1-117">.NET Framework</span></span> | [<span data-ttu-id="124d1-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="124d1-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="124d1-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="124d1-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="124d1-120">N/D</span><span class="sxs-lookup"><span data-stu-id="124d1-120">N/A</span></span> |
| <span data-ttu-id="124d1-121">Java</span><span class="sxs-lookup"><span data-stu-id="124d1-121">Java</span></span> | [<span data-ttu-id="124d1-122">Maven</span><span class="sxs-lookup"><span data-stu-id="124d1-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="124d1-123">Maven</span><span class="sxs-lookup"><span data-stu-id="124d1-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="124d1-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="124d1-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="124d1-125">Nó</span><span class="sxs-lookup"><span data-stu-id="124d1-125">Node</span></span> | [<span data-ttu-id="124d1-126">NPM</span><span class="sxs-lookup"><span data-stu-id="124d1-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="124d1-127">N/D</span><span class="sxs-lookup"><span data-stu-id="124d1-127">N/A</span></span> | [<span data-ttu-id="124d1-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="124d1-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="124d1-129">C</span><span class="sxs-lookup"><span data-stu-id="124d1-129">C</span></span> | <span data-ttu-id="124d1-130">N/D</span><span class="sxs-lookup"><span data-stu-id="124d1-130">N/A</span></span> | <span data-ttu-id="124d1-131">N/D</span><span class="sxs-lookup"><span data-stu-id="124d1-131">N/A</span></span> | [<span data-ttu-id="124d1-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="124d1-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="124d1-133">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="124d1-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="124d1-134">.NET</span><span class="sxs-lookup"><span data-stu-id="124d1-134">.NET</span></span>
<span data-ttu-id="124d1-135">ecossistema do .NET Olá tem vários tempos de execução, portanto, há várias bibliotecas .NET para Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="124d1-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="124d1-136">biblioteca .NET padrão Olá pode ser executada usando o .NET Core ou saudação do .NET Framework, enquanto a biblioteca do .NET Framework Olá só pode ser executada em um ambiente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="124d1-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="124d1-137">Para saber mais sobre o .NET Framework, veja [versões da estrutura](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="124d1-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="124d1-138">Nó</span><span class="sxs-lookup"><span data-stu-id="124d1-138">Node</span></span>

<span data-ttu-id="124d1-139">biblioteca de Node. js Hello está atualmente em visualização e é mantida como um projeto por funcionários da Microsoft e colaboradores externos.</span><span class="sxs-lookup"><span data-stu-id="124d1-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="124d1-140">Todas as contribuições, incluindo código-fonte são bem-vindas e serão analisadas.</span><span class="sxs-lookup"><span data-stu-id="124d1-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="124d1-141">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="124d1-141">Management APIs</span></span>

<span data-ttu-id="124d1-142">a seguir Olá é uma lista de todas as bibliotecas específicas de gerenciamento disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="124d1-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="124d1-143">Nenhuma dessas bibliotecas contêm operações de tempo de execução e são o único propósito de saudação do gerenciamento de entidades de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="124d1-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="124d1-144">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="124d1-144">Language/Platform</span></span> | <span data-ttu-id="124d1-145">Pacote de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="124d1-145">Management package</span></span> | <span data-ttu-id="124d1-146">Repositório</span><span class="sxs-lookup"><span data-stu-id="124d1-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="124d1-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="124d1-147">.NET Standard</span></span> | [<span data-ttu-id="124d1-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="124d1-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="124d1-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="124d1-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="124d1-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="124d1-150">Next steps</span></span>
<span data-ttu-id="124d1-151">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="124d1-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="124d1-152">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="124d1-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="124d1-153">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="124d1-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="124d1-154">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="124d1-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)