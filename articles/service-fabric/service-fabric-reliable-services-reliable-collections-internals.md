---
title: "aaaAzure recursos internos do Gerenciador de estado confiável do serviço de malha e coleção confiável | Microsoft Docs"
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="c613c-103">Gerenciador de Estado Confiável do Azure Service Fabric e elementos internos de Coleções Confiáveis</span><span class="sxs-lookup"><span data-stu-id="c613c-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="c613c-104">Este documento se aprofunda dentro do Gerenciador de estado confiável e coleções confiável toosee como componentes principais do trabalham em segundo plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="c613c-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="c613c-105">Este documento é um trabalho em andamento.</span><span class="sxs-lookup"><span data-stu-id="c613c-105">This document is work in-progress.</span></span> <span data-ttu-id="c613c-106">Adicionar comentários toothis artigo tootell nos quais tópico você gostaria que toolearn mais sobre.</span><span class="sxs-lookup"><span data-stu-id="c613c-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="c613c-107">Modelo de persistência local: ponto de verificação e de log</span><span class="sxs-lookup"><span data-stu-id="c613c-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="c613c-108">Olá Gerenciador de estado confiável e coleções confiável seguem um modelo de persistência que é chamado de ponto de verificação e de Log.</span><span class="sxs-lookup"><span data-stu-id="c613c-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="c613c-109">Nesse modelo, cada alteração de estado é registrada primeiro no disco e, em seguida, aplicada na memória.</span><span class="sxs-lookup"><span data-stu-id="c613c-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="c613c-110">Olá estado completa em si é mantido somente ocasionalmente (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="c613c-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="c613c-111">ponto de verificação).</span><span class="sxs-lookup"><span data-stu-id="c613c-111">Checkpoint).</span></span>
<span data-ttu-id="c613c-112">benefício de saudação é que os deltas são transformados em sequenciais somente de acréscimo gravações em disco para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="c613c-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="c613c-113">toobetter entender hello Log e o modelo de ponto de verificação, vejamos primeiro cenário de saudação de disco infinito.</span><span class="sxs-lookup"><span data-stu-id="c613c-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="c613c-114">Olá Gerenciador de estado confiável registra cada operação antes que seja replicada.</span><span class="sxs-lookup"><span data-stu-id="c613c-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="c613c-115">Log permite que a operação de Olá Olá coleções confiável tooapply apenas na memória.</span><span class="sxs-lookup"><span data-stu-id="c613c-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="c613c-116">Desde que os logs são mantidos, mesmo quando a réplica Olá falha e precisa toobe reiniciado, Olá Gerenciador de estado confiável tem informações suficientes em seu log tooreplay todas as operações de saudação réplica Olá perdeu.</span><span class="sxs-lookup"><span data-stu-id="c613c-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="c613c-117">Como disco Olá é infinito, registros de log nunca precisam ter toobe removido e coleção confiável hello precisa estado do toomanage somente Olá na memória.</span><span class="sxs-lookup"><span data-stu-id="c613c-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="c613c-118">Agora vamos dar uma olhada no cenário de saudação de disco finito.</span><span class="sxs-lookup"><span data-stu-id="c613c-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="c613c-119">Como registros de log acumulam, Olá Gerenciador de estado confiável será executado sem espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="c613c-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="c613c-120">Antes que ocorram, Olá Gerenciador de estado confiável precisa tootruncate da sala de toomake de log para os registros mais recentes hello.</span><span class="sxs-lookup"><span data-stu-id="c613c-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="c613c-121">Solicitações do Gerenciador de estado confiável Olá coleções confiável toocheckpoint toodisk seu estado na memória.</span><span class="sxs-lookup"><span data-stu-id="c613c-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="c613c-122">Neste ponto, Olá coleções confiável persistir estado na memória.</span><span class="sxs-lookup"><span data-stu-id="c613c-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="c613c-123">Depois de coleções confiável Olá concluir seus pontos de verificação, Olá Gerenciador de estado confiável pode truncar Olá log toofree espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="c613c-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="c613c-124">Quando a réplica Olá precisa toobe reiniciado, coleções confiável recuperar seu estado de ponto de verificação e hello Gerenciador de estado confiável recupera e reproduz todas as alterações de estado de saudação que ocorreram desde o último ponto de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c613c-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="c613c-125">A adição de outro valor de ponto de verificação aprimora os tempos de recuperação em cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="c613c-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="c613c-126">Log contém todas as operações que ocorreram desde o último ponto de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c613c-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="c613c-127">Portanto, ele pode incluir várias versões de um item, tal como vários valores para uma determinada linha no Dicionário Confiável.</span><span class="sxs-lookup"><span data-stu-id="c613c-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="c613c-128">Por outro lado, pontos de verificação um conjunto confiável Olá somente a versão mais recente de cada valor de uma chave.</span><span class="sxs-lookup"><span data-stu-id="c613c-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c613c-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c613c-129">Next steps</span></span>
* [<span data-ttu-id="c613c-130">Transações e Bloqueios</span><span class="sxs-lookup"><span data-stu-id="c613c-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

