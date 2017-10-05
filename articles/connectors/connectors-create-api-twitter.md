---
title: "Saiba como usar o conector de Twitter em aplicativos lógicos | Microsoft Docs"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="a181a-103">Introdução ao conector do Twitter</span><span class="sxs-lookup"><span data-stu-id="a181a-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="a181a-104">Com o conector do Twitter, você pode:</span><span class="sxs-lookup"><span data-stu-id="a181a-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="a181a-105">Postar tweets e obter tweets</span><span class="sxs-lookup"><span data-stu-id="a181a-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="a181a-106">Acessar linhas do tempo, amigos e seguidores</span><span class="sxs-lookup"><span data-stu-id="a181a-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="a181a-107">Executar qualquer um dos gatilhos e ações descritos abaixo</span><span class="sxs-lookup"><span data-stu-id="a181a-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="a181a-108">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a181a-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="a181a-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a181a-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="a181a-110">Conectar-se ao Twitter</span><span class="sxs-lookup"><span data-stu-id="a181a-110">Connect to Twitter</span></span>
<span data-ttu-id="a181a-111">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="a181a-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="a181a-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="a181a-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="a181a-113">Criar uma conexão com o Twitter</span><span class="sxs-lookup"><span data-stu-id="a181a-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="a181a-114">Usar um gatilho do Twitter</span><span class="sxs-lookup"><span data-stu-id="a181a-114">Use a Twitter trigger</span></span>
<span data-ttu-id="a181a-115">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a181a-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="a181a-116">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a181a-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="a181a-117">Neste exemplo, mostrarei como usar o gatilho **Quando um novo tweet é postado** para procurar #Seattle e, se #Seattle for encontrada, mostrarei como atualizar um arquivo no Dropbox com o texto do tweet.</span><span class="sxs-lookup"><span data-stu-id="a181a-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="a181a-118">Em um exemplo corporativo, você pode pesquisar o nome da sua empresa e atualizar um banco de dados SQL com o texto do tweet.</span><span class="sxs-lookup"><span data-stu-id="a181a-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="a181a-119">Digite *twitter* na caixa de pesquisa no designer de aplicativos lógicos e escolha o gatilho **Twitter – quando um novo tweet é postado**</span><span class="sxs-lookup"><span data-stu-id="a181a-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="a181a-120">![Imagem 1 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="a181a-121">Digite *#Seattle* no controle **Texto de Pesquisa**</span><span class="sxs-lookup"><span data-stu-id="a181a-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="a181a-122">![Imagem 2 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="a181a-123">Neste ponto, seu aplicativo lógico foi configurado com um gatilho que iniciará uma execução de outros gatilhos e ações no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a181a-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="a181a-124">Para que um aplicativo lógico funcione, ele deve conter pelo menos um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="a181a-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="a181a-125">Siga as etapas na próxima seção para adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="a181a-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="a181a-126">Adicione uma condição</span><span class="sxs-lookup"><span data-stu-id="a181a-126">Add a condition</span></span>
<span data-ttu-id="a181a-127">Uma vez que estamos interessados em tweets de usuários com mais de 50 usuários, uma condição que confirma o número de seguidores deve ser adicionada ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a181a-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="a181a-128">Escolha **+ Nova etapa** para adicionar a ação que deseja tomar quando #Seattle for encontrada em um novo tweet</span><span class="sxs-lookup"><span data-stu-id="a181a-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="a181a-129">![Imagem 1 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="a181a-130">Escolha o link **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="a181a-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="a181a-131">![Imagem 1 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="a181a-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="a181a-132">Isso abre o controle **Condição**, onde é possível verificar condições como *é igual a*, *é menor que*, *é maior que*, *contém*, etc.</span><span class="sxs-lookup"><span data-stu-id="a181a-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="a181a-133">![Imagem 2 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="a181a-134">Selecione o controle **Escolher um valor**.</span><span class="sxs-lookup"><span data-stu-id="a181a-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="a181a-135">Nesse controle, é possível selecionar, como valor, uma ou mais propriedades de quaisquer ações ou gatilhos anteriores, cuja condição será avaliada como verdadeira ou falsa.</span><span class="sxs-lookup"><span data-stu-id="a181a-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="a181a-136">![Imagem 3 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="a181a-137">Escolha **...** para expandir a lista de propriedades, de modo que você possa ver todas as propriedades que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a181a-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="a181a-138">![Imagem 4 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="a181a-139">Escolha a propriedade **Contagem de seguidores**.</span><span class="sxs-lookup"><span data-stu-id="a181a-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="a181a-140">![Imagem 5 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="a181a-141">Observe que a propriedade Contagem de seguidores agora está no controle de valor.</span><span class="sxs-lookup"><span data-stu-id="a181a-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Imagem 6 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="a181a-143">Escolha **é maior que** na lista de operadores.</span><span class="sxs-lookup"><span data-stu-id="a181a-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="a181a-144">![Imagem 7 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="a181a-145">Digite 50 como o operando para o operador *é maior que*.</span><span class="sxs-lookup"><span data-stu-id="a181a-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="a181a-146">Agora a condição está adicionada.</span><span class="sxs-lookup"><span data-stu-id="a181a-146">The condition is now added.</span></span> <span data-ttu-id="a181a-147">Salve seu trabalho usando o link **Salvar** no menu acima.</span><span class="sxs-lookup"><span data-stu-id="a181a-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="a181a-148">![Imagem 8 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="a181a-149">Usar uma ação do Twitter</span><span class="sxs-lookup"><span data-stu-id="a181a-149">Use a Twitter action</span></span>
<span data-ttu-id="a181a-150">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a181a-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="a181a-151">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a181a-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="a181a-152">Agora que você adicionou um gatilho, siga estas etapas para adicionar uma ação que postará um novo tweet com o conteúdo dos tweets encontrados pelo gatilho.</span><span class="sxs-lookup"><span data-stu-id="a181a-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="a181a-153">Para este passo a passo, serão postados apenas tweets de usuários com mais de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="a181a-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="a181a-154">Na próxima etapa, você adicionará uma ação do Twitter que postará um tweet usando algumas das propriedades de cada tweet que foi postado por um usuário com mais de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="a181a-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="a181a-155">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="a181a-155">Select **Add an action**.</span></span> <span data-ttu-id="a181a-156">Isso abre o controle de pesquisa, onde é possível procurar outros gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="a181a-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="a181a-157">![Imagem 9 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="a181a-158">Insira *twitter* na caixa de pesquisa e escolha a ação **Twitter – postar um tweet**.</span><span class="sxs-lookup"><span data-stu-id="a181a-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="a181a-159">Isso abre o controle **Postar um tweet**, onde você vai inserir todos os detalhes para o tweet que está sendo postado.</span><span class="sxs-lookup"><span data-stu-id="a181a-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="a181a-160">![Imagem de 1 a 5 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="a181a-161">Escolha o controle **Texto do tweet**.</span><span class="sxs-lookup"><span data-stu-id="a181a-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="a181a-162">Todas as saídas de ações e gatilhos anteriores no aplicativo lógico agora estão visíveis.</span><span class="sxs-lookup"><span data-stu-id="a181a-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="a181a-163">Você pode escolher qualquer um deles e usá-los como parte do texto do tweet do novo tweet.</span><span class="sxs-lookup"><span data-stu-id="a181a-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="a181a-164">![Imagem 2 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="a181a-165">Escolha **Nome de usuário**</span><span class="sxs-lookup"><span data-stu-id="a181a-165">Select **User name**</span></span>   
5. <span data-ttu-id="a181a-166">Digite *diz:* no controle de texto do tweet.</span><span class="sxs-lookup"><span data-stu-id="a181a-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="a181a-167">Faça isso logo após o Nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="a181a-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="a181a-168">Escolha *Texto do tweet*.</span><span class="sxs-lookup"><span data-stu-id="a181a-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="a181a-169">![Imagem 3 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="a181a-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="a181a-170">Salve seu trabalho e envie um tweet com a hashtag #Seattle para ativar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a181a-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="a181a-171">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="a181a-171">Connector-specific details</span></span>

<span data-ttu-id="a181a-172">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="a181a-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a181a-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a181a-173">Next steps</span></span>
[<span data-ttu-id="a181a-174">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a181a-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

