---
title: "Olá aaaSet backup e use a API de recomendações de aprendizado de máquina | Microsoft Docs"
description: "API de RECOMENDAÇÕES da Microsoft criada com as perguntas Frequentes do Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="6fb67-103">Perguntas frequentes sobre configuração e uso da API de Recomendações do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6fb67-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="6fb67-104">**O que são as RECOMENDAÇÕES?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="6fb67-105">Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="6fb67-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="6fb67-106">Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe.</span><span class="sxs-lookup"><span data-stu-id="6fb67-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="6fb67-107">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="6fb67-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="6fb67-108">Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="6fb67-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="6fb67-109">Para organizações e empresas que dependem de venda toocross recomendações e a venda produtos e clientes de tootheir de serviços, as recomendações no aprendizado de máquina do Azure fornece um mecanismo de recomendações de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="6fb67-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="6fb67-110">É uma implementação de filtragem  colaborativa que usa a fatoração de matriz como seu algoritmo central.</span><span class="sxs-lookup"><span data-stu-id="6fb67-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="6fb67-111">Os desenvolvedores de aplicativos podem acessar RECOMENDAÇÕES usando APIs REST.</span><span class="sxs-lookup"><span data-stu-id="6fb67-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="6fb67-112">**O que posso fazer com as RECOMENDAÇÕES?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="6fb67-113">RECOMENDAÇÕES utiliza como entrada um item ou um conjunto de itens e retorna uma lista de recomendações relevantes.</span><span class="sxs-lookup"><span data-stu-id="6fb67-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="6fb67-114">Por exemplo: um cliente de uma loja online clica em um produto.</span><span class="sxs-lookup"><span data-stu-id="6fb67-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="6fb67-115">loja online Olá envia esse produto como entrada tooRECOMMENDATIONS, obtém uma lista de produtos de retorno e decide qual desses produtos serão mostradas toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="6fb67-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="6fb67-116">Você pode desejar toouse recomendações toooptimize sua loja online ou até mesmo tooinform seu interior center chamada ou o departamento de vendas.</span><span class="sxs-lookup"><span data-stu-id="6fb67-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="6fb67-117">**Há limitações de uso?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="6fb67-118">Recomendações tem Olá limitações de uso a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fb67-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="6fb67-119">Número máximo de modelos por assinatura: 10</span><span class="sxs-lookup"><span data-stu-id="6fb67-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="6fb67-120">Número máximo de itens que um catálogo pode conter: 100.000</span><span class="sxs-lookup"><span data-stu-id="6fb67-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="6fb67-121">número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="6fb67-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="6fb67-122">Olá mais antigo será excluído se novas serão carregadas ou relatadas.</span><span class="sxs-lookup"><span data-stu-id="6fb67-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="6fb67-123">O volume máximo de dados que podem ser enviados no email (por exemplo, importar dados de catálogo e importar dados de uso) é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="6fb67-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="6fb67-124">O número de TPS (transações por segundo) para um build de modelo da Recomendação que não está ativo é de cerca de 2 TPS.</span><span class="sxs-lookup"><span data-stu-id="6fb67-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="6fb67-125">Uma compilação de modelo de recomendações está ativa pode conter backup too20 TPS.</span><span class="sxs-lookup"><span data-stu-id="6fb67-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="6fb67-126">Compra e cobrança</span><span class="sxs-lookup"><span data-stu-id="6fb67-126">Purchase and Billing</span></span>
<span data-ttu-id="6fb67-127">**Quanto custa recomendações durante o período de início Olá?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="6fb67-128">As Recomendações são um serviço por assinatura.</span><span class="sxs-lookup"><span data-stu-id="6fb67-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="6fb67-129">A cobrança é feita com base no volume de transações por mês.</span><span class="sxs-lookup"><span data-stu-id="6fb67-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="6fb67-130">Você pode verificar Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) no Microsoft Azure Marketplace para obter informações sobre preços.</span><span class="sxs-lookup"><span data-stu-id="6fb67-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="6fb67-131">**Existem custos associados a fazer as Recomendações acompanharem e armazenarem a atividade do usuário para mim?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="6fb67-132">Não no momento da saudação.</span><span class="sxs-lookup"><span data-stu-id="6fb67-132">Not at hello moment.</span></span>

<span data-ttu-id="6fb67-133">**As Recomendações têm uma avaliação gratuita?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="6fb67-134">Há uma trilha livre que é restrita too10, 000 transações por mês.</span><span class="sxs-lookup"><span data-stu-id="6fb67-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="6fb67-135">**Quando serei cobrado por Recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="6fb67-136">Uma assinatura paga é qualquer assinatura para a qual há uma taxa mensal.</span><span class="sxs-lookup"><span data-stu-id="6fb67-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="6fb67-137">Quando você compra uma assinatura paga, você é cobrado imediatamente para Olá primeiro uso do mês.</span><span class="sxs-lookup"><span data-stu-id="6fb67-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="6fb67-138">Você é cobrado quantidade Olá associado a oferta de saudação na página de assinatura da saudação (mais impostos aplicáveis).</span><span class="sxs-lookup"><span data-stu-id="6fb67-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="6fb67-139">A cobrança mensal é feita por mês em Olá mesmo calendário data da sua primeira compra até cancelar a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fb67-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="6fb67-140">**Como atualizar o serviço de camada superior tooa?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="6fb67-141">Você pode comprar ou atualizar sua assinatura do hello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) página no Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6fb67-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="6fb67-142">Quando você atualiza uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="6fb67-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="6fb67-143">As transações que permanecem em sua antiga assinatura não serão adicionadas tooyour nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="6fb67-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="6fb67-144">Você paga o preço total para nova assinatura de hello, mesmo que haja transações não utilizadas em sua antiga assinatura.</span><span class="sxs-lookup"><span data-stu-id="6fb67-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="6fb67-145">Processo tooupgrade uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="6fb67-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="6fb67-146">Nevigate toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="6fb67-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="6fb67-147">Entrar no Marketplace de toohello se você ainda não tiver entrado.</span><span class="sxs-lookup"><span data-stu-id="6fb67-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="6fb67-148">No painel direito da saudação, todos os planos de saudação disponíveis são listados.</span><span class="sxs-lookup"><span data-stu-id="6fb67-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="6fb67-149">Clique o botão de opção de saudação plano Olá para que deseja tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="6fb67-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="6fb67-150">Se você quiser tooupgrade, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6fb67-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="6fb67-151">Se você não quiser tooupgrade, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="6fb67-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="6fb67-152">**Importante** caixa de diálogo Olá leia com atenção antes de atualizar porque há implicações de cobrança e uso.</span><span class="sxs-lookup"><span data-stu-id="6fb67-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="6fb67-153">**Quando terminará tooRecommendations minha assinatura?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="6fb67-154">Sua assinatura será encerrada quando você a cancelar.</span><span class="sxs-lookup"><span data-stu-id="6fb67-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="6fb67-155">Se você quiser toocancel suas assinaturas, consulte Olá instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="6fb67-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="6fb67-156">**Como cancelo minha assinatura de Recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="6fb67-157">toocancel sua assinatura, use Olá seguindo as etapas.</span><span class="sxs-lookup"><span data-stu-id="6fb67-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="6fb67-158">Se sua assinatura atual for uma assinatura paga, sua assinatura continua em vigor até o final de saudação do hello atual período de cobrança.</span><span class="sxs-lookup"><span data-stu-id="6fb67-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="6fb67-159">Se você precisar hello cancelamento toobe efetiva imediatamente, entre em contato conosco em [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="6fb67-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="6fb67-160">**Observação** nenhum reembolso é concedido se você cancelar antes do final de saudação de um período de cobrança ou por transações não utilizadas em um período de cobrança.</span><span class="sxs-lookup"><span data-stu-id="6fb67-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="6fb67-161">Navegue toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="6fb67-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="6fb67-162">Entrar no Marketplace de toohello se você ainda não tiver entrado.</span><span class="sxs-lookup"><span data-stu-id="6fb67-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="6fb67-163">Clique em **Cancelar** toohello direita do nome do conjunto de dados hello e status.</span><span class="sxs-lookup"><span data-stu-id="6fb67-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="6fb67-164">Você pode usar essa assinatura até o final de saudação do hello atual de seu limite de transação ou de período de cobrança é atingido (o que ocorrer primeiro).</span><span class="sxs-lookup"><span data-stu-id="6fb67-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="6fb67-165">Se você quiser toocancel sua assinatura imediatamente assim que você pode adquirir uma nova assinatura, uma permissão no arquivo [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="6fb67-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="6fb67-166">Introdução às Recomendações</span><span class="sxs-lookup"><span data-stu-id="6fb67-166">Getting started with Recommendations</span></span>
<span data-ttu-id="6fb67-167">**As Recomendações são para mim?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="6fb67-168">As recomendações no aprendizado de máquina é para organizações e empresas que dependem de recomendações toocross venda e vendas produtos ou serviços tootheir clientes.</span><span class="sxs-lookup"><span data-stu-id="6fb67-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="6fb67-169">Se você tiver um site voltado para o cliente, uma equipe de vendas, uma equipe de vendas interna ou um call center e se oferecer um catálogo de mais de algumas dezenas de produtos ou serviços, seu resultado final poderá se beneficiar do uso de Recomendações.</span><span class="sxs-lookup"><span data-stu-id="6fb67-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="6fb67-170">Experimentar recomendações é projetado toobe bastante simples.</span><span class="sxs-lookup"><span data-stu-id="6fb67-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="6fb67-171">Olá atual API versão exige habilidades básicas de programação.</span><span class="sxs-lookup"><span data-stu-id="6fb67-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="6fb67-172">Se você precisar de assistência, contate o fornecedor de saudação que desenvolveu o seu site.</span><span class="sxs-lookup"><span data-stu-id="6fb67-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="6fb67-173">Se você tiver um departamento de TI interno ou desenvolvedor interno, eles devem ser capazes de tooget toowork de recomendações para você.</span><span class="sxs-lookup"><span data-stu-id="6fb67-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="6fb67-174">**Quais são os pré-requisitos de saudação para configuração de recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="6fb67-175">Recomendações exige que você tenha um log de opções de usuário relacionado tooyour catálogo.</span><span class="sxs-lookup"><span data-stu-id="6fb67-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="6fb67-176">Se você não tiver um log e tiver um site voltado para o cliente, as Recomendações poderão coletar a atividade de usuário para você.</span><span class="sxs-lookup"><span data-stu-id="6fb67-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="6fb67-177">As Recomendações também exigem um catálogo de produtos ou serviços.</span><span class="sxs-lookup"><span data-stu-id="6fb67-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="6fb67-178">Se você não tiver o catálogo Olá, recomendações podem dados de uso do cliente real hello e criar um catálogo.</span><span class="sxs-lookup"><span data-stu-id="6fb67-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="6fb67-179">Um catálogo implícito não incluirá itens que não tenham sido relatados como parte das transações de usuário.</span><span class="sxs-lookup"><span data-stu-id="6fb67-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="6fb67-180">**Como configurar as recomendações para Olá primeira vez?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="6fb67-181">Depois de [assinatura](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, você deve usar a documentação da API de saudação em Olá [recomendações de aprendizado de máquina do Azure - guia de início rápido](machine-learning-recommendation-api-quick-start-guide.md) tooset o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fb67-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="6fb67-182">**Onde posso encontrar a documentação da API?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="6fb67-183">Olá documentação da API é [recomendações de aprendizado de máquina do Azure-guia de início rápido](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6fb67-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="6fb67-184">**O que fazem opções tenho tooRecommendations de dados de catálogo e o uso de tooupload?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="6fb67-185">Você tem duas opções para carregar os dados de catálogo e de uso: você pode exportar os dados de saudação do seu sistema CRM ou outros logs e carregá-lo tooRecommendations, ou você pode adicionar marcas tooyour site controlar atividades de usuário.</span><span class="sxs-lookup"><span data-stu-id="6fb67-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="6fb67-186">Se você usar o método último hello, Olá dados serão armazenados no Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb67-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="6fb67-187">Manutenção e suporte</span><span class="sxs-lookup"><span data-stu-id="6fb67-187">Maintenance and support</span></span>
<span data-ttu-id="6fb67-188">**Que tamanho meu conjunto de dados pode ter?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-188">**How large can my data set be?**</span></span>

<span data-ttu-id="6fb67-189">Cada conjunto de dados pode conter too100, 000 itens de catálogo e too2048 MB de dados de uso.</span><span class="sxs-lookup"><span data-stu-id="6fb67-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="6fb67-190">Além disso, uma assinatura pode conter os conjuntos de dados de too10 (modelos).</span><span class="sxs-lookup"><span data-stu-id="6fb67-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="6fb67-191">**Onde posso obter suporte técnico para Recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="6fb67-192">O suporte técnico está disponível no hello [suporte do Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="6fb67-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="6fb67-193">**Onde encontrar os termos de uso do Olá?**</span><span class="sxs-lookup"><span data-stu-id="6fb67-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="6fb67-194">[Termos de Serviço da API de Recomendações do Microsoft Azure Machine Learning](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="6fb67-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

