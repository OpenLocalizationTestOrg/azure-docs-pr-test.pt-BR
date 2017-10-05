---
title: "Chamar, disparar ou aninhar fluxos de trabalho com pontos de extremidade HTTP – Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Configurar pontos de extremidade HTTP para chamar, disparar ou aninhar fluxos de trabalho para Aplicativos Lógicos do Azure"
services: logic-apps
keywords: fluxos de trabalho, pontos de extremidade HTTP
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="d33c9-104">Chamar, disparar ou aninhar fluxos de trabalho com pontos de extremidade HTTP em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d33c9-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="d33c9-105">Você pode expor nativamente pontos de extremidade HTTP síncronos como gatilhos em aplicativos lógicos para que seja possível disparar ou chamar aplicativos lógicos por meio de uma URL.</span><span class="sxs-lookup"><span data-stu-id="d33c9-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="d33c9-106">Também é possível aninhar fluxos de trabalho em aplicativos lógicos usando um padrão de pontos de extremidade resgatáveis.</span><span class="sxs-lookup"><span data-stu-id="d33c9-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="d33c9-107">Para criar pontos de extremidade HTTP, você pode adicionar esses gatilhos para que seus aplicativos lógicos possam receber solicitações de entrada:</span><span class="sxs-lookup"><span data-stu-id="d33c9-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="d33c9-108">Solicitação</span><span class="sxs-lookup"><span data-stu-id="d33c9-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="d33c9-109">Webhook de Conexão de API</span><span class="sxs-lookup"><span data-stu-id="d33c9-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="d33c9-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="d33c9-111">Embora nossos exemplos usem o gatilho **Solicitar**, você pode usar qualquer um dos gatilhos HTTP listados e todos os princípios se aplicam de modo idêntico a outros tipos de gatilho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="d33c9-112">Configurar um ponto de extremidade HTTP para o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="d33c9-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="d33c9-113">Para criar um ponto de extremidade HTTP, adicione um gatilho que possa receber solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="d33c9-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="d33c9-114">Entre no [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="d33c9-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="d33c9-115">Vá até o aplicativo lógico e abra o Designer do Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="d33c9-116">Adicione um gatilho que permita ao aplicativo lógico receber solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="d33c9-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="d33c9-117">Por exemplo, adicione o gatilho **Solicitação** em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="d33c9-118">Em **Esquema JSON do Corpo da Solicitação**, se desejar, você pode inserir um esquema JSON para o conteúdo que espera receber.</span><span class="sxs-lookup"><span data-stu-id="d33c9-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="d33c9-119">O designer usa esse esquema para gerar tokens que o aplicativo lógico pode usar para consumir, analisar e transmitir dados do gatilho por meio do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="d33c9-120">Saiba mais sobre [tokens gerados de esquemas JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="d33c9-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="d33c9-121">Para este exemplo, digite o esquema mostrado no designer:</span><span class="sxs-lookup"><span data-stu-id="d33c9-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Adicionar a ação Solicitar][1]

    > [!TIP]
    > 
    > <span data-ttu-id="d33c9-123">Você pode gerar um esquema para um conteúdo JSON de exemplo usando uma ferramenta como [jsonschema.net](http://jsonschema.net/) ou no gatilho **Solicitar** escolhendo **Use o conteúdo de amostra para gerar o esquema**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="d33c9-124">Insira o conteúdo de exemplo e escolha **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="d33c9-125">Por exemplo, este conteúdo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="d33c9-126">gera este esquema:</span><span class="sxs-lookup"><span data-stu-id="d33c9-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="d33c9-127">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-127">Save your logic app.</span></span> <span data-ttu-id="d33c9-128">Em **HTTP POST para esta URL**, agora você deve encontrar uma URL de retorno de chamada gerada, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL de retorno de chamada gerada para ponto de extremidade](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="d33c9-130">Essa URL contém uma chave de SAS (Assinatura de Acesso Compartilhado) nos parâmetros de consulta usados para autenticação.</span><span class="sxs-lookup"><span data-stu-id="d33c9-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="d33c9-131">Você também pode obter a URL de ponto de extremidade HTTP da visão geral do aplicativo lógico no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d33c9-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="d33c9-132">Em **Histórico de Gatilho**, selecione o gatilho:</span><span class="sxs-lookup"><span data-stu-id="d33c9-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obter a URL de ponto de extremidade HTTP no portal do Azure][2]

    <span data-ttu-id="d33c9-134">Ou você pode obter a URL fazendo esta chamada:</span><span class="sxs-lookup"><span data-stu-id="d33c9-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="d33c9-135">Alterar o método HTTP para o gatilho</span><span class="sxs-lookup"><span data-stu-id="d33c9-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="d33c9-136">Por padrão, o gatilho **Solicitar** espera uma solicitação HTTP POST, mas você pode usar um método HTTP diferente.</span><span class="sxs-lookup"><span data-stu-id="d33c9-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="d33c9-137">Você pode especificar somente um tipo de método.</span><span class="sxs-lookup"><span data-stu-id="d33c9-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="d33c9-138">No gatilho **Solicitar**, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="d33c9-139">Abra a lista **Método**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-139">Open the **Method** list.</span></span> <span data-ttu-id="d33c9-140">Para este exemplo, selecione **GET** para que você possa testar posteriormente sua URL de ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="d33c9-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d33c9-141">É possível selecionar qualquer outro método HTTP ou especificar um método personalizado para seu próprio aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Alterar método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="d33c9-143">Aceitar parâmetros por meio da URL de ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="d33c9-144">Quando desejar que a URL de ponto de extremidade HTTP aceite parâmetros, personalize o caminho relativo do gatilho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="d33c9-145">No gatilho **Solicitar**, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="d33c9-146">Em **Método**, especifique o método HTTP que deseja que sua solicitação use.</span><span class="sxs-lookup"><span data-stu-id="d33c9-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="d33c9-147">Para este exemplo, selecione o método **GET**, se ainda não o fez, para que seja possível testar a URL de ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="d33c9-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d33c9-148">Ao especificar um caminho relativo para o gatilho, você deve especificar explicitamente um método HTTP para o gatilho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="d33c9-149">Em **Caminho relativo**, especifique o caminho relativo para o parâmetro que sua URL deve aceitar, por exemplo, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="d33c9-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Especificar o método HTTP e o caminho relativo para o parâmetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="d33c9-151">Para usar o parâmetro, adicione uma ação **Resposta** ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="d33c9-152">(No gatilho, escolha **Nova etapa** > **Adicionar uma ação** > **Resposta**)</span><span class="sxs-lookup"><span data-stu-id="d33c9-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="d33c9-153">No **Corpo** da resposta, inclua o token para o parâmetro que você especificou no caminho relativo do gatilho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="d33c9-154">Por exemplo, para retornar `Hello {customerID}`, atualize o **Corpo** da resposta com `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="d33c9-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="d33c9-155">A lista de conteúdo dinâmica deve aparecer e mostrar o `customerID` token para você selecionar.</span><span class="sxs-lookup"><span data-stu-id="d33c9-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Adicionar parâmetro ao corpo da resposta](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="d33c9-157">O **Corpo** deve se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-157">Your **Body** should look like this example:</span></span>

    ![Corpo de resposta com parâmetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="d33c9-159">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-159">Save your logic app.</span></span> 

    <span data-ttu-id="d33c9-160">A URL de ponto de extremidade HTTP agora inclui o caminho relativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="d33c9-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="d33c9-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="d33c9-162">Para testar o ponto de extremidade HTTP, copie e cole a URL atualizada em outra janela do navegador, mas substitua `{customerID}` por `123456` e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="d33c9-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="d33c9-163">O navegador agora deve mostrar este texto:</span><span class="sxs-lookup"><span data-stu-id="d33c9-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="d33c9-164">Tokens gerados de esquemas JSON para o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="d33c9-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="d33c9-165">Quando você fornece um esquema JSON no gatilho **Solicitar**, o Designer de Aplicativo Lógico gera tokens para propriedades nesse esquema.</span><span class="sxs-lookup"><span data-stu-id="d33c9-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="d33c9-166">Assim, você pode usar esses tokens para transmitir dados por meio do fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d33c9-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="d33c9-167">Para este exemplo, se você adicionar as propriedades `title` e `name` ao esquema JSON, seus tokens estarão disponíveis para uso nas etapas posteriores do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="d33c9-168">Veja a seguir o esquema JSON completo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="d33c9-169">Criar fluxos de trabalho aninhados para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d33c9-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="d33c9-170">Você pode aninhar os fluxos de trabalho no aplicativo lógico adicionando outros aplicativos lógicos que podem receber solicitações.</span><span class="sxs-lookup"><span data-stu-id="d33c9-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="d33c9-171">Para incluir esses aplicativos lógicos, adicione a ação **Aplicativos Lógicos do Azure – Escolha um fluxo de trabalho de Aplicativos Lógicos** ao gatilho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="d33c9-172">Você pode selecionar dentre aplicativos lógicos qualificados.</span><span class="sxs-lookup"><span data-stu-id="d33c9-172">You can then select from eligible logic apps.</span></span>

![Adicionar outro aplicativo lógico](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="d33c9-174">Chamar ou disparar aplicativos lógicos por meio de pontos de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="d33c9-175">Depois de criar o ponto de extremidade HTTP, é possível disparar o aplicativo lógico por meio de um método `POST` para a URL completa.</span><span class="sxs-lookup"><span data-stu-id="d33c9-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="d33c9-176">Os aplicativos lógicos têm suporte interno para pontos de extremidade de acesso direto.</span><span class="sxs-lookup"><span data-stu-id="d33c9-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="d33c9-177">Fazer referência ao conteúdo de uma solicitação de entrada</span><span class="sxs-lookup"><span data-stu-id="d33c9-177">Reference content from an incoming request</span></span>

<span data-ttu-id="d33c9-178">Se o tipo do conteúdo for `application/json`, você poderá fazer referência às propriedades da solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="d33c9-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="d33c9-179">Caso contrário, o conteúdo será tratado como uma única unidade binária que você pode passar para outras APIs.</span><span class="sxs-lookup"><span data-stu-id="d33c9-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="d33c9-180">Para fazer referência a esse conteúdo no fluxo de trabalho, você deve converter esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d33c9-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="d33c9-181">Por exemplo, se transmitir o conteúdo de `application/xml`, você poderá usar `@xpath()` para uma extração de XPath ou `@json()` para converter XML em JSON.</span><span class="sxs-lookup"><span data-stu-id="d33c9-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="d33c9-182">Saiba mais sobre [como trabalhar com tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="d33c9-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="d33c9-183">Para obter a saída de uma solicitação de entrada, você poderá usar a função `@triggerOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="d33c9-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="d33c9-184">A saída pode se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="d33c9-185">Para acessar a propriedade `body` de forma específica, você pode usar o atalho `@triggerBody()`.</span><span class="sxs-lookup"><span data-stu-id="d33c9-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="d33c9-186">Responder às solicitações</span><span class="sxs-lookup"><span data-stu-id="d33c9-186">Respond to requests</span></span>

<span data-ttu-id="d33c9-187">Talvez você queira responder a determinadas solicitações que iniciam um aplicativo lógico retornando conteúdo a outro chamador.</span><span class="sxs-lookup"><span data-stu-id="d33c9-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="d33c9-188">Para construir o código de status, o cabeçalho e o corpo da resposta, você pode usar a ação **Resposta**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="d33c9-189">Essa ação pode aparecer em qualquer lugar no aplicativo lógico, não apenas no fim do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d33c9-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="d33c9-190">Se o aplicativo lógico não incluir uma **Resposta**, o ponto de extremidade HTTP responderá *imediatamente* com um status **202 Aceito**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="d33c9-191">Além disso, para a solicitação original obter a resposta, todas as etapas exigidas para a resposta devem ser finalizadas dentro do [tempo limite da solicitação](./logic-apps-limits-and-config.md), a menos que você chame o fluxo de trabalho como um aplicativo lógico aninhado.</span><span class="sxs-lookup"><span data-stu-id="d33c9-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="d33c9-192">Se não houver resposta dentro desse limite, a solicitação de entrada atingirá o tempo limite e receberá a resposta HTTP **408 Tempo limite de cliente**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="d33c9-193">Para aplicativos lógicos aninhados, o aplicativo lógico pai continuará a aguardar uma resposta até a conclusão, independentemente de quanto tempo for necessário.</span><span class="sxs-lookup"><span data-stu-id="d33c9-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="d33c9-194">Construir a resposta</span><span class="sxs-lookup"><span data-stu-id="d33c9-194">Construct the response</span></span>

<span data-ttu-id="d33c9-195">Você pode incluir mais de um cabeçalho e qualquer tipo de conteúdo no corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="d33c9-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="d33c9-196">Em nossa resposta de exemplo, o cabeçalho especifica que a resposta tem o tipo de conteúdo `application/json`.</span><span class="sxs-lookup"><span data-stu-id="d33c9-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="d33c9-197">E o corpo contém `title` e `name`, com base no esquema JSON atualizado anteriormente para o gatilho **Solicitar**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![Ação Resposta HTTP][3]

<span data-ttu-id="d33c9-199">As respostas têm estas propriedades:</span><span class="sxs-lookup"><span data-stu-id="d33c9-199">Responses have these properties:</span></span>

| <span data-ttu-id="d33c9-200">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d33c9-200">Property</span></span> | <span data-ttu-id="d33c9-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="d33c9-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d33c9-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="d33c9-202">statusCode</span></span> |<span data-ttu-id="d33c9-203">Especifica o código de status HTTP para responder à solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="d33c9-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="d33c9-204">Este código pode ser qualquer código de status válido que comece com 2xx, 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="d33c9-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="d33c9-205">No entanto, não há permissão para códigos de status 3xx.</span><span class="sxs-lookup"><span data-stu-id="d33c9-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="d33c9-206">headers</span><span class="sxs-lookup"><span data-stu-id="d33c9-206">headers</span></span> |<span data-ttu-id="d33c9-207">Define qualquer número de cabeçalhos a serem incluídos na resposta.</span><span class="sxs-lookup"><span data-stu-id="d33c9-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="d33c9-208">Corpo</span><span class="sxs-lookup"><span data-stu-id="d33c9-208">body</span></span> |<span data-ttu-id="d33c9-209">Especifica um objeto de corpo que pode ser uma cadeia de caracteres, um objeto JSON ou, até mesmo, o conteúdo binário referenciado em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="d33c9-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="d33c9-210">Veja a seguir como o esquema JSON se parece agora para a ação **Resposta**:</span><span class="sxs-lookup"><span data-stu-id="d33c9-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="d33c9-211">Para exibir a definição completa de JSON para seu aplicativo lógico, no Designer de Aplicativo Lógico, escolha **Exibição de código**.</span><span class="sxs-lookup"><span data-stu-id="d33c9-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="d33c9-212">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="d33c9-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="d33c9-213">P: O que dizer sobre a segurança de URL?</span><span class="sxs-lookup"><span data-stu-id="d33c9-213">Q: What about URL security?</span></span>

<span data-ttu-id="d33c9-214">R: O Azure gera com segurança URLs de retorno de chamada do aplicativo lógico usando uma SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="d33c9-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="d33c9-215">Essa assinatura é transmitida como um parâmetro de consulta e deve ser validada antes do aplicativo lógico ser acionado.</span><span class="sxs-lookup"><span data-stu-id="d33c9-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="d33c9-216">O Azure gera a assinatura usando uma combinação exclusiva de uma chave secreta por aplicativo lógico, o nome do gatilho e a operação que é executada.</span><span class="sxs-lookup"><span data-stu-id="d33c9-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="d33c9-217">Portanto, a menos que alguém tenha acesso à chave secreta do aplicativo lógico, não é possível gerar uma assinatura válida.</span><span class="sxs-lookup"><span data-stu-id="d33c9-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d33c9-218">Para sistemas seguros e de produção, é altamente recomendável não chamar o aplicativo lógico de chamada diretamente do navegador porque:</span><span class="sxs-lookup"><span data-stu-id="d33c9-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="d33c9-219">A chave de acesso compartilhado é exibida na URL.</span><span class="sxs-lookup"><span data-stu-id="d33c9-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="d33c9-220">Você não pode gerenciar políticas de conteúdo seguras devido a domínios compartilhados entre clientes de Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="d33c9-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="d33c9-221">P: Posso configurar pontos de extremidade HTTP mais tarde?</span><span class="sxs-lookup"><span data-stu-id="d33c9-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="d33c9-222">R: Sim, os pontos de extremidade HTTP dão suporte à configuração mais avançada por meio do [**Gerenciamento de API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="d33c9-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="d33c9-223">Esse serviço também oferece a capacidade de gerenciar todas as suas APIs de modo consistente, incluindo aplicativos lógicos, configurar os nomes de domínio personalizados, usar mais métodos de autenticação e mais, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d33c9-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="d33c9-224">Alterar o método de solicitação</span><span class="sxs-lookup"><span data-stu-id="d33c9-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="d33c9-225">Alterar os segmentos de URL da solicitação</span><span class="sxs-lookup"><span data-stu-id="d33c9-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="d33c9-226">Configurar os domínios de Gerenciamento de API no [portal do Azure](https://portal.azure.com/ "portal do Azure")</span><span class="sxs-lookup"><span data-stu-id="d33c9-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="d33c9-227">Configurar a política para verificar a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="d33c9-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="d33c9-228">P: O que mudou quando o esquema migrou do modo de visualização de 1º de dezembro de 2014?</span><span class="sxs-lookup"><span data-stu-id="d33c9-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="d33c9-229">R: Veja um resumo sobre essas alterações:</span><span class="sxs-lookup"><span data-stu-id="d33c9-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="d33c9-230">Visualização de 1º de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="d33c9-230">December 1, 2014 preview</span></span> | <span data-ttu-id="d33c9-231">1º de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="d33c9-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="d33c9-232">Clique no aplicativo de API **Ouvinte HTTP**</span><span class="sxs-lookup"><span data-stu-id="d33c9-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="d33c9-233">Clique em **Gatilho manual** (nenhum aplicativo de API é necessário)</span><span class="sxs-lookup"><span data-stu-id="d33c9-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="d33c9-234">Configuração “*Envia a resposta automaticamente*” do Ouvinte HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="d33c9-235">Inclua uma ação **Resposta** ou não na definição do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="d33c9-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="d33c9-236">Configure a autenticação Básica ou OAuth</span><span class="sxs-lookup"><span data-stu-id="d33c9-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="d33c9-237">por meio do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d33c9-237">via API Management</span></span> |
| <span data-ttu-id="d33c9-238">Configurar o método HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-238">Configure HTTP method</span></span> |<span data-ttu-id="d33c9-239">Em **Mostrar opções avançadas**, escolha um método HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="d33c9-240">Configurar o caminho relativo</span><span class="sxs-lookup"><span data-stu-id="d33c9-240">Configure relative path</span></span> |<span data-ttu-id="d33c9-241">Em **Mostrar opções avançadas**, adicione um caminho relativo</span><span class="sxs-lookup"><span data-stu-id="d33c9-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="d33c9-242">Fazer referência ao corpo de entrada por meio de `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="d33c9-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="d33c9-243">Fazer referência por meio de `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="d33c9-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="d33c9-244">**Enviar resposta HTTP** no Ouvinte HTTP</span><span class="sxs-lookup"><span data-stu-id="d33c9-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="d33c9-245">Clique em **Responder à solicitação HTTP** (nenhum aplicativo de API é necessário)</span><span class="sxs-lookup"><span data-stu-id="d33c9-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="d33c9-246">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="d33c9-246">Get help</span></span>

<span data-ttu-id="d33c9-247">Para fazer perguntas, responder a perguntas e saber o que os outros usuários dos Aplicativos Lógicos do Azure estão fazendo, visite o [fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d33c9-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d33c9-248">Para ajudar a melhorar os Aplicativos Lógicos do Azure e conectores, vote ou envie ideias no [site de comentários do usuário dos Aplicativos Lógicos do Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d33c9-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d33c9-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d33c9-249">Next steps</span></span>

* [<span data-ttu-id="d33c9-250">Criar definições de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="d33c9-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="d33c9-251">Processar erros e exceções</span><span class="sxs-lookup"><span data-stu-id="d33c9-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
