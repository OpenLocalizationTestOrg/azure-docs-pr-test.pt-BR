---
title: "aaaLearn como toouse Olá conector Twitter em aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do Twitter com os parâmetros da API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="0ad3a-103">Introdução ao conector do Twitter Olá</span><span class="sxs-lookup"><span data-stu-id="0ad3a-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="0ad3a-104">Com o conector do Twitter hello, você pode:</span><span class="sxs-lookup"><span data-stu-id="0ad3a-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="0ad3a-105">Postar tweets e obter tweets</span><span class="sxs-lookup"><span data-stu-id="0ad3a-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="0ad3a-106">Acessar linhas do tempo, amigos e seguidores</span><span class="sxs-lookup"><span data-stu-id="0ad3a-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="0ad3a-107">Executar qualquer Olá outras ações e gatilhos descritos abaixo</span><span class="sxs-lookup"><span data-stu-id="0ad3a-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="0ad3a-108">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="0ad3a-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0ad3a-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="0ad3a-110">Conecte-se tooTwitter</span><span class="sxs-lookup"><span data-stu-id="0ad3a-110">Connect tooTwitter</span></span>
<span data-ttu-id="0ad3a-111">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="0ad3a-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="0ad3a-113">Criar uma conexão tooTwitter</span><span class="sxs-lookup"><span data-stu-id="0ad3a-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="0ad3a-114">Usar um gatilho do Twitter</span><span class="sxs-lookup"><span data-stu-id="0ad3a-114">Use a Twitter trigger</span></span>
<span data-ttu-id="0ad3a-115">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="0ad3a-116">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0ad3a-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="0ad3a-117">Neste exemplo, mostrarei como Olá toouse **quando um novo tweet for lançado** disparar toosearch para #Seattle e, se #Seattle for encontrado, atualizar um arquivo em Dropbox com o texto de saudação do tweet hello.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="0ad3a-118">Um exemplo de empresa, você pode pesquisar por nome de saudação da sua empresa e atualizar um banco de dados do SQL com o texto de saudação do tweet hello.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="0ad3a-119">Digite *twitter* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **Twitter - quando um novo tweet é postado** gatilho</span><span class="sxs-lookup"><span data-stu-id="0ad3a-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="0ad3a-120">![Imagem 1 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="0ad3a-121">Digite *#Seattle* em Olá **texto de pesquisa** controle</span><span class="sxs-lookup"><span data-stu-id="0ad3a-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="0ad3a-122">![Imagem 2 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="0ad3a-123">Neste ponto, seu aplicativo lógica foi configurado com um gatilho que iniciará uma execução de saudação outros gatilhos e ações no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ad3a-124">Para uma lógica aplicativo toobe funcional, ele deve conter pelo menos um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="0ad3a-125">Siga as etapas de Olá Olá tooadd próximo da seção uma ação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="0ad3a-126">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="0ad3a-126">Add a condition</span></span>
<span data-ttu-id="0ad3a-127">Como estamos interessados apenas em tweets de usuários com mais de 50 usuários, uma condição que confirma o número de saudação do seguidores deve primeiro ser adicionada toohello lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="0ad3a-128">Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando #Seattle é encontrado em um tweet novo</span><span class="sxs-lookup"><span data-stu-id="0ad3a-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="0ad3a-129">![Imagem 1 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="0ad3a-130">Selecione Olá **adicionar uma condição** link.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="0ad3a-131">![Imagem 1 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="0ad3a-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="0ad3a-132">Isso abre o hello **condição** controle onde você pode verificar condições como *é igual a*, *é menor que*, *é maior do que*, *contém*, etc.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="0ad3a-133">![Imagem 2 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="0ad3a-134">Selecione Olá **escolha um valor** controle.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="0ad3a-135">Nesse controle, você pode selecionar uma ou mais das propriedades de saudação de todas as ações anteriores ou disparadores como valor Olá cuja condição será avaliado tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="0ad3a-136">![Imagem 3 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="0ad3a-137">Selecione Olá **...**  tooexpand lista de saudação de propriedades para ver todas as propriedades de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="0ad3a-138">![Imagem 4 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="0ad3a-139">Selecione Olá **contagem seguidores** propriedade.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="0ad3a-140">![Imagem 5 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="0ad3a-141">Observe seguidores Olá propriedade count agora está no controle de valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Imagem 6 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="0ad3a-143">Selecione **é maior do que** na lista de operadores de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="0ad3a-144">![Imagem 7 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="0ad3a-145">Digite 50 como Olá operando para Olá *é maior do que* operador.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="0ad3a-146">condição de saudação agora é adicionada.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-146">hello condition is now added.</span></span> <span data-ttu-id="0ad3a-147">Salve seu trabalho usando Olá **salvar** link no menu de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="0ad3a-148">![Imagem 8 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="0ad3a-149">Usar uma ação do Twitter</span><span class="sxs-lookup"><span data-stu-id="0ad3a-149">Use a Twitter action</span></span>
<span data-ttu-id="0ad3a-150">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="0ad3a-151">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0ad3a-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="0ad3a-152">Agora que você adicionou um gatilho, siga essas etapas tooadd uma ação que publicará um tweet novo com conteúdo Olá Olá tweets encontrados pelo gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="0ad3a-153">Para fins de saudação deste passo a passo somente tweets de usuários com mais de 50 seguidores serão lançadas.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="0ad3a-154">Na próxima etapa de saudação, você irá adicionar uma ação do Twitter que publicará um tweet usando algumas das propriedades de saudação de cada tweet que foi lançado por um usuário que tem mais de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="0ad3a-155">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-155">Select **Add an action**.</span></span> <span data-ttu-id="0ad3a-156">Isso abre o controle de pesquisa Olá onde você pode procurar outras ações e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="0ad3a-157">![Imagem 9 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="0ad3a-158">Digite *twitter* na caixa de pesquisa Olá selecione Olá **Twitter - lançar um tweet** ação.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="0ad3a-159">Isso abre o hello **lançar um tweet** controlar onde você irá inserir todos os detalhes para tweet hello está sendo lançada.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="0ad3a-160">![Imagem de 1 a 5 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="0ad3a-161">Selecione Olá **Tweet texto** controle.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="0ad3a-162">Todas as saídas de ações anteriores e gatilhos no aplicativo de lógica de saudação agora estão visíveis.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="0ad3a-163">Você pode selecionar qualquer uma dessas e usá-los como parte do texto de tweet Olá de tweet novo hello.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="0ad3a-164">![Imagem 2 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="0ad3a-165">Escolha **Nome de usuário**</span><span class="sxs-lookup"><span data-stu-id="0ad3a-165">Select **User name**</span></span>   
5. <span data-ttu-id="0ad3a-166">Digite *diz:* no controle de texto tweet hello.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="0ad3a-167">Faça isso logo após o Nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="0ad3a-168">Escolha *Texto do tweet*.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="0ad3a-169">![Imagem 3 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="0ad3a-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="0ad3a-170">Salve seu trabalho e enviar um tweet com hello #Seattle hashtag tooactivate seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0ad3a-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="0ad3a-171">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="0ad3a-171">Connector-specific details</span></span>

<span data-ttu-id="0ad3a-172">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="0ad3a-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0ad3a-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ad3a-173">Next steps</span></span>
[<span data-ttu-id="0ad3a-174">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="0ad3a-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

