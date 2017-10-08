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
# <a name="get-started-with-hello-http-action"></a>Introdução ao Olá ação HTTP

Com hello ação HTTP, você pode estender os fluxos de trabalho para a sua organização e comunicar-se o ponto de extremidade tooany via HTTP.

Você pode:

* Crie fluxos de trabalho de aplicativo lógico que são ativados (disparam) quando um site que você gerencia é desativado.
* Se comunicam tooany de ponto de extremidade por HTTP tooextend seus fluxos de trabalho em outros serviços.

tooget iniciado usando a ação de saudação HTTP em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Use o gatilho Olá HTTP
Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico. [Saiba mais sobre gatilhos](connectors-overview.md).

Aqui está uma sequência de exemplo de como tooset backup Olá HTTP gatilho Olá Designer de lógica do aplicativo.

1. Adicione o gatilho HTTP de saudação em seu aplicativo de lógica.
2. Preencha os parâmetros de saudação para o ponto de extremidade de saudação HTTP que você deseja toopoll.
3. Modificar o intervalo de recorrência de saudação na frequência com a qual ele deve pesquisar.

   Olá lógica aplicativo agora é acionado com qualquer conteúdo que é retornado durante cada verificação.

   ![Gatilho HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Como funciona o gatilho HTTP Olá

gatilho HTTP Olá envia um ponto de extremidade de tooHTTP chamada em um intervalo recorrente. Por padrão, qualquer código de resposta HTTP é menor que 300 faz com que um toorun de aplicativo lógica. toospecify se deve acionar o aplicativo lógico de Olá, você pode editar aplicativo de lógica de saudação na exibição de código e adicionar uma condição que é avaliada após Olá chamada HTTP. Aqui está um exemplo de um gatilho HTTP que é acionado quando a saudação retornou o código de status é maior que ou igual a muito`400`.

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

Detalhes completos sobre os parâmetros de gatilho Olá HTTP estão disponíveis em [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Use a ação Olá HTTP

Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico. 
[Saiba mais sobre ações](connectors-overview.md).

1. Escolha **Nova Etapa** > **Adicionar uma ação**.
3. Na caixa de pesquisa de ação hello, digite **http** ações de saudação HTTP toolist.
   
    ![Selecione a ação Olá HTTP](./media/connectors-native-http/using-action-1.png)

4. Adicione os parâmetros necessários para a chamada de saudação HTTP.
   
    ![Olá completa ação HTTP](./media/connectors-native-http/using-action-2.png)

5. Na barra de ferramentas designer hello, clique em **salvar**. Seu aplicativo lógico é salvo e publicado (ativado) no hello simultaneamente.

## <a name="http-trigger"></a>Gatilho HTTP
Aqui estão os detalhes de saudação disparador Olá que oferece suporte a esse conector. conector HTTP Olá tem um gatilho.

| Gatilho | Descrição |
| --- | --- |
| HTTP |Faz uma chamada HTTP e retorna o conteúdo de resposta de saudação. |

## <a name="http-action"></a>Ação HTTP
Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector. conector HTTP Olá tem uma ação possível.

| Ação | Descrição |
| --- | --- |
| HTTP |Faz uma chamada HTTP e retorna o conteúdo de resposta de saudação. |

## <a name="http-details"></a>Detalhes do HTTP
Olá tabelas a seguir descrevem hello necessárias e os campos de entrada opcionais para ação hello e Olá correspondente saída detalhes associados usando a ação de saudação.

#### <a name="http-request"></a>Solicitação HTTP
Olá seguem campos de entrada para a ação de saudação, que faz uma solicitação HTTP de saída.
Um * significa que é um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Método* |estático |Olá HTTP verbo toouse |
| URI* |uri |Olá URI de solicitação HTTP de saudação |
| Cabeçalhos |headers |Um objeto JSON de tooinclude de cabeçalhos HTTP |
| Corpo |body |saudação de corpo de solicitação HTTP |
| Autenticação |Autenticação |Detalhes de saudação [autenticação](#authentication) seção |

<br>

#### <a name="output-details"></a>Detalhes de saída
Olá seguem detalhes de saída de hello resposta HTTP.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| headers |objeto |Cabeçalhos de resposta |
| Corpo |objeto |Objeto de resposta |
| Código de status |int |Código de status HTTP |

## <a name="authentication"></a>Autenticação
recurso de aplicativos lógicos Olá permite toouse diferentes tipos de autenticação em relação a pontos de extremidade HTTP. Você pode usar essa autenticação com hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  conectores. Olá, tipos de autenticação a seguir podem ser configurado:

* [Autenticação básica](#basic-authentication)
* [Autenticação de certificado de cliente](#client-certificate-authentication)
* [Autenticação OAuth do Azure AD (Azure Active Directory)](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Autenticação básica

Olá, objeto de autenticação a seguir é necessário para a autenticação básica.
Um * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Type* |type |Tipo de autenticação (deve ser `Basic` para a autenticação básica) |
| Username* |Nome de Usuário |Tooauthenticate de nome de usuário |
| Password* |Senha |Senha tooauthenticate |

> [!TIP]
> Se você quiser toouse uma senha que não é possível recuperar definição hello, use um `securestring` parâmetro e hello `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).

Por exemplo:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Autenticação de certificado de cliente

Olá seguinte objeto de autenticação é necessária para autenticação de certificado de cliente. Um * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Type* |type |Olá o tipo de autenticação (deve ser `ClientCertificate` para certificados de cliente SSL) |
| PFX* |pfx |conteúdo codificado com Base64 de saudação do arquivo de troca de informações pessoais (PFX) Olá |
| Password* |Senha |Olá senha tooaccess Olá arquivo PFX |

> [!TIP]
> um parâmetro que não será legível na definição de saudação depois de salvar o aplicativo de lógica de saudação do toouse, você pode usar um `securestring` parâmetro e hello `@parameters()`  
>  [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs).

Por exemplo:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Autenticação OAuth do Azure AD
Olá, objeto de autenticação a seguir é necessário para autenticação OAuth do AD do Azure. Um * significa que é um campo obrigatório.

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| Type* |type |Olá o tipo de autenticação (deve ser `ActiveDirectoryOAuth` para OAuth do AD do Azure) |
| Tenant* |locatário |Identificador do locatário Olá para o locatário de saudação do AD do Azure |
| Audience* |audiência |recurso Hello está solicitando toouse de autorização. Por exemplo: `https://management.core.windows.net/` |
| Client ID* |clientId |Olá identificador de cliente para o aplicativo hello AD do Azure |
| Secret* |segredo |segredo de saudação do cliente de saudação que está solicitando o token Olá |

> [!TIP]
> Você pode usar um `securestring` parâmetro e hello `@parameters()` [função da definição de fluxo de trabalho](http://aka.ms/logicappdocs) toouse um parâmetro que não será legível na definição de saudação depois de salvar.
> 
> 

Por exemplo:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Próximas etapas
Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).

