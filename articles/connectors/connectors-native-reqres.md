---
title: "ações de solicitação e resposta aaaUse | Microsoft Docs"
description: "Visão geral de gatilho de solicitação e resposta hello e ação em um aplicativo do Azure lógica"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="8be1a-103">Começar com os componentes de solicitação e resposta Olá</span><span class="sxs-lookup"><span data-stu-id="8be1a-103">Get started with hello request and response components</span></span>
<span data-ttu-id="8be1a-104">Com componentes Olá de solicitação e resposta em um aplicativo da lógica, você pode responder em tempo real tooevents.</span><span class="sxs-lookup"><span data-stu-id="8be1a-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="8be1a-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="8be1a-105">For example, you can:</span></span>

* <span data-ttu-id="8be1a-106">Responda tooan solicitação HTTP com dados de um banco de dados no local por meio de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8be1a-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="8be1a-107">Dispare um aplicativo lógico de um evento de webhook externo.</span><span class="sxs-lookup"><span data-stu-id="8be1a-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="8be1a-108">Chamar um aplicativo lógico com uma ação de solicitação e resposta de dentro de outro aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8be1a-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="8be1a-109">tooget iniciado usando ações de solicitação e resposta de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="8be1a-110">Use Olá gatilho de solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="8be1a-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="8be1a-111">Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8be1a-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="8be1a-112">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="8be1a-113">Aqui está uma sequência de exemplo de como tooset um HTTP solicitar em Olá Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8be1a-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="8be1a-114">Adicionar gatilho Olá **solicitar - quando HTTP de uma solicitação é recebida** em seu aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="8be1a-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="8be1a-115">Opcionalmente, você pode fornecer um esquema JSON (usando uma ferramenta como [JSONSchema.net](http://jsonschema.net)) para o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="8be1a-116">Isso permite que os tokens de designer toogenerate Olá para as propriedades na solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="8be1a-117">Adicione outra ação para que você pode salvar o aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="8be1a-118">Depois de salvar o aplicativo de lógica de hello, você pode obter URL de solicitação HTTP de saudação do cartão de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="8be1a-119">Um HTTP POST (você pode usar uma ferramenta como [carteiro](https://www.getpostman.com/)) gatilhos de URL toohello Olá aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8be1a-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="8be1a-120">Se você não definir uma ação de resposta, um `202 ACCEPTED` resposta é retornada imediatamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="8be1a-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="8be1a-121">Você pode usar o hello resposta ação toocustomize uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8be1a-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Gatilho de resposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="8be1a-123">Use Olá ação de resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="8be1a-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="8be1a-124">Olá ação de resposta HTTP só é válida quando você usá-lo em um fluxo de trabalho que é disparado por uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="8be1a-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="8be1a-125">Se você não definir uma ação de resposta, um `202 ACCEPTED` resposta é retornada imediatamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="8be1a-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="8be1a-126">Você pode adicionar uma ação de resposta em qualquer etapa do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="8be1a-127">Olá lógica aplicativo mantém apenas solicitação de entrada hello aberto por um minuto por uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8be1a-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="8be1a-128">Após um minuto, se nenhuma resposta foi enviada do fluxo de trabalho da saudação (e existe uma ação de resposta na definição de saudação), um `504 GATEWAY TIMEOUT` é retornado toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="8be1a-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="8be1a-129">Aqui está como tooadd uma ação de resposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="8be1a-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="8be1a-130">Selecione Olá **nova etapa** botão.</span><span class="sxs-lookup"><span data-stu-id="8be1a-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="8be1a-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="8be1a-132">Na caixa de pesquisa de ação hello, digite **resposta** Olá toolist ação de resposta.</span><span class="sxs-lookup"><span data-stu-id="8be1a-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Selecione a ação de resposta Olá](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="8be1a-134">Adicione quaisquer parâmetros que são necessários para a mensagem de resposta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Ação de resposta Olá concluída](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="8be1a-136">Clique o canto superior esquerdo de saudação de saudação da barra de ferramentas toosave e sua lógica aplicativo salvará os dois e publicar (Ativar).</span><span class="sxs-lookup"><span data-stu-id="8be1a-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="8be1a-137">Gatilho de solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-137">Request trigger</span></span>
<span data-ttu-id="8be1a-138">Aqui estão os detalhes de saudação disparador Olá que oferece suporte a esse conector.</span><span class="sxs-lookup"><span data-stu-id="8be1a-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="8be1a-139">Há um único gatilho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-139">There is a single request trigger.</span></span>

| <span data-ttu-id="8be1a-140">Gatilho</span><span class="sxs-lookup"><span data-stu-id="8be1a-140">Trigger</span></span> | <span data-ttu-id="8be1a-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="8be1a-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8be1a-142">Solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-142">Request</span></span> |<span data-ttu-id="8be1a-143">Ocorre quando uma solicitação HTTP é recebida</span><span class="sxs-lookup"><span data-stu-id="8be1a-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="8be1a-144">Ação de resposta</span><span class="sxs-lookup"><span data-stu-id="8be1a-144">Response action</span></span>
<span data-ttu-id="8be1a-145">Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector.</span><span class="sxs-lookup"><span data-stu-id="8be1a-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="8be1a-146">Há uma única ação de resposta que pode ser usada apenas quando acompanhada por um gatilho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="8be1a-147">Ação</span><span class="sxs-lookup"><span data-stu-id="8be1a-147">Action</span></span> | <span data-ttu-id="8be1a-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="8be1a-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8be1a-149">Resposta</span><span class="sxs-lookup"><span data-stu-id="8be1a-149">Response</span></span> |<span data-ttu-id="8be1a-150">Retorna que uma resposta toohello correlacionado a solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="8be1a-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="8be1a-151">Detalhes de gatilho e da ação</span><span class="sxs-lookup"><span data-stu-id="8be1a-151">Trigger and action details</span></span>
<span data-ttu-id="8be1a-152">Olá tabelas a seguir descrevem os campos de entrada hello para Olá trigger e action e Olá detalhes de saída correspondente.</span><span class="sxs-lookup"><span data-stu-id="8be1a-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="8be1a-153">Gatilho de solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-153">Request trigger</span></span>
<span data-ttu-id="8be1a-154">a seguir Olá é um campo de entrada para o disparador de saudação de uma solicitação HTTP de entrada.</span><span class="sxs-lookup"><span data-stu-id="8be1a-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="8be1a-155">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="8be1a-155">Display name</span></span> | <span data-ttu-id="8be1a-156">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="8be1a-156">Property name</span></span> | <span data-ttu-id="8be1a-157">Descrição</span><span class="sxs-lookup"><span data-stu-id="8be1a-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8be1a-158">Esquema JSON</span><span class="sxs-lookup"><span data-stu-id="8be1a-158">JSON Schema</span></span> |<span data-ttu-id="8be1a-159">schema</span><span class="sxs-lookup"><span data-stu-id="8be1a-159">schema</span></span> |<span data-ttu-id="8be1a-160">esquema JSON Olá Olá HTTP do corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="8be1a-161">**Detalhes de saída**</span><span class="sxs-lookup"><span data-stu-id="8be1a-161">**Output details**</span></span>

<span data-ttu-id="8be1a-162">Olá seguem detalhes de saída de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8be1a-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="8be1a-163">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="8be1a-163">Property name</span></span> | <span data-ttu-id="8be1a-164">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="8be1a-164">Data type</span></span> | <span data-ttu-id="8be1a-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="8be1a-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8be1a-166">headers</span><span class="sxs-lookup"><span data-stu-id="8be1a-166">Headers</span></span> |<span data-ttu-id="8be1a-167">objeto</span><span class="sxs-lookup"><span data-stu-id="8be1a-167">object</span></span> |<span data-ttu-id="8be1a-168">Cabeçalhos da solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-168">Request headers</span></span> |
| <span data-ttu-id="8be1a-169">Corpo</span><span class="sxs-lookup"><span data-stu-id="8be1a-169">Body</span></span> |<span data-ttu-id="8be1a-170">objeto</span><span class="sxs-lookup"><span data-stu-id="8be1a-170">object</span></span> |<span data-ttu-id="8be1a-171">Objeto da solicitação</span><span class="sxs-lookup"><span data-stu-id="8be1a-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="8be1a-172">Ação de resposta</span><span class="sxs-lookup"><span data-stu-id="8be1a-172">Response action</span></span>
<span data-ttu-id="8be1a-173">Olá seguem campos de entrada para Olá ação de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="8be1a-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="8be1a-174">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8be1a-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="8be1a-175">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="8be1a-175">Display name</span></span> | <span data-ttu-id="8be1a-176">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="8be1a-176">Property name</span></span> | <span data-ttu-id="8be1a-177">Descrição</span><span class="sxs-lookup"><span data-stu-id="8be1a-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8be1a-178">Código de status*</span><span class="sxs-lookup"><span data-stu-id="8be1a-178">Status Code*</span></span> |<span data-ttu-id="8be1a-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="8be1a-179">statusCode</span></span> |<span data-ttu-id="8be1a-180">Olá, código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="8be1a-180">hello HTTP status code</span></span> |
| <span data-ttu-id="8be1a-181">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="8be1a-181">Headers</span></span> |<span data-ttu-id="8be1a-182">headers</span><span class="sxs-lookup"><span data-stu-id="8be1a-182">headers</span></span> |<span data-ttu-id="8be1a-183">Um objeto JSON de qualquer tooinclude de cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="8be1a-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="8be1a-184">Corpo</span><span class="sxs-lookup"><span data-stu-id="8be1a-184">Body</span></span> |<span data-ttu-id="8be1a-185">body</span><span class="sxs-lookup"><span data-stu-id="8be1a-185">body</span></span> |<span data-ttu-id="8be1a-186">corpo da resposta Olá</span><span class="sxs-lookup"><span data-stu-id="8be1a-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8be1a-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8be1a-187">Next steps</span></span>
<span data-ttu-id="8be1a-188">Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8be1a-189">Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

