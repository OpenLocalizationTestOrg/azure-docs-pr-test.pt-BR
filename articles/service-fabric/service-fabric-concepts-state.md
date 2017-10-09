---
title: aaaDefinine e gerenciar o estado no Azure microservices | Microsoft Docs
description: "Como toodefine e gerenciar o estado do serviço no Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="dc716-103">Estado do serviço</span><span class="sxs-lookup"><span data-stu-id="dc716-103">Service state</span></span>
<span data-ttu-id="dc716-104">**Estado do serviço** refere-se toohello na memória ou nos dados de disco, um serviço requer toofunction.</span><span class="sxs-lookup"><span data-stu-id="dc716-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="dc716-105">Ele inclui, por exemplo, estruturas de dados hello e variáveis de membro desse serviço Olá lê e grava toodo trabalho.</span><span class="sxs-lookup"><span data-stu-id="dc716-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="dc716-106">Dependendo de como o serviço Olá é desenvolvido, também pode incluir arquivos ou outros recursos que são armazenados no disco.</span><span class="sxs-lookup"><span data-stu-id="dc716-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="dc716-107">Por exemplo, Olá arquivos de um banco de dados usaria toostore dados e logs de transação.</span><span class="sxs-lookup"><span data-stu-id="dc716-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="dc716-108">Como um exemplo de serviço, vamos considerar uma calculadora.</span><span class="sxs-lookup"><span data-stu-id="dc716-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="dc716-109">Um serviço de calculadora básica pega dois números e retorna sua soma.</span><span class="sxs-lookup"><span data-stu-id="dc716-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="dc716-110">Executar este cálculo não envolve nenhuma variável de membro ou outras informações.</span><span class="sxs-lookup"><span data-stu-id="dc716-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="dc716-111">Agora considere Olá Calculadora mesmo, mas com um método adicional para armazenar e retornando soma última Olá ele calculado.</span><span class="sxs-lookup"><span data-stu-id="dc716-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="dc716-112">Agora, trata-se de um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="dc716-112">This service is now stateful.</span></span> <span data-ttu-id="dc716-113">Monitoração de estado significa que contém algum estado que ele grava toowhen, ele calcula uma soma de novo e lê a partir quando você pedir sum calculado do tooreturn Olá último.</span><span class="sxs-lookup"><span data-stu-id="dc716-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="dc716-114">No Azure Service Fabric, o primeiro serviço de saudação é chamado de serviço sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="dc716-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="dc716-115">segundo serviço de saudação é chamado de serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="dc716-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="dc716-116">Armazenando o estado do serviço</span><span class="sxs-lookup"><span data-stu-id="dc716-116">Storing service state</span></span>
<span data-ttu-id="dc716-117">Estado pode ser externalizado ou colocalizado com o código de saudação que é manipular o estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc716-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="dc716-118">Externalização de estado geralmente é feita usando um banco de dados externo ou outros dados de repositório que é executado em máquinas diferentes pela rede hello ou fora do processo em Olá mesma máquina.</span><span class="sxs-lookup"><span data-stu-id="dc716-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="dc716-119">Em nosso exemplo de cálculo, Olá repositório de dados pode ser uma instância de armazenamento de tabela do Azure ou o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="dc716-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="dc716-120">Soma de saudação de toocompute cada solicitação executa uma atualização de dados e solicitações toohello serviço tooreturn Olá valor resultam no valor atual de saudação sendo buscada no repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc716-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="dc716-121">Estado também pode ser colocalizado com o código de saudação que manipula o estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc716-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="dc716-122">Serviços com estado no Service Fabric normalmente são criados usando esse modelo.</span><span class="sxs-lookup"><span data-stu-id="dc716-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="dc716-123">Malha do serviço fornece Olá tooensure de infraestrutura que esse estado é altamente disponível, consistente e duráveis e serviços Olá criado dessa maneira pode dimensionar com facilidade.</span><span class="sxs-lookup"><span data-stu-id="dc716-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc716-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc716-124">Next steps</span></span>
<span data-ttu-id="dc716-125">Para obter mais informações sobre os conceitos de malha do serviço, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc716-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="dc716-126">Disponibilidade dos serviços de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="dc716-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="dc716-127">Escalabilidade de serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="dc716-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="dc716-128">Particionando serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="dc716-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="dc716-129">Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dc716-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
