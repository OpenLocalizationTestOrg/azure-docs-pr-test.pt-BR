---
title: "aaaOverview do modelo de segurança e autenticação de Hubs de eventos do Azure | Microsoft Docs"
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
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Visão geral do modelo de autenticação e segurança dos Hubs de Eventos
modelo de segurança de Hubs de eventos do Azure Olá atende Olá requisitos a seguir:

* Somente os clientes que apresentam credenciais válidas podem enviar hub de eventos de tooan de dados.
* Um cliente não pode representar outro cliente.
* Um cliente não autorizado pode ser impedido de enviar o hub de eventos de tooan de dados.

## <a name="client-authentication"></a>Autenticação de cliente
modelo de segurança de Hubs de eventos Olá baseia-se em uma combinação de [assinatura de acesso compartilhado (SAS)](../service-bus-messaging/service-bus-sas.md) tokens e *editores de eventos*. Um editor de eventos define um ponto de extremidade virtual para um hub de eventos. publicador de saudação só pode ser usado toosend hub de eventos de tooan de mensagens. Não é possível tooreceive mensagens de um publicador.

Normalmente, um hub de eventos emprega um editor por cliente. Todas as mensagens são enviadas tooany de editores de saudação de um hub de eventos são colocadas dentro desse hub de eventos. Os editores habilitam o controle de acesso detalhado e a limitação.

Cada cliente de Hubs de eventos é atribuído um token exclusivo, que é carregado toohello cliente. tokens de saudação são produzidos, de modo que cada token exclusivo conceda publicador exclusivo diferente de tooa acesso. Um cliente que possui um token só pode enviar tooone publisher, mas nenhum outro editor. Se o compartilhamento de vários clientes Olá mesmo token, em seguida, cada um deles compartilha um publicador.

Embora não seja recomendado, é possível tooequip dispositivos com tokens que concedam hub de eventos de tooan acesso direto. Qualquer dispositivo que contenha esse token pode enviar mensagens diretamente para esse hub de eventos. Tal dispositivo não poderá ser toothrottling de assunto. Além disso, dispositivo Olá não pode estar na lista negra de envio toothat hub de eventos.

Todos os tokens são assinados com uma chave SAS. Normalmente, todos os tokens são assinados com hello mesma chave. Os clientes não estão cientes da chave Olá; Isso impede que outros clientes criem tokens.

### <a name="create-hello-sas-key"></a>Criar chave SAS Olá

Ao criar um namespace de Hubs de eventos, o serviço hello gera uma chave SAS de 256 bits chamada **RootManageSharedAccessKey**. Essa chave concede envia, ouvir e gerenciar direitos toohello namespace. Você também pode criar chaves adicionais. É recomendável que você gere uma chave que concede envia hub de eventos específicos de toohello de permissões. Restante Olá deste tópico, supõe-se que você nomeou esta chave **EventHubSendKey**.

saudação de exemplo a seguir cria uma chave de somente de envio ao criar o hub de eventos hello:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Gerar tokens

Você pode gerar tokens usando a chave de SAS hello. Você deve criar somente um token por cliente. Tokens podem ser gerados usando o seguinte método de saudação. Todos os tokens são gerados usando Olá **EventHubSendKey** chave. A cada token é atribuído um URI exclusivo.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Ao chamar esse método, Olá URI deve ser especificado como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Para todos os tokens, Olá URI é idêntico, com exceção de saudação do `PUBLISHER_NAME`, que deve ser diferente para cada token. Idealmente, `PUBLISHER_NAME` representa Olá ID do cliente Olá que recebe esse token.

Este método gera um token com hello estrutura a seguir:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

tempo de expiração do token de saudação é especificado em segundos desde 1º de janeiro de 1970. Olá seguinte é um exemplo de um token:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Normalmente, os tokens de saudação têm um tempo de vida que é semelhante ou excede o tempo de vida de saudação do cliente hello. Se cliente Olá Olá recurso tooobtain um novo token, tokens com um tempo de vida mais curto podem ser usados.

### <a name="sending-data"></a>Enviar dados
Após a criação de tokens hello, cada cliente é configurado com seu próprio token exclusivo.

Quando o cliente Olá envia dados a um hub de eventos, marcas de sua solicitação de envio com o token de saudação. tooprevent um invasor intercepte e roube o token hello, a comunicação de saudação entre cliente hello e hub de eventos Olá deve ocorrer em um canal criptografado.

### <a name="blacklisting-clients"></a>Colocando clientes na lista de bloqueio
Se um token for roubado por um invasor, o invasor Olá pode representar o cliente de saudação cujo token foi roubado. Colocar um cliente na lista de bloqueio o inutilizará até ele receber um novo token que usa um outro editor.

## <a name="authentication-of-back-end-applications"></a>Autenticação de aplicativos back-end

aplicativos de back-end tooauthenticate que consomem dados Olá gerados por clientes de Hubs de eventos, os Hubs de eventos emprega um modelo de segurança que é modelo toohello semelhante que é usado para tópicos do barramento de serviço. Um grupo de consumidores de Hubs de eventos é um tópico de barramento de serviço do tooa equivalente assinatura tooa. Um cliente pode criar um grupo de consumidores, se o grupo de consumidores do hello solicitação toocreate Olá é acompanhado por um token que concede privilégios para o hub de eventos de saudação de gerenciamento ou para Olá namespace toowhich hub de eventos Olá pertence. Um cliente pode tooconsume dados de um grupo de consumidores se Olá receber a solicitação são acompanhados por um token que concede direitos no grupo de consumidores de recebimento, hello hub de eventos ou hub de eventos Olá namespace toowhich Olá pertence.

versão atual de saudação do barramento de serviço não dá suporte a regras SAS para assinaturas individuais. Olá que mesmo se aplica para grupos de consumidores de Hubs de eventos. Suporte a SAS será adicionado para ambos os recursos no hello futuras.

Na ausência de saudação de autenticação de SAS para grupos de consumidores individuais, você pode usar SAS chaves toosecure todos os grupos de consumidores com uma chave comum. Essa abordagem permite que os dados de tooconsume um aplicativo de qualquer um dos grupos de consumidores de saudação de um hub de eventos.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre Hubs de eventos, visite Olá seguintes tópicos:

* [Visão Geral dos Hubs de Eventos]
* [Visão Geral de Assinatura de Acesso Compartilhado]
* [Aplicativos de exemplo que usam Hub de Eventos]

[Visão Geral dos Hubs de Eventos]: event-hubs-what-is-event-hubs.md
[Aplicativos de exemplo que usam Hub de Eventos]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Visão Geral de Assinatura de Acesso Compartilhado]: ../service-bus-messaging/service-bus-sas.md

