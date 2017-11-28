---
title: Provisionar a produtividade do Azure Cosmos DB | Microsoft Docs
description: "Saiba como definir a produtividade provisionada para contêineres, coleções, gráficos e tabelas do Azure Cosmos DB."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="09d67-103">Definir a produtividade de contêineres do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="09d67-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="09d67-104">Você pode definir a produtividade dos contêineres do Azure Cosmos DB no portal do Azure ou usando os SDKs do cliente.</span><span class="sxs-lookup"><span data-stu-id="09d67-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="09d67-105">A tabela a seguir lista a produtividade disponível para cada contêiner:</span><span class="sxs-lookup"><span data-stu-id="09d67-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-106"><strong>Contêiner de partição única</strong></span><span class="sxs-lookup"><span data-stu-id="09d67-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-107"><strong>Contêiner particionado</strong></span><span class="sxs-lookup"><span data-stu-id="09d67-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="09d67-108">Produtividade mínima</span><span class="sxs-lookup"><span data-stu-id="09d67-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-109">400 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="09d67-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-110">2.500 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="09d67-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="09d67-111">Produtividade máxima</span><span class="sxs-lookup"><span data-stu-id="09d67-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-112">10.000 unidades de solicitação por segundo</span><span class="sxs-lookup"><span data-stu-id="09d67-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="09d67-113">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="09d67-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="09d67-114">Para definir a taxa de transferência usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="09d67-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="09d67-115">Em uma nova janela, abra o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09d67-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="09d67-116">Na barra esquerda, clique em **Azure Cosmos DB** ou em **Mais Serviços** na parte inferior, role até **Bancos de dados** e, depois, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="09d67-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="09d67-117">Selecione sua conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09d67-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="09d67-118">Na nova janela, clique em **Data Explorer (Versão prévia)** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="09d67-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="09d67-119">Na nova janela, expanda o banco de dados e o contêiner e, em seguida, clique em **Dimensionamento e Configurações**.</span><span class="sxs-lookup"><span data-stu-id="09d67-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="09d67-120">Na nova janela, digite o novo valor de produtividade na caixa **Produtividade** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="09d67-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="09d67-121">Para definir a produtividade usando a API do DocumentDB do .NET</span><span class="sxs-lookup"><span data-stu-id="09d67-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="09d67-122">Perguntas frequentes sobre taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="09d67-122">Throughput FAQ</span></span>

<span data-ttu-id="09d67-123">**Posso definir minha taxa de transferência com valor menor que 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="09d67-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="09d67-124">400 RU/s é a produtividade mínima disponível em coleções de partição única do Cosmos DB (2500 RU/s é o mínimo para coleções particionadas).</span><span class="sxs-lookup"><span data-stu-id="09d67-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="09d67-125">Unidades de solicitação são definidas em intervalos de 100 RU/s, mas a taxa de transferência não pode ser definida como 100 RU/s ou qualquer valor menor que 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="09d67-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="09d67-126">Se você estiver procurando um método econômico para desenvolver e testar o Cosmos DB, poderá usar o [Emulador do Azure Cosmos DB](local-emulator.md) gratuito, que pode ser implantado localmente sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="09d67-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="09d67-127">**Como defino a produtividade usando a API do MongoDB?**</span><span class="sxs-lookup"><span data-stu-id="09d67-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="09d67-128">Não há nenhuma extensão de API do MongoDB para definir a produtividade.</span><span class="sxs-lookup"><span data-stu-id="09d67-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="09d67-129">A recomendação é usar a API do DocumentDB, conforme mostrado em [Para definir a produtividade usando a API do DocumentDB para .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="09d67-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09d67-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09d67-130">Next steps</span></span>

<span data-ttu-id="09d67-131">Para saber mais sobre o provisionamento e atingir uma escala mundial com o Cosmos DB, consulte [Particionamento e escala com o Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="09d67-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
