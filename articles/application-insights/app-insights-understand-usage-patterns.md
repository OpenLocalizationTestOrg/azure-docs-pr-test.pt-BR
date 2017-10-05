---
title: Funis do Azure Application Insights
description: "Saiba como você pode usar Funis para descobrir como os clientes estão interagindo com seu aplicativo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="0dcc4-103">Descobrir como os clientes estão usando seu aplicativo com os Funis do Application Insights</span><span class="sxs-lookup"><span data-stu-id="0dcc4-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="0dcc4-104">Entender a experiência do cliente é de extrema importância para seus negócios.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="0dcc4-105">Se o aplicativo envolver vários estágios, você precisará saber se a maioria dos clientes está progredindo por todo o processo ou se eles estão encerrando o processo em algum momento.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="0dcc4-106">A progressão por uma série de etapas em um aplicativo Web é conhecida como “funil”.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="0dcc4-107">Use os Funis do Application Insights para obter informações sobre os usuários e monitorar as taxas de conversão passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="0dcc4-108">Introdução à folha Funis</span><span class="sxs-lookup"><span data-stu-id="0dcc4-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="0dcc4-109">A maneira mais fácil de saber mais sobre os Funis é acompanhar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="0dcc4-110">As ilustrações a seguir demonstram as etapas que os proprietários de uma empresa de comércio eletrônico realizarão para saber como seus clientes interagem com seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="0dcc4-111">Criar o funil</span><span class="sxs-lookup"><span data-stu-id="0dcc4-111">Create your funnel</span></span>
<span data-ttu-id="0dcc4-112">Antes de criar o funil, você precisa decidir qual pergunta você deseja responder.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="0dcc4-113">Por exemplo, talvez você deseje saber quantos clientes que exibem a home page clicam em um anúncio.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="0dcc4-114">Neste exemplo, os proprietários da empresa Fabrikam Fiber desejam saber o percentual de clientes que fazem uma compra depois de adicionar itens ao carrinho de compras durante o mês passado.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="0dcc4-115">Estas são as etapas que eles realizam para criar seu funil.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="0dcc4-116">Clique no botão Novo na folha Funis.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="0dcc4-117">Selecione o intervalo de tempo “Mês passado” na lista suspensa **Intervalo de Tempo**.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="0dcc4-118">Selecione o evento **Página do produto** na lista suspensa **Etapa 1**.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="0dcc4-119">Selecione o evento **Adicionar ao carrinho de compras** na lista suspensa **Etapa 2**.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="0dcc4-120">Selecione o evento **Clicar em Comprar** na lista suspensa **Etapa 3**.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="0dcc4-121">Adicione um nome ao funil e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="0dcc4-122">A ilustração a seguir demonstra os dados gerados na folha Funis.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="0dcc4-123">Nessa folha, os proprietários da Fabrikam podem ver que, durante a última semana, 22,7% de seus clientes que adicionaram um item ao carrinho de compras concluíram a compra.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="0dcc4-124">Eles também podem ver que 1% dos clientes clicou em um anúncio antes de visitar a página do produto e que 20% de seus clientes saíram do site depois de concluírem a compra.</span><span class="sxs-lookup"><span data-stu-id="0dcc4-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Folha Funis com os dados](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="0dcc4-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dcc4-126">Next steps</span></span>
- <span data-ttu-id="0dcc4-127">Saiba mais sobre a [análise de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dcc4-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
