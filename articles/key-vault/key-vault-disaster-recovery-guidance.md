---
title: "toodo aaaWhat no evento de saudação de uma interrupção de serviço do Azure que afeta o Cofre de chaves do Azure | Microsoft Docs"
description: "Saiba quais toodo no evento de saudação de uma interrupção de serviço do Azure que afeta o Cofre de chaves do Azure."
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="e7594-103">Redundância e disponibilidade de Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="e7594-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="e7594-104">Cofre de chaves do Azure apresenta várias camadas de redundância toomake se suas chaves e segredos permanecem disponíveis tooyour aplicativo mesmo se os componentes individuais do hello serviço falhar.</span><span class="sxs-lookup"><span data-stu-id="e7594-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="e7594-105">Olá conteúdo de seu Cofre de chaves é replicado dentro Olá regiões e tooa secundário, pelo menos, 150 milhas imediatamente, mas dentro de saudação mesmo Geografia.</span><span class="sxs-lookup"><span data-stu-id="e7594-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="e7594-106">Isso mantém a alta durabilidade de seus segredos e chaves.</span><span class="sxs-lookup"><span data-stu-id="e7594-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="e7594-107">Consulte Olá [Azure emparelhado regiões](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) documento para obter detalhes sobre os pares de região específica.</span><span class="sxs-lookup"><span data-stu-id="e7594-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="e7594-108">Se os componentes individuais no serviço de Cofre de chaves Olá falharem, componentes alternativos na região Olá etapa na tooserve seu toomake solicitação se não há nenhuma degradação de funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="e7594-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="e7594-109">Você não precisa tootake tootrigger qualquer ação isso.</span><span class="sxs-lookup"><span data-stu-id="e7594-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="e7594-110">Ela ocorre automaticamente e será tooyou transparente.</span><span class="sxs-lookup"><span data-stu-id="e7594-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="e7594-111">No evento raro Olá que toda a uma região do Azure está disponível, Olá solicitações feitas de Cofre de chaves do Azure nessa região são roteadas automaticamente (*failover*) região secundária tooa.</span><span class="sxs-lookup"><span data-stu-id="e7594-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="e7594-112">Quando a região primária Olá esteja disponível novamente, as solicitações são roteadas novamente (*falha volta*) região primária toohello.</span><span class="sxs-lookup"><span data-stu-id="e7594-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="e7594-113">Novamente, não é necessário tootake qualquer ação porque isso ocorre automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7594-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="e7594-114">Há alguns toobe de advertências atento:</span><span class="sxs-lookup"><span data-stu-id="e7594-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="e7594-115">Evento de saudação de um failover de região, levará alguns minutos para Olá serviço toofail.</span><span class="sxs-lookup"><span data-stu-id="e7594-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="e7594-116">As solicitações feitas durante esse tempo podem falhar até a conclusão do failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7594-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="e7594-117">Após a conclusão de um failover, o cofre de chaves estará no modo somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e7594-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="e7594-118">As solicitações permitidas nesse modo são:</span><span class="sxs-lookup"><span data-stu-id="e7594-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="e7594-119">Listar cofres de chave</span><span class="sxs-lookup"><span data-stu-id="e7594-119">List key vaults</span></span>
  * <span data-ttu-id="e7594-120">Obter propriedades de cofres de chave</span><span class="sxs-lookup"><span data-stu-id="e7594-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="e7594-121">Listar segredos</span><span class="sxs-lookup"><span data-stu-id="e7594-121">List secrets</span></span>
  * <span data-ttu-id="e7594-122">Obter segredos</span><span class="sxs-lookup"><span data-stu-id="e7594-122">Get secrets</span></span>
  * <span data-ttu-id="e7594-123">Listar chaves</span><span class="sxs-lookup"><span data-stu-id="e7594-123">List keys</span></span>
  * <span data-ttu-id="e7594-124">Obter (propriedades das) chaves</span><span class="sxs-lookup"><span data-stu-id="e7594-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="e7594-125">Criptografar</span><span class="sxs-lookup"><span data-stu-id="e7594-125">Encrypt</span></span>
  * <span data-ttu-id="e7594-126">Descriptografar</span><span class="sxs-lookup"><span data-stu-id="e7594-126">Decrypt</span></span>
  * <span data-ttu-id="e7594-127">Encapsular</span><span class="sxs-lookup"><span data-stu-id="e7594-127">Wrap</span></span>
  * <span data-ttu-id="e7594-128">Desencapsular</span><span class="sxs-lookup"><span data-stu-id="e7594-128">Unwrap</span></span>
  * <span data-ttu-id="e7594-129">Verificar</span><span class="sxs-lookup"><span data-stu-id="e7594-129">Verify</span></span>
  * <span data-ttu-id="e7594-130">Assinar</span><span class="sxs-lookup"><span data-stu-id="e7594-130">Sign</span></span>
  * <span data-ttu-id="e7594-131">Backup</span><span class="sxs-lookup"><span data-stu-id="e7594-131">Backup</span></span>
* <span data-ttu-id="e7594-132">Após o failback de um failover, todos os tipos de solicitação (ou seja, solicitações de leitura *e* de gravação) são disponibilizados.</span><span class="sxs-lookup"><span data-stu-id="e7594-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

