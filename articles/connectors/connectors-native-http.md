---
title: "aaaCommunicate com qualquer ponto de extremidade via HTTP - os aplicativos lógicos do Azure | Microsoft Docs"
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
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="b1fd3-103">Introdução ao Olá ação HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="b1fd3-104">Com hello ação HTTP, você pode estender os fluxos de trabalho para a sua organização e comunicar-se o ponto de extremidade tooany via HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="b1fd3-105">Você pode:</span><span class="sxs-lookup"><span data-stu-id="b1fd3-105">You can:</span></span>

* <span data-ttu-id="b1fd3-106">Crie fluxos de trabalho de aplicativo lógico que são ativados (disparam) quando um site que você gerencia é desativado.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="b1fd3-107">Se comunicam tooany de ponto de extremidade por HTTP tooextend seus fluxos de trabalho em outros serviços.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="b1fd3-108">tooget iniciado usando a ação de saudação HTTP em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="b1fd3-109">Use o gatilho Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="b1fd3-110">Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="b1fd3-111">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="b1fd3-112">Aqui está uma sequência de exemplo de como tooset backup Olá HTTP gatilho Olá Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="b1fd3-113">Adicione o gatilho HTTP de saudação em seu aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="b1fd3-114">Preencha os parâmetros de saudação para o ponto de extremidade de saudação HTTP que você deseja toopoll.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="b1fd3-115">Modificar o intervalo de recorrência de saudação na frequência com a qual ele deve pesquisar.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="b1fd3-116">Olá lógica aplicativo agora é acionado com qualquer conteúdo que é retornado durante cada verificação.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Gatilho HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="b1fd3-118">Como funciona o gatilho HTTP Olá</span><span class="sxs-lookup"><span data-stu-id="b1fd3-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="b1fd3-119">gatilho HTTP Olá envia um ponto de extremidade de tooHTTP chamada em um intervalo recorrente.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="b1fd3-120">Por padrão, qualquer código de resposta HTTP é menor que 300 faz com que um toorun de aplicativo lógica.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="b1fd3-121">toospecify se deve acionar o aplicativo lógico de Olá, você pode editar aplicativo de lógica de saudação na exibição de código e adicionar uma condição que é avaliada após Olá chamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="b1fd3-122">Aqui está um exemplo de um gatilho HTTP que é acionado quando a saudação retornou o código de status é maior que ou igual a muito`400`.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

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

<span data-ttu-id="b1fd3-123">Detalhes completos sobre os parâmetros de gatilho Olá HTTP estão disponíveis em [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="b1fd3-124">Use a ação Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-124">Use hello HTTP action</span></span>

<span data-ttu-id="b1fd3-125">Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="b1fd3-126">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="b1fd3-127">Escolha **Nova Etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="b1fd3-128">Na caixa de pesquisa de ação hello, digite **http** ações de saudação HTTP toolist.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Selecione a ação Olá HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="b1fd3-130">Adicione os parâmetros necessários para a chamada de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Olá completa ação HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="b1fd3-132">Na barra de ferramentas designer hello, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="b1fd3-133">Seu aplicativo lógico é salvo e publicado (ativado) no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="b1fd3-134">Gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-134">HTTP trigger</span></span>
<span data-ttu-id="b1fd3-135">Aqui estão os detalhes de saudação disparador Olá que oferece suporte a esse conector.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="b1fd3-136">conector HTTP Olá tem um gatilho.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="b1fd3-137">Gatilho</span><span class="sxs-lookup"><span data-stu-id="b1fd3-137">Trigger</span></span> | <span data-ttu-id="b1fd3-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1fd3-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-139">HTTP</span></span> |<span data-ttu-id="b1fd3-140">Faz uma chamada HTTP e retorna o conteúdo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="b1fd3-141">Ação HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-141">HTTP action</span></span>
<span data-ttu-id="b1fd3-142">Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="b1fd3-143">conector HTTP Olá tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="b1fd3-144">Ação</span><span class="sxs-lookup"><span data-stu-id="b1fd3-144">Action</span></span> | <span data-ttu-id="b1fd3-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1fd3-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-146">HTTP</span></span> |<span data-ttu-id="b1fd3-147">Faz uma chamada HTTP e retorna o conteúdo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="b1fd3-148">Detalhes do HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-148">HTTP details</span></span>
<span data-ttu-id="b1fd3-149">Olá tabelas a seguir descrevem hello necessárias e os campos de entrada opcionais para ação hello e Olá correspondente saída detalhes associados usando a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="b1fd3-150">Solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-150">HTTP request</span></span>
<span data-ttu-id="b1fd3-151">Olá seguem campos de entrada para a ação de saudação, que faz uma solicitação HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="b1fd3-152">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="b1fd3-153">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-153">Display name</span></span> | <span data-ttu-id="b1fd3-154">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="b1fd3-154">Property name</span></span> | <span data-ttu-id="b1fd3-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1fd3-156">Método*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-156">Method*</span></span> |<span data-ttu-id="b1fd3-157">estático</span><span class="sxs-lookup"><span data-stu-id="b1fd3-157">method</span></span> |<span data-ttu-id="b1fd3-158">Olá HTTP verbo toouse</span><span class="sxs-lookup"><span data-stu-id="b1fd3-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="b1fd3-159">URI*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-159">URI*</span></span> |<span data-ttu-id="b1fd3-160">uri</span><span class="sxs-lookup"><span data-stu-id="b1fd3-160">uri</span></span> |<span data-ttu-id="b1fd3-161">Olá URI de solicitação HTTP de saudação</span><span class="sxs-lookup"><span data-stu-id="b1fd3-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="b1fd3-162">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="b1fd3-162">Headers</span></span> |<span data-ttu-id="b1fd3-163">headers</span><span class="sxs-lookup"><span data-stu-id="b1fd3-163">headers</span></span> |<span data-ttu-id="b1fd3-164">Um objeto JSON de tooinclude de cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="b1fd3-165">Corpo</span><span class="sxs-lookup"><span data-stu-id="b1fd3-165">Body</span></span> |<span data-ttu-id="b1fd3-166">body</span><span class="sxs-lookup"><span data-stu-id="b1fd3-166">body</span></span> |<span data-ttu-id="b1fd3-167">saudação de corpo de solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-167">hello HTTP request body</span></span> |
| <span data-ttu-id="b1fd3-168">Autenticação</span><span class="sxs-lookup"><span data-stu-id="b1fd3-168">Authentication</span></span> |<span data-ttu-id="b1fd3-169">Autenticação</span><span class="sxs-lookup"><span data-stu-id="b1fd3-169">authentication</span></span> |<span data-ttu-id="b1fd3-170">Detalhes de saudação [autenticação](#authentication) seção</span><span class="sxs-lookup"><span data-stu-id="b1fd3-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="b1fd3-171">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="b1fd3-171">Output details</span></span>
<span data-ttu-id="b1fd3-172">Olá seguem detalhes de saída de hello resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="b1fd3-173">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="b1fd3-173">Property name</span></span> | <span data-ttu-id="b1fd3-174">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="b1fd3-174">Data type</span></span> | <span data-ttu-id="b1fd3-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1fd3-176">headers</span><span class="sxs-lookup"><span data-stu-id="b1fd3-176">Headers</span></span> |<span data-ttu-id="b1fd3-177">objeto</span><span class="sxs-lookup"><span data-stu-id="b1fd3-177">object</span></span> |<span data-ttu-id="b1fd3-178">Cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="b1fd3-178">Response headers</span></span> |
| <span data-ttu-id="b1fd3-179">Corpo</span><span class="sxs-lookup"><span data-stu-id="b1fd3-179">Body</span></span> |<span data-ttu-id="b1fd3-180">objeto</span><span class="sxs-lookup"><span data-stu-id="b1fd3-180">object</span></span> |<span data-ttu-id="b1fd3-181">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="b1fd3-181">Response object</span></span> |
| <span data-ttu-id="b1fd3-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="b1fd3-182">Status Code</span></span> |<span data-ttu-id="b1fd3-183">int</span><span class="sxs-lookup"><span data-stu-id="b1fd3-183">int</span></span> |<span data-ttu-id="b1fd3-184">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="b1fd3-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="b1fd3-185">Autenticação</span><span class="sxs-lookup"><span data-stu-id="b1fd3-185">Authentication</span></span>
<span data-ttu-id="b1fd3-186">recurso de aplicativos lógicos Olá permite toouse diferentes tipos de autenticação em relação a pontos de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="b1fd3-187">Você pode usar essa autenticação com hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  conectores.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="b1fd3-188">Olá, tipos de autenticação a seguir podem ser configurado:</span><span class="sxs-lookup"><span data-stu-id="b1fd3-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="b1fd3-189">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="b1fd3-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="b1fd3-190">Autenticação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b1fd3-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="b1fd3-191">Autenticação OAuth do Azure AD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="b1fd3-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="b1fd3-192">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="b1fd3-192">Basic authentication</span></span>

<span data-ttu-id="b1fd3-193">Olá, objeto de autenticação a seguir é necessário para a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="b1fd3-194">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="b1fd3-195">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="b1fd3-195">Property name</span></span> | <span data-ttu-id="b1fd3-196">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="b1fd3-196">Data type</span></span> | <span data-ttu-id="b1fd3-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1fd3-198">Type*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-198">Type*</span></span> |<span data-ttu-id="b1fd3-199">type</span><span class="sxs-lookup"><span data-stu-id="b1fd3-199">type</span></span> |<span data-ttu-id="b1fd3-200">Tipo de autenticação (deve ser `Basic` para a autenticação básica)</span><span class="sxs-lookup"><span data-stu-id="b1fd3-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="b1fd3-201">Username*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-201">Username*</span></span> |<span data-ttu-id="b1fd3-202">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="b1fd3-202">username</span></span> |<span data-ttu-id="b1fd3-203">Tooauthenticate de nome de usuário</span><span class="sxs-lookup"><span data-stu-id="b1fd3-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="b1fd3-204">Password*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-204">Password*</span></span> |<span data-ttu-id="b1fd3-205">Senha</span><span class="sxs-lookup"><span data-stu-id="b1fd3-205">password</span></span> |<span data-ttu-id="b1fd3-206">Senha tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="b1fd3-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="b1fd3-207">Se você quiser toouse uma senha que não é possível recuperar definição hello, use um `securestring` parâmetro e hello `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="b1fd3-208">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1fd3-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="b1fd3-209">Autenticação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b1fd3-209">Client certificate authentication</span></span>

<span data-ttu-id="b1fd3-210">Olá seguinte objeto de autenticação é necessária para autenticação de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="b1fd3-211">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="b1fd3-212">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="b1fd3-212">Property name</span></span> | <span data-ttu-id="b1fd3-213">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="b1fd3-213">Data type</span></span> | <span data-ttu-id="b1fd3-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1fd3-215">Type*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-215">Type*</span></span> |<span data-ttu-id="b1fd3-216">type</span><span class="sxs-lookup"><span data-stu-id="b1fd3-216">type</span></span> |<span data-ttu-id="b1fd3-217">Olá o tipo de autenticação (deve ser `ClientCertificate` para certificados de cliente SSL)</span><span class="sxs-lookup"><span data-stu-id="b1fd3-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="b1fd3-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-218">PFX*</span></span> |<span data-ttu-id="b1fd3-219">pfx</span><span class="sxs-lookup"><span data-stu-id="b1fd3-219">pfx</span></span> |<span data-ttu-id="b1fd3-220">conteúdo codificado com Base64 de saudação do arquivo de troca de informações pessoais (PFX) Olá</span><span class="sxs-lookup"><span data-stu-id="b1fd3-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="b1fd3-221">Password*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-221">Password*</span></span> |<span data-ttu-id="b1fd3-222">Senha</span><span class="sxs-lookup"><span data-stu-id="b1fd3-222">password</span></span> |<span data-ttu-id="b1fd3-223">Olá senha tooaccess Olá arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="b1fd3-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="b1fd3-224">um parâmetro que não será legível na definição de saudação depois de salvar o aplicativo de lógica de saudação do toouse, você pode usar um `securestring` parâmetro e hello `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="b1fd3-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1fd3-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="b1fd3-226">Autenticação OAuth do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1fd3-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="b1fd3-227">Olá, objeto de autenticação a seguir é necessário para autenticação OAuth do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="b1fd3-228">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="b1fd3-229">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="b1fd3-229">Property name</span></span> | <span data-ttu-id="b1fd3-230">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="b1fd3-230">Data type</span></span> | <span data-ttu-id="b1fd3-231">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1fd3-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1fd3-232">Type*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-232">Type*</span></span> |<span data-ttu-id="b1fd3-233">type</span><span class="sxs-lookup"><span data-stu-id="b1fd3-233">type</span></span> |<span data-ttu-id="b1fd3-234">Olá o tipo de autenticação (deve ser `ActiveDirectoryOAuth` para OAuth do AD do Azure)</span><span class="sxs-lookup"><span data-stu-id="b1fd3-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="b1fd3-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-235">Tenant*</span></span> |<span data-ttu-id="b1fd3-236">locatário</span><span class="sxs-lookup"><span data-stu-id="b1fd3-236">tenant</span></span> |<span data-ttu-id="b1fd3-237">Identificador do locatário Olá para o locatário de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b1fd3-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="b1fd3-238">Audience*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-238">Audience*</span></span> |<span data-ttu-id="b1fd3-239">audiência</span><span class="sxs-lookup"><span data-stu-id="b1fd3-239">audience</span></span> |<span data-ttu-id="b1fd3-240">recurso Hello está solicitando toouse de autorização.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="b1fd3-241">Por exemplo: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="b1fd3-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="b1fd3-242">Client ID*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-242">Client ID*</span></span> |<span data-ttu-id="b1fd3-243">clientId</span><span class="sxs-lookup"><span data-stu-id="b1fd3-243">clientId</span></span> |<span data-ttu-id="b1fd3-244">Olá identificador de cliente para o aplicativo hello AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b1fd3-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="b1fd3-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="b1fd3-245">Secret*</span></span> |<span data-ttu-id="b1fd3-246">segredo</span><span class="sxs-lookup"><span data-stu-id="b1fd3-246">secret</span></span> |<span data-ttu-id="b1fd3-247">segredo de saudação do cliente de saudação que está solicitando o token Olá</span><span class="sxs-lookup"><span data-stu-id="b1fd3-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="b1fd3-248">Você pode usar um `securestring` parâmetro e hello `@parameters()` [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs) toouse um parâmetro que não será legível na definição de saudação depois de salvar.</span><span class="sxs-lookup"><span data-stu-id="b1fd3-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="b1fd3-249">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1fd3-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="b1fd3-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1fd3-250">Next steps</span></span>
<span data-ttu-id="b1fd3-251">Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b1fd3-252">Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b1fd3-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

