---
title: "Definir e gerenciar o estado nos microsserviços do Azure | Microsoft Docs"
description: "Como definir e gerenciar o estado do serviço na malha de serviço"
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
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="c526d-103">Estado do serviço</span><span class="sxs-lookup"><span data-stu-id="c526d-103">Service state</span></span>
<span data-ttu-id="c526d-104">**Estado do serviço** refere-se aos dados em disco ou na memória que um serviço requer para funcionar.</span><span class="sxs-lookup"><span data-stu-id="c526d-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="c526d-105">Inclui, por exemplo, as estruturas de dados e variáveis de membro que o serviço lê e grava para realizar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c526d-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="c526d-106">Dependendo de como o serviço é estruturado, também pode incluir arquivos ou outros recursos armazenados em disco.</span><span class="sxs-lookup"><span data-stu-id="c526d-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="c526d-107">Por exemplo, os arquivos que um banco de dados usaria para armazenar dados e logs de transação.</span><span class="sxs-lookup"><span data-stu-id="c526d-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="c526d-108">Como um exemplo de serviço, vamos considerar uma calculadora.</span><span class="sxs-lookup"><span data-stu-id="c526d-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="c526d-109">Um serviço de calculadora básica pega dois números e retorna sua soma.</span><span class="sxs-lookup"><span data-stu-id="c526d-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="c526d-110">Executar este cálculo não envolve nenhuma variável de membro ou outras informações.</span><span class="sxs-lookup"><span data-stu-id="c526d-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="c526d-111">Agora, considere a mesma calculadora, mas com um método adicional para armazenar e retornar a última soma computada.</span><span class="sxs-lookup"><span data-stu-id="c526d-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="c526d-112">Agora, trata-se de um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="c526d-112">This service is now stateful.</span></span> <span data-ttu-id="c526d-113">Com estado significa que ele contém algum estado no qual grava quando calcula uma nova soma e do qual lê quando você solicita que ele retorne a última soma calculada.</span><span class="sxs-lookup"><span data-stu-id="c526d-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="c526d-114">No Service Fabric do Azure, o primeiro serviço é chamado de serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="c526d-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="c526d-115">O segundo serviço é chamado de serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="c526d-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="c526d-116">Armazenando o estado do serviço</span><span class="sxs-lookup"><span data-stu-id="c526d-116">Storing service state</span></span>
<span data-ttu-id="c526d-117">O estado pode ser externalizado ou localizado em conjunto com o código que está manipulando o estado.</span><span class="sxs-lookup"><span data-stu-id="c526d-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="c526d-118">Normalmente, a externalização do estado é feita usando um banco de dados externo ou outro armazenamento de dados que é executado em máquinas diferentes na rede ou fora do processo no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="c526d-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="c526d-119">Em nosso exemplo da calculadora, o armazenamento de dados poderia ser uma um banco de dados SQL ou uma instância do Armazenamento de Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="c526d-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="c526d-120">Cada solicitação para calcular a soma executa uma atualização desses dados e solicitações para o serviço retornar o valor fazem com que o valor atual seja buscado no repositório.</span><span class="sxs-lookup"><span data-stu-id="c526d-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="c526d-121">O estado também pode ser localizado com o código que manipula o estado.</span><span class="sxs-lookup"><span data-stu-id="c526d-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="c526d-122">Serviços com estado no Service Fabric normalmente são criados usando esse modelo.</span><span class="sxs-lookup"><span data-stu-id="c526d-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="c526d-123">O Service Fabric fornece a infraestrutura para garantir que esse estado seja altamente disponível, consistente e durável e que serviços criados dessa maneira possam ser dimensionados com facilidade.</span><span class="sxs-lookup"><span data-stu-id="c526d-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c526d-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c526d-124">Next steps</span></span>
<span data-ttu-id="c526d-125">Para saber mais sobre os conceitos do Service Fabric, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c526d-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="c526d-126">Disponibilidade dos serviços de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="c526d-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="c526d-127">Escalabilidade de serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="c526d-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="c526d-128">Particionando serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="c526d-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="c526d-129">Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c526d-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
