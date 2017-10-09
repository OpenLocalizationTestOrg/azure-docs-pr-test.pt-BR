---
title: "aaaAzure SDK .NET do DocumentDB alteração Feed processador & recursos | Microsoft Docs"
description: "Saiba tudo sobre Olá API do processador de Feed de alteração e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello SDK .NET do DocumentDB alteração Feed processador."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="19ab6-103">SDK do processador do feed de alterações do .NET no DocumentDB: download e notas de versão</span><span class="sxs-lookup"><span data-stu-id="19ab6-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19ab6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="19ab6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="19ab6-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="19ab6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="19ab6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="19ab6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="19ab6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="19ab6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="19ab6-108">Java</span><span class="sxs-lookup"><span data-stu-id="19ab6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="19ab6-109">Python</span><span class="sxs-lookup"><span data-stu-id="19ab6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="19ab6-110">REST</span><span class="sxs-lookup"><span data-stu-id="19ab6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="19ab6-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="19ab6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="19ab6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="19ab6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="19ab6-113">**Baixe o SDK**</span><span class="sxs-lookup"><span data-stu-id="19ab6-113">**SDK download**</span></span></td><td>[<span data-ttu-id="19ab6-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="19ab6-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="19ab6-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="19ab6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="19ab6-116">Alterar a documentação de referência de API da biblioteca do Processador de Feed</span><span class="sxs-lookup"><span data-stu-id="19ab6-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="19ab6-117">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="19ab6-117">**Get started**</span></span></td><td>[<span data-ttu-id="19ab6-118">Introdução ao Olá alteração Feed processador SDK do DocumentDB .NET</span><span class="sxs-lookup"><span data-stu-id="19ab6-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="19ab6-119">**Framework atualmente com suporte**</span><span class="sxs-lookup"><span data-stu-id="19ab6-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="19ab6-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="19ab6-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="19ab6-121">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="19ab6-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="19ab6-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="19ab6-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="19ab6-123">Adicionado um método tooobtain uma estimativa do restante toobe de trabalho processado em Olá Feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="19ab6-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="19ab6-124">Compatível com o [SDK do .NET para DocumentDB](documentdb-sdk-dotnet.md) versões 1.13.2 e superiores.</span><span class="sxs-lookup"><span data-stu-id="19ab6-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="19ab6-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="19ab6-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="19ab6-126">SDK DO GA</span><span class="sxs-lookup"><span data-stu-id="19ab6-126">GA SDK</span></span>
* <span data-ttu-id="19ab6-127">Compatível com [SDK do .NET do DocumentDB](documentdb-sdk-dotnet.md) versões 1.14.1 e inferiores.</span><span class="sxs-lookup"><span data-stu-id="19ab6-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="19ab6-128">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="19ab6-128">Release & Retirement dates</span></span>
<span data-ttu-id="19ab6-129">A Microsoft fornecerá notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.</span><span class="sxs-lookup"><span data-stu-id="19ab6-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="19ab6-130">Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.</span><span class="sxs-lookup"><span data-stu-id="19ab6-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="19ab6-131">TooCosmos qualquer solicitação usando um SDK obsoleto do banco de dados serão rejeitados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="19ab6-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="19ab6-132">Versão</span><span class="sxs-lookup"><span data-stu-id="19ab6-132">Version</span></span> | <span data-ttu-id="19ab6-133">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="19ab6-133">Release Date</span></span> | <span data-ttu-id="19ab6-134">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="19ab6-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="19ab6-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="19ab6-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="19ab6-136">13 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="19ab6-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="19ab6-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="19ab6-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="19ab6-138">07 de julho de 2017</span><span class="sxs-lookup"><span data-stu-id="19ab6-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="19ab6-139">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="19ab6-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="19ab6-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="19ab6-140">See also</span></span>
<span data-ttu-id="19ab6-141">toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.</span><span class="sxs-lookup"><span data-stu-id="19ab6-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

