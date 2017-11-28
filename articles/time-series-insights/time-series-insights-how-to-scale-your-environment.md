---
title: "aaaHow tooscale seu ambiente do Azure Insights de série de tempo | Microsoft Docs"
description: "Este tutorial aborda como tooscale seu ambiente do Azure Insights de série de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="e2df3-103">Como tooscale seu ambiente de informações da série de tempo</span><span class="sxs-lookup"><span data-stu-id="e2df3-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="e2df3-104">Este tutorial aborda como tooscale seu ambiente de informações da série de tempo.</span><span class="sxs-lookup"><span data-stu-id="e2df3-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="e2df3-105">Escalar verticalmente os tipos de sku não é permitido.</span><span class="sxs-lookup"><span data-stu-id="e2df3-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="e2df3-106">Um ambiente com um Sku S1 não pode ser convertido em um ambiente de S2.</span><span class="sxs-lookup"><span data-stu-id="e2df3-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="e2df3-107">As taxas e as capacidades de entrada de SKU S1</span><span class="sxs-lookup"><span data-stu-id="e2df3-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="e2df3-108">Capacidade de SKU S1</span><span class="sxs-lookup"><span data-stu-id="e2df3-108">S1 SKU Capacity</span></span> | <span data-ttu-id="e2df3-109">Taxa de entrada</span><span class="sxs-lookup"><span data-stu-id="e2df3-109">Ingress Rate</span></span> | <span data-ttu-id="e2df3-110">Capacidade de armazenamento máxima</span><span class="sxs-lookup"><span data-stu-id="e2df3-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="e2df3-111">1</span><span class="sxs-lookup"><span data-stu-id="e2df3-111">1</span></span> | <span data-ttu-id="e2df3-112">1 GB (1 milhão de eventos)</span><span class="sxs-lookup"><span data-stu-id="e2df3-112">1 GB (1 million events)</span></span> | <span data-ttu-id="e2df3-113">30 GB (30 milhões de eventos) por mês</span><span class="sxs-lookup"><span data-stu-id="e2df3-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="e2df3-114">10</span><span class="sxs-lookup"><span data-stu-id="e2df3-114">10</span></span> | <span data-ttu-id="e2df3-115">10 GB (10 milhões de eventos)</span><span class="sxs-lookup"><span data-stu-id="e2df3-115">10 GB (10 million events)</span></span> | <span data-ttu-id="e2df3-116">300 GB (300 milhões de eventos) por mês</span><span class="sxs-lookup"><span data-stu-id="e2df3-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="e2df3-117">As taxas e as capacidades de entrada de SKU S2</span><span class="sxs-lookup"><span data-stu-id="e2df3-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="e2df3-118">Capacidade de SKU S2</span><span class="sxs-lookup"><span data-stu-id="e2df3-118">S2 SKU Capacity</span></span> | <span data-ttu-id="e2df3-119">Taxa de entrada</span><span class="sxs-lookup"><span data-stu-id="e2df3-119">Ingress Rate</span></span> | <span data-ttu-id="e2df3-120">Capacidade de armazenamento máxima</span><span class="sxs-lookup"><span data-stu-id="e2df3-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="e2df3-121">1</span><span class="sxs-lookup"><span data-stu-id="e2df3-121">1</span></span> | <span data-ttu-id="e2df3-122">10 GB (10 milhões de eventos)</span><span class="sxs-lookup"><span data-stu-id="e2df3-122">10 GB (10 million events)</span></span> | <span data-ttu-id="e2df3-123">300 GB (300 milhões de eventos) por mês</span><span class="sxs-lookup"><span data-stu-id="e2df3-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="e2df3-124">10</span><span class="sxs-lookup"><span data-stu-id="e2df3-124">10</span></span> | <span data-ttu-id="e2df3-125">100 GB (100 milhões de eventos)</span><span class="sxs-lookup"><span data-stu-id="e2df3-125">100 GB (100 million events)</span></span> | <span data-ttu-id="e2df3-126">3 TB (3 bilhões de eventos) por mês</span><span class="sxs-lookup"><span data-stu-id="e2df3-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="e2df3-127">As capacidades são dimensionadas linearmente, portanto, uma sku S1 com capacidade 2 dá suporte a 2 GB (2 milhões) de eventos por taxa de entrada por dia e 60 GB (60 milhões de eventos) por mês.</span><span class="sxs-lookup"><span data-stu-id="e2df3-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="e2df3-128">Alterando a capacidade de saudação do seu ambiente</span><span class="sxs-lookup"><span data-stu-id="e2df3-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="e2df3-129">No portal do Azure de Olá, selecione Olá ambiente cuja capacidade deseja toochange.</span><span class="sxs-lookup"><span data-stu-id="e2df3-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="e2df3-130">Em Configurações, clique em Configurar.</span><span class="sxs-lookup"><span data-stu-id="e2df3-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="e2df3-131">Use Olá capacidade controle deslizante tooselect Olá capacidade que atenda aos requisitos de saudação para suas taxas de entrada e a capacidade de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2df3-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2df3-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2df3-132">Next steps</span></span>

* <span data-ttu-id="e2df3-133">Verifique se que a nova capacidade de saudação é suficiente tooprevent limitação.</span><span class="sxs-lookup"><span data-stu-id="e2df3-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="e2df3-134">Para obter mais detalhes, consulte Olá *seu ambiente pode ser ser limitado* seção [aqui](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="e2df3-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
