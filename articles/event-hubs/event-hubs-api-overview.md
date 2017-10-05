---
title: "Visão geral da API dos Hubs de Eventos do Azure | Microsoft Docs"
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
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="e5268-103">APIs de Hubs de Eventos disponíveis</span><span class="sxs-lookup"><span data-stu-id="e5268-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="e5268-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="e5268-104">Runtime APIs</span></span>

<span data-ttu-id="e5268-105">Veja a seguir uma descrição de todos os clientes de tempo de execução dos Hubs de Eventos do Azure atualmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e5268-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="e5268-106">Embora algumas dessas bibliotecas também incluem a funcionalidade de gerenciamento limitado, também há [bibliotecas específicas](#management-apis) dedicada às operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="e5268-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="e5268-107">O foco principal dessas bibliotecas é enviar e receber mensagens de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5268-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="e5268-108">Veja [informações adicionais](#additional-information) para obter mais detalhes sobre o status atual de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e5268-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="e5268-109">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="e5268-109">Language/Platform</span></span> | <span data-ttu-id="e5268-110">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="e5268-110">Client package</span></span> | <span data-ttu-id="e5268-111">Pacote EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e5268-111">EventProcessorHost package</span></span> | <span data-ttu-id="e5268-112">Repositório</span><span class="sxs-lookup"><span data-stu-id="e5268-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5268-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="e5268-113">.NET Standard</span></span> | [<span data-ttu-id="e5268-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="e5268-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="e5268-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="e5268-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="e5268-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="e5268-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="e5268-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="e5268-117">.NET Framework</span></span> | [<span data-ttu-id="e5268-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="e5268-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="e5268-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="e5268-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="e5268-120">N/D</span><span class="sxs-lookup"><span data-stu-id="e5268-120">N/A</span></span> |
| <span data-ttu-id="e5268-121">Java</span><span class="sxs-lookup"><span data-stu-id="e5268-121">Java</span></span> | [<span data-ttu-id="e5268-122">Maven</span><span class="sxs-lookup"><span data-stu-id="e5268-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="e5268-123">Maven</span><span class="sxs-lookup"><span data-stu-id="e5268-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="e5268-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="e5268-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="e5268-125">Nó</span><span class="sxs-lookup"><span data-stu-id="e5268-125">Node</span></span> | [<span data-ttu-id="e5268-126">NPM</span><span class="sxs-lookup"><span data-stu-id="e5268-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="e5268-127">N/D</span><span class="sxs-lookup"><span data-stu-id="e5268-127">N/A</span></span> | [<span data-ttu-id="e5268-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="e5268-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="e5268-129">C</span><span class="sxs-lookup"><span data-stu-id="e5268-129">C</span></span> | <span data-ttu-id="e5268-130">N/D</span><span class="sxs-lookup"><span data-stu-id="e5268-130">N/A</span></span> | <span data-ttu-id="e5268-131">N/D</span><span class="sxs-lookup"><span data-stu-id="e5268-131">N/A</span></span> | [<span data-ttu-id="e5268-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="e5268-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="e5268-133">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="e5268-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="e5268-134">.NET</span><span class="sxs-lookup"><span data-stu-id="e5268-134">.NET</span></span>
<span data-ttu-id="e5268-135">O ecossistema do .NET tem vários tempos de execução, portanto, há várias bibliotecas .NET de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="e5268-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="e5268-136">A biblioteca .NET Standard pode ser executada usando o .NET Core ou o .NET Framework, enquanto a biblioteca do .NET Framework só pode ser executada em um ambiente do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e5268-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="e5268-137">Para saber mais sobre o .NET Framework, veja [versões da estrutura](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="e5268-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="e5268-138">Nó</span><span class="sxs-lookup"><span data-stu-id="e5268-138">Node</span></span>

<span data-ttu-id="e5268-139">A biblioteca do Node. js está atualmente em visualização e é mantida como um projeto de lado por funcionários da Microsoft e colaboradores externos.</span><span class="sxs-lookup"><span data-stu-id="e5268-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="e5268-140">Todas as contribuições, incluindo código-fonte são bem-vindas e serão analisadas.</span><span class="sxs-lookup"><span data-stu-id="e5268-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="e5268-141">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e5268-141">Management APIs</span></span>

<span data-ttu-id="e5268-142">A seguir está uma lista de todas as bibliotecas específicas de gerenciamento disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="e5268-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="e5268-143">Nenhuma dessas bibliotecas contém operações de tempo de execução e elas têm o único propósito de gerenciar as entidades de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="e5268-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="e5268-144">Linguagem/plataforma</span><span class="sxs-lookup"><span data-stu-id="e5268-144">Language/Platform</span></span> | <span data-ttu-id="e5268-145">Pacote de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e5268-145">Management package</span></span> | <span data-ttu-id="e5268-146">Repositório</span><span class="sxs-lookup"><span data-stu-id="e5268-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5268-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="e5268-147">.NET Standard</span></span> | [<span data-ttu-id="e5268-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="e5268-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="e5268-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="e5268-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="e5268-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5268-150">Next steps</span></span>
<span data-ttu-id="e5268-151">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="e5268-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e5268-152">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="e5268-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e5268-153">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e5268-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e5268-154">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="e5268-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)