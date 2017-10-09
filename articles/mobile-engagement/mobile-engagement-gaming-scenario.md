---
title: "implementação do Mobile Engagement aaaAzure para o aplicativo de jogos"
description: "Jogos tooimplement de cenário de aplicativo do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="108fc-103">Implementar o Mobile Engagement com o Aplicativo de Jogos</span><span class="sxs-lookup"><span data-stu-id="108fc-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="108fc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="108fc-104">Overview</span></span>
<span data-ttu-id="108fc-105">Uma empresa de jogos em fase inicial lançou um novo aplicativo de jogo de pescar baseado em role-play/estratégia.</span><span class="sxs-lookup"><span data-stu-id="108fc-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="108fc-106">jogo Olá foi ligado e em execução por 6 meses.</span><span class="sxs-lookup"><span data-stu-id="108fc-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="108fc-107">Este jogo é um enorme sucesso e tem milhões de downloads e retenção de saudação é muito alta tooother comparados inicialização jogo aplicativos.</span><span class="sxs-lookup"><span data-stu-id="108fc-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="108fc-108">Reunião de revisão trimestral hello, participantes concordam que precisam tooincrease a receita média por usuário (ARPU).</span><span class="sxs-lookup"><span data-stu-id="108fc-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="108fc-109">Pacotes de jogo premium estão disponíveis como ofertas especiais.</span><span class="sxs-lookup"><span data-stu-id="108fc-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="108fc-110">Esses pacotes de jogos permitem a aparência de saudação tooupgrade usuários e o desempenho de suas linhas de pesca e iscas ou soluciona em jogo hello.</span><span class="sxs-lookup"><span data-stu-id="108fc-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="108fc-111">No entanto, as vendas dos pacotes são muito baixas.</span><span class="sxs-lookup"><span data-stu-id="108fc-111">However, package sales are very low.</span></span> <span data-ttu-id="108fc-112">Para que eles decidirem tooanalyze Prezado cliente primeira experiência com uma ferramenta de análise e, em seguida, toodevelop um contrato programa tooincrease vendas usando avançados de segmentação.</span><span class="sxs-lookup"><span data-stu-id="108fc-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="108fc-113">Com base em Olá [Azure Mobile Engagement - guia de Introdução com as práticas recomendadas](mobile-engagement-getting-started-best-practices.md) que criam uma estratégia de contrato.</span><span class="sxs-lookup"><span data-stu-id="108fc-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="108fc-114">Objetivos e KPIs</span><span class="sxs-lookup"><span data-stu-id="108fc-114">Objectives and KPIs</span></span>
<span data-ttu-id="108fc-115">Atender às principais partes interessadas para jogo hello.</span><span class="sxs-lookup"><span data-stu-id="108fc-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="108fc-116">Todos têm um objetivo principal - vendas de pacote tooincrease premium 15%.</span><span class="sxs-lookup"><span data-stu-id="108fc-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="108fc-117">Criar unidade e negócios indicadores chave de desempenho (KPIs) toomeasure esse objetivo</span><span class="sxs-lookup"><span data-stu-id="108fc-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="108fc-118">Em que nível de jogo Olá esses pacotes são comprados?</span><span class="sxs-lookup"><span data-stu-id="108fc-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="108fc-119">O que é a receita Olá por usuário, sessão, semana e por mês?</span><span class="sxs-lookup"><span data-stu-id="108fc-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="108fc-120">Quais são os tipos de compra favorito de Olá?</span><span class="sxs-lookup"><span data-stu-id="108fc-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="108fc-121">Parte 1 de saudação [guia de Introdução](mobile-engagement-getting-started-best-practices.md) explica como toodefine Olá objetivos e KPIs.</span><span class="sxs-lookup"><span data-stu-id="108fc-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="108fc-122">Com hello que KPIs da empresa agora estão definidos, Olá Mobile produto Manager cria KPIs contrato toodetermine novas tendências de usuário e de retenção.</span><span class="sxs-lookup"><span data-stu-id="108fc-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="108fc-123">Monitorar a retenção e use em Olá intervalos a seguir: diariamente, cada 2 dias, semanal, mensal e a cada 3 meses</span><span class="sxs-lookup"><span data-stu-id="108fc-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="108fc-124">Contagens de usuários ativos</span><span class="sxs-lookup"><span data-stu-id="108fc-124">Active user counts</span></span>
* <span data-ttu-id="108fc-125">classificação do aplicativo Hello em Olá armazenar</span><span class="sxs-lookup"><span data-stu-id="108fc-125">hello app rating in hello store</span></span>

<span data-ttu-id="108fc-126">Com base nas recomendações da equipe de TI do hello, Olá KPIs técnicas a seguir foram adicionada Olá tooanswer perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="108fc-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="108fc-127">Qual é o caminho do meu usuário (qual página é visitada, quanto tempo os usuários passam nela)</span><span class="sxs-lookup"><span data-stu-id="108fc-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="108fc-128">Número de falhas ou erros encontrados por sessão</span><span class="sxs-lookup"><span data-stu-id="108fc-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="108fc-129">Quais versões de sistema operacional meus usuários estão executando?</span><span class="sxs-lookup"><span data-stu-id="108fc-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="108fc-130">O que é o tamanho médio de saudação da tela para meus usuários?</span><span class="sxs-lookup"><span data-stu-id="108fc-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="108fc-131">Que tipo de conectividade com a Internet meus usuários têm?</span><span class="sxs-lookup"><span data-stu-id="108fc-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="108fc-132">Para cada KPI Olá Mobile produto Manager Especifica dados de saudação precisa e onde ele está localizado em sua guia estratégico.</span><span class="sxs-lookup"><span data-stu-id="108fc-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="108fc-133">Integração e programa de envolvimento</span><span class="sxs-lookup"><span data-stu-id="108fc-133">Engagement program and integration</span></span>
<span data-ttu-id="108fc-134">Antes de criar um programa de contrato avançado, Olá diretor de projeto Mobile responsável por projeto Olá deve ter uma profunda compreensão de como e quando os produtos são consumidos por usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="108fc-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="108fc-135">Depois de 3 meses, Olá diretor de projeto Mobile coletou suficiente tooenhance dados suas vendas de notificação no aplicativo de envio.</span><span class="sxs-lookup"><span data-stu-id="108fc-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="108fc-136">Ele descobre que:</span><span class="sxs-lookup"><span data-stu-id="108fc-136">He learns that:</span></span>

* <span data-ttu-id="108fc-137">primeira compra de saudação geralmente ocorre em nível de saudação 14.</span><span class="sxs-lookup"><span data-stu-id="108fc-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="108fc-138">Para 90% dos casos, a compra Olá é armas lendária novo para $3.</span><span class="sxs-lookup"><span data-stu-id="108fc-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="108fc-139">Em 80% dos casos, os usuários que compraram, continue com o produto hello e fazer mais compras.</span><span class="sxs-lookup"><span data-stu-id="108fc-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="108fc-140">Os usuários que foram aprovadas nível Olá 20, iniciar toospend mais de US $10/ semana.</span><span class="sxs-lookup"><span data-stu-id="108fc-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="108fc-141">Os usuários tendem a pacotes de premium toobuy no nível 16, 24 e 32.</span><span class="sxs-lookup"><span data-stu-id="108fc-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="108fc-142">Obrigado analysis toothis Olá diretor de projeto Mobile decide toocreate push específico notificação sequências tooincrease nas vendas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="108fc-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="108fc-143">Ele cria três sequências de push que ele chama de: Programa de Boas-vindas, Programa de Vendas e o Programa Inativo.</span><span class="sxs-lookup"><span data-stu-id="108fc-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="108fc-144">Para obter mais informações, consulte toohello [Guias estratégicos](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="108fc-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
