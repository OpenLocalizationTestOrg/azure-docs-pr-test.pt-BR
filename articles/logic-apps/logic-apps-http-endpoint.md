---
title: "aaaCall, gatilho ou aninhar fluxos de trabalho com pontos de extremidade HTTP - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Configurar fluxos de trabalho aninhados, gatilho ou toocall de pontos de extremidade HTTP para os aplicativos lógicos do Azure"
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
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="f60f8-104">Chamar, disparar ou aninhar fluxos de trabalho com pontos de extremidade HTTP em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="f60f8-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="f60f8-105">Você pode expor nativamente pontos de extremidade HTTP síncronos como gatilhos em aplicativos lógicos para que seja possível disparar ou chamar aplicativos lógicos por meio de uma URL.</span><span class="sxs-lookup"><span data-stu-id="f60f8-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="f60f8-106">Também é possível aninhar fluxos de trabalho em aplicativos lógicos usando um padrão de pontos de extremidade resgatáveis.</span><span class="sxs-lookup"><span data-stu-id="f60f8-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="f60f8-107">pontos de extremidade HTTP toocreate, você pode adicionar esses gatilhos para que seus aplicativos lógicos podem receber solicitações de entrada:</span><span class="sxs-lookup"><span data-stu-id="f60f8-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="f60f8-108">Solicitação</span><span class="sxs-lookup"><span data-stu-id="f60f8-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="f60f8-109">Webhook de Conexão de API</span><span class="sxs-lookup"><span data-stu-id="f60f8-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="f60f8-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="f60f8-111">Embora os exemplos usam Olá **solicitar** gatilho, você pode usar qualquer um dos Olá listados gatilhos HTTP e todos os princípios identicamente aplicam toohello outros tipos de disparadores.</span><span class="sxs-lookup"><span data-stu-id="f60f8-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="f60f8-112">Configurar um ponto de extremidade HTTP para o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="f60f8-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="f60f8-113">toocreate um ponto de extremidade HTTP, adicione um gatilho que pode receber solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="f60f8-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="f60f8-114">Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="f60f8-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="f60f8-115">Vá tooyour lógica aplicativo e, em seguida, abra o Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f60f8-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="f60f8-116">Adicione um gatilho que permita ao aplicativo lógico receber solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="f60f8-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="f60f8-117">Por exemplo, adicionar Olá **solicitação** gatilho tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f60f8-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="f60f8-118">Em **esquema de JSON de corpo de solicitação**, opcionalmente, você pode inserir um esquema JSON para carga hello (dados) que você espera Olá gatilho tooreceive.</span><span class="sxs-lookup"><span data-stu-id="f60f8-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="f60f8-119">designer de saudação usa este esquema para a geração de tokens que seu aplicativo lógico pode usar tooconsume, análise e passar dados do disparador Olá por meio de seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="f60f8-120">Saiba mais sobre [tokens gerados de esquemas JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="f60f8-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="f60f8-121">Para este exemplo, digite esquema Olá mostrada no designer de saudação:</span><span class="sxs-lookup"><span data-stu-id="f60f8-121">For this example, enter hello schema shown in hello designer:</span></span>

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

    ![Adicionar ação de solicitação de saudação][1]

    > [!TIP]
    > 
    > <span data-ttu-id="f60f8-123">Você pode gerar um esquema para uma carga JSON de exemplo de uma ferramenta como [jsonschema.net](http://jsonschema.net/), ou em Olá **solicitação** gatilho escolhendo **esquema de toogenerate de carga de exemplo de uso**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="f60f8-124">Insira o conteúdo de exemplo e escolha **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="f60f8-125">Por exemplo, este conteúdo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="f60f8-126">gera este esquema:</span><span class="sxs-lookup"><span data-stu-id="f60f8-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="f60f8-127">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f60f8-127">Save your logic app.</span></span> <span data-ttu-id="f60f8-128">Em **HTTP POST toothis URL**, agora você deve encontrar uma URL de retorno de chamada gerado, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL de retorno de chamada gerada para ponto de extremidade](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="f60f8-130">Essa URL contém uma chave de assinatura de acesso compartilhado (SAS) em parâmetros de consulta de saudação que são usados para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="f60f8-131">Você também pode obter a URL de ponto de extremidade HTTP de saudação de visão geral do seu aplicativo lógica em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f60f8-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="f60f8-132">Em **Histórico de Gatilho**, selecione o gatilho:</span><span class="sxs-lookup"><span data-stu-id="f60f8-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obter a URL de ponto de extremidade HTTP no portal do Azure][2]

    <span data-ttu-id="f60f8-134">Ou você pode obter a URL de saudação ao fazer essa chamada:</span><span class="sxs-lookup"><span data-stu-id="f60f8-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="f60f8-135">Alterar método HTTP Olá para o disparador</span><span class="sxs-lookup"><span data-stu-id="f60f8-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="f60f8-136">Por padrão, Olá **solicitação** gatilho espera uma solicitação HTTP POST, mas você pode usar um método diferente de HTTP.</span><span class="sxs-lookup"><span data-stu-id="f60f8-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f60f8-137">Você pode especificar somente um tipo de método.</span><span class="sxs-lookup"><span data-stu-id="f60f8-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="f60f8-138">No gatilho **Solicitar**, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="f60f8-139">Olá abrir **método** lista.</span><span class="sxs-lookup"><span data-stu-id="f60f8-139">Open hello **Method** list.</span></span> <span data-ttu-id="f60f8-140">Para este exemplo, selecione **GET** para que você possa testar posteriormente sua URL de ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="f60f8-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f60f8-141">É possível selecionar qualquer outro método HTTP ou especificar um método personalizado para seu próprio aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f60f8-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Alterar método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="f60f8-143">Aceitar parâmetros por meio da URL de ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="f60f8-144">Quando você quiser que os parâmetros de tooaccept de URL de ponto de extremidade HTTP, personalize o caminho relativo do gatilho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="f60f8-145">No gatilho **Solicitar**, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="f60f8-146">Em **método**, especifique o método hello HTTP que você deseja toouse sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="f60f8-147">Neste exemplo, selecione Olá **obter** método, se você ainda não fez isso, para que você pode testar a URL do ponto de extremidade o HTTP.</span><span class="sxs-lookup"><span data-stu-id="f60f8-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f60f8-148">Ao especificar um caminho relativo para o gatilho, você deve especificar explicitamente um método HTTP para o gatilho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="f60f8-149">Em **caminho relativo**, especifique o caminho relativo para o parâmetro hello que sua URL deve aceitar, por exemplo, o hello `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="f60f8-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Especifique o método HTTP hello e o caminho relativo para o parâmetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="f60f8-151">toouse Olá parâmetro, adicione uma **resposta** ação tooyour lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f60f8-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="f60f8-152">(No gatilho, escolha **Nova etapa** > **Adicionar uma ação** > **Resposta**)</span><span class="sxs-lookup"><span data-stu-id="f60f8-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="f60f8-153">Em sua resposta **corpo**, inclui um token Olá para o parâmetro hello especificado no caminho relativo do gatilho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="f60f8-154">Por exemplo, tooreturn `Hello {customerID}`, atualize sua resposta **corpo** com `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="f60f8-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="f60f8-155">lista de conteúdo dinâmico Olá deve aparecer e mostrar Olá `customerID` token para você tooselect.</span><span class="sxs-lookup"><span data-stu-id="f60f8-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Adicionar o corpo do parâmetro tooresponse](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="f60f8-157">O **Corpo** deve se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-157">Your **Body** should look like this example:</span></span>

    ![Corpo de resposta com parâmetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="f60f8-159">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f60f8-159">Save your logic app.</span></span> 

    <span data-ttu-id="f60f8-160">A URL do ponto de extremidade HTTP agora inclui caminho relativo do hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="f60f8-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="f60f8-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="f60f8-162">tootest seu ponto de extremidade HTTP, copiar e colar Olá URL atualizada em outra janela do navegador, mas substituam `{customerID}` com `123456`, e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="f60f8-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="f60f8-163">O navegador agora deve mostrar este texto:</span><span class="sxs-lookup"><span data-stu-id="f60f8-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="f60f8-164">Tokens gerados de esquemas JSON para o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="f60f8-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="f60f8-165">Quando você fornece um esquema JSON no seu **solicitação** disparar, hello lógica de aplicativo Designer gera tokens para propriedades nesse esquema.</span><span class="sxs-lookup"><span data-stu-id="f60f8-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="f60f8-166">Assim, você pode usar esses tokens para transmitir dados por meio do fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f60f8-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="f60f8-167">Neste exemplo, se você adicionar Olá `title` e `name` esquema JSON tooyour propriedades, seus tokens agora estão disponível toouse em etapas posteriores do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="f60f8-168">Aqui está o esquema JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="f60f8-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="f60f8-169">Criar fluxos de trabalho aninhados para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="f60f8-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="f60f8-170">Você pode aninhar os fluxos de trabalho no aplicativo lógico adicionando outros aplicativos lógicos que podem receber solicitações.</span><span class="sxs-lookup"><span data-stu-id="f60f8-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="f60f8-171">tooinclude esses aplicativos lógicos, adicionar Olá **os aplicativos lógicos do Azure - escolha um fluxo de trabalho de aplicativos lógicos** tooyour de disparo de ação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="f60f8-172">Você pode selecionar dentre aplicativos lógicos qualificados.</span><span class="sxs-lookup"><span data-stu-id="f60f8-172">You can then select from eligible logic apps.</span></span>

![Adicionar outro aplicativo lógico](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="f60f8-174">Chamar ou disparar aplicativos lógicos por meio de pontos de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="f60f8-175">Depois de criar seu ponto de extremidade HTTP, você pode disparar o seu aplicativo lógica por meio de um `POST` método toohello a URL completa.</span><span class="sxs-lookup"><span data-stu-id="f60f8-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="f60f8-176">Os aplicativos lógicos têm suporte interno para pontos de extremidade de acesso direto.</span><span class="sxs-lookup"><span data-stu-id="f60f8-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="f60f8-177">Fazer referência ao conteúdo de uma solicitação de entrada</span><span class="sxs-lookup"><span data-stu-id="f60f8-177">Reference content from an incoming request</span></span>

<span data-ttu-id="f60f8-178">Se Olá conteúdo do tipo for `application/json`, você pode fazer referência a propriedades da solicitação de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f60f8-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="f60f8-179">Caso contrário, conteúdo é tratado como uma única unidade de binária que você pode passar tooother APIs.</span><span class="sxs-lookup"><span data-stu-id="f60f8-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="f60f8-180">tooreference esse conteúdo dentro do fluxo de trabalho hello, você deve converter esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f60f8-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="f60f8-181">Por exemplo, se você passar `application/xml` conteúdo, você pode usar `@xpath()` para uma extração de XPath, ou `@json()` para converter tooJSON XML.</span><span class="sxs-lookup"><span data-stu-id="f60f8-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="f60f8-182">Saiba mais sobre [como trabalhar com tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="f60f8-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="f60f8-183">Olá tooget de saída de uma solicitação de entrada, você pode usar o hello `@triggerOutputs()` função.</span><span class="sxs-lookup"><span data-stu-id="f60f8-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="f60f8-184">saída de Hello pode parecer semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="f60f8-185">Olá tooaccess `body` propriedade especificamente, você pode usar Olá `@triggerBody()` atalho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="f60f8-186">Responder toorequests</span><span class="sxs-lookup"><span data-stu-id="f60f8-186">Respond toorequests</span></span>

<span data-ttu-id="f60f8-187">Talvez você queira toorespond toocertain solicitações que iniciar um aplicativo lógico, retornando conteúdo toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="f60f8-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="f60f8-188">código de status tooconstruct hello, cabeçalho e corpo de resposta, você pode usar o hello **resposta** ação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="f60f8-189">Esta ação pode aparecer em qualquer lugar no seu aplicativo lógico, não apenas no final de saudação do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="f60f8-190">Se seu aplicativo lógico não incluir um **resposta**, ponto de extremidade HTTP de saudação responde *imediatamente* com um **202 aceito** status.</span><span class="sxs-lookup"><span data-stu-id="f60f8-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="f60f8-191">Além disso, para Olá solicitação tooget Olá resposta original, todas as etapas necessárias para a resposta de saudação deverá ser concluída em Olá [limite de solicitação](./logic-apps-limits-and-config.md) , a menos que você chamar o fluxo de trabalho hello como um aplicativo lógica aninhada.</span><span class="sxs-lookup"><span data-stu-id="f60f8-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="f60f8-192">Se nenhuma resposta acontece dentro desse limite, solicitação de entrada hello expirar e recebe a resposta HTTP de saudação **408 tempo limite do cliente**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="f60f8-193">Para aplicativos lógicos aninhadas, Olá aplicativo-pai lógica continuará toowait por uma resposta até a conclusão, independentemente de quanto tempo é necessário.</span><span class="sxs-lookup"><span data-stu-id="f60f8-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="f60f8-194">Resposta de saudação de construção</span><span class="sxs-lookup"><span data-stu-id="f60f8-194">Construct hello response</span></span>

<span data-ttu-id="f60f8-195">Você pode incluir mais de um cabeçalho e qualquer tipo de conteúdo no corpo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="f60f8-196">Em nosso exemplo de resposta, o cabeçalho de saudação especifica a resposta Olá tem tipo de conteúdo `application/json`.</span><span class="sxs-lookup"><span data-stu-id="f60f8-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="f60f8-197">e o corpo da saudação contém `title` e `name`, com base no esquema JSON Olá atualizada anteriormente para Olá **solicitação** gatilho.</span><span class="sxs-lookup"><span data-stu-id="f60f8-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Ação Resposta HTTP][3]

<span data-ttu-id="f60f8-199">As respostas têm estas propriedades:</span><span class="sxs-lookup"><span data-stu-id="f60f8-199">Responses have these properties:</span></span>

| <span data-ttu-id="f60f8-200">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f60f8-200">Property</span></span> | <span data-ttu-id="f60f8-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="f60f8-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f60f8-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="f60f8-202">statusCode</span></span> |<span data-ttu-id="f60f8-203">Especifica o código de status HTTP de saudação respondendo toohello solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="f60f8-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="f60f8-204">Este código pode ser qualquer código de status válido que comece com 2xx, 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="f60f8-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="f60f8-205">No entanto, não há permissão para códigos de status 3xx.</span><span class="sxs-lookup"><span data-stu-id="f60f8-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="f60f8-206">headers</span><span class="sxs-lookup"><span data-stu-id="f60f8-206">headers</span></span> |<span data-ttu-id="f60f8-207">Define qualquer número de tooinclude cabeçalhos na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="f60f8-208">body</span><span class="sxs-lookup"><span data-stu-id="f60f8-208">body</span></span> |<span data-ttu-id="f60f8-209">Especifica um objeto de corpo que pode ser uma cadeia de caracteres, um objeto JSON ou, até mesmo, o conteúdo binário referenciado em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f60f8-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="f60f8-210">Aqui está o esquema JSON Olá aparência agora para Olá **resposta** ação:</span><span class="sxs-lookup"><span data-stu-id="f60f8-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="f60f8-211">tooview Olá JSON definição completa para seu aplicativo de lógica, no hello Designer de lógica do aplicativo, escolha **exibição de código**.</span><span class="sxs-lookup"><span data-stu-id="f60f8-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="f60f8-212">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="f60f8-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="f60f8-213">P: O que dizer sobre a segurança de URL?</span><span class="sxs-lookup"><span data-stu-id="f60f8-213">Q: What about URL security?</span></span>

<span data-ttu-id="f60f8-214">R: O Azure gera com segurança URLs de retorno de chamada do aplicativo lógico usando uma SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="f60f8-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="f60f8-215">Essa assinatura é transmitida como um parâmetro de consulta e deve ser validada antes do aplicativo lógico ser acionado.</span><span class="sxs-lookup"><span data-stu-id="f60f8-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="f60f8-216">Azure gera assinatura hello usando uma combinação exclusiva de uma chave secreta por aplicativo lógico, nome do disparador hello e operação de saudação que é executada.</span><span class="sxs-lookup"><span data-stu-id="f60f8-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="f60f8-217">Portanto, a menos que alguém tem a chave de segredo lógica de aplicativo do acesso toohello, eles não é possível gerar uma assinatura válida.</span><span class="sxs-lookup"><span data-stu-id="f60f8-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f60f8-218">Para proteger sistemas de produção e, é altamente recomendável em relação a sua lógica de aplicativo de chamada diretamente do navegador de saudação porque:</span><span class="sxs-lookup"><span data-stu-id="f60f8-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="f60f8-219">chave de acesso compartilhado Olá aparece na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f8-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="f60f8-220">Você não pode gerenciar políticas de conteúdo seguras devido tooshared domínios entre os clientes do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f60f8-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="f60f8-221">P: Posso configurar pontos de extremidade HTTP mais tarde?</span><span class="sxs-lookup"><span data-stu-id="f60f8-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="f60f8-222">R: Sim, os pontos de extremidade HTTP dão suporte à configuração mais avançada por meio do [**Gerenciamento de API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f60f8-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="f60f8-223">Esse serviço também oferece recursos de saudação para você tooconsistently gerencie todas as suas APIs, incluindo aplicativos lógicos, configurar os nomes de domínio personalizado, use os métodos de autenticação mais e mais, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f60f8-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="f60f8-224">Alterar o método de solicitação hello</span><span class="sxs-lookup"><span data-stu-id="f60f8-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="f60f8-225">Alterar os segmentos de URL de saudação da solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="f60f8-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="f60f8-226">Configurar seus domínios de gerenciamento de API no hello [portal do Azure](https://portal.azure.com/ "portal do Azure")</span><span class="sxs-lookup"><span data-stu-id="f60f8-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="f60f8-227">Configurar a política toocheck para autenticação básica</span><span class="sxs-lookup"><span data-stu-id="f60f8-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="f60f8-228">P: o que mudou quando esquema Olá migrado de visualização de 1 de dezembro de 2014 Olá?</span><span class="sxs-lookup"><span data-stu-id="f60f8-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="f60f8-229">R: Veja um resumo sobre essas alterações:</span><span class="sxs-lookup"><span data-stu-id="f60f8-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="f60f8-230">Visualização de 1º de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="f60f8-230">December 1, 2014 preview</span></span> | <span data-ttu-id="f60f8-231">1º de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="f60f8-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="f60f8-232">Clique no aplicativo de API **Ouvinte HTTP**</span><span class="sxs-lookup"><span data-stu-id="f60f8-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="f60f8-233">Clique em **Gatilho manual** (nenhum aplicativo de API é necessário)</span><span class="sxs-lookup"><span data-stu-id="f60f8-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="f60f8-234">Configuração “*Envia a resposta automaticamente*” do Ouvinte HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="f60f8-235">O inclui um **resposta** ação ou não na definição de fluxo de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="f60f8-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="f60f8-236">Configure a autenticação Básica ou OAuth</span><span class="sxs-lookup"><span data-stu-id="f60f8-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="f60f8-237">por meio do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="f60f8-237">via API Management</span></span> |
| <span data-ttu-id="f60f8-238">Configurar o método HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-238">Configure HTTP method</span></span> |<span data-ttu-id="f60f8-239">Em **Mostrar opções avançadas**, escolha um método HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="f60f8-240">Configurar o caminho relativo</span><span class="sxs-lookup"><span data-stu-id="f60f8-240">Configure relative path</span></span> |<span data-ttu-id="f60f8-241">Em **Mostrar opções avançadas**, adicione um caminho relativo</span><span class="sxs-lookup"><span data-stu-id="f60f8-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="f60f8-242">Corpo de entrada hello referência por meio de`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="f60f8-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="f60f8-243">Fazer referência por meio de `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="f60f8-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="f60f8-244">**Enviar a resposta HTTP** ação Olá ouvinte HTTP</span><span class="sxs-lookup"><span data-stu-id="f60f8-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="f60f8-245">Clique em **responder tooHTTP solicitação** (nenhuma API App necessário)</span><span class="sxs-lookup"><span data-stu-id="f60f8-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="f60f8-246">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="f60f8-246">Get help</span></span>

<span data-ttu-id="f60f8-247">tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f60f8-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f60f8-248">toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f60f8-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f60f8-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f60f8-249">Next steps</span></span>

* [<span data-ttu-id="f60f8-250">Criar definições de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="f60f8-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="f60f8-251">Processar erros e exceções</span><span class="sxs-lookup"><span data-stu-id="f60f8-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
