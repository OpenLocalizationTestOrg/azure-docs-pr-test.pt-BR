---
title: "Expiração de mensagens do Barramento de Serviço do Azure | Microsoft Docs"
description: "Expiração e a vida útil de mensagens do Barramento de Serviço do Azure"
services: service-bus-messaging
documentationcenter: 
author: clemensv
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: sethm
ms.openlocfilehash: 504010a39a4012b9a9edb60bb9a5b33ac20499c1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="message-expiration-time-to-live"></a>Expiração da mensagem (vida útil)

O conteúdo dentro de uma mensagem ou um comando ou consulta que uma mensagem transmite para um destinatário, está quase sempre sujeito a alguma forma de prazo de expiração de nível de aplicativo. Após o prazo, o conteúdo não é mais entregue ou a operação solicitada não é mais executada.

Para ambientes de desenvolvimento e teste em que as consultas e tópicos são frequentemente usadas no contexto de execuções parciais de aplicativos ou partes de aplicativos, também é desejável que as mensagens de teste presas sejam automaticamente coletadas no lixo para que a próxima execução de teste possa começar limpa.

A expiração para qualquer mensagem individual pode ser controlada pela configuração da propriedade do sistema [TimeToLive](/dotnet/api/microsoft.azure.servicebus.message.timetolive#Microsoft_Azure_ServiceBus_Message_TimeToLive), que especifica uma duração relativa. A expiração se torna um instante absoluto quando a mensagem é enfileirada na entidade. Nesse momento, a propriedade [ExpiresAtUtc](/dotnet/api/microsoft.azure.servicebus.message.expiresatutc) obtém o valor [**EnqueuedTimeUtc**](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.enqueuedtimeutc#Microsoft_ServiceBus_Messaging_BrokeredMessage_EnqueuedTimeUtc) + [**TimeToLive**](/dotnet/api/microsoft.azure.servicebus.message.timetolive#Microsoft_Azure_ServiceBus_Message_TimeToLive).

Após o instante **ExpiresAtUtc**, as mensagens se tornam não qualificadas para recuperação. A expiração não afeta as mensagens que estão bloqueadas no momento para entrega, essas mensagens ainda são manipuladas normalmente. Se o bloqueio expirar ou se a mensagem for abandonada, a expiração entrará em vigor imediatamente.

Enquanto a mensagem estiver em um bloqueio, o aplicativo poderá estar em posse de uma mensagem que expirou nominalmente. Se o aplicativo está disposto a prosseguir com o processamento ou opta por abandonar a mensagem cabe ao implementador.

## <a name="entity-level-expiration"></a>Expiração de nível de entidade

Todas as mensagens enviadas para uma fila ou tópico estão sujeitas a uma expiração padrão que é definida no nível da entidade com a propriedade [defaultMessageTimeToLive](/azure/templates/microsoft.servicebus/namespaces/queues) e que também pode ser definida no portal durante a criação e ajustada posteriormente. A expiração padrão é usada para todas as mensagens enviadas para a entidade em que [TimeToLive](/dotnet/api/microsoft.azure.servicebus.message.timetolive#Microsoft_Azure_ServiceBus_Message_TimeToLive) não é definida explicitamente. A expiração padrão também funciona como um limite para o valor de **TimeToLive**. Mensagens que têm uma expiração de **TimeToLive** maior do que o valor padrão são silenciosamente ajustadas para o valor de **defaultMessageTimeToLive** antes de serem enfileiradas.

As mensagens expiradas podem, opcionalmente, ser movidas para uma [fila de mensagens mortas](service-bus-dead-letter-queues.md) definindo a propriedade [EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enabledeadletteringonmessageexpiration#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) ou marcando a caixa respectiva no portal. Se a opção estiver desabilitada, as mensagens expiradas serão descartadas. As mensagens expiradas movidas para a fila de mensagens mortas podem ser distinguidas de outras mensagens mortas avaliando a propriedade [DeadletterReason](service-bus-dead-letter-queues.md#moving-messages-to-the-dlq) que o agente armazena na seção de propriedades do usuário, o valor é [TTLExpiredException](service-bus-dead-letter-queues.md#moving-messages-to-the-dlq) nesse caso.

No caso mencionado acima em que a mensagem está protegida contra expiração enquanto está bloqueada e se o sinalizador está definido na entidade, a mensagem é movida para a fila de mensagens mortas assim que o bloqueio é abandonado ou expira. No entanto, ela não é movida se a mensagem está estabelecida com êxito, o que assume então que o aplicativo a manipulou com êxito, apesar da expiração nominal.

A combinação de [TimeToLive](/dotnet/api/microsoft.azure.servicebus.message.timetolive#Microsoft_Azure_ServiceBus_Message_TimeToLive) e mensagens mortas automáticas (e transacionais) na expiração são uma ferramenta valiosa para estabelecer confiança em se um trabalho atribuído a um manipulador ou um grupo de manipuladores em um prazo é recuperado para processamento conforme o prazo é alcançado.

Por exemplo, considere um site da Web que precisa executar trabalhos de forma confiável em um back-end com restrição de escala e que ocasionalmente enfrente picos de tráfego ou deseje ser isolado contra episódios de disponibilidade de tal back-end. No caso normal, o manipulador do lado do servidor para os dados de usuário enviados envia por push as informações em uma fila e subsequentemente recebe uma resposta confirmando o tratamento bem-sucedido da transação em uma fila de resposta. Se houver um aumento de tráfego e o manipulador de back-end não puder processar seus itens de lista de pendências no prazo, os trabalhos expirados serão retornados na fila de mensagens mortas. O usuário interativo pode ser notificado de que a operação solicitada levará um pouco mais do que o normal e a solicitação poderá então ser colocada em uma fila diferente para um caminho de processamento em que o resultado do processamento eventual é enviado para o usuário por email. 

## <a name="temporary-entities"></a>Entidades temporárias

As assinaturas, os tópicos e as consultas do Barramento de Serviço podem ser criados como entidades temporárias, que são removidas automaticamente quando não forem usadas por um período de tempo especificado.
 
A limpeza automática é útil em cenários de desenvolvimento e teste nos quais as entidades são criadas dinamicamente em não são limpas após o uso, devido ao teste ou à execução de depuração ter sido interrompida. Isso também é útil quando um aplicativo cria entidades dinâmicas, como uma fila de resposta, para receber respostas de volta para um processo do servidor Web ou em outro objeto de duração relativamente curta, no qual é difícil limpar essas entidades de forma confiável quando a instância do objeto desaparece.

O recurso é habilitado usando a propriedade [autoDeleteOnIdle](/azure/templates/microsoft.servicebus/namespaces/queues), que é definida para a duração pela qual uma entidade deve estar ociosa (não utilizada) antes de ser excluída automaticamente. A duração mínima é de 5 minutos.
 
A propriedade deve ser definida por meio de uma operação do Azure Resource Manager ou por meio de APIs [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) do cliente .NET Framework. Ela não pode ser definida por meio do portal.


## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre as mensagens do Barramento de Serviço, consulte os tópicos a seguir:

* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Filas, tópicos e assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md)
* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
* [Como usar tópicos e assinaturas do Barramento de Serviço](service-bus-dotnet-how-to-use-topics-subscriptions.md)