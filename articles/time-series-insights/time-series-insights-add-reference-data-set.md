---
title: "Adicione um conjunto de dados de referência ao ambiente de Análise de Séries Temporais do Azure | Microsoft Docs"
description: "Neste tutorial, você deve adicionar o conjunto de dados de referência ao seu ambiente de Análise de Séries Temporais"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="8bee9-103">Criar um conjunto de dados de referência para o seu ambiente de Análise de Séries Temporais usando o portal do Ibiza</span><span class="sxs-lookup"><span data-stu-id="8bee9-103">Create a reference data set for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="8bee9-104">Um conjunto de dados de referência é uma coleção de itens que são aumentados com os eventos da fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="8bee9-104">A Reference Data Set is a collection of items that are augmented with the events from your event source.</span></span> <span data-ttu-id="8bee9-105">O mecanismo de entrada da Análise de Séries Temporais une um evento da fonte de evento a um item em seu conjunto de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="8bee9-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="8bee9-106">Esse evento aumentado é disponibilizado para consulta.</span><span class="sxs-lookup"><span data-stu-id="8bee9-106">This augmented event is then available for query.</span></span> <span data-ttu-id="8bee9-107">Essa junção baseia-se nas chaves definidas no conjunto de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="8bee9-107">This join is based on the keys defined in your reference data set.</span></span>

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a><span data-ttu-id="8bee9-108">Etapas para adicionar um conjunto de dados de referência ao seu ambiente</span><span class="sxs-lookup"><span data-stu-id="8bee9-108">Steps to add a reference data set to your environment</span></span>

1. <span data-ttu-id="8bee9-109">Entre no [portal do Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bee9-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8bee9-110">Clique em "Todos os recursos" no menu à esquerda do portal do Ibiza.</span><span class="sxs-lookup"><span data-stu-id="8bee9-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3. <span data-ttu-id="8bee9-111">Selecione o seu ambiente de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="8bee9-111">Select your Time Series Insights environment.</span></span>

    ![Criar o conjunto de dados de referência Análises de Séries Temporais](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="8bee9-113">Selecione "Conjuntos de dados de referência" e clique em "+ Adicionar".</span><span class="sxs-lookup"><span data-stu-id="8bee9-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Criar o conjunto de dados de referência Análises de Séries Temporais - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="8bee9-115">Especifique o nome do conjunto de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="8bee9-115">Specify the name of the reference data set.</span></span>
6. <span data-ttu-id="8bee9-116">Especifique o nome da chave e seu tipo.</span><span class="sxs-lookup"><span data-stu-id="8bee9-116">Specify the key name and its type.</span></span> <span data-ttu-id="8bee9-117">Esse nome e o tipo são usados para selecionar a propriedade correta do evento na fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="8bee9-117">This name and type is used to pick the correct property from the event in your event source.</span></span> <span data-ttu-id="8bee9-118">Por exemplo, se você fornecer o nome da chave como "DeviceId" e digitar como "String", em seguida, o mecanismo de entrada da Análise de Séries Temporais procurará uma propriedade com o nome "DeviceId" do tipo "String" no evento de entrada.</span><span class="sxs-lookup"><span data-stu-id="8bee9-118">For instance, if you provide key name as “DeviceId” and type as “String”, then the Time Series Insights ingress engine looks for a property with the name “DeviceId” of type “String” in the incoming event.</span></span> <span data-ttu-id="8bee9-119">Você pode fornecer mais de uma chave para unir ao evento.</span><span class="sxs-lookup"><span data-stu-id="8bee9-119">You can provide more than one key to join with the event.</span></span> <span data-ttu-id="8bee9-120">A correspondência de nome de propriedade diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8bee9-120">The property name match is case-sensitive.</span></span>

     ![Criar o conjunto de dados de referência Análises de Séries Temporais - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="8bee9-122">Clique em “Criar”.</span><span class="sxs-lookup"><span data-stu-id="8bee9-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bee9-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8bee9-123">Next steps</span></span>

* <span data-ttu-id="8bee9-124">[Gerenciar dados de referência](time-series-insights-manage-reference-data-csharp.md) programaticamente.</span><span class="sxs-lookup"><span data-stu-id="8bee9-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="8bee9-125">Para obter a referência completa de API, confira o documento [API de Dados de Referência](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api).</span><span class="sxs-lookup"><span data-stu-id="8bee9-125">For the complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>