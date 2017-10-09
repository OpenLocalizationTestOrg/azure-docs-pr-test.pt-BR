---
title: "Recomendações de Machine Learning: integração do JavaScript | Microsoft Docs"
description: "Recomendações do Azure Machine Learning - Integração do JavaScript - documentação"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="5e2df-103">Recomendações do Azure Machine Learning - Integração do JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e2df-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="5e2df-104">Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="5e2df-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="5e2df-105">Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe.</span><span class="sxs-lookup"><span data-stu-id="5e2df-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="5e2df-106">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="5e2df-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="5e2df-107">Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="5e2df-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="5e2df-108">Este documento descrevem como toointegrate seu site usando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5e2df-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="5e2df-109">Olá JavaScript permite que você toosend eventos de aquisição de dados e as recomendações de tooconsume depois de criar um modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="5e2df-110">Todas as operações realizadas via JS também podem ser feitas do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="5e2df-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="5e2df-111">1. Visão geral</span><span class="sxs-lookup"><span data-stu-id="5e2df-111">1. General Overview</span></span>
<span data-ttu-id="5e2df-112">Integrando seu site com o AM do Azure As recomendações consistem em duas fases:</span><span class="sxs-lookup"><span data-stu-id="5e2df-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="5e2df-113">Enviar Eventos para as Recomendações do AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e2df-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="5e2df-114">Isso permitirá toobuild um modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="5e2df-115">Consuma recomendações hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-115">Consume hello recommendations.</span></span> <span data-ttu-id="5e2df-116">Depois Olá modelo é criado, você pode consumir recomendações hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="5e2df-117">(Este documento não explica como toobuild um modelo, ler Olá tooget do guia de início rápido para obter mais informações sobre como).</span><span class="sxs-lookup"><span data-stu-id="5e2df-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="5e2df-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="5e2df-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="5e2df-119">Em Olá primeira fase, que você inserir em suas páginas html uma pequena biblioteca JavaScript que permite Olá eventos da página toosend conforme elas ocorrem na página html de saudação em servidores de recomendações de ML do Azure (por meio do mercado de dados):</span><span class="sxs-lookup"><span data-stu-id="5e2df-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Desenho1][1]

<span data-ttu-id="5e2df-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="5e2df-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="5e2df-122">Em Olá segunda fase, quando você quiser tooshow recomendações de saudação na página Olá você selecionar uma das Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="5e2df-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="5e2df-123">1. o servidor (na fase de saudação de renderização da página) chama recomendações de tooget do servidor do Azure ML recomendações (por meio do mercado de dados).</span><span class="sxs-lookup"><span data-stu-id="5e2df-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="5e2df-124">resultados da saudação incluem uma lista de IDs de itens. O servidor precisa tooenrich Olá resultados com itens de saudação dados de metadados (por exemplo, imagens, descrição) e enviar Olá criado página toohello navegador.</span><span class="sxs-lookup"><span data-stu-id="5e2df-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Desenho2][2]

<span data-ttu-id="5e2df-126">2. hello, outra opção é toouse Olá pequeno arquivo JavaScript de fase um tooget uma lista simples de itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="5e2df-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="5e2df-127">dados de saudação recebidos aqui são mais enxutos que Olá na opção de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="5e2df-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Desenho3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="5e2df-129">2. Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5e2df-129">2. Prerequisites</span></span>
1. <span data-ttu-id="5e2df-130">Crie um novo modelo usando APIs de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="5e2df-131">Consulte o guia de início rápido de saudação sobre como toodo-lo.</span><span class="sxs-lookup"><span data-stu-id="5e2df-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="5e2df-132">Codifique seu &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; com base64.</span><span class="sxs-lookup"><span data-stu-id="5e2df-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="5e2df-133">(Isso será usado para Olá autenticação básica tooenable Olá JS código toocall Olá APIs).</span><span class="sxs-lookup"><span data-stu-id="5e2df-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="5e2df-134">3. Enviar eventos de Aquisição de Dados usando o JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e2df-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="5e2df-135">Olá, as etapas a seguir facilitam a enviar eventos:</span><span class="sxs-lookup"><span data-stu-id="5e2df-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="5e2df-136">Inclua a biblioteca JQuery em seu código.</span><span class="sxs-lookup"><span data-stu-id="5e2df-136">Include JQuery library in your code.</span></span> <span data-ttu-id="5e2df-137">Você pode baixá-lo do nuget em Olá URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e2df-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="5e2df-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="5e2df-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="5e2df-139">Incluir a biblioteca de Script de Java recomendações Olá da saudação URL a seguir: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="5e2df-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="5e2df-140">Inicialize a biblioteca do Azure ML recomendações com parâmetros adequados Olá.</span><span class="sxs-lookup"><span data-stu-id="5e2df-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="5e2df-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Evento apropriado de saudação de envio.</span><span class="sxs-lookup"><span data-stu-id="5e2df-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="5e2df-142">Confira a seção detalhada abaixo em todos os tipos de eventos (exemplo de evento de clique) <script> se (typeof AzureMLRecommendationsEvent=="undefined") {</span><span class="sxs-lookup"><span data-stu-id="5e2df-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="5e2df-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ evento: "clique", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="5e2df-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="5e2df-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="5e2df-144">3.1.</span></span>    <span data-ttu-id="5e2df-145">Limitações e Suporte ao Navegador</span><span class="sxs-lookup"><span data-stu-id="5e2df-145">Limitations and Browser Support</span></span>
<span data-ttu-id="5e2df-146">Isso é uma implementação de referência e é fornecida como está.</span><span class="sxs-lookup"><span data-stu-id="5e2df-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="5e2df-147">Deve oferecer suporte a todos os principais navegadores.</span><span class="sxs-lookup"><span data-stu-id="5e2df-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="5e2df-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="5e2df-148">3.2.</span></span>    <span data-ttu-id="5e2df-149">Tipo de Eventos</span><span class="sxs-lookup"><span data-stu-id="5e2df-149">Type of Events</span></span>
<span data-ttu-id="5e2df-150">Há 5 tipos de evento que Olá biblioteca oferece suporte a: clique em, clique em recomendação, adicionar tooShop carrinho, remover do carrinho de compras e compra.</span><span class="sxs-lookup"><span data-stu-id="5e2df-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="5e2df-151">Há um evento adicional que é o contexto de usuário Olá tooset usado chamado logon.</span><span class="sxs-lookup"><span data-stu-id="5e2df-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="5e2df-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="5e2df-152">3.2.1.</span></span> <span data-ttu-id="5e2df-153">Evento Clicar</span><span class="sxs-lookup"><span data-stu-id="5e2df-153">Click Event</span></span>
<span data-ttu-id="5e2df-154">Esse evento deve ser usado sempre que um usuário clicou em um item.</span><span class="sxs-lookup"><span data-stu-id="5e2df-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="5e2df-155">Normalmente quando o usuário clica em um item uma nova página é aberta com detalhes do item Olá; Esse evento deve ser disparado nesta página.</span><span class="sxs-lookup"><span data-stu-id="5e2df-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="5e2df-156">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-156">Parameters:</span></span>

* <span data-ttu-id="5e2df-157">evento (cadeia de caracteres, obrigatória) - “clique”</span><span class="sxs-lookup"><span data-stu-id="5e2df-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="5e2df-158">item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="5e2df-159">nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="5e2df-160">itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="5e2df-161">itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="5e2df-162">Ou com dados opcionais:</span><span class="sxs-lookup"><span data-stu-id="5e2df-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="5e2df-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="5e2df-163">3.2.2.</span></span> <span data-ttu-id="5e2df-164">Evento do Clique de Recomendação</span><span class="sxs-lookup"><span data-stu-id="5e2df-164">Recommendation Click Event</span></span>
<span data-ttu-id="5e2df-165">Esse evento deve ser usado sempre que um usuário clicou em um item que foi recebido das Recomendações do AM do Azure como um item recomendado.</span><span class="sxs-lookup"><span data-stu-id="5e2df-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="5e2df-166">Normalmente quando o usuário clica em um item uma nova página é aberta com detalhes do item Olá; Esse evento deve ser disparado nesta página.</span><span class="sxs-lookup"><span data-stu-id="5e2df-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="5e2df-167">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-167">Parameters:</span></span>

* <span data-ttu-id="5e2df-168">evento (cadeia de caracteres, obrigatória) - “recommendationclick”</span><span class="sxs-lookup"><span data-stu-id="5e2df-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="5e2df-169">item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="5e2df-170">nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="5e2df-171">itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="5e2df-172">itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="5e2df-173">sementes (cadeia de caracteres array, opcional) - Olá propagações que gerou a consulta de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="5e2df-174">recoList (cadeia de caracteres array, opcional) - Olá resultado da solicitação de recomendação de saudação que gerou o item de saudação que foi clicado.</span><span class="sxs-lookup"><span data-stu-id="5e2df-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="5e2df-175">Ou com dados opcionais:</span><span class="sxs-lookup"><span data-stu-id="5e2df-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="5e2df-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="5e2df-176">3.2.3.</span></span> <span data-ttu-id="5e2df-177">Evento Adicionar ao Carrinho de Compras</span><span class="sxs-lookup"><span data-stu-id="5e2df-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="5e2df-178">Esse evento deve ser usado quando o usuário Olá adiciona um toohello item carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="5e2df-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="5e2df-179">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-179">Parameters:</span></span>

* <span data-ttu-id="5e2df-180">evento (cadeia de caracteres, obrigatória) - “addshopcart”</span><span class="sxs-lookup"><span data-stu-id="5e2df-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="5e2df-181">item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="5e2df-182">nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="5e2df-183">itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="5e2df-184">itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="5e2df-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="5e2df-185">3.2.4.</span></span> <span data-ttu-id="5e2df-186">Evento Remover do Carrinho de Compras</span><span class="sxs-lookup"><span data-stu-id="5e2df-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="5e2df-187">Esse evento deve ser usado quando o usuário Olá remove um carrinho de compras de toohello do item.</span><span class="sxs-lookup"><span data-stu-id="5e2df-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="5e2df-188">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-188">Parameters:</span></span>

* <span data-ttu-id="5e2df-189">evento (cadeia de caracteres, obrigatória) - “removeshopcart”</span><span class="sxs-lookup"><span data-stu-id="5e2df-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="5e2df-190">item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="5e2df-191">nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="5e2df-192">itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="5e2df-193">itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="5e2df-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="5e2df-194">3.2.5.</span></span> <span data-ttu-id="5e2df-195">Evento Comprar</span><span class="sxs-lookup"><span data-stu-id="5e2df-195">Purchase Event</span></span>
<span data-ttu-id="5e2df-196">Esse evento deve ser usado quando o usuário Olá adquirido seu carrinho de compras.</span><span class="sxs-lookup"><span data-stu-id="5e2df-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="5e2df-197">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-197">Parameters:</span></span>

* <span data-ttu-id="5e2df-198">evento (cadeia de caracteres) – “adquirir”</span><span class="sxs-lookup"><span data-stu-id="5e2df-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="5e2df-199">itens ( Adquiridos[] ) - A matriz que contém uma entrada para cada item adquirido.</span><span class="sxs-lookup"><span data-stu-id="5e2df-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="5e2df-200">Formato adquirido:</span><span class="sxs-lookup"><span data-stu-id="5e2df-200">Purchased format:</span></span>
  * <span data-ttu-id="5e2df-201">item (string) - o identificador exclusivo do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="5e2df-202">contagem (int ou cadeia de caracteres) - número de itens que foram adquiridos.</span><span class="sxs-lookup"><span data-stu-id="5e2df-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="5e2df-203">preço (float ou cadeia de caracteres) - campo opcional - Olá preço de item de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="5e2df-204">exemplo Hello abaixo mostra a compra de 3 itens (33, 34, 35), dois com todos os campos preenchidos (item, contagem, preço) e outro (item 34) sem um preço.</span><span class="sxs-lookup"><span data-stu-id="5e2df-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="5e2df-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="5e2df-205">3.2.6.</span></span> <span data-ttu-id="5e2df-206">Evento Logon do Usuário</span><span class="sxs-lookup"><span data-stu-id="5e2df-206">User Login Event</span></span>
<span data-ttu-id="5e2df-207">Azure ML recomendações evento biblioteca cria e usar um cookie em eventos de tooidentify ordem que veio Olá mesmo navegador.</span><span class="sxs-lookup"><span data-stu-id="5e2df-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="5e2df-208">No modelo de saudação do pedido tooimprove resultados do Azure ML recomendações permite tooset um identificador exclusivo do usuário que substituirá o uso de cookie hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="5e2df-209">Esse evento deve ser usado após o site de tooyour de logon de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="5e2df-210">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-210">Parameters:</span></span>

* <span data-ttu-id="5e2df-211">evento (cadeia de caracteres) - “userlogin”</span><span class="sxs-lookup"><span data-stu-id="5e2df-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="5e2df-212">usuário (string) - identificação exclusiva do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="5e2df-213">4. Usar Recomendações via JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e2df-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="5e2df-214">código de saudação que consome a recomendação de saudação é disparado por algum evento JavaScript por página de Web do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="5e2df-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="5e2df-215">resposta de recomendação de saudação inclui Olá recomendado Ids de itens, seus nomes e suas classificações.</span><span class="sxs-lookup"><span data-stu-id="5e2df-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="5e2df-216">É melhor toouse esta opção apenas para uma exibição de lista de saudação recomendada itens - mais complexos tratamento (como adicionar metadados do item Olá) deve ser feita na integração do lado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="5e2df-217">4.1 Usar as Recomendações</span><span class="sxs-lookup"><span data-stu-id="5e2df-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="5e2df-218">recomendações de tooconsume que necessário tooinclude Olá necessário bibliotecas JavaScript em sua página e toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="5e2df-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="5e2df-219">Consulte a seção 2.</span><span class="sxs-lookup"><span data-stu-id="5e2df-219">See section 2.</span></span>

<span data-ttu-id="5e2df-220">recomendações de tooconsume para um ou mais itens que você precisa toocall um método chamado: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="5e2df-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="5e2df-221">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5e2df-221">Parameters:</span></span>

* <span data-ttu-id="5e2df-222">itens (matriz de cadeias de caracteres) - um ou mais itens tooget as recomendações para.</span><span class="sxs-lookup"><span data-stu-id="5e2df-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="5e2df-223">Se você consumir um build Fbt, você poderá, então, definir somente um item aqui.</span><span class="sxs-lookup"><span data-stu-id="5e2df-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="5e2df-224">numberOfResults (int) - número de resultados necessários.</span><span class="sxs-lookup"><span data-stu-id="5e2df-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="5e2df-225">includeMetadata (booliano, opcional) - se definir too'true' indica o campo Olá metadados deve ser preenchido em resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e2df-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="5e2df-226">Função de processamento - uma função que tratará recomendações Olá retornadas.</span><span class="sxs-lookup"><span data-stu-id="5e2df-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="5e2df-227">Olá dados são retornados como uma matriz de:</span><span class="sxs-lookup"><span data-stu-id="5e2df-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="5e2df-228">Item - ID exclusiva do item</span><span class="sxs-lookup"><span data-stu-id="5e2df-228">Item - item unique id</span></span>
  * <span data-ttu-id="5e2df-229">nome - nome do item (se existir no catálogo)</span><span class="sxs-lookup"><span data-stu-id="5e2df-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="5e2df-230">classificação - classificação da recomendação</span><span class="sxs-lookup"><span data-stu-id="5e2df-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="5e2df-231">metadados - uma cadeia de caracteres que representa os metadados de saudação do item de saudação</span><span class="sxs-lookup"><span data-stu-id="5e2df-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="5e2df-232">Exemplo: Olá código a seguir solicita 8 recomendações para o item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (e não especificando includeMetadata - implicitamente diz que não há metadados são necessário), ele, em seguida, concatenar resultados Olá em um buffer.</span><span class="sxs-lookup"><span data-stu-id="5e2df-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
