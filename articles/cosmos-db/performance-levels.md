---
title: "Níveis de desempenho da API do DocumentDB | Microsoft Docs"
description: "Saiba como os níveis de desempenho da API do DocumentDB permitem reservar a produtividade por contêiner."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d4733e57eb760dbb8e8ca96f6ba55671d1742f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="637d1-103">Desativando os níveis de desempenho S1, S2 e S3</span><span class="sxs-lookup"><span data-stu-id="637d1-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="637d1-104">Os níveis de desempenho S1, S2 e S3 abordados neste artigo estão sendo desativados e não estão mais disponíveis para novas contas da API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="637d1-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="637d1-105">Este artigo fornece uma visão geral dos níveis de desempenho S1, S2 e S3 e analisa como as coleções que usam esses níveis serão migradas para as coleções de partição única em 1º de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="637d1-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="637d1-106">Após ler este artigo, você poderá responder as perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="637d1-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="637d1-107">Por que os níveis de desempenho S1, S2 e S3 estão sendo desativados?</span><span class="sxs-lookup"><span data-stu-id="637d1-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="637d1-108">Como as coleções de partição única e as coleções particionadas se comparam com os níveis de desempenho S1, S2 e S3?</span><span class="sxs-lookup"><span data-stu-id="637d1-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="637d1-109">O que é necessário fazer para garantir o acesso ininterrupto aos meus dados?</span><span class="sxs-lookup"><span data-stu-id="637d1-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="637d1-110">Como a minha coleção mudará após a migração?</span><span class="sxs-lookup"><span data-stu-id="637d1-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="637d1-111">Como minha cobrança mudará depois que eu migrar para as coleções de partição única?</span><span class="sxs-lookup"><span data-stu-id="637d1-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="637d1-112">E se eu precisar de mais de 10 GB de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="637d1-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="637d1-113">Posso mudar entre os níveis de desempenho S1, S2 e S3 antes de 1º de agosto de 2017?</span><span class="sxs-lookup"><span data-stu-id="637d1-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="637d1-114">Como saberei quando minha coleção migrou?</span><span class="sxs-lookup"><span data-stu-id="637d1-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="637d1-115">Como eu migro dos níveis de desempenho S1, S2 e S3 para as coleções de partição única sozinho?</span><span class="sxs-lookup"><span data-stu-id="637d1-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="637d1-116">Como serei afetado se eu for um cliente EA?</span><span class="sxs-lookup"><span data-stu-id="637d1-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="637d1-117">Por que os níveis de desempenho S1, S2 e S3 estão sendo desativados?</span><span class="sxs-lookup"><span data-stu-id="637d1-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="637d1-118">Os níveis de desempenho S1, S2 e S3 não oferecem a flexibilidade que as coleções da API do DocumentDB oferecem.</span><span class="sxs-lookup"><span data-stu-id="637d1-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="637d1-119">Com os níveis de desempenho S1, S2, S3, a produtividade e a capacidade de armazenamento eram predefinidas e não ofereciam elasticidade.</span><span class="sxs-lookup"><span data-stu-id="637d1-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="637d1-120">Agora, o Azure Cosmos DB oferece a capacidade de personalizar a produtividade e o armazenamento, oferecendo muito mais flexibilidade em sua capacidade de dimensionar, conforme suas necessidades mudam.</span><span class="sxs-lookup"><span data-stu-id="637d1-120">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="637d1-121">Como as coleções de partição única e as coleções particionadas se comparam com os níveis de desempenho S1, S2 e S3?</span><span class="sxs-lookup"><span data-stu-id="637d1-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="637d1-122">A tabela a seguir compara as opções da taxa de transferência e armazenamento disponíveis nas coleções de partição única, coleções particionadas e níveis de desempenho S1, S2 e S3.</span><span class="sxs-lookup"><span data-stu-id="637d1-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="637d1-123">Aqui está um exemplo para a região no Leste dos EUA 2:</span><span class="sxs-lookup"><span data-stu-id="637d1-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="637d1-124">Coleção particionada</span><span class="sxs-lookup"><span data-stu-id="637d1-124">Partitioned collection</span></span>|<span data-ttu-id="637d1-125">Coleção de partição única</span><span class="sxs-lookup"><span data-stu-id="637d1-125">Single partition collection</span></span>|<span data-ttu-id="637d1-126">S1</span><span class="sxs-lookup"><span data-stu-id="637d1-126">S1</span></span>|<span data-ttu-id="637d1-127">S2</span><span class="sxs-lookup"><span data-stu-id="637d1-127">S2</span></span>|<span data-ttu-id="637d1-128">S3</span><span class="sxs-lookup"><span data-stu-id="637d1-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="637d1-129">Taxa de transferência máxima</span><span class="sxs-lookup"><span data-stu-id="637d1-129">Maximum throughput</span></span>|<span data-ttu-id="637d1-130">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="637d1-130">Unlimited</span></span>|<span data-ttu-id="637d1-131">10 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-131">10K RU/s</span></span>|<span data-ttu-id="637d1-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-132">250 RU/s</span></span>|<span data-ttu-id="637d1-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-133">1 K RU/s</span></span>|<span data-ttu-id="637d1-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="637d1-135">Taxa de transferência mínima</span><span class="sxs-lookup"><span data-stu-id="637d1-135">Minimum throughput</span></span>|<span data-ttu-id="637d1-136">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-136">2.5K RU/s</span></span>|<span data-ttu-id="637d1-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-137">400 RU/s</span></span>|<span data-ttu-id="637d1-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-138">250 RU/s</span></span>|<span data-ttu-id="637d1-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-139">1 K RU/s</span></span>|<span data-ttu-id="637d1-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="637d1-141">Armazenamento máximo</span><span class="sxs-lookup"><span data-stu-id="637d1-141">Maximum storage</span></span>|<span data-ttu-id="637d1-142">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="637d1-142">Unlimited</span></span>|<span data-ttu-id="637d1-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="637d1-143">10 GB</span></span>|<span data-ttu-id="637d1-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="637d1-144">10 GB</span></span>|<span data-ttu-id="637d1-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="637d1-145">10 GB</span></span>|<span data-ttu-id="637d1-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="637d1-146">10 GB</span></span>|
|<span data-ttu-id="637d1-147">Preço (mensal)</span><span class="sxs-lookup"><span data-stu-id="637d1-147">Price (monthly)</span></span>|<span data-ttu-id="637d1-148">Taxa de transferência: $ 6/100 RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="637d1-149">Armazenamento: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="637d1-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="637d1-150">Taxa de transferência: $ 6/100 RU/s</span><span class="sxs-lookup"><span data-stu-id="637d1-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="637d1-151">Armazenamento: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="637d1-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="637d1-152">$ 25 dólares americanos</span><span class="sxs-lookup"><span data-stu-id="637d1-152">$25 USD</span></span>|<span data-ttu-id="637d1-153">$ 50 dólares americanos</span><span class="sxs-lookup"><span data-stu-id="637d1-153">$50 USD</span></span>|<span data-ttu-id="637d1-154">$ 100 dólares americanos</span><span class="sxs-lookup"><span data-stu-id="637d1-154">$100 USD</span></span>|

<span data-ttu-id="637d1-155">Você é um cliente EA?</span><span class="sxs-lookup"><span data-stu-id="637d1-155">Are you an EA customer?</span></span> <span data-ttu-id="637d1-156">Se for, consulte [Como serei afetado se eu for um cliente EA?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="637d1-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="637d1-157">O que é necessário fazer para garantir o acesso ininterrupto aos meus dados?</span><span class="sxs-lookup"><span data-stu-id="637d1-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="637d1-158">Nada. O Cosmos DB cuida da migração para você.</span><span class="sxs-lookup"><span data-stu-id="637d1-158">Nothing, Cosmos DB handles the migration for you.</span></span> <span data-ttu-id="637d1-159">Se você tiver uma coleção S1, S2 ou S3, a coleção atual será migrada para uma coleção de partição única em 31 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="637d1-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="637d1-160">Como a minha coleção mudará após a migração?</span><span class="sxs-lookup"><span data-stu-id="637d1-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="637d1-161">Se você tiver uma coleção S1, será migrado para uma coleção de partição única com uma taxa de transferência de 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="637d1-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="637d1-162">400 RU/s é a taxa de transferência mais baixa disponível com as coleções de partição única.</span><span class="sxs-lookup"><span data-stu-id="637d1-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="637d1-163">No entanto, o custo de 400 RU/s em uma coleção de partição única é aproximadamente igual ao que você estava pagando com sua coleção S1 e 250 RU/s – assim, você não está pagando por 150 RU/s extras disponíveis.</span><span class="sxs-lookup"><span data-stu-id="637d1-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="637d1-164">Se você tiver uma coleção S2, será migrado para uma coleção de partição única com 1 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="637d1-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="637d1-165">Você não verá nenhuma alteração no nível da taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="637d1-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="637d1-166">Se tiver uma coleção S3, será migrado para uma coleção de partição única com 2.5 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="637d1-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="637d1-167">Você não verá nenhuma alteração no nível da taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="637d1-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="637d1-168">Em cada um desses casos, após a migração de sua coleção, você poderá personalizar o nível da taxa de transferência, aumentar ou reduzir conforme o necessário para fornecer um acesso de baixa latência para os usuários.</span><span class="sxs-lookup"><span data-stu-id="637d1-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="637d1-169">Para alterar o nível de produtividade após a migração de sua coleção, basta abrir sua conta do Cosmos DB no portal do Azure, clicar em Escala, escolher sua coleção e, em seguida, ajustar o nível de produtividade, conforme mostrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="637d1-169">To change the throughput level after your collection has migrated, simply open your Cosmos DB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![Como dimensionar a taxa de transferência no portal do Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="637d1-171">Como minha cobrança mudará depois que eu migrar para as coleções de partição única?</span><span class="sxs-lookup"><span data-stu-id="637d1-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="637d1-172">Supondo que você tem 10 coleções S1, 1 GB de armazenamento para cada uma, na região Leste dos EUA, e migra essas 10 coleções S1 para 10 coleções de partição única em 400 RU/s (o nível mínimo).</span><span class="sxs-lookup"><span data-stu-id="637d1-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="637d1-173">Se você mantiver as 10 coleções de partição única por um mês inteiro, sua fatura será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="637d1-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![Como o preço de S1 para 10 coleções se compara a 10 coleções usando o preço para uma coleção de partição única](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="637d1-175">E se eu precisar de mais de 10 GB de armazenamento?</span><span class="sxs-lookup"><span data-stu-id="637d1-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="637d1-176">Se você tiver uma coleção com um nível de desempenho S1, S2 ou S3 ou uma coleção de partição única, todas com 10 GB de armazenamento disponível, poderá usar a ferramenta de Migração de Dados do Cosmos DB para migrar seus dados para uma coleção particionada com um armazenamento praticamente ilimitado.</span><span class="sxs-lookup"><span data-stu-id="637d1-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="637d1-177">Para obter informações sobre os benefícios de uma coleção particionada, consulte [Particionamento e escala no Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="637d1-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="637d1-178">Para obter informações sobre como migrar seu S1, S2, S3 ou coleção de partição única para uma coleção particionada, consulte [Migrando da partição única para coleções particionadas](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="637d1-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="637d1-179">Posso mudar entre os níveis de desempenho S1, S2 e S3 antes de 1º de agosto de 2017?</span><span class="sxs-lookup"><span data-stu-id="637d1-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="637d1-180">Somente as contas existentes com os desempenhos S1, S2 e S3 conseguirão mudar e alterar as camadas do nível de desempenho no portal ou por meio da programação.</span><span class="sxs-lookup"><span data-stu-id="637d1-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="637d1-181">Em 1º de agosto de 2017, os níveis de desempenho S1, S2 e S3 não estarão mais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="637d1-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="637d1-182">Se você mudar de S1, S3 ou S3 para uma coleção de partição único, não será possível retornar aos níveis de desempenho S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="637d1-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="637d1-183">Como saberei quando minha coleção migrou?</span><span class="sxs-lookup"><span data-stu-id="637d1-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="637d1-184">A migração ocorrerá em 31 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="637d1-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="637d1-185">Se você tiver uma coleção que usa os níveis de desempenho S1, S2 ou S3, a equipe do Cosmos DB o contatará por email antes da migração.</span><span class="sxs-lookup"><span data-stu-id="637d1-185">If you have a collection that uses the S1, S2 or S3 performance levels, the Cosmos DB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="637d1-186">Quando a migração for concluída, em 1º de agosto de 2017, o portal do Azure mostrará que sua coleção usa o preço Standard.</span><span class="sxs-lookup"><span data-stu-id="637d1-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![Como confirmar se sua coleção migrou para a tipo de preço Standard](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="637d1-188">Como eu migro dos níveis de desempenho S1, S2 e S3 para as coleções de partição única sozinho?</span><span class="sxs-lookup"><span data-stu-id="637d1-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="637d1-189">Você pode migrar dos níveis de desempenho S1, S2 e S3 para coleções de partição única usando o portal do Azure ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="637d1-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="637d1-190">Você pode fazer isso sozinho antes de 1º de agosto para aproveitar as opções flexíveis da taxa de transferência disponíveis com as coleções de partição única ou migraremos suas coleções em 31 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="637d1-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="637d1-191">**Para migrar para coleções de partição única usando o portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="637d1-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="637d1-192">No [**portal do Azure**](https://portal.azure.com), clique em **Azure Cosmos DB** e, em seguida, selecione a conta do Cosmos DB a ser modificada.</span><span class="sxs-lookup"><span data-stu-id="637d1-192">In the [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select the Cosmos DB account to modify.</span></span> 
 
    <span data-ttu-id="637d1-193">Se o **Azure Cosmos DB** não estiver na barra de atalhos, clique em >, role até **Bancos de dados**, selecione **Azure Cosmos DB** e, em seguida, selecione a conta do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="637d1-193">If **Azure Cosmos DB** is not on the Jumpbar, click >, scroll to **Databases**, select **Azure Cosmos DB**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="637d1-194">No menu de recursos, em **Contêineres**, clique em **Escala**, selecione a coleção a ser modificada na lista suspensa e, em seguida, clique em **Tipo de Preço**.</span><span class="sxs-lookup"><span data-stu-id="637d1-194">On the resource menu, under **Containers**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="637d1-195">As contas que usam a taxa de transferência predefinida têm um tipo de preço de S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="637d1-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="637d1-196">Na folha **Escolha o tipo de preço**, clique em **Standard** para alterar a taxa de transferência definida pelo usuário e, em seguida, clique em **Selecionar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="637d1-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![Captura de tela da folha Configurações, mostrando em que lugar alterar o valor da taxa de transferência](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="637d1-198">De volta na folha **Escala**, o **Tipo de Preço** foi alterado para **Standard** e a caixa **Produtividade (RU/s)** é exibida com um valor padrão de 400.</span><span class="sxs-lookup"><span data-stu-id="637d1-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="637d1-199">Defina a produtividade entre 400 e 10.000 [Unidades de Solicitação](request-units.md)/segundo (RUS/s).</span><span class="sxs-lookup"><span data-stu-id="637d1-199">Set the throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="637d1-200">A **Fatura mensal estimada** na parte inferior da página é atualizada automaticamente para fornecer uma estimativa do custo mensal.</span><span class="sxs-lookup"><span data-stu-id="637d1-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="637d1-201">Depois de salvar as alterações e ir para o tipo de preço Standard, você não poderá voltar para os níveis de desempenho S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="637d1-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="637d1-202">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="637d1-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="637d1-203">Se determinar que precisa de uma taxa de transferência maior (mais de 10.000 RU/s) ou mais armazenamento (mais de 10 GB), você poderá criar uma coleção particionada.</span><span class="sxs-lookup"><span data-stu-id="637d1-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="637d1-204">Para migrar uma coleção de partição única para uma coleção particionada, consulte [Migrando da partição única para coleções particionadas](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="637d1-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="637d1-205">Mudar de S1, S2 ou S3 para o Standard pode levar até 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="637d1-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="637d1-206">**Para migrar para coleções de partição única usando o .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="637d1-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="637d1-207">Outra opção para alterar os níveis de desempenho de suas coleções é por meio de nossos SDKs.</span><span class="sxs-lookup"><span data-stu-id="637d1-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="637d1-208">Esta seção aborda apenas a alteração do nível de desempenho da coleção usando nossa [API .NET do DocumentDB](documentdb-sdk-dotnet.md), mas o processo é semelhante para nossos outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="637d1-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="637d1-209">Aqui está um trecho de código para mudar a taxa de transferência da coleção para 5.000 unidades de solicitação por segundo:</span><span class="sxs-lookup"><span data-stu-id="637d1-209">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="637d1-210">Visite o [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) para exibir exemplos adicionais e saber mais sobre os métodos oferecidos:</span><span class="sxs-lookup"><span data-stu-id="637d1-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="637d1-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="637d1-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="637d1-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="637d1-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="637d1-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="637d1-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="637d1-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="637d1-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="637d1-215">Como serei afetado se eu for um cliente EA?</span><span class="sxs-lookup"><span data-stu-id="637d1-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="637d1-216">Os clientes EA terão o preço protegido até o final do contrato atual.</span><span class="sxs-lookup"><span data-stu-id="637d1-216">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="637d1-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="637d1-217">Next steps</span></span>
<span data-ttu-id="637d1-218">Para saber mais sobre os preços e como gerenciar dados com o Azure Cosmos DB, conheça estes recursos:</span><span class="sxs-lookup"><span data-stu-id="637d1-218">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="637d1-219">[Particionando dados no Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="637d1-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="637d1-220">Compreenda a diferença entre contêineres de partição única e contêineres particionados, além de obter dicas de como implementar uma estratégia de particionamento para uma escala perfeita.</span><span class="sxs-lookup"><span data-stu-id="637d1-220">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="637d1-221">[Preços do Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="637d1-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="637d1-222">Saiba mais sobre o custo de provisionar a taxa de transferência e consumir o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="637d1-222">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="637d1-223">[Unidades de solicitação](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="637d1-223">[Request units](request-units.md).</span></span> <span data-ttu-id="637d1-224">Compreenda o consumo da taxa de transferência para os diferentes tipos de operação, por exemplo, Leitura, Gravação e Consulta.</span><span class="sxs-lookup"><span data-stu-id="637d1-224">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
