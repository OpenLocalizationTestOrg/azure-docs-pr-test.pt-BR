---
title: "aaaAMQP 1.0 em operações baseadas em solicitação-resposta do barramento de serviço do Azure | Microsoft Docs"
description: "Lista de operações baseadas em solicitação-resposta do Barramento de Serviço do Microsoft Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>AMQP 1.0 no Barramento de Serviço do Microsoft Azure: operações baseadas em solicitação-resposta

Este tópico define a lista de saudação de operações baseado em solicitação/resposta do barramento de serviço do Microsoft Azure. Estas informações são baseadas no rascunho de trabalho Olá AMQP gerenciamento versão 1.0.  
  
Para um nível de transmissão AMQP 1.0 protocolo guia detalhado, que explica como o barramento de serviço implementa e se baseia no hello especificações técnicas do OASIS AMQP, consulte Olá [AMQP 1.0 no guia de protocolo do barramento de serviço do Azure e Hubs de eventos](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Conceitos  
  
### <a name="entity-description"></a>Descrição de entidade  

Uma descrição da entidade refere-se a um barramento de serviço do tooeither [classe QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription classe](/dotnet/api/microsoft.servicebus.messaging.topicdescription), ou [SubscriptionDescription classe](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) objeto.  
  
### <a name="brokered-message"></a>Mensagem agenciada  

Representa uma mensagem no barramento de serviço, que é a mensagem do AMQP mapeado tooan. mapeamento de saudação é definido em hello [guia do protocolo AMQP do barramento de serviço](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Anexar o nó de gerenciamento de tooentity  

Todas as operações de saudação descritas neste documento seguem um padrão de solicitação/resposta, são entidade tooan no escopo e exigem anexando tooan nó de gerenciamento de entidade.  
  
### <a name="create-link-for-sending-requests"></a>Criar link para enviar solicitações  

Cria um nó de gerenciamento de toohello link para enviar solicitações.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Criar link para receber respostas  

Cria um link para receber respostas de nó de gerenciamento de saudação.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Transferir uma mensagem de solicitação  

Transfere uma mensagem de solicitação.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Receber uma mensagem de resposta  

Recebe a mensagem de resposta de saudação do link de resposta de saudação.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
mensagem de resposta Hello está Olá formulário a seguir:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Endereço de entidade do Barramento de Serviço  

As entidades do Barramento de Serviço devem ser abordadas da seguinte maneira:  
  
|Tipo de entidade|Endereço|Exemplo|  
|-----------------|-------------|-------------|  
|fila|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|topic|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|subscription|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Operações de mensagem  
  
### <a name="message-renew-lock"></a>Renovar Bloqueio da Mensagem  

Estende o bloqueio de saudação de uma mensagem pelo tempo de saudação especificado na descrição da entidade hello.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
 corpo de mensagem de solicitação de saudação deve consistir em uma seção do valor do amqp que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|matriz de uuid|Sim|Toorenew de tokens de bloqueio de mensagem.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha.|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma seção do valor do amqp que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|expirations|matriz de carimbo de data/hora|Sim|Mensagem de bloqueio token novo expiração correspondente toohello solicitar bloqueio tokens.|  
  
### <a name="peek-message"></a>Espiar mensagem  

Espia mensagens sem bloqueio.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|longo|Sim|Número de sequência do qual toostart inspeção.|  
|`message-count`|int|Sim|Número máximo de mensagens toopeek.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – tem mais mensagens<br /><br /> 0xcc: nenhum conteúdo – não há mais mensagens|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|da nuvem para o dispositivo|lista de mapas|Sim|Lista de mensagens na qual cada mapa representa uma mensagem.|  
  
mapa de saudação que representa uma mensagem deve conter Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|message|matriz de bytes|Sim|Mensagem codificada por transmissão AMQP 1.0.|  
  
### <a name="schedule-message"></a>Agendar mensagem  

Agenda mensagens.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|da nuvem para o dispositivo|lista de mapas|Sim|Lista de mensagens na qual cada mapa representa uma mensagem.|  
  
mapa de saudação que representa uma mensagem deve conter Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|message-id|string|Sim|`amqpMessage.Properties.MessageId` como uma cadeia de caracteres|  
|session-id|string|Sim|`amqpMessage.Properties.GroupId as string`|  
|partition-key|string|Sim|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|message|matriz de bytes|Sim|Mensagem codificada por transmissão AMQP 1.0.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha.|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matriz de long|Sim|Número de sequência das mensagens agendadas. Número de sequência é toocancel usado.|  
  
### <a name="cancel-scheduled-message"></a>Cancelar mensagem agendada  

Cancela as mensagens agendadas.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matriz de long|Sim|Números de sequência de mensagens programadas toocancel.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha.|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matriz de long|Sim|Número de sequência das mensagens agendadas. Número de sequência é toocancel usado.|  
  
## <a name="session-operations"></a>Operações da sessão  
  
### <a name="session-renew-lock"></a>Renovar Bloqueio da Sessão  

Estende o bloqueio de saudação de uma mensagem pelo tempo de saudação especificado na descrição da entidade hello.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sim|ID da sessão.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – tem mais mensagens<br /><br /> 0xcc: nenhum conteúdo – não há mais mensagens|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|expiração|timestamp|Sim|Nova expiração.|  
  
### <a name="peek-session-message"></a>Espirar Mensagem da Sessão  

Espia as mensagens da sessão sem bloqueio.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|longo|Sim|Número de sequência do qual toostart inspeção.|  
|message-count|int|Sim|Número máximo de mensagens toopeek.|  
|session-id|string|Sim|ID da sessão.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – tem mais mensagens<br /><br /> 0xcc: nenhum conteúdo – não há mais mensagens|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém um mapa com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|da nuvem para o dispositivo|lista de mapas|Sim|Lista de mensagens na qual cada mapa representa uma mensagem.|  
  
 mapa de saudação que representa uma mensagem deve conter Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|message|matriz de bytes|Sim|Mensagem codificada por transmissão AMQP 1.0.|  
  
### <a name="set-session-state"></a>Definir Estado de Sessão  

Conjuntos de Olá estado da sessão.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sim|ID da sessão.|  
|session-state|matriz de bytes|Sim|Dados binários opacos.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
### <a name="get-session-state"></a>Obter Estado de Sessão  

Obtém o estado de saudação de uma sessão.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sim|ID da sessão.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|session-state|matriz de bytes|Sim|Dados binários opacos.|  
  
### <a name="enumerate-sessions"></a>Enumerar Sessões  

Enumera as sessões em uma entidade de mensagens.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|Sim|Filtre tooinclude sessões somente atualizadas após um determinado momento.|  
|skip|int|Sim|Ignore um número de sessões.|  
|top|int|Sim|Número máximo de sessões.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – tem mais mensagens<br /><br /> 0xcc: nenhum conteúdo – não há mais mensagens|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|skip|int|Sim|Número de sessões ignoradas se o código de status for 200.|  
|sessions-ids|matriz de cadeias de caracteres|Sim|Matriz de IDs de sessão se o código de status for 200.|  
  
## <a name="rule-operations"></a>Operações de regra  
  
### <a name="add-rule"></a>Adicionar regra  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sim|Nome da regra, não incluindo nomes de tópico e assinatura.|  
|rule-description|map|Sim|Descrição da regra, conforme especificado na próxima seção.|  
  
Olá **descrição da regra** mapa deve incluir Olá seguintes entradas, onde **filtro sql** e **filtro de correlação** são mutuamente exclusivos:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|Sim|`sql-filter`, conforme especificado na próxima seção, Olá.|  
|correlation-filter|map|Sim|`correlation-filter`, conforme especificado na próxima seção, Olá.|  
|sql-rule-action|map|Sim|`sql-rule-action`, conforme especificado na próxima seção, Olá.|  
  
mapa de filtro sql Olá deve incluir Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|expressão|string|Sim|Expressão de filtro SQL.|  
  
Olá **filtro de correlação** mapa deve incluir pelo menos um dos Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|correlation-id|string|Não||  
|message-id|string|Não||  
|para|string|Não||  
|reply-to|string|Não||  
|label|string|Não||  
|session-id|string|Não||  
|reply-to-session-id|string|Não||  
|content-type|string|Não||  
|propriedades|map|Não|Mapeia tooService barramento [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Olá **ação de regra sql** mapa deve incluir Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|expressão|string|Sim|Expressão de ação do SQL.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
### <a name="remove-rule"></a>Remover Regra  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sim|Nome da regra, não incluindo nomes de tópico e assinatura.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
## <a name="deferred-message-operations"></a>Operações de mensagem adiada  
  
### <a name="receive-by-sequence-number"></a>Receber pelo número de sequência  

Recebe as mensagens adiadas por número de sequência.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matriz de long|Sim|Números de sequência.|  
|receiver-settle-mode|ubyte|Sim|Modo de **liquidação do receptor**, conforme especificado no AMQP Core v1.0.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|  
  
corpo de mensagem de resposta de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|da nuvem para o dispositivo|lista de mapas|Sim|Lista de mensagens, em que cada mapa representa uma mensagem.|  
  
mapa de saudação que representa uma mensagem deve conter Olá entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|Sim|Token de bloqueio se `receiver-settle-mode` for 1.|  
|message|matriz de bytes|Sim|Mensagem codificada por transmissão AMQP 1.0.|  
  
### <a name="update-disposition-status"></a>Atualizar status de disposição  

Atualiza o status de disposição de saudação das mensagens adiadas.  
  
#### <a name="request"></a>Solicitação  

mensagem de solicitação de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sim|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|Não|Tempo limite da operação no servidor em milissegundos.|  
  
corpo de mensagem de solicitação de saudação deve consistir em uma **amqp valor** seção que contém uma **mapa** com hello entradas a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|Sim|concluído<br /><br /> abandonado<br /><br /> suspenso|  
|lock-tokens|matriz de uuid|Sim|Status de disposição de tooupdate de tokens de bloqueio de mensagem.|  
|deadletter-reason|string|Não|Pode ser definido se o status de disposição está definido muito**suspenso**.|  
|deadletter-description|string|Não|Pode ser definido se o status de disposição está definido muito**suspenso**.|  
|properties-to-modify|map|Não|Lista de barramento de serviço orientadas toomodify de propriedades de mensagem.|  
  
#### <a name="response"></a>Resposta  

mensagem de resposta de saudação deve incluir Olá propriedades do aplicativo a seguir:  
  
|Chave|Tipo de valor|Obrigatório|Conteúdo de valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sim|Código de resposta HTTP [RFC2616]<br /><br /> 200: OK – êxito; caso contrário, falha|  
|statusDescription|string|Não|Descrição do status de saudação.|

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre AMQP e barramento de serviço, visite Olá links a seguir:

* [Visão geral do Barramento de Serviço para AMQP]
* [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]
* [AMQP no Barramento de Serviço para Windows Server]

[Visão geral do Barramento de Serviço para AMQP]: service-bus-amqp-overview.md
[Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP no Barramento de Serviço para Windows Server]: https://msdn.microsoft.com/library/dn574799.asp