---
title: "Comunicar-se com qualquer ponto de extremidade por meio de HTTP – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie aplicativos lógicos que possam se comunicar com qualquer ponto de extremidade via HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="619b9-103">Introdução à ação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-103">Get started with the HTTP action</span></span>

<span data-ttu-id="619b9-104">Com a ação HTTP, você pode estender os fluxos de trabalho para a sua organização e se comunicar com qualquer ponto de extremidade por HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="619b9-105">Você pode:</span><span class="sxs-lookup"><span data-stu-id="619b9-105">You can:</span></span>

* <span data-ttu-id="619b9-106">Crie fluxos de trabalho de aplicativo lógico que são ativados (disparam) quando um site que você gerencia é desativado.</span><span class="sxs-lookup"><span data-stu-id="619b9-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="619b9-107">Comunique-se com qualquer ponto de extremidade por HTTP para estender seus fluxos de trabalho para outros serviços.</span><span class="sxs-lookup"><span data-stu-id="619b9-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="619b9-108">Para começar a usar a ação HTTP em um aplicativo lógico, confira [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="619b9-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="619b9-109">Usar o gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-109">Use the HTTP trigger</span></span>
<span data-ttu-id="619b9-110">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="619b9-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="619b9-111">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="619b9-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="619b9-112">Veja uma sequência de exemplo de como configurar um gatilho HTTP no Designer de Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="619b9-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="619b9-113">Adicione o gatilho HTTP no seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="619b9-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="619b9-114">Preencha os parâmetros do ponto de extremidade HTTP que deseja sondar.</span><span class="sxs-lookup"><span data-stu-id="619b9-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="619b9-115">Modifique o intervalo de recorrência quanto à frequência que ele deve ser sondado.</span><span class="sxs-lookup"><span data-stu-id="619b9-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="619b9-116">Agora, o aplicativo lógico é disparado com qualquer conteúdo retornado durante cada verificação.</span><span class="sxs-lookup"><span data-stu-id="619b9-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![Gatilho HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="619b9-118">Como o gatilho HTTP funciona</span><span class="sxs-lookup"><span data-stu-id="619b9-118">How the HTTP trigger works</span></span>

<span data-ttu-id="619b9-119">O gatilho HTTP envia uma chamada para um ponto de extremidade HTTP em um intervalo recorrente.</span><span class="sxs-lookup"><span data-stu-id="619b9-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="619b9-120">Por padrão, qualquer código de resposta HTTP menor do que 300 faz com que um aplicativo lógico seja executado.</span><span class="sxs-lookup"><span data-stu-id="619b9-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="619b9-121">Para especificar se o aplicativo lógico deve ser disparado, você pode editar o aplicativo lógico no modo de exibição de código e adicionar uma condição que é avaliada após a chamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="619b9-122">Veja um exemplo de um gatilho HTTP que será disparado sempre que o código de status retornado for maior ou igual a `400`.</span><span class="sxs-lookup"><span data-stu-id="619b9-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="619b9-123">Os detalhes completos sobre os parâmetros de gatilho HTTP estão disponíveis no [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="619b9-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="619b9-124">Usar a ação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-124">Use the HTTP action</span></span>

<span data-ttu-id="619b9-125">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="619b9-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="619b9-126">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="619b9-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="619b9-127">Escolha **Nova Etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="619b9-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="619b9-128">Na caixa de pesquisa de ação, digite **http** para listar as ações HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Selecionar a ação HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="619b9-130">Adicione quaisquer parâmetros necessários para a chamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Concluir a ação HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="619b9-132">Clique em **Salvar** na barra de ferramentas do designer.</span><span class="sxs-lookup"><span data-stu-id="619b9-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="619b9-133">Seu aplicativo lógico é salvo e publicado (ativado) simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="619b9-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="619b9-134">Gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-134">HTTP trigger</span></span>
<span data-ttu-id="619b9-135">Veja os detalhes do gatilho com suporte deste conector.</span><span class="sxs-lookup"><span data-stu-id="619b9-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="619b9-136">O conector HTTP tem um gatilho.</span><span class="sxs-lookup"><span data-stu-id="619b9-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="619b9-137">Gatilho</span><span class="sxs-lookup"><span data-stu-id="619b9-137">Trigger</span></span> | <span data-ttu-id="619b9-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="619b9-139">http</span><span class="sxs-lookup"><span data-stu-id="619b9-139">HTTP</span></span> |<span data-ttu-id="619b9-140">Faz uma chamada HTTP e retorna o conteúdo da resposta.</span><span class="sxs-lookup"><span data-stu-id="619b9-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="619b9-141">Ação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-141">HTTP action</span></span>
<span data-ttu-id="619b9-142">Veja os detalhes da ação com suporte deste conector.</span><span class="sxs-lookup"><span data-stu-id="619b9-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="619b9-143">O conector HTTP tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="619b9-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="619b9-144">Ação</span><span class="sxs-lookup"><span data-stu-id="619b9-144">Action</span></span> | <span data-ttu-id="619b9-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="619b9-146">http</span><span class="sxs-lookup"><span data-stu-id="619b9-146">HTTP</span></span> |<span data-ttu-id="619b9-147">Faz uma chamada HTTP e retorna o conteúdo da resposta.</span><span class="sxs-lookup"><span data-stu-id="619b9-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="619b9-148">Detalhes do HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-148">HTTP details</span></span>
<span data-ttu-id="619b9-149">As tabelas a seguir descrevem os campos de entrada obrigatórios e opcionais para a ação e os detalhes de saída correspondentes associados ao uso da ação.</span><span class="sxs-lookup"><span data-stu-id="619b9-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="619b9-150">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-150">HTTP request</span></span>
<span data-ttu-id="619b9-151">Estes são os campos de entrada para a ação, o que cria uma solicitação HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="619b9-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="619b9-152">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="619b9-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="619b9-153">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="619b9-153">Display name</span></span> | <span data-ttu-id="619b9-154">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="619b9-154">Property name</span></span> | <span data-ttu-id="619b9-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619b9-156">Método*</span><span class="sxs-lookup"><span data-stu-id="619b9-156">Method*</span></span> |<span data-ttu-id="619b9-157">estático</span><span class="sxs-lookup"><span data-stu-id="619b9-157">method</span></span> |<span data-ttu-id="619b9-158">Verbo HTTP a ser usado</span><span class="sxs-lookup"><span data-stu-id="619b9-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="619b9-159">URI*</span><span class="sxs-lookup"><span data-stu-id="619b9-159">URI*</span></span> |<span data-ttu-id="619b9-160">uri</span><span class="sxs-lookup"><span data-stu-id="619b9-160">uri</span></span> |<span data-ttu-id="619b9-161">O URI para a solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="619b9-162">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="619b9-162">Headers</span></span> |<span data-ttu-id="619b9-163">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="619b9-163">headers</span></span> |<span data-ttu-id="619b9-164">Um objeto JSON de cabeçalhos HTTP a serem incluídos</span><span class="sxs-lookup"><span data-stu-id="619b9-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="619b9-165">Corpo</span><span class="sxs-lookup"><span data-stu-id="619b9-165">Body</span></span> |<span data-ttu-id="619b9-166">Corpo</span><span class="sxs-lookup"><span data-stu-id="619b9-166">body</span></span> |<span data-ttu-id="619b9-167">O corpo da solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-167">The HTTP request body</span></span> |
| <span data-ttu-id="619b9-168">Autenticação</span><span class="sxs-lookup"><span data-stu-id="619b9-168">Authentication</span></span> |<span data-ttu-id="619b9-169">Autenticação</span><span class="sxs-lookup"><span data-stu-id="619b9-169">authentication</span></span> |<span data-ttu-id="619b9-170">Os detalhes na seção [Autenticação](#authentication)</span><span class="sxs-lookup"><span data-stu-id="619b9-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="619b9-171">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="619b9-171">Output details</span></span>
<span data-ttu-id="619b9-172">A seguir, os detalhes de saída para a resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="619b9-173">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="619b9-173">Property name</span></span> | <span data-ttu-id="619b9-174">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="619b9-174">Data type</span></span> | <span data-ttu-id="619b9-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619b9-176">headers</span><span class="sxs-lookup"><span data-stu-id="619b9-176">Headers</span></span> |<span data-ttu-id="619b9-177">objeto</span><span class="sxs-lookup"><span data-stu-id="619b9-177">object</span></span> |<span data-ttu-id="619b9-178">Cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="619b9-178">Response headers</span></span> |
| <span data-ttu-id="619b9-179">Corpo</span><span class="sxs-lookup"><span data-stu-id="619b9-179">Body</span></span> |<span data-ttu-id="619b9-180">objeto</span><span class="sxs-lookup"><span data-stu-id="619b9-180">object</span></span> |<span data-ttu-id="619b9-181">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="619b9-181">Response object</span></span> |
| <span data-ttu-id="619b9-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="619b9-182">Status Code</span></span> |<span data-ttu-id="619b9-183">int</span><span class="sxs-lookup"><span data-stu-id="619b9-183">int</span></span> |<span data-ttu-id="619b9-184">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="619b9-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="619b9-185">Autenticação</span><span class="sxs-lookup"><span data-stu-id="619b9-185">Authentication</span></span>
<span data-ttu-id="619b9-186">O recurso de Aplicativos Lógicos permitem que você use diferentes tipos de autenticação em pontos de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="619b9-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="619b9-187">Você pode usar essa autenticação com os conectores **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)** e **[Webhook HTTP](connectors-native-webhook.md)**.</span><span class="sxs-lookup"><span data-stu-id="619b9-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="619b9-188">Os seguintes tipos de autenticação são configuráveis:</span><span class="sxs-lookup"><span data-stu-id="619b9-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="619b9-189">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="619b9-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="619b9-190">Autenticação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="619b9-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="619b9-191">Autenticação OAuth do Azure AD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="619b9-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="619b9-192">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="619b9-192">Basic authentication</span></span>

<span data-ttu-id="619b9-193">O seguinte objeto de autenticação é necessário para a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="619b9-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="619b9-194">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="619b9-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="619b9-195">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="619b9-195">Property name</span></span> | <span data-ttu-id="619b9-196">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="619b9-196">Data type</span></span> | <span data-ttu-id="619b9-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619b9-198">Type*</span><span class="sxs-lookup"><span data-stu-id="619b9-198">Type*</span></span> |<span data-ttu-id="619b9-199">type</span><span class="sxs-lookup"><span data-stu-id="619b9-199">type</span></span> |<span data-ttu-id="619b9-200">Tipo de autenticação (deve ser `Basic` para a autenticação básica)</span><span class="sxs-lookup"><span data-stu-id="619b9-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="619b9-201">Username*</span><span class="sxs-lookup"><span data-stu-id="619b9-201">Username*</span></span> |<span data-ttu-id="619b9-202">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="619b9-202">username</span></span> |<span data-ttu-id="619b9-203">Nome de usuário para autenticar</span><span class="sxs-lookup"><span data-stu-id="619b9-203">User name to authenticate</span></span> |
| <span data-ttu-id="619b9-204">Password*</span><span class="sxs-lookup"><span data-stu-id="619b9-204">Password*</span></span> |<span data-ttu-id="619b9-205">Senha</span><span class="sxs-lookup"><span data-stu-id="619b9-205">password</span></span> |<span data-ttu-id="619b9-206">Senha para autenticação</span><span class="sxs-lookup"><span data-stu-id="619b9-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="619b9-207">Se você quiser usar uma senha que não é possível recuperar na definição, use um parâmetro `securestring` e a `@parameters()` 
> [função de definição do fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="619b9-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="619b9-208">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="619b9-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="619b9-209">Autenticação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="619b9-209">Client certificate authentication</span></span>

<span data-ttu-id="619b9-210">O seguinte objeto de autenticação é necessário para a autenticação de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="619b9-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="619b9-211">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="619b9-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="619b9-212">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="619b9-212">Property name</span></span> | <span data-ttu-id="619b9-213">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="619b9-213">Data type</span></span> | <span data-ttu-id="619b9-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619b9-215">Type*</span><span class="sxs-lookup"><span data-stu-id="619b9-215">Type*</span></span> |<span data-ttu-id="619b9-216">type</span><span class="sxs-lookup"><span data-stu-id="619b9-216">type</span></span> |<span data-ttu-id="619b9-217">O tipo de autenticação (deve ser `ClientCertificate` para certificados de cliente SSL)</span><span class="sxs-lookup"><span data-stu-id="619b9-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="619b9-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="619b9-218">PFX*</span></span> |<span data-ttu-id="619b9-219">pfx</span><span class="sxs-lookup"><span data-stu-id="619b9-219">pfx</span></span> |<span data-ttu-id="619b9-220">O conteúdo codificado na Base64 do arquivo Personal Information Exchange (PFX)</span><span class="sxs-lookup"><span data-stu-id="619b9-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="619b9-221">Password*</span><span class="sxs-lookup"><span data-stu-id="619b9-221">Password*</span></span> |<span data-ttu-id="619b9-222">Senha</span><span class="sxs-lookup"><span data-stu-id="619b9-222">password</span></span> |<span data-ttu-id="619b9-223">A senha para acessar o arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="619b9-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="619b9-224">Para usar um parâmetro que não será legível na definição após salvar o aplicativo lógico, você poderá usar um parâmetro `securestring` e a `@parameters()` 
> [função de definição do fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="619b9-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="619b9-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="619b9-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="619b9-226">Autenticação OAuth do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619b9-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="619b9-227">O seguinte objeto de autenticação é necessário para a autenticação OAuth do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="619b9-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="619b9-228">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="619b9-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="619b9-229">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="619b9-229">Property name</span></span> | <span data-ttu-id="619b9-230">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="619b9-230">Data type</span></span> | <span data-ttu-id="619b9-231">Descrição</span><span class="sxs-lookup"><span data-stu-id="619b9-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="619b9-232">Type*</span><span class="sxs-lookup"><span data-stu-id="619b9-232">Type*</span></span> |<span data-ttu-id="619b9-233">type</span><span class="sxs-lookup"><span data-stu-id="619b9-233">type</span></span> |<span data-ttu-id="619b9-234">O tipo de autenticação (deve ser `ActiveDirectoryOAuth` para a autenticação OAuth do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="619b9-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="619b9-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="619b9-235">Tenant*</span></span> |<span data-ttu-id="619b9-236">locatário</span><span class="sxs-lookup"><span data-stu-id="619b9-236">tenant</span></span> |<span data-ttu-id="619b9-237">O identificador do locatário para o locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619b9-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="619b9-238">Audience*</span><span class="sxs-lookup"><span data-stu-id="619b9-238">Audience*</span></span> |<span data-ttu-id="619b9-239">audiência</span><span class="sxs-lookup"><span data-stu-id="619b9-239">audience</span></span> |<span data-ttu-id="619b9-240">O recurso para cujo uso você está solicitando autorização.</span><span class="sxs-lookup"><span data-stu-id="619b9-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="619b9-241">Por exemplo: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="619b9-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="619b9-242">Client ID*</span><span class="sxs-lookup"><span data-stu-id="619b9-242">Client ID*</span></span> |<span data-ttu-id="619b9-243">clientId</span><span class="sxs-lookup"><span data-stu-id="619b9-243">clientId</span></span> |<span data-ttu-id="619b9-244">O identificador de cliente para o aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619b9-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="619b9-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="619b9-245">Secret*</span></span> |<span data-ttu-id="619b9-246">segredo</span><span class="sxs-lookup"><span data-stu-id="619b9-246">secret</span></span> |<span data-ttu-id="619b9-247">O segredo do cliente que está solicitando o token</span><span class="sxs-lookup"><span data-stu-id="619b9-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="619b9-248">Você pode usar um parâmetro `securestring` e a `@parameters()` [função de definição do fluxo de trabalho](http://aka.ms/logicappdocs) para usar um parâmetro que não será legível na definição depois de salvar.</span><span class="sxs-lookup"><span data-stu-id="619b9-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="619b9-249">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="619b9-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="619b9-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="619b9-250">Next steps</span></span>
<span data-ttu-id="619b9-251">Agora, experimente a plataforma e [crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="619b9-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="619b9-252">Você pode explorar os outros conectores disponíveis em aplicativos lógicos examinando nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="619b9-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

