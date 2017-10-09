---
title: "exceções de mensagens de barramento de serviço aaaAzure | Microsoft Docs"
description: "Lista de exceções de mensagens do Barramento de Serviço e ações sugeridas."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Exceções de mensagens do Barramento de Serviço
Este artigo lista algumas exceções geradas pelo Olá barramento de serviço do Microsoft Azure APIs do sistema de mensagens. Essa referência é toochange de assunto, portanto, verifique as atualizações.

## <a name="exception-categories"></a>Categorias de exceções
APIs de mensagens Hello geram exceções que podem se enquadrar em Olá categorias a seguir, junto com a ação de saudação associada, você pode tomar tootry toofix-los. Observe que o significado de saudação e faz com que uma exceção pode variar dependendo do tipo de saudação da entidade de mensagens (filas/tópicos ou Hubs de eventos):

1. Erro de codificação do usuário ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Ação geral: tentar toofix Olá código antes de continuar.
2. Erro de instalação/configuração ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Ação geral: examinar sua configuração e alterá-la, se necessário.
3. Exceções temporárias ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Ação geral: repita a operação de saudação ou notificar os usuários.
4. Outras exceções ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Ação geral: tipo de exceção específico toohello; Consulte toohello tabela Olá seção a seguir. 

## <a name="exception-types"></a>Tipos de exceção
Olá tabela a seguir lista tipos mensagens de exceção e suas causas e ação sugerida anotações, que você pode executar.

| **Tipo de exceção** | **Descrição/Causa/Exemplos** | **Ação sugerida** | **Observação sobre repetição automática/imediata** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Olá servidor não respondeu toohello solicitado operação dentro de saudação especificado de tempo que é controlado pela [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). servidor de saudação pode ter sido concluída Olá a operação solicitada. Isso pode acontecer devido a toonetwork ou outros atrasos de infraestrutura. |Estado do sistema Olá para manter a consistência e tente novamente se necessário. Confira [TimeoutException](#timeoutexception). |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Olá solicitou uma operação de usuário não é permitida no servidor de saudação ou serviço. Consulte a mensagem de exceção Olá para obter detalhes. Por exemplo, [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) gerará esta exceção se a mensagem foi recebida no [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo. |Verifique o código hello e documentação de saudação. Certifique-se de saudação solicitou a operação é válida. |Tentar novamente não ajudará. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Uma tentativa for feita tooinvoke uma operação em um objeto que já foi fechado, cancelada ou descartada. Em casos raros, a transação de ambiente Olá já foi descartada. |Verifique o código de hello e verifique se que ele não invocar operações em um objeto descartado. |Tentar novamente não ajudará. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto não foi possível adquirir um token, Olá token é inválido ou Olá token não contém Olá declarações necessárias tooperform Olá operação. |Verifique se o provedor de token Olá é criado com valores corretos hello. Verifique a configuração de saudação do hello serviço de controle de acesso. |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Um ou mais método de toohello de argumentos fornecidos são inválidos.<br /> Olá URI fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contém o segmento de caminho (s).<br /> o esquema de URI Olá fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) é inválido. <br />o valor da propriedade Olá é maior do que 32KB. |Verifique o código de chamada hello e certifique-se de argumentos Olá estão corretos. |Tentar novamente não ajudará. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Entidade associada à operação de saudação não existe ou foi excluído. |Certifique-se de entidade Olá existe. |Tentar novamente não ajudará. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tentativa de tooreceive uma mensagem com um número de sequência específica. Esta mensagem não foi encontrada. |Verifique se a mensagem de saudação já não foi recebida. Se a mensagem de saudação foi morta, verifique Olá toosee de fila de mensagens mortas. |Tentar novamente não ajudará. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Cliente não é capaz de tooestablish tooService uma conexão barramento. |Verifique se o nome de host Olá fornecido está correto e Olá host esteja acessível. |Tentar novamente poderá ajudar se houver problemas intermitentes de conectividade. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Serviço não é capaz de tooprocess Olá solicitação no momento. |Cliente pode aguardar um período de tempo e repita a operação de saudação. |O cliente pode tentar novamente após um intervalo determinado. Se uma nova tentativa resultar em uma exceção diferente, verifique o comportamento de repetição de tal exceção. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Símbolo de bloqueio associado a mensagem de saudação expirou ou token de bloqueio Olá não foi encontrado. |Descarte a mensagem de saudação. |Tentar novamente não ajudará. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |O bloqueio associado a esta sessão foi perdido. |Anular Olá [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objeto. |Tentar novamente não ajudará. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Genérico de mensagens de exceção que pode ser acionada em Olá casos a seguir:<br /> Uma tentativa de toocreate um [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) usando um nome ou caminho ao qual pertence o tipo de entidade diferente tooa (por exemplo, um tópico).<br />  Uma tentativa for feita toosend uma mensagem maior do que 256KB. saudação de servidor ou serviço encontrou um erro durante o processamento da solicitação de saudação. Consulte a mensagem de exceção Olá para obter detalhes. Isso geralmente é uma exceção temporária. |Verifique o código de saudação e certifique-se de que apenas os objetos serializáveis são usados para o corpo da mensagem de saudação (ou usar um serializador personalizado). Consulte a documentação de saudação para tipos de valor de saudação com suporte das propriedades de saudação e somente os tipos de uso com suporte. Verificar Olá [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propriedade. Se for **true**, você poderá repetir a operação de saudação. |O comportamento de repetição é indefinido e pode não ajudar. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Tentativa de toocreate uma entidade com um nome que já está sendo usado por outra entidade no namespace de serviço. |Excluir entidade existente hello ou escolha um nome diferente para Olá entidade toobe criado. |Tentar novamente não ajudará. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |saudação de entidade de mensagens atingiu seu tamanho máximo permitido, ou Olá o número máximo de conexões tooa namespace foi excedido. |Crie espaço na entidade Olá recebendo mensagens da entidade hello ou seus filas sub. Confira [QuotaExceededException](#quotaexceededexception). |Pode ajudar a repetição se as mensagens foram removidas do hello enquanto isso. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Barramento de serviço retorna essa exceção, se você tentar toocreate uma ação de regra inválida. Barramento de serviço anexa essa mensagem de morta tooa exceção se ocorrer um erro ao processar a ação de regra Olá para essa mensagem. |Verificar ação de regra Olá estão corretos. |Tentar novamente não ajudará. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Barramento de serviço retorna essa exceção, se você tentar toocreate um filtro inválido. Barramento de serviço anexa essa mensagem de morta tooa exceção se ocorreu um erro durante o processamento de filtro Olá para essa mensagem. |Verifique o filtro Olá estão corretos. |Tentar novamente não ajudará. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Tentativa de tooaccept que uma sessão com uma ID de sessão específica, mas a sessão hello está bloqueado por outro cliente. |Certifique-se de sessão Olá é desbloqueado por outros clientes. |Pode ajudar a repetição se sessão Olá foi lançado em Olá intermediários. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Muitas operações fazem parte da transação de saudação. |Reduza o número de saudação de operações que fazem parte dessa transação. |Tentar novamente não ajudará. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Solicitação para uma operação de tempo de execução em uma entidade desabilitada. |Ative entidade hello. |Pode ajudar a repetição se entidade Olá tiver sido ativada no hello intermediários. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Barramento de serviço retorna essa exceção, se você enviar um tópico de tooa de mensagem que foi previamente filtragem ativada e corresponder a nenhum dos filtros de saudação. |Verifique se pelo menos um filtro é compatível. |Tentar novamente não ajudará. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Conteúdo de uma mensagem excede o limite de 256 KB de saudação. Observe que o limite de 256 KB Olá Olá tamanho total de mensagens, que pode incluir propriedades do sistema e qualquer sobrecarga de .NET. |Reduzir o tamanho de saudação da carga de mensagem de saudação e repita a operação de saudação. |Tentar novamente não ajudará. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Olá transação de ambiente (*Transaction*) é inválido. Ela pode ter sido concluída ou anulada. A exceção interna pode fornecer informações adicionais. | |Tentar novamente não ajudará. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Uma operação é tentada em uma transação que está em dúvida, ou uma tentativa de transação de saudação toocommit e transação Olá torna-se em dúvida. |Seu aplicativo deve tratar essa exceção (como um caso especial), como transações Olá podem ter sido confirmada. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que uma cota para uma entidade específica foi excedida.

### <a name="queues-and-topics"></a>Filas e tópicos
Para filas e tópicos, isso geralmente é tamanho de saudação da fila de saudação. propriedade de mensagem de erro Olá conterá mais detalhes, como no exemplo a seguir de saudação:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

mensagem de saudação estados que tópico Olá excedeu seu limite de tamanho, neste caso 1 GB (limite de tamanho padrão Olá). 

### <a name="namespaces"></a>Namespaces

Para namespaces, [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) pode indicar que um aplicativo excedeu o número máximo de saudação do espaço para nome tooa de conexões. Por exemplo:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Causas comuns
Há duas causas comuns desse erro: Olá a fila de mensagens mortas e receptores de mensagens não está funcionando.

1. **Fila de mensagens mortas** um leitor está falhando toocomplete mensagens e mensagens de saudação são retornadas toohello fila/tópico quando Olá bloqueio expirar. Isso pode acontecer se o leitor Olá encontra uma exceção que impede que ele chamar [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Depois que uma mensagem foi lida 10 vezes, ele move a fila de mensagens mortas toohello por padrão. Esse comportamento é controlado pelo Olá [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) propriedade e tem um valor padrão de 10. Como as mensagens são acumuladas na fila de mensagens mortas hello, eles ocupam espaço.
   
    problema de saudação tooresolve, mensagens de saudação completa e leitura da fila de mensagens mortas hello, como você faria de qualquer outra fila. Olá [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) classe contiver até mesmo um [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) o caminho da fila de mensagens mortas método toohelp formato hello.
2. **Receptor interrompido** Um receptor parou de receber mensagens de uma fila ou de uma assinatura. Olá tooidentify de maneira trata toolook em Olá [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) propriedade, que mostra a análise completa Olá das mensagens de saudação. Se hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) propriedade for alto ou em expansão, mensagens de saudação não estão sendo lidos mais rápido estão sendo gravados.

### <a name="event-hubs"></a>Hubs de Eventos
Os Hubs de Eventos têm um limite de 20 grupos de consumidores por Hub de Eventos. Quando você tenta toocreate mais, você receberá um [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Um [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que uma operação iniciada pelo usuário está demorando mais que o tempo limite da operação hello. 

Você deve verificar o valor de saudação da saudação [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) a propriedade, como atingir esse limite também pode causar uma [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Filas e tópicos
Para filas e tópicos, o tempo limite de saudação é especificado em Olá [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) propriedade, como parte da cadeia de caracteres de conexão hello, ou por meio de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensagem de erro de saudação em si pode variar, mas ele sempre contém o valor de tempo limite de saudação especificado para a operação atual de saudação. 

### <a name="event-hubs"></a>Hubs de Eventos
Para Hubs de eventos, tempo limite de saudação é especificado como parte da cadeia de caracteres de conexão hello, ou por meio de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensagem de erro de saudação em si pode variar, mas ele sempre contém o valor de tempo limite de saudação especificado para a operação atual de saudação. 

### <a name="common-causes"></a>Causas comuns
Há duas causas comuns desse erro: configuração incorreta ou um erro de serviço transitório.

1. **Configuração incorreta** Olá tempo limite da operação pode ser muito pequeno para a condição operacional hello. valor padrão Olá Olá tempo limite da operação no SDK do cliente Olá é 60 segundos. Verifique toosee se seu código tem valor Olá definida toosomething muito pequeno. Observe a condição da rede Olá Olá e uso da CPU pode afetar o tempo de saudação que leva para uma determinada operação toocomplete, para que o tempo limite da operação Olá não deve ser definido valor muito pequeno tooa.
2. **Erro de serviço transitória** às vezes Olá barramento de serviço pode enfrentar atrasos no processamento de solicitações, por exemplo, durante os períodos de tráfego intenso. Nesses casos, você poderá repetir a operação após um atraso até que a operação de saudação for bem-sucedida. Se hello mesma operação ainda falhar após várias tentativas, visite Olá [site de status do serviço do Azure](https://azure.microsoft.com/status/) toosee se houver quaisquer interrupções de serviço conhecido.

## <a name="next-steps"></a>Próximas etapas

Para obter referência de API de .NET do barramento de serviço completa hello, consulte Olá [referência da API do Azure .NET](/dotnet/api/overview/azure/servicebus).

toolearn mais sobre [Service Bus](https://azure.microsoft.com/services/service-bus/), consulte os seguintes tópicos de saudação.

* [Visão geral de mensagens do Barramento de Serviço](service-bus-messaging-overview.md)
* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Arquitetura do Barramento de Serviço](service-bus-architecture.md)

