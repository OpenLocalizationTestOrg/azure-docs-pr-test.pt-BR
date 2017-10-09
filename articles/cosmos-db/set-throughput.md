---
title: "taxa de transferência aaaProvision para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooset provisionados taxa de transferência para seu banco de dados do Azure Cosmos containsers coleções, gráficos e tabelas."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="211b8-103">Definir a produtividade de contêineres do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="211b8-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="211b8-104">Você pode definir a taxa de transferência para os contêineres de banco de dados do Azure Cosmos Olá portal do Azure ou usando Olá SDKs de cliente.</span><span class="sxs-lookup"><span data-stu-id="211b8-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="211b8-105">Olá a tabela a seguir lista a taxa de transferência Olá disponível para os contêineres:</span><span class="sxs-lookup"><span data-stu-id="211b8-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-106"><strong>Contêiner de partição única</strong></span><span class="sxs-lookup"><span data-stu-id="211b8-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-107"><strong>Contêiner particionado</strong></span><span class="sxs-lookup"><span data-stu-id="211b8-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="211b8-108">Produtividade mínima</span><span class="sxs-lookup"><span data-stu-id="211b8-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-109">400 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="211b8-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-110">2.500 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="211b8-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="211b8-111">Produtividade máxima</span><span class="sxs-lookup"><span data-stu-id="211b8-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-112">10.000 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="211b8-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="211b8-113">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="211b8-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="211b8-114">taxa de transferência tooset hello usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="211b8-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="211b8-115">Em uma nova janela, abra Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="211b8-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="211b8-116">Na barra de saudação à esquerda, clique em **o banco de dados do Azure Cosmos**, ou clique em **mais serviços** na parte inferior do hello, role muito**bancos de dados**e, em seguida, clique em **banco de dados do Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="211b8-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="211b8-117">Selecione sua conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="211b8-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="211b8-118">Na nova janela de hello, clique em **Gerenciador de dados (visualização)** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="211b8-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="211b8-119">Na nova janela de hello, expanda o banco de dados e o contêiner e, em seguida, clique em **configurações de escala &**.</span><span class="sxs-lookup"><span data-stu-id="211b8-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="211b8-120">Na nova janela de hello, digite o novo valor de taxa de transferência hello, em Olá **taxa de transferência** caixa e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="211b8-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="211b8-121">taxa de transferência tooset hello usando Olá API DocumentDB para .NET</span><span class="sxs-lookup"><span data-stu-id="211b8-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="211b8-122">Perguntas frequentes sobre taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="211b8-122">Throughput FAQ</span></span>

<span data-ttu-id="211b8-123">**Posso configurar meu tooless de taxa de transferência de 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="211b8-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="211b8-124">400 RU/s é Olá taxa de transferência mínima disponível em coleções de partição única de banco de dados do Cosmos (2500 RU/s é Olá mínimo para as coleções particionadas).</span><span class="sxs-lookup"><span data-stu-id="211b8-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="211b8-125">Solicitação de unidades são definidas em intervalos de 100 RU/s, mas a taxa de transferência não é possível definir too100 RU/s ou qualquer valor menor do que 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="211b8-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="211b8-126">Se você estiver procurando por um método econômico toodevelop e Cosmos banco de dados de teste, você pode usar o hello livre [emulador de banco de dados do Azure Cosmos](local-emulator.md), que pode ser implantado localmente, sem nenhum custo.</span><span class="sxs-lookup"><span data-stu-id="211b8-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="211b8-127">**Como definir o througput usando Olá MongoDB API?**</span><span class="sxs-lookup"><span data-stu-id="211b8-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="211b8-128">Não há nenhuma taxa de transferência do MongoDB API extensão tooset.</span><span class="sxs-lookup"><span data-stu-id="211b8-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="211b8-129">Olá recomendação é toouse hello API DocumentDB, conforme mostrado no [tooset taxa de transferência de saudação usando Olá API DocumentDB para .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="211b8-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="211b8-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="211b8-130">Next steps</span></span>

<span data-ttu-id="211b8-131">toolearn mais sobre o provisionamento e escala planeta contínuo com Cosmos DB, consulte [particionamento e o dimensionamento com o banco de dados do Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="211b8-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
