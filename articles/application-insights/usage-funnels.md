---
title: aaaAzure Funis do Application Insights
description: "Saiba como você pode usar os Funis toodiscover como os clientes estão interagindo com o seu aplicativo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 2a6125cf596570cfaee30bb3ff757916e90d7676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="31784-103">Descobrir como os clientes estão usando o seu aplicativo com hello Funis do Application Insights</span><span class="sxs-lookup"><span data-stu-id="31784-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="31784-104">Experiência do cliente compreensão é de negócios de tooyour tem importância hello.</span><span class="sxs-lookup"><span data-stu-id="31784-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="31784-105">Se seu aplicativo envolve várias etapas, você precisará tooknow se a maioria dos clientes que estão em andamento por meio de todo o processo de hello, ou se eles são encerrar o processo de saudação em algum momento.</span><span class="sxs-lookup"><span data-stu-id="31784-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="31784-106">progressão Olá por meio de uma série de etapas em um aplicativo web é conhecido como um funil"".</span><span class="sxs-lookup"><span data-stu-id="31784-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="31784-107">Você pode usar o hello Application Insights Funis toogain aprofundar-se os usuários e as taxas de conversão de passo a passo do monitor.</span><span class="sxs-lookup"><span data-stu-id="31784-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="31784-108">Introdução à folha de Funis Olá</span><span class="sxs-lookup"><span data-stu-id="31784-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="31784-109">Olá toolearn de maneira mais fácil sobre os Funis é toowalk, embora um exemplo.</span><span class="sxs-lookup"><span data-stu-id="31784-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="31784-110">Olá ilustrações a seguir demonstram os proprietários de etapas de saudação de uma empresa de comércio eletrônico levaria toolearn como os clientes interagem com seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="31784-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="31784-111">Criar o funil</span><span class="sxs-lookup"><span data-stu-id="31784-111">Create your funnel</span></span>
<span data-ttu-id="31784-112">Antes de criar o funil, é necessário toodecide na pergunta Olá deseja tooanswer.</span><span class="sxs-lookup"><span data-stu-id="31784-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="31784-113">Por exemplo, convém tooknow quantos clientes exibindo o página inicial, clique em um anúncio.</span><span class="sxs-lookup"><span data-stu-id="31784-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="31784-114">Neste exemplo, proprietários de saudação do hello da empresa de fibra Fabrikam deseja tooknow percentual de saudação de clientes que fazer uma compra depois da adição de itens tootheir carrinho de compras durante a saudação no último mês.</span><span class="sxs-lookup"><span data-stu-id="31784-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="31784-115">Aqui estão Olá etapas que levam toocreate seu funil.</span><span class="sxs-lookup"><span data-stu-id="31784-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="31784-116">Clique em novo botão Olá na folha de Funis hello.</span><span class="sxs-lookup"><span data-stu-id="31784-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="31784-117">Selecione intervalo de tempo de saudação do "Mês passado" hello **intervalo de tempo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="31784-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="31784-118">Selecione Olá **página** eventos de saudação **etapa 1** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="31784-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="31784-119">Selecione Olá **adicionar tooshopping carrinho** eventos de saudação **etapa 2** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="31784-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="31784-120">Selecione Olá **clique em comprar** eventos de saudação **etapa 3** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="31784-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="31784-121">Adicionar um funil de toohello nome e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="31784-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="31784-122">Olá ilustração a seguir demonstra gera Olá dados Olá Funis folha.</span><span class="sxs-lookup"><span data-stu-id="31784-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="31784-123">Olá aqui Fabrikam proprietários podem ver que, durante a saudação última semana, 22,7% de seus clientes que adicionou um item de compras de tootheir Carrinho compra Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="31784-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="31784-124">Eles também podem ver que 1% dos clientes Olá clicado um anúncio para que visitar a página de produto hello e 20% de seus clientes desconectados depois de concluir a compra.</span><span class="sxs-lookup"><span data-stu-id="31784-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Folha Funis com os dados](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="31784-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31784-126">Next steps</span></span>
  * [<span data-ttu-id="31784-127">Visão geral do uso</span><span class="sxs-lookup"><span data-stu-id="31784-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="31784-128">Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="31784-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="31784-129">Retenção</span><span class="sxs-lookup"><span data-stu-id="31784-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="31784-130">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="31784-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="31784-131">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="31784-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
