---
title: "autenticação e segurança de grade de eventos aaaAzure"
description: Descreve a Grade de Eventos do Azure e seus conceitos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Segurança e autenticação da Grade de Eventos 

A Grade de Eventos do Azure tem três tipos de autenticação:

* Assinaturas de evento
* Publicação de evento
* Entrega de eventos do WebHook

## <a name="webhook-event-delivery"></a>Entrega de eventos do WebHook

Webhooks são um dos muitos eventos tooreceive de maneiras em tempo real da grade de eventos do Azure.

Sempre que houver um novo toobe pronto do evento entregue, grade de eventos envia uma solicitação HTTP com tooyour WebHook com o evento Olá no corpo de saudação.

Quando você registra seu próprio ponto de extremidade de WebHook com a grade de eventos, envia uma solicitação POST com um código de validação simples na propriedade de ponto de extremidade de tooprove de ordem. Seu aplicativo precisa toorespond exibindo o código de validação back hello. Grade de eventos não fornecerá eventos tooWebHook pontos de extremidade que não passaram na validação de saudação.
 
### <a name="validation-details"></a>Detalhes da validação:

* Em tempo de saudação de criação/atualização de assinatura de evento, a grade de eventos lança um ponto de extremidade de destino de toohello do evento de "SubscriptionValidationEvent".
* evento de saudação contém um valor de cabeçalho "Tipo de evento: validação".
* corpo do evento Olá tem Olá mesmo esquema que outros eventos de grade de eventos.
* dados de evento de saudação incluem uma propriedade de "Validação" com uma cadeia de caracteres gerada aleatoriamente, por exemplo "ValidationCode: acb13…".

Na propriedade de ponto de extremidade de tooprove ordem, por exemplo, o código de validação back Olá de eco "ValidationResponse: acb13...".

Por fim, é importante toonote que grade de eventos do Azure oferece suporte somente a pontos de extremidade HTTPS webhook.
## <a name="event-subscription"></a>Assinatura do evento

toosubscribe tooan eventos, você deve ter Olá **Microsoft.EventGrid/EventSubscriptions/Write** necessária a permissão em Olá recursos. Essa permissão é necessária porque você está escrevendo uma nova assinatura no escopo de saudação do recurso de saudação. Olá necessário recursos varia de acordo com se você estiver assinando tooa sistema tópico ou personalizado. Ambos os tipos são descritos nesta seção.

### <a name="system-topics-azure-service-publishers"></a>Tópicos do sistema (publicadores de serviço do Azure)

Tópicos do sistema, você precisa de permissão toowrite uma nova assinatura de evento no escopo de saudação do evento de publicação Olá Olá recursos. formato de saudação do recurso de saudação é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Por exemplo, o evento de tooan toosubscribe em uma conta de armazenamento denominada **myacct**, você precisa de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Tópicos personalizados

Para tópicos personalizados, você precisa de permissão toowrite uma nova assinatura de evento no escopo de saudação do tópico de grade de eventos de saudação. formato de saudação do recurso de saudação é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Por exemplo, toosubscribe tooa tópico personalizado chamado **mytopic**, você precisa de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Publicação de tópico

Os tópicos usam a Assinatura de Acesso Compartilhado (SAS) ou a autenticação de chave. Recomendamos a SAS, mas a autenticação de chave fornece programação simples e é compatível com vários publicadores de webhook existentes. 

Incluir o valor de autenticação Olá no cabeçalho HTTP de saudação. SAS, use **token de sas aeg** para valor de cabeçalho de saudação. Para autenticação de chave, use **aeg chave de sas** para valor de cabeçalho de saudação.

### <a name="key-authentication"></a>Autenticação de chave

Autenticação de chave é a forma mais simples de saudação de autenticação. Use o formato de saudação:`aeg-sas-key: <your key>`

Por exemplo, você pode passar uma chave com: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Tokens SAS

Tokens SAS para a grade de eventos incluem recursos hello, um tempo de expiração e uma assinatura. Olá formato do token SAS Olá é: `r={resource}&e={expiration}&s={signature}`.

recurso Hello é caminho Olá para Olá tópico toowhich estiver enviando eventos. Por exemplo, um caminho de recurso válido é:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Você pode gerar assinatura de saudação de uma chave.

Por exemplo, um valor válido de **aeg-sas-token** é:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

saudação de exemplo a seguir cria um token SAS para uso com a grade de eventos:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Controle de acesso de gerenciamento

Grade de eventos do Azure permite que você toocontrol Olá nível de acesso fornecido toodifferent usuários toodo várias operações de gerenciamento, como assinaturas de evento de lista, criar novos e gerar chaves. A Grade de Eventos utiliza a verificação RBAC (Verificação de acesso com base em função) do Azure para isso.

### <a name="operation-types"></a>Tipos de operação

Grade de eventos do Azure dá suporte a saudação ações a seguir:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Olá três operações retorno potencialmente informações secretas que obtém filtrado normais das operações de leitura. É prática recomendada para você, operações de toothese toorestrict acesso. Funções personalizadas podem ser criadas usando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Interface de linha de comando (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)e hello [API REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Aplicação da Verificação RBAC (Verificação de acesso com base em função)

Use Olá etapas tooenforce RBAC para diferentes usuários a seguir:

#### <a name="create-a-custom-role-definition-file-json"></a>Criar um arquivo de definição de função personalizado (.json)

Olá seguem definições de função de grade de eventos de exemplo que permitem aos usuários tooperform diferentes conjuntos de ações.

**EventGridReadOnlyRole.json**: permitir apenas operações somente leitura.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: permitir ações restritas posteriores, mas impedir ações de exclusão.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: permitir todas as ações da grade de eventos.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Instalar e logon tooAzure CLI

* CLI do Azure versão 0.8.8 ou posterior. versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).
* Azure Resource Manager na Azure CLI. Vá muito[usando Olá CLI do Azure com o Gerenciador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.

#### <a name="create-a-custom-role"></a>Criar uma função personalizada

toocreate uma função personalizada, use:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Atribuir Olá função tooa usuário


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Próximas etapas

* Para uma introdução tooEvent grade, consulte [sobre a grade de eventos](overview.md)
