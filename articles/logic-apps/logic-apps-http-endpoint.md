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
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Chamar, disparar ou aninhar fluxos de trabalho com pontos de extremidade HTTP em aplicativos lógicos

Você pode expor nativamente pontos de extremidade HTTP síncronos como gatilhos em aplicativos lógicos para que seja possível disparar ou chamar aplicativos lógicos por meio de uma URL. Também é possível aninhar fluxos de trabalho em aplicativos lógicos usando um padrão de pontos de extremidade resgatáveis.

pontos de extremidade HTTP toocreate, você pode adicionar esses gatilhos para que seus aplicativos lógicos podem receber solicitações de entrada:

* [Solicitação](../connectors/connectors-native-reqres.md)

* [Webhook de Conexão de API](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Webhook HTTP](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Embora os exemplos usam Olá **solicitar** gatilho, você pode usar qualquer um dos Olá listados gatilhos HTTP e todos os princípios identicamente aplicam toohello outros tipos de disparadores.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Configurar um ponto de extremidade HTTP para o aplicativo lógico

toocreate um ponto de extremidade HTTP, adicione um gatilho que pode receber solicitações de entrada.

1. Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure"). Vá tooyour lógica aplicativo e, em seguida, abra o Designer de lógica do aplicativo.

2. Adicione um gatilho que permita ao aplicativo lógico receber solicitações de entrada. Por exemplo, adicionar Olá **solicitação** gatilho tooyour lógica aplicativo.

3.  Em **esquema de JSON de corpo de solicitação**, opcionalmente, você pode inserir um esquema JSON para carga hello (dados) que você espera Olá gatilho tooreceive.

    designer de saudação usa este esquema para a geração de tokens que seu aplicativo lógico pode usar tooconsume, análise e passar dados do disparador Olá por meio de seu fluxo de trabalho. 
    Saiba mais sobre [tokens gerados de esquemas JSON](#generated-tokens).

    Para este exemplo, digite esquema Olá mostrada no designer de saudação:

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
    > Você pode gerar um esquema para uma carga JSON de exemplo de uma ferramenta como [jsonschema.net](http://jsonschema.net/), ou em Olá **solicitação** gatilho escolhendo **esquema de toogenerate de carga de exemplo de uso**. 
    > Insira o conteúdo de exemplo e escolha **Concluído**.

    Por exemplo, este conteúdo de exemplo:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    gera este esquema:

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

4.  Salve seu aplicativo lógico. Em **HTTP POST toothis URL**, agora você deve encontrar uma URL de retorno de chamada gerado, como neste exemplo:

    ![URL de retorno de chamada gerada para ponto de extremidade](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Essa URL contém uma chave de assinatura de acesso compartilhado (SAS) em parâmetros de consulta de saudação que são usados para autenticação. 
    Você também pode obter a URL de ponto de extremidade HTTP de saudação de visão geral do seu aplicativo lógica em Olá portal do Azure. Em **Histórico de Gatilho**, selecione o gatilho:

    ![Obter a URL de ponto de extremidade HTTP no portal do Azure][2]

    Ou você pode obter a URL de saudação ao fazer essa chamada:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Alterar método HTTP Olá para o disparador

Por padrão, Olá **solicitação** gatilho espera uma solicitação HTTP POST, mas você pode usar um método diferente de HTTP. 

> [!NOTE]
> Você pode especificar somente um tipo de método.

1. No gatilho **Solicitar**, escolha **Mostrar opções avançadas**.

2. Olá abrir **método** lista. Para este exemplo, selecione **GET** para que você possa testar posteriormente sua URL de ponto de extremidade HTTP.

    > [!NOTE]
    > É possível selecionar qualquer outro método HTTP ou especificar um método personalizado para seu próprio aplicativo lógico.

    ![Alterar método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Aceitar parâmetros por meio da URL de ponto de extremidade HTTP

Quando você quiser que os parâmetros de tooaccept de URL de ponto de extremidade HTTP, personalize o caminho relativo do gatilho.

1. No gatilho **Solicitar**, escolha **Mostrar opções avançadas**. 

2. Em **método**, especifique o método hello HTTP que você deseja toouse sua solicitação. Neste exemplo, selecione Olá **obter** método, se você ainda não fez isso, para que você pode testar a URL do ponto de extremidade o HTTP.

      > [!NOTE]
      > Ao especificar um caminho relativo para o gatilho, você deve especificar explicitamente um método HTTP para o gatilho.

3. Em **caminho relativo**, especifique o caminho relativo para o parâmetro hello que sua URL deve aceitar, por exemplo, o hello `customers/{customerID}`.

    ![Especifique o método HTTP hello e o caminho relativo para o parâmetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse Olá parâmetro, adicione uma **resposta** ação tooyour lógica aplicativo. (No gatilho, escolha **Nova etapa** > **Adicionar uma ação** > **Resposta**) 

5. Em sua resposta **corpo**, inclui um token Olá para o parâmetro hello especificado no caminho relativo do gatilho.

    Por exemplo, tooreturn `Hello {customerID}`, atualize sua resposta **corpo** com `Hello {customerID token}`. 
    lista de conteúdo dinâmico Olá deve aparecer e mostrar Olá `customerID` token para você tooselect.

    ![Adicionar o corpo do parâmetro tooresponse](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    O **Corpo** deve se parecer com este exemplo:

    ![Corpo de resposta com parâmetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Salve seu aplicativo lógico. 

    A URL do ponto de extremidade HTTP agora inclui caminho relativo do hello, por exemplo: 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest seu ponto de extremidade HTTP, copiar e colar Olá URL atualizada em outra janela do navegador, mas substituam `{customerID}` com `123456`, e pressione Enter.

    O navegador agora deve mostrar este texto: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Tokens gerados de esquemas JSON para o aplicativo lógico

Quando você fornece um esquema JSON no seu **solicitação** disparar, hello lógica de aplicativo Designer gera tokens para propriedades nesse esquema. Assim, você pode usar esses tokens para transmitir dados por meio do fluxo de trabalho do aplicativo lógico.

Neste exemplo, se você adicionar Olá `title` e `name` esquema JSON tooyour propriedades, seus tokens agora estão disponível toouse em etapas posteriores do fluxo de trabalho. 

Aqui está o esquema JSON completo hello:

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

## <a name="create-nested-workflows-for-logic-apps"></a>Criar fluxos de trabalho aninhados para aplicativos lógicos

Você pode aninhar os fluxos de trabalho no aplicativo lógico adicionando outros aplicativos lógicos que podem receber solicitações. tooinclude esses aplicativos lógicos, adicionar Olá **os aplicativos lógicos do Azure - escolha um fluxo de trabalho de aplicativos lógicos** tooyour de disparo de ação. Você pode selecionar dentre aplicativos lógicos qualificados.

![Adicionar outro aplicativo lógico](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Chamar ou disparar aplicativos lógicos por meio de pontos de extremidade HTTP

Depois de criar seu ponto de extremidade HTTP, você pode disparar o seu aplicativo lógica por meio de um `POST` método toohello a URL completa. Os aplicativos lógicos têm suporte interno para pontos de extremidade de acesso direto.

## <a name="reference-content-from-an-incoming-request"></a>Fazer referência ao conteúdo de uma solicitação de entrada

Se Olá conteúdo do tipo for `application/json`, você pode fazer referência a propriedades da solicitação de entrada hello. Caso contrário, conteúdo é tratado como uma única unidade de binária que você pode passar tooother APIs. tooreference esse conteúdo dentro do fluxo de trabalho hello, você deve converter esse conteúdo. Por exemplo, se você passar `application/xml` conteúdo, você pode usar `@xpath()` para uma extração de XPath, ou `@json()` para converter tooJSON XML. Saiba mais sobre [como trabalhar com tipos de conteúdo](../logic-apps/logic-apps-content-type.md).

Olá tooget de saída de uma solicitação de entrada, você pode usar o hello `@triggerOutputs()` função. saída de Hello pode parecer semelhante a este exemplo:

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

Olá tooaccess `body` propriedade especificamente, você pode usar Olá `@triggerBody()` atalho. 

## <a name="respond-toorequests"></a>Responder toorequests

Talvez você queira toorespond toocertain solicitações que iniciar um aplicativo lógico, retornando conteúdo toohello chamador. código de status tooconstruct hello, cabeçalho e corpo de resposta, você pode usar o hello **resposta** ação. Esta ação pode aparecer em qualquer lugar no seu aplicativo lógico, não apenas no final de saudação do fluxo de trabalho.

> [!NOTE] 
> Se seu aplicativo lógico não incluir um **resposta**, ponto de extremidade HTTP de saudação responde *imediatamente* com um **202 aceito** status. Além disso, para Olá solicitação tooget Olá resposta original, todas as etapas necessárias para a resposta de saudação deverá ser concluída em Olá [limite de solicitação](./logic-apps-limits-and-config.md) , a menos que você chamar o fluxo de trabalho hello como um aplicativo lógica aninhada. Se nenhuma resposta acontece dentro desse limite, solicitação de entrada hello expirar e recebe a resposta HTTP de saudação **408 tempo limite do cliente**. Para aplicativos lógicos aninhadas, Olá aplicativo-pai lógica continuará toowait por uma resposta até a conclusão, independentemente de quanto tempo é necessário.

### <a name="construct-hello-response"></a>Resposta de saudação de construção

Você pode incluir mais de um cabeçalho e qualquer tipo de conteúdo no corpo de resposta de saudação. Em nosso exemplo de resposta, o cabeçalho de saudação especifica a resposta Olá tem tipo de conteúdo `application/json`. e o corpo da saudação contém `title` e `name`, com base no esquema JSON Olá atualizada anteriormente para Olá **solicitação** gatilho.

![Ação Resposta HTTP][3]

As respostas têm estas propriedades:

| Propriedade | Descrição |
| --- | --- |
| statusCode |Especifica o código de status HTTP de saudação respondendo toohello solicitação de entrada. Este código pode ser qualquer código de status válido que comece com 2xx, 4xx ou 5xx. No entanto, não há permissão para códigos de status 3xx. |
| headers |Define qualquer número de tooinclude cabeçalhos na resposta de saudação. |
| body |Especifica um objeto de corpo que pode ser uma cadeia de caracteres, um objeto JSON ou, até mesmo, o conteúdo binário referenciado em uma etapa anterior. |

Aqui está o esquema JSON Olá aparência agora para Olá **resposta** ação:

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
> tooview Olá JSON definição completa para seu aplicativo de lógica, no hello Designer de lógica do aplicativo, escolha **exibição de código**.

## <a name="q--a"></a>Perguntas e respostas

#### <a name="q-what-about-url-security"></a>P: O que dizer sobre a segurança de URL?

R: O Azure gera com segurança URLs de retorno de chamada do aplicativo lógico usando uma SAS (Assinatura de Acesso Compartilhado). Essa assinatura é transmitida como um parâmetro de consulta e deve ser validada antes do aplicativo lógico ser acionado. Azure gera assinatura hello usando uma combinação exclusiva de uma chave secreta por aplicativo lógico, nome do disparador hello e operação de saudação que é executada. Portanto, a menos que alguém tem a chave de segredo lógica de aplicativo do acesso toohello, eles não é possível gerar uma assinatura válida.

   > [!IMPORTANT]
   > Para proteger sistemas de produção e, é altamente recomendável em relação a sua lógica de aplicativo de chamada diretamente do navegador de saudação porque:
   > 
   > * chave de acesso compartilhado Olá aparece na URL de saudação.
   > * Você não pode gerenciar políticas de conteúdo seguras devido tooshared domínios entre os clientes do aplicativo lógico.

#### <a name="q-can-i-configure-http-endpoints-further"></a>P: Posso configurar pontos de extremidade HTTP mais tarde?

R: Sim, os pontos de extremidade HTTP dão suporte à configuração mais avançada por meio do [**Gerenciamento de API**](../api-management/api-management-key-concepts.md). Esse serviço também oferece recursos de saudação para você tooconsistently gerencie todas as suas APIs, incluindo aplicativos lógicos, configurar os nomes de domínio personalizado, use os métodos de autenticação mais e mais, por exemplo:

* [Alterar o método de solicitação hello](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Alterar os segmentos de URL de saudação da solicitação de saudação](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Configurar seus domínios de gerenciamento de API no hello [portal do Azure](https://portal.azure.com/ "portal do Azure")
* Configurar a política toocheck para autenticação básica

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>P: o que mudou quando esquema Olá migrado de visualização de 1 de dezembro de 2014 Olá?

R: Veja um resumo sobre essas alterações:

| Visualização de 1º de dezembro de 2014 | 1º de junho de 2016 |
| --- | --- |
| Clique no aplicativo de API **Ouvinte HTTP** |Clique em **Gatilho manual** (nenhum aplicativo de API é necessário) |
| Configuração “*Envia a resposta automaticamente*” do Ouvinte HTTP |O inclui um **resposta** ação ou não na definição de fluxo de trabalho de saudação |
| Configure a autenticação Básica ou OAuth |por meio do Gerenciamento de API |
| Configurar o método HTTP |Em **Mostrar opções avançadas**, escolha um método HTTP |
| Configurar o caminho relativo |Em **Mostrar opções avançadas**, adicione um caminho relativo |
| Corpo de entrada hello referência por meio de`@triggerOutputs().body.Content` |Fazer referência por meio de `@triggerOutputs().body` |
| **Enviar a resposta HTTP** ação Olá ouvinte HTTP |Clique em **responder tooHTTP solicitação** (nenhuma API App necessário) |

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

* [Criar definições de aplicativo lógico](./logic-apps-author-definitions.md)
* [Processar erros e exceções](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
