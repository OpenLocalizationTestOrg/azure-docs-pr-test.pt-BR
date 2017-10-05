---
title: "Usar ações de solicitação e resposta | Microsoft Docs"
description: "Visão geral do gatilho e da ação da solicitação e da resposta em um aplicativo lógico do Azure"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="6bcfa-103">Introdução aos componentes de solicitação e resposta</span><span class="sxs-lookup"><span data-stu-id="6bcfa-103">Get started with the request and response components</span></span>
<span data-ttu-id="6bcfa-104">Com os componentes de solicitação e resposta em um aplicativo lógico, você pode responder em tempo real a eventos.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="6bcfa-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="6bcfa-105">For example, you can:</span></span>

* <span data-ttu-id="6bcfa-106">Responder a uma solicitação HTTP com dados de um banco de dados local por meio de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="6bcfa-107">Dispare um aplicativo lógico de um evento de webhook externo.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="6bcfa-108">Chamar um aplicativo lógico com uma ação de solicitação e resposta de dentro de outro aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="6bcfa-109">Para começar a usar as ações de solicitação e resposta em um aplicativo lógico, confira [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6bcfa-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="6bcfa-110">Usar o gatilho de Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="6bcfa-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="6bcfa-111">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="6bcfa-112">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bcfa-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="6bcfa-113">Veja uma sequência de exemplo de como configurar uma solicitação HTTP no Designer de Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="6bcfa-114">Adicione o gatilho **Solicitação — quando uma solicitação HTTP é recebida** no seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="6bcfa-115">Como opção, você pode fornecer um esquema JSON (usando uma ferramenta como [JSONSchema.net](http://jsonschema.net)) para o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="6bcfa-116">Isso permite que o designer gere tokens para propriedades na solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="6bcfa-117">Adicione outra ação para que seja possível salvar o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="6bcfa-118">Depois de salvar o aplicativo lógico, você pode obter a URL da solicitação HTTP do cartão de solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="6bcfa-119">Um HTTP POST (você pode usar uma ferramenta como [Postman](https://www.getpostman.com/)) para a URL que dispara o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="6bcfa-120">Se você não definir uma ação de resposta, uma resposta `202 ACCEPTED` será retornada imediatamente ao chamador.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="6bcfa-121">Você pode usar a ação de resposta para personalizar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-121">You can use the response action to customize a response.</span></span>
> 
> 

![Gatilho de resposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="6bcfa-123">Usar a ação de Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="6bcfa-123">Use the HTTP Response action</span></span>
<span data-ttu-id="6bcfa-124">A ação de Resposta HTTP só será válida quando usada em um fluxo de trabalho disparado por uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="6bcfa-125">Se você não definir uma ação de resposta, uma resposta `202 ACCEPTED` será retornada imediatamente ao chamador.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="6bcfa-126">Você pode adicionar uma ação de resposta a qualquer etapa do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="6bcfa-127">O aplicativo lógico só mantém a solicitação de entrada aberta por um minuto para uma resposta.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="6bcfa-128">Após um minuto, se nenhuma resposta for enviada do fluxo de trabalho (e se existir uma ação de resposta na definição), um `504 GATEWAY TIMEOUT` será retornado ao chamador.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="6bcfa-129">Veja como adicionar uma ação de Resposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="6bcfa-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="6bcfa-130">Selecione o botão **Nova Etapa** .</span><span class="sxs-lookup"><span data-stu-id="6bcfa-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="6bcfa-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="6bcfa-132">Na caixa de pesquisa de ação, digite **resposta** para listar a ação de Resposta.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Selecionar a ação de resposta](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="6bcfa-134">Adicione todos os parâmetros necessários para a mensagem de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Concluir a ação de resposta](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="6bcfa-136">Clique no canto superior esquerdo da barra de ferramentas para salvar e seu aplicativo lógico será salvo e publicado (ativado).</span><span class="sxs-lookup"><span data-stu-id="6bcfa-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="6bcfa-137">Gatilho de solicitação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-137">Request trigger</span></span>
<span data-ttu-id="6bcfa-138">Veja os detalhes do gatilho com suporte deste conector.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="6bcfa-139">Há um único gatilho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-139">There is a single request trigger.</span></span>

| <span data-ttu-id="6bcfa-140">Gatilho</span><span class="sxs-lookup"><span data-stu-id="6bcfa-140">Trigger</span></span> | <span data-ttu-id="6bcfa-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bcfa-142">Solicitação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-142">Request</span></span> |<span data-ttu-id="6bcfa-143">Ocorre quando uma solicitação HTTP é recebida</span><span class="sxs-lookup"><span data-stu-id="6bcfa-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="6bcfa-144">Ação de resposta</span><span class="sxs-lookup"><span data-stu-id="6bcfa-144">Response action</span></span>
<span data-ttu-id="6bcfa-145">Veja os detalhes da ação com suporte deste conector.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="6bcfa-146">Há uma única ação de resposta que pode ser usada apenas quando acompanhada por um gatilho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="6bcfa-147">Ação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-147">Action</span></span> | <span data-ttu-id="6bcfa-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bcfa-149">resposta</span><span class="sxs-lookup"><span data-stu-id="6bcfa-149">Response</span></span> |<span data-ttu-id="6bcfa-150">Retorna uma resposta à solicitação HTTP correlacionada</span><span class="sxs-lookup"><span data-stu-id="6bcfa-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="6bcfa-151">Detalhes de gatilho e da ação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-151">Trigger and action details</span></span>
<span data-ttu-id="6bcfa-152">As tabelas a seguir descrevem os campos de entrada para o gatilho e a ação e os detalhes de saída correspondentes.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="6bcfa-153">Gatilho de solicitação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-153">Request trigger</span></span>
<span data-ttu-id="6bcfa-154">A seguir, um campo de entrada para o gatilho de uma solicitação HTTP de entrada.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="6bcfa-155">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-155">Display name</span></span> | <span data-ttu-id="6bcfa-156">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="6bcfa-156">Property name</span></span> | <span data-ttu-id="6bcfa-157">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bcfa-158">Esquema JSON</span><span class="sxs-lookup"><span data-stu-id="6bcfa-158">JSON Schema</span></span> |<span data-ttu-id="6bcfa-159">schema</span><span class="sxs-lookup"><span data-stu-id="6bcfa-159">schema</span></span> |<span data-ttu-id="6bcfa-160">O esquema JSON do corpo da solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="6bcfa-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="6bcfa-161">**Detalhes de saída**</span><span class="sxs-lookup"><span data-stu-id="6bcfa-161">**Output details**</span></span>

<span data-ttu-id="6bcfa-162">A seguir, os detalhes de saída para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-162">The following are output details for the request.</span></span>

| <span data-ttu-id="6bcfa-163">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="6bcfa-163">Property name</span></span> | <span data-ttu-id="6bcfa-164">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="6bcfa-164">Data type</span></span> | <span data-ttu-id="6bcfa-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bcfa-166">headers</span><span class="sxs-lookup"><span data-stu-id="6bcfa-166">Headers</span></span> |<span data-ttu-id="6bcfa-167">objeto</span><span class="sxs-lookup"><span data-stu-id="6bcfa-167">object</span></span> |<span data-ttu-id="6bcfa-168">Cabeçalhos da solicitação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-168">Request headers</span></span> |
| <span data-ttu-id="6bcfa-169">Corpo</span><span class="sxs-lookup"><span data-stu-id="6bcfa-169">Body</span></span> |<span data-ttu-id="6bcfa-170">objeto</span><span class="sxs-lookup"><span data-stu-id="6bcfa-170">object</span></span> |<span data-ttu-id="6bcfa-171">Objeto da solicitação</span><span class="sxs-lookup"><span data-stu-id="6bcfa-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="6bcfa-172">Ação de resposta</span><span class="sxs-lookup"><span data-stu-id="6bcfa-172">Response action</span></span>
<span data-ttu-id="6bcfa-173">Estes são os campos de entrada da ação de Resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="6bcfa-174">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="6bcfa-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="6bcfa-175">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-175">Display name</span></span> | <span data-ttu-id="6bcfa-176">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="6bcfa-176">Property name</span></span> | <span data-ttu-id="6bcfa-177">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bcfa-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bcfa-178">Código de status*</span><span class="sxs-lookup"><span data-stu-id="6bcfa-178">Status Code*</span></span> |<span data-ttu-id="6bcfa-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="6bcfa-179">statusCode</span></span> |<span data-ttu-id="6bcfa-180">O código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="6bcfa-180">The HTTP status code</span></span> |
| <span data-ttu-id="6bcfa-181">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="6bcfa-181">Headers</span></span> |<span data-ttu-id="6bcfa-182">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="6bcfa-182">headers</span></span> |<span data-ttu-id="6bcfa-183">Um objeto JSON de cabeçalhos de resposta a serem incluídos</span><span class="sxs-lookup"><span data-stu-id="6bcfa-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="6bcfa-184">Corpo</span><span class="sxs-lookup"><span data-stu-id="6bcfa-184">Body</span></span> |<span data-ttu-id="6bcfa-185">Corpo</span><span class="sxs-lookup"><span data-stu-id="6bcfa-185">body</span></span> |<span data-ttu-id="6bcfa-186">O corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="6bcfa-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6bcfa-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bcfa-187">Next steps</span></span>
<span data-ttu-id="6bcfa-188">Agora, experimente a plataforma e [crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6bcfa-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="6bcfa-189">Você pode explorar os outros conectores disponíveis em aplicativos lógicos examinando nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6bcfa-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

