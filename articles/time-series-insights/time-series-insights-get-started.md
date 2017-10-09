---
title: "um ambiente do Azure Insights de série de tempo de aaaCreate | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toocreate ambiente da série de tempo, conecte-a origem do evento tooan e pronto tooanalyze seus dados de evento em minutos."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="7a773-103">Criar um novo ambiente de informações da série de tempo no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7a773-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="7a773-104">O ambiente de Análise de Séries Temporais é um recurso do Azure com capacidade de entrada e o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7a773-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="7a773-105">Os clientes provisionar ambientes via Olá portal do Azure com capacidade de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="7a773-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="7a773-106">Ambiente de saudação toocreate etapas</span><span class="sxs-lookup"><span data-stu-id="7a773-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="7a773-107">Siga estas etapas toocreate seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="7a773-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="7a773-108">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a773-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="7a773-109">Clique em hello mais sinal ("+") no hello canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="7a773-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="7a773-110">Procure "Insights de série de tempo" na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a773-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Criar ambiente de informações da série de tempo de saudação](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="7a773-112">Selecione "Análise de Séries Temporais", clique em "Criar".</span><span class="sxs-lookup"><span data-stu-id="7a773-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Criar grupo de recursos de informações da série de tempo de saudação](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="7a773-114">Especifique o nome do ambiente.</span><span class="sxs-lookup"><span data-stu-id="7a773-114">Specify environment name.</span></span> <span data-ttu-id="7a773-115">Este nome representa ambiente Olá [explorer da série de tempo](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a773-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="7a773-116">Selecione uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7a773-116">Select a subscription.</span></span> <span data-ttu-id="7a773-117">Escolha uma que contenha a sua fonte de eventos.</span><span class="sxs-lookup"><span data-stu-id="7a773-117">Choose one that contains your event source.</span></span> <span data-ttu-id="7a773-118">Informações da série de tempo pode detectar automaticamente Azure IoT Hub e recursos do Hub de eventos existentes no Olá a mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7a773-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="7a773-119">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a773-119">Select or create a resource group.</span></span> <span data-ttu-id="7a773-120">Um grupo de recursos é uma coleção de recursos do Azure que são usados juntos.</span><span class="sxs-lookup"><span data-stu-id="7a773-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="7a773-121">Selecione um local de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="7a773-121">Select a hosting location.</span></span> <span data-ttu-id="7a773-122">tooavoid mover dados entre data centers, escolha um local que contém a origem do evento.</span><span class="sxs-lookup"><span data-stu-id="7a773-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="7a773-123">Selecione um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="7a773-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="7a773-124">Selecione a capacidade.</span><span class="sxs-lookup"><span data-stu-id="7a773-124">Select capacity.</span></span> <span data-ttu-id="7a773-125">Você pode alterar a capacidade de um ambiente após a criação.</span><span class="sxs-lookup"><span data-stu-id="7a773-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="7a773-126">Crie seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="7a773-126">Create your environment.</span></span> <span data-ttu-id="7a773-127">Você também pode fixar o dashboard de toohello seu ambiente para facilitar o acesso sempre que você entrar.</span><span class="sxs-lookup"><span data-stu-id="7a773-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Criar hello toodashboard de pin de informações da série de tempo](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="7a773-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a773-129">Next steps</span></span>

* <span data-ttu-id="7a773-130">[Definir políticas de acesso de dados](time-series-insights-data-access.md) tooaccess seu ambiente no [Portal de Insights de série de tempo](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7a773-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="7a773-131">Criar uma fonte de eventos</span><span class="sxs-lookup"><span data-stu-id="7a773-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="7a773-132">[Enviar eventos](time-series-insights-send-events.md) toohello origem do evento</span><span class="sxs-lookup"><span data-stu-id="7a773-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
