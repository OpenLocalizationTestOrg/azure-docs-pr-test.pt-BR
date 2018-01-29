---
title: "Visão geral do modelo de autenticação e de segurança dos Hubs de Eventos do Azure | Microsoft Docs"
description: "Visão geral do modelo de autenticação e segurança dos Hubs de Eventos"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2017
ms.author: sethm;clemensv
ms.openlocfilehash: bfe7b95236c1a5336c1bb3a93d0eb5ca880adabf
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Visão geral do modelo de autenticação e segurança dos Hubs de Eventos

O modelo de segurança dos Hubs de Eventos do Azure atende aos seguintes requisitos:

* Somente clientes que apresentam credenciais válidas podem enviar dados para um hub de eventos.
* Um cliente não pode representar outro cliente.
* Um cliente invasor pode ser impedido de enviar dados para um hub de eventos.

## <a name="client-authentication"></a>Autenticação de cliente

O modelo de segurança dos Hubs de Eventos se baseia em uma combinação de tokens [SAS (Assinatura de Acesso Compartilhado)](../service-bus-messaging/service-bus-sas.md) e de *editores de eventos*. Um editor de eventos define um ponto de extremidade virtual para um hub de eventos. O editor só pode ser usado para enviar mensagens a um hub de eventos. Não é possível receber mensagens de um editor.

Normalmente, um hub de eventos emprega um editor por cliente. Todas as mensagens enviadas a um dos publicadores de um hub de eventos são enfileiradas nesse hub de eventos. Os editores habilitam o controle de acesso detalhado e a limitação.

Cada cliente dos hubs de eventos recebe um token exclusivo que é carregado no cliente. Os tokens são produzidos de modo que cada token exclusivo concede acesso a um editor exclusivo diferente. Um cliente que possui um token só pode enviar para um editor específico, e para nenhum outro. Se vários clientes compartilharem o mesmo token, cada um desses deles compartilhará um editor.

Embora não seja recomendado, é possível equipar os dispositivos com tokens que concedem acesso direto a um hub de eventos. Qualquer dispositivo que contenha esse token pode enviar mensagens diretamente para esse hub de eventos. Esse dispositivo não estará sujeito à limitação. Além disso, o dispositivo não pode ser incluído na lista de bloqueios para ser impedido de enviar para esse hub de eventos.

Todos os tokens são assinados com uma chave SAS. Normalmente, todos os tokens são assinados com a mesma chave. Os clientes não estão cientes da chave; isso impede que outros clientes criem tokens.

### <a name="create-the-sas-key"></a>Criar a chave SAS

Ao criar um namespace de Hubs de Eventos, o serviço gera automaticamente uma chave SAS de 256 bits chamada **RootManageSharedAccessKey**. Essa regra tem um par associado de chaves primárias e secundárias que permitem enviar, escutar e gerenciar os direitos para o namespace. Você também pode criar chaves adicionais. É recomendável que você crie uma chave que concede permissões de envio para o hub de eventos específico. No restante deste tópico, pressupõe-se que você tenha nomeado esta chave como **EventHubSendKey**.

O exemplo a seguir cria uma chave somente de envio ao criar o hub de eventos:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Gerar tokens

Você pode gerar tokens usando a chave SAS. Você deve criar somente um token por cliente. Tokens podem ser criados usando o seguinte método. Todos os tokens são gerados usando a chave **EventHubSendKey** . A cada token é atribuído um URI exclusivo.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Ao chamar esse método, o URI deve ser especificado como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Para todos os tokens, o URI é idêntico, com exceção de `PUBLISHER_NAME`, que deve ser diferente para cada token. O ideal é que `PUBLISHER_NAME` represente a ID do cliente que recebe esse token.

Esse método gera um token com a seguinte estrutura:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

O tempo de expiração do token é especificado em segundos desde 1º de janeiro de 1970. Segue um exemplo de um token:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Normalmente, os tokens têm um tempo de vida semelhante a superior ao tempo de vida do cliente. Se o cliente tiver a capacidade de obter um novo token, tokens com um tempo de vida mais curto podem ser usados.

### <a name="sending-data"></a>Enviar dados

Depois que os tokens são criados, cada cliente é configurado com seu próprio token exclusivo.

Quando o cliente envia dados a um hub de eventos, ele marca a solicitação de envio com o token. Para evitar que um invasor intercepte e roube o token, a comunicação entre o cliente e o hub de eventos deve ocorrer em um canal criptografado.

### <a name="blacklisting-clients"></a>Colocando clientes na lista de bloqueio

Se um token for roubado por um invasor, este poderá representar o cliente cujo token foi roubado. Colocar um cliente na lista de bloqueio o inutilizará até ele receber um novo token que usa um outro editor.

## <a name="authentication-of-back-end-applications"></a>Autenticação de aplicativos back-end

Para autenticar aplicativos back-end que consomem os dados gerados por clientes dos Hubs de Eventos, estes empregam um modelo de segurança semelhante ao modelo usado para os tópicos do Barramento de Serviço. Um grupo de consumidores de Hubs de Eventos é equivalente a uma assinatura de um tópico do Barramento de Serviço. Um cliente pode criar um grupo de consumidores se a solicitação para criar o grupo for acompanhada por um token que concede privilégios de gerenciamento para o hub de eventos ou para o namespace ao qual o hub de eventos pertence. Um cliente pode consumir dados de um grupo de consumidores, se a solicitação de recebimento for acompanhada por um token que concede direitos de recebimento no grupo de consumidores, o hub de eventos ou o namespace ao qual o hub de eventos pertence.

A versão atual do Barramento de Serviço não dá suporte a regras SAS para assinaturas individuais. O mesmo se aplica a grupos de consumidores de Hubs de Eventos. O suporte a SAS será adicionado para os dois recursos no futuro.

Na ausência de autenticação SAS para grupos de consumidores individuais, você pode utilizar chaves SAS para proteger todos os grupos de consumidores com uma chave comum. Essa abordagem permite que um aplicativo consuma dados de qualquer grupo de consumidores de um hub de eventos.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os Hubs de Eventos, veja os tópicos a seguir:

* [Visão geral de Hubs de Evento]
* [Visão Geral de Assinatura de Acesso Compartilhado]
* [Aplicativos de exemplo que usam Hub de Eventos]

[Visão geral de Hubs de Evento]: event-hubs-what-is-event-hubs.md
[Aplicativos de exemplo que usam Hub de Eventos]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Visão Geral de Assinatura de Acesso Compartilhado]: ../service-bus-messaging/service-bus-sas.md

