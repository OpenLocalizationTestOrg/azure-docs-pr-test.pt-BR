---
title: "O que fazer no caso de uma interrupção de serviço do Azure afetar o Cofre de Chaves do Azure | Microsoft Docs"
description: "Saiba o que fazer no caso de uma interrupção de serviço do Azure afetar o Cofre de Chaves do Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="69178-103">Redundância e disponibilidade de Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="69178-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="69178-104">O Cofre de Chaves do Azure tem várias camadas de redundância, a fim de garantir que seus segredos e chaves permaneçam disponíveis para seu aplicativo até mesmo se os componentes individuais do serviço falharem.</span><span class="sxs-lookup"><span data-stu-id="69178-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="69178-105">O conteúdo de seu cofre de chaves é replicado na região e em uma região secundária a pelo menos 150 milhas de distância, mas na mesma região geográfica.</span><span class="sxs-lookup"><span data-stu-id="69178-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="69178-106">Isso mantém a alta durabilidade de seus segredos e chaves.</span><span class="sxs-lookup"><span data-stu-id="69178-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="69178-107">Consulte o documento [Regiões emparelhadas do Azure](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) para obter detalhes sobre pares de regiões específicos.</span><span class="sxs-lookup"><span data-stu-id="69178-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="69178-108">Se os componentes individuais dentro do serviço de cofre de chaves falharem, os componentes alternativos dentro da região interferirão para atender à sua solicitação, de modo a garantir que não haja degradação da funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="69178-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="69178-109">Você não precisa executar qualquer ação para disparar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="69178-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="69178-110">Ele ocorre automaticamente de modo transparente para você.</span><span class="sxs-lookup"><span data-stu-id="69178-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="69178-111">No eventual caso de uma região inteira do Azure ficar indisponível, as solicitações que você faz do Cofre de Chaves do Azure nessa região são roteadas automaticamente (*failover*) para uma região secundária.</span><span class="sxs-lookup"><span data-stu-id="69178-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="69178-112">Quando a região primária estiver disponível novamente, as solicitações serão roteadas de volta (*failback*) para a região primária.</span><span class="sxs-lookup"><span data-stu-id="69178-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="69178-113">Novamente, não é necessário executar nenhuma ação, pois isso acontecerá de modo automático.</span><span class="sxs-lookup"><span data-stu-id="69178-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="69178-114">Há algumas advertências que você deve conhecer:</span><span class="sxs-lookup"><span data-stu-id="69178-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="69178-115">No caso de um failover de região, pode levar alguns minutos para o serviço executar failover.</span><span class="sxs-lookup"><span data-stu-id="69178-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="69178-116">Solicitações feitas durante esse período podem falhar até que o failover seja concluído.</span><span class="sxs-lookup"><span data-stu-id="69178-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="69178-117">Após a conclusão de um failover, o cofre de chaves estará no modo somente leitura.</span><span class="sxs-lookup"><span data-stu-id="69178-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="69178-118">As solicitações permitidas nesse modo são:</span><span class="sxs-lookup"><span data-stu-id="69178-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="69178-119">Listar cofres de chave</span><span class="sxs-lookup"><span data-stu-id="69178-119">List key vaults</span></span>
  * <span data-ttu-id="69178-120">Obter propriedades de cofres de chave</span><span class="sxs-lookup"><span data-stu-id="69178-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="69178-121">Listar segredos</span><span class="sxs-lookup"><span data-stu-id="69178-121">List secrets</span></span>
  * <span data-ttu-id="69178-122">Obter segredos</span><span class="sxs-lookup"><span data-stu-id="69178-122">Get secrets</span></span>
  * <span data-ttu-id="69178-123">Listar chaves</span><span class="sxs-lookup"><span data-stu-id="69178-123">List keys</span></span>
  * <span data-ttu-id="69178-124">Obter (propriedades das) chaves</span><span class="sxs-lookup"><span data-stu-id="69178-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="69178-125">Criptografar</span><span class="sxs-lookup"><span data-stu-id="69178-125">Encrypt</span></span>
  * <span data-ttu-id="69178-126">Descriptografar</span><span class="sxs-lookup"><span data-stu-id="69178-126">Decrypt</span></span>
  * <span data-ttu-id="69178-127">Encapsular</span><span class="sxs-lookup"><span data-stu-id="69178-127">Wrap</span></span>
  * <span data-ttu-id="69178-128">Desencapsular</span><span class="sxs-lookup"><span data-stu-id="69178-128">Unwrap</span></span>
  * <span data-ttu-id="69178-129">Verificar</span><span class="sxs-lookup"><span data-stu-id="69178-129">Verify</span></span>
  * <span data-ttu-id="69178-130">Assinar</span><span class="sxs-lookup"><span data-stu-id="69178-130">Sign</span></span>
  * <span data-ttu-id="69178-131">Backup</span><span class="sxs-lookup"><span data-stu-id="69178-131">Backup</span></span>
* <span data-ttu-id="69178-132">Após o failback de um failover, todos os tipos de solicitação (ou seja, solicitações de leitura *e* de gravação) são disponibilizados.</span><span class="sxs-lookup"><span data-stu-id="69178-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

