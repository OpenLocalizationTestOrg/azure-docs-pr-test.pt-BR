---
title: "Gerenciador de estado confiável do Azure Service Fabric e elementos internos de Coleções Confiáveis | Microsoft Docs"
description: "Aprofunde-se nos conceitos e design de coleções confiáveis no Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="3b299-103">Gerenciador de Estado Confiável do Azure Service Fabric e elementos internos de Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="3b299-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="3b299-104">Este documento se aprofunda no Gerenciador de Estado Confiável e Coleções Confiáveis para ver como os componentes principais funcionam nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="3b299-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="3b299-105">Este documento é um trabalho em andamento.</span><span class="sxs-lookup"><span data-stu-id="3b299-105">This document is work in-progress.</span></span> <span data-ttu-id="3b299-106">Adicione comentários a este artigo e diga-nos sobre qual tópico você gostaria de saber mais.</span><span class="sxs-lookup"><span data-stu-id="3b299-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="3b299-107">Modelo de persistência local: ponto de verificação e de log</span><span class="sxs-lookup"><span data-stu-id="3b299-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="3b299-108">O Gerenciador de Estado Confiável e as Coleções Confiáveis seguem um modelo de persistência chamado Log e Ponto de Verificação.</span><span class="sxs-lookup"><span data-stu-id="3b299-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="3b299-109">Nesse modelo, cada alteração de estado é registrada primeiro no disco e, em seguida, aplicada na memória.</span><span class="sxs-lookup"><span data-stu-id="3b299-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="3b299-110">O estado de conclusão em si é persistido apenas ocasionalmente (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="3b299-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="3b299-111">ponto de verificação).</span><span class="sxs-lookup"><span data-stu-id="3b299-111">Checkpoint).</span></span>
<span data-ttu-id="3b299-112">O benefício é que deltas são transformados em gravações sequenciais somente de acréscimo em disco para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="3b299-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="3b299-113">Para entender melhor o modelo de Log e Ponto de verificação, primeiro vamos analisar o cenário de disco infinito.</span><span class="sxs-lookup"><span data-stu-id="3b299-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="3b299-114">O Gerenciador de Estado Confiável registra cada operação antes que ela seja replicada.</span><span class="sxs-lookup"><span data-stu-id="3b299-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="3b299-115">O registro em log permite que as Coleções Confiáveis apliquem a operação somente na memória.</span><span class="sxs-lookup"><span data-stu-id="3b299-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="3b299-116">Já que os logs são persistidos, mesmo quando a réplica falha e precisa ser reiniciada, o Gerenciador de Estado Confiável tem informações suficientes em seu log para repetir todas as operações que a réplica perdeu.</span><span class="sxs-lookup"><span data-stu-id="3b299-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="3b299-117">Como o disco é infinito, registros de log nunca precisam ser removidos e a Coleção Confiável precisa apenas gerenciar o estado na memória.</span><span class="sxs-lookup"><span data-stu-id="3b299-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="3b299-118">Agora vamos examinar o cenário de disco finito.</span><span class="sxs-lookup"><span data-stu-id="3b299-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="3b299-119">Os registros do log se acumulam, o Gerenciador de Estado Confiável ficará sem espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="3b299-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="3b299-120">Antes que isso ocorra, o Gerenciador de Estado Confiável precisa truncar seu log para liberar espaço para os registros mais recentes.</span><span class="sxs-lookup"><span data-stu-id="3b299-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="3b299-121">O Gerenciador de Estado Confiável solicita às Coleções Confiáveis que criem, em disco, um ponto de verificação do seu estado na memória.</span><span class="sxs-lookup"><span data-stu-id="3b299-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="3b299-122">Neste ponto, as Coleções Confiáveis persistiririam seu estado na memória.</span><span class="sxs-lookup"><span data-stu-id="3b299-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="3b299-123">Depois que as Coleções Confiáveis concluírem seus pontos de verificação, o Gerenciador de Estado Confiável poderá truncar o log para liberar espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="3b299-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="3b299-124">Quando a réplica precisa ser reiniciada, as Coleções Confiáveis recuperam seu estado com ponto de verificação e o Gerenciador de Estado Confiável recupera e reproduz todas as alterações de estado que ocorreram desde o último ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="3b299-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="3b299-125">A adição de outro valor de ponto de verificação aprimora os tempos de recuperação em cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="3b299-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="3b299-126">O log contém todas as operações que ocorreram desde o último ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="3b299-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="3b299-127">Portanto, ele pode incluir várias versões de um item, tal como vários valores para uma determinada linha no Dicionário Confiável.</span><span class="sxs-lookup"><span data-stu-id="3b299-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="3b299-128">Em contraste, uma Coleção Confiável grava em pontos de verificação somente a versão mais recente de cada valor de uma chave.</span><span class="sxs-lookup"><span data-stu-id="3b299-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b299-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b299-129">Next steps</span></span>
* [<span data-ttu-id="3b299-130">Transações e Bloqueios</span><span class="sxs-lookup"><span data-stu-id="3b299-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

