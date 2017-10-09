---
title: "aaaAdd um ambiente de Azure Insights de série de tempo do evento fonte tooyour | Microsoft Docs"
description: "Neste tutorial, você se conectar a um ambiente de informações da série de tempo do evento fonte tooyour"
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
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="d7901-103">Criar uma fonte de evento para o seu ambiente de informações da série de tempo usando o portal do Ibiza Olá</span><span class="sxs-lookup"><span data-stu-id="d7901-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="d7901-104">Uma Origem de Evento da Análise de Séries Temporais é derivada de um agente de evento, como o Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7901-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="d7901-105">Informações da série de tempo se conecta diretamente fontes tooEvent, ingestão de fluxo de dados de saudação sem a necessidade dos usuários toowrite uma única linha de código.</span><span class="sxs-lookup"><span data-stu-id="d7901-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="d7901-106">Atualmente, a Análise de Séries Temporais dá suporte a Hubs de Eventos do Azure e a Hubs IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7901-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="d7901-107">Em Olá futuras, mais fontes de evento serão adicionadas.</span><span class="sxs-lookup"><span data-stu-id="d7901-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="d7901-108">Etapas tooadd um ambiente de tooyour de origem do evento</span><span class="sxs-lookup"><span data-stu-id="d7901-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="d7901-109">Entrar toohello [portal do Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7901-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="d7901-110">Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do portal do Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="d7901-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="d7901-111">Selecione o seu ambiente de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="d7901-111">Select your Time Series Insights environment.</span></span>

  ![Criar origem do evento de informações da série de tempo de saudação](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="d7901-113">Selecione "Origens de Evento", clique em "+ Adicionar".</span><span class="sxs-lookup"><span data-stu-id="d7901-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Criar fonte de evento de informações da série de tempo Olá - detalhes](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="d7901-115">Especifique o nome de saudação de origem do evento hello.</span><span class="sxs-lookup"><span data-stu-id="d7901-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="d7901-116">Esse nome é associado a todos os eventos dessa origem de evento e está disponível no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="d7901-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="d7901-117">Selecione um hub de eventos da lista de saudação de recursos do Hub de eventos na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="d7901-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="d7901-118">Caso contrário, escolha a opção de importação "configurações do Hub de eventos fornecem manualmente" toospecify um hub de eventos em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="d7901-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="d7901-119">Os eventos devem ser publicados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d7901-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="d7901-120">Selecione a política que tem permissão no hub de eventos de saudação de leitura.</span><span class="sxs-lookup"><span data-stu-id="d7901-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="d7901-121">Especifique o grupo de consumidores do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="d7901-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d7901-122">Verifique se esse grupo de consumidores não é usado por qualquer outro serviço (como um trabalho do Stream Analytics ou outro ambiente de Análise de Séries Temporais).</span><span class="sxs-lookup"><span data-stu-id="d7901-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="d7901-123">Se o grupo de consumidores é usado por outros serviços, leia a operação é afetada negativamente para esse ambiente e Olá outros serviços.</span><span class="sxs-lookup"><span data-stu-id="d7901-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="d7901-124">Se você estiver usando "$Default" como o grupo de consumidores hello, isso pode levar a reutilização de toopotential por outros leitores.</span><span class="sxs-lookup"><span data-stu-id="d7901-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="d7901-125">Clique em “Criar”.</span><span class="sxs-lookup"><span data-stu-id="d7901-125">Click “Create.”</span></span>

<span data-ttu-id="d7901-126">Após a criação da origem do evento hello, Insights de série de tempo iniciará automaticamente o fluxo de dados em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="d7901-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7901-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7901-127">Next steps</span></span>

* <span data-ttu-id="d7901-128">[Enviar eventos](time-series-insights-send-events.md) toohello origem do evento</span><span class="sxs-lookup"><span data-stu-id="d7901-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="d7901-129">Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d7901-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
