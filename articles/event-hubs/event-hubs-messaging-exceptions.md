---
title: "exceções de mensagens de Hubs de eventos aaaAzure | Microsoft Docs"
description: "Lista de exceções de mensagens dos Hubs de Eventos e ações sugeridas."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Exceções de mensagens dos Hubs de Eventos
Este artigo lista algumas das exceções Olá geradas pelo hello Azure Service Bus APIs, que incluem os Hubs de eventos do sistema de mensagens. Essa referência é toochange de assunto, portanto, verifique as atualizações.

## <a name="exception-categories"></a>Categorias de exceções
APIs de Hubs de evento Hello gerar exceções que podem se enquadrar em Olá categorias a seguir, junto com a ação de saudação associada, você pode tomar tootry toofix-los.

1. Erro de codificação do usuário: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Ação geral: tentar toofix Olá código antes de continuar.
2. Erro de instalação/configuração: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System. UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Ação geral: examinar sua configuração e alterá-la, se necessário.
3. Exceções temporárias: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Ação geral: repita a operação de saudação ou notificar os usuários.
4. Outras exceções: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Ação geral: tipo de exceção específico toohello; Consulte toohello tabela Olá seção a seguir. 

## <a name="exception-types"></a>Tipos de exceção
Olá tabela a seguir lista tipos mensagens de exceção e suas causas e ação sugerida anotações, que você pode executar.

| **Tipo de exceção** | **Descrição/Causa/Exemplos** | **Ação sugerida** | **Observação sobre repetição automática/imediata** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Olá servidor não respondeu toohello solicitado operação dentro de saudação especificado tempo, o que é controlado pelo [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). servidor de saudação pode ter sido concluída Olá a operação solicitada. Isso pode acontecer devido a toonetwork ou outros atrasos de infraestrutura. |Estado do sistema Olá para manter a consistência e tente novamente se necessário.<br /> Veja [TimeoutException](#timeoutexception). |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Olá solicitou uma operação de usuário não é permitida no servidor de saudação ou serviço. Consulte a mensagem de exceção Olá para obter detalhes. Por exemplo, [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) gera esta exceção se a mensagem foi recebida no [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo. |Verifique o código hello e documentação de saudação. Certifique-se de saudação solicitou a operação é válida. |Tentar novamente não ajudará. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Uma tentativa for feita tooinvoke uma operação em um objeto que já foi fechado, cancelada ou descartada. Em casos raros, a transação de ambiente Olá já foi descartada. |Verifique o código de hello e verifique se que ele não invocar operações em um objeto descartado. |Tentar novamente não ajudará. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto não foi possível adquirir um token, Olá token é inválido ou Olá token não contém Olá declarações necessárias tooperform Olá operação. |Verifique se o provedor de token Olá é criado com valores corretos hello. Verifique a configuração de saudação do hello serviço de controle de acesso. |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Um ou mais método de toohello de argumentos fornecidos são inválidos. Olá URI fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contém o segmento de caminho (s). o esquema de URI Olá fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) é inválido. o valor da propriedade Olá é maior do que 32KB. |Verifique o código de chamada hello e certifique-se de argumentos Olá estão corretos. |Tentar novamente não ajudará. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entidade associada à operação de saudação não existe ou foi excluído. |Certifique-se de entidade Olá existe. |Tentar novamente não ajudará. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tentativa de tooreceive uma mensagem com um número de sequência específica. Esta mensagem não foi encontrada. |Verifique se a mensagem de saudação já não foi recebida. Se a mensagem de saudação foi morta, verifique Olá toosee de fila de mensagens mortas. |Tentar novamente não ajudará. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Cliente não é capaz de tooestablish tooEvent uma conexão Hub. |Verifique se o nome de host Olá fornecido está correto e Olá host esteja acessível. |Tentar novamente poderá ajudar se houver problemas intermitentes de conectividade. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Serviço não é capaz de tooprocess Olá solicitação no momento. |Cliente pode aguardar um período de tempo e repita a operação de saudação. <br /> Veja [ServerBusyException](#serverbusyexception). |O cliente pode tentar novamente após um intervalo determinado. Se uma nova tentativa resultar em uma exceção diferente, verifique o comportamento de repetição de tal exceção. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Símbolo de bloqueio associado a mensagem de saudação expirou ou token de bloqueio Olá não foi encontrado. |Descarte a mensagem de saudação. |Tentar novamente não ajudará. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |O bloqueio associado a esta sessão foi perdido. | Anular Olá [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objeto. |Tentar novamente não ajudará. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Genérico de mensagens de exceção que pode ser acionada em Olá casos a seguir: é feita uma tentativa toocreate um [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) usando um nome ou caminho ao qual pertence o tipo de entidade diferente tooa (por exemplo, um tópico). Uma tentativa for feita toosend uma mensagem maior do que 256KB. saudação de servidor ou serviço encontrou um erro durante o processamento da solicitação de saudação. Consulte a mensagem de exceção Olá para obter detalhes. Isso geralmente é uma exceção temporária. |Verifique o código de saudação e certifique-se de que apenas os objetos serializáveis são usados para o corpo da mensagem de saudação (ou usar um serializador personalizado). Consulte a documentação de saudação para tipos de valor de saudação com suporte das propriedades de saudação e somente os tipos de uso com suporte. Verificar Olá [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propriedade. Se for **true**, você poderá repetir a operação de saudação. |O comportamento de repetição é indefinido e pode não ajudar. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Tentativa de toocreate uma entidade com um nome que já está sendo usado por outra entidade no namespace de serviço. |Excluir entidade existente hello ou escolha um nome diferente para Olá entidade toobe criado. |Tentar novamente não ajudará. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |saudação de entidade de mensagens atingiu seu tamanho máximo permitido. Isso pode acontecer se Olá número máximo de receptores (que é 5) já foi aberto em um nível de grupo por consumidor. |Crie espaço na entidade Olá recebendo mensagens da entidade hello ou seus filas sub. <br /> See [QuotaExceededException](#quotaexceededexception) |Pode ajudar a repetição se as mensagens foram removidas do hello enquanto isso. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Tentativa de tooaccept que uma sessão com uma ID de sessão específica, mas a sessão hello está bloqueado por outro cliente. |Certifique-se de sessão Olá é desbloqueado por outros clientes. |Pode ajudar a repetição se sessão Olá foi lançado em Olá intermediários. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Muitas operações fazem parte da transação de saudação. |Reduza o número de saudação de operações que fazem parte dessa transação. |Tentar novamente não ajudará. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Solicitação para uma operação de tempo de execução em uma entidade desabilitada. |Ative entidade hello. |Pode ajudar a repetição se entidade Olá tiver sido ativada no hello intermediários. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Conteúdo de uma mensagem excede o limite de saudação 256K. Observe que o limite de 256K de Olá Olá tamanho total de mensagens, que pode incluir propriedades do sistema e qualquer sobrecarga de .NET. |Reduzir o tamanho de saudação da carga de mensagem de saudação e repita a operação de saudação. |Tentar novamente não ajudará. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Olá transação de ambiente (*Transaction*) é inválido. Ela pode ter sido concluída ou anulada. A exceção interna pode fornecer informações adicionais. | |Tentar novamente não ajudará. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Uma operação é tentada em uma transação que está em dúvida, ou uma tentativa de transação de saudação toocommit e transação Olá torna-se em dúvida. |Seu aplicativo deve tratar essa exceção (como um caso especial), como transações Olá podem ter sido confirmada. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que uma cota para uma entidade específica foi excedida.

Isso pode acontecer se o número máximo de saudação de destinatários (5) já foi aberto em um nível de grupo por consumidor.

### <a name="event-hubs"></a>Hubs de Eventos
Os Hubs de Eventos têm um limite de 20 grupos de consumidores por Hub de Eventos. Quando você tenta toocreate mais, você receberá um [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Um [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que uma operação iniciada pelo usuário está demorando mais que o tempo limite da operação hello. 

Para Hubs de eventos, tempo limite de saudação é especificado como parte da cadeia de caracteres de conexão hello, ou por meio de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensagem de erro de saudação em si pode variar, mas ele sempre contém o valor de tempo limite de saudação especificado para a operação atual de saudação. 

### <a name="common-causes"></a>Causas comuns
Há duas causas comuns desse erro: configuração incorreta ou um erro de serviço transitório.

1. **Configuração incorreta** Olá tempo limite da operação pode ser muito pequeno para a condição operacional hello. valor padrão Olá Olá tempo limite da operação no SDK do cliente Olá é 60 segundos. Verifique toosee se seu código tem valor Olá definida toosomething muito pequeno. Observe a condição da rede Olá Olá e uso da CPU pode afetar o tempo de saudação que leva para uma determinada operação toocomplete, para que o tempo limite da operação Olá não deve ser definido valor muito pequeno tooa.
2. **Erro de serviço transitória** Olá às vezes o serviço de Hubs de eventos pode enfrentar atrasos no processamento de solicitações, por exemplo, durante os períodos de tráfego intenso. Nesses casos, você poderá repetir a operação após um atraso até que a operação de saudação for bem-sucedida. Se hello mesma operação ainda falhar após várias tentativas, visite Olá [site de status do serviço do Azure](https://azure.microsoft.com/status/) toosee se houver quaisquer interrupções de serviço conhecido.

## <a name="serverbusyexception"></a>ServerBusyException

A [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) ou [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indica que um servidor está sobrecarregado. Há dois códigos de erro relevantes para essa exceção.

### <a name="error-code-50002"></a>Código do erro 50002

Esse erro pode ocorrer por um dos seguintes motivos:

1. carga de saudação não será distribuída igualmente entre todas as partições de saudação Hub de eventos e uma partição acertos Olá taxa de transferência local unidade limitação.
    
    Resolução: Revisar a estratégia de distribuição de partição hello ou tentar [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) pode ajudar.

2. namespace de Hubs de eventos de saudação não tem unidades de taxa de transferência suficiente (você pode verificar Olá **métricas** folha na folha de namespace de Hubs de eventos no hello [portal do Azure](https://portal.azure.com) tooconfirm). Observe que o portal Olá mostra informações agregadas (1 minuto), mas podemos medir a taxa de transferência de saudação em tempo real – portanto, é apenas uma estimativa.

    Resolução: Aumenta o processamento de saudação unidades no namespace Olá podem ajudar. Você pode fazer isso no portal de saudação em Olá **escala** folha da folha de namespace Olá Hubs de eventos.

### <a name="error-code-50001"></a>Código do erro 50001

Esse erro deve ocorrer raramente. Isso acontece quando o contêiner Olá executando o código para o namespace está com pouca CPU – carregar de Hubs de eventos não mais do que alguns segundos antes de saudação balanceador começa.


## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)
