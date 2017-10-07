---
title: "ambiente do Azure Insights de série de tempo do aaaAdd Referência conjunto de dados tooyour | Microsoft Docs"
description: "Neste tutorial, você adiciona o ambiente de informações da série de tempo de tooyour de conjunto de dados de referência"
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
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="2e86a-103">Criar um conjunto de dados de referência para o seu ambiente de informações da série de tempo usando o portal do Ibiza Olá</span><span class="sxs-lookup"><span data-stu-id="2e86a-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="2e86a-104">Um conjunto de dados de referência é uma coleção de itens que são aumentados com eventos de saudação da fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="2e86a-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="2e86a-105">O mecanismo de entrada da Análise de Séries Temporais une um evento da fonte de evento a um item em seu conjunto de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="2e86a-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="2e86a-106">Esse evento aumentado é disponibilizado para consulta.</span><span class="sxs-lookup"><span data-stu-id="2e86a-106">This augmented event is then available for query.</span></span> <span data-ttu-id="2e86a-107">Essa junção for baseada em chaves de saudação definidas em seu conjunto de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="2e86a-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="2e86a-108">Etapas tooadd um ambiente de tooyour do conjunto de dados de referência</span><span class="sxs-lookup"><span data-stu-id="2e86a-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="2e86a-109">Entrar toohello [portal do Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e86a-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e86a-110">Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do portal do Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="2e86a-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="2e86a-111">Selecione o seu ambiente de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="2e86a-111">Select your Time Series Insights environment.</span></span>

    ![Criar conjunto de dados de referência de informações da série de tempo de saudação](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="2e86a-113">Selecione "Conjuntos de dados de referência" e clique em "+ Adicionar".</span><span class="sxs-lookup"><span data-stu-id="2e86a-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Criar conjunto de dados de referência de informações da série de tempo de saudação - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="2e86a-115">Especifique o nome de Olá Olá referência do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="2e86a-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="2e86a-116">Especifique o nome da chave hello e seu tipo.</span><span class="sxs-lookup"><span data-stu-id="2e86a-116">Specify hello key name and its type.</span></span> <span data-ttu-id="2e86a-117">Este nome e o tipo é toopick usado Olá correto da propriedade de evento Olá na fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="2e86a-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="2e86a-118">Por exemplo, se você fornecer o nome da chave como "DeviceId" e digite como "String", em seguida, Olá Insights de série de tempo mecanismo de entrada procura uma propriedade com nome hello "DeviceId" do tipo "Cadeia de caracteres" no evento de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="2e86a-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="2e86a-119">Você pode fornecer mais de um toojoin chave evento hello.</span><span class="sxs-lookup"><span data-stu-id="2e86a-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="2e86a-120">correspondência de nome de propriedade Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2e86a-120">hello property name match is case-sensitive.</span></span>

     ![Criar conjunto de dados de referência de informações da série de tempo de saudação - detalhes](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="2e86a-122">Clique em “Criar”.</span><span class="sxs-lookup"><span data-stu-id="2e86a-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e86a-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e86a-123">Next steps</span></span>

* <span data-ttu-id="2e86a-124">[Gerenciar dados de referência](time-series-insights-manage-reference-data-csharp.md) programaticamente.</span><span class="sxs-lookup"><span data-stu-id="2e86a-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="2e86a-125">Para obter referência de API completa hello, consulte [API de dados de referência](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.</span><span class="sxs-lookup"><span data-stu-id="2e86a-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
