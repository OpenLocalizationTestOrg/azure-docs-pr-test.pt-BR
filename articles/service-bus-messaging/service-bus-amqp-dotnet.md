---
title: aaaService Bus com o .NET e AMQP 1.0 | Microsoft Docs
description: "Usando o Barramento de Serviço do Azure no .NET com AMQP"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Usando o Barramento de Serviço do .NET com AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Baixando Olá SDK do barramento de serviço

Suporte a AMQP 1.0 está disponível no hello SDK do barramento de serviço versão 2.1 ou posterior. Você pode garantir que você tem a versão mais recente do hello baixando os bits de barramento de serviço de saudação do [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Configurando toouse de aplicativos .NET AMQP 1.0

Por padrão, a biblioteca de cliente .NET do barramento de serviço Olá se comunica com hello usando um protocolo de dedicado baseado em SOAP do barramento de serviço do serviço. toouse AMQP 1.0 em vez de protocolo de padrão de saudação requer configuração explícita na cadeia de conexão do barramento de serviço hello, conforme descrito na próxima seção, Olá. Além dessa alteração, o código do aplicativo permanece inalterado ao usar o AMQP 1.0.

Na versão atual do hello, há alguns recursos da API que não são suportados ao usar o AMQP. Esses recursos não suportados são listados posteriormente na seção de saudação [sem suporte a recursos, restrições e diferenças de comportamento](#unsupported-features-restrictions-and-behavioral-differences). Algumas das configurações avançada de saudação também têm um significado diferente ao usar o AMQP.

### <a name="configuration-using-appconfig"></a>Configuração usando App.config

É uma boa prática para aplicativos toouse Olá App. config arquivo toostore de configuração. Para aplicativos do barramento de serviço, você pode usar a cadeia de conexão do App. config toostore Olá barramento de serviço. Um exemplo do arquivo App.config é mostrado abaixo:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Olá valor Olá `Microsoft.ServiceBus.ConnectionString` configuração é a cadeia de conexão do barramento de serviço Olá é usado tooconfigure Olá conexão tooService barramento. formato de saudação é o seguinte:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Onde `[namespace]` e `SharedAccessKey` são obtidos do hello [portal do Azure] [ Azure portal] quando você cria um namespace de barramento de serviço. Para obter mais informações, consulte [criar um namespace de barramento de serviço usando o portal do Azure de saudação][Create a Service Bus namespace using hello Azure portal].

Ao usar AMQP, acrescente a cadeia de caracteres de conexão de saudação com `;TransportType=Amqp`. Esta notação instrui toomake de biblioteca de cliente Olá tooService sua conexão barramento usando AMQP 1.0.

## <a name="message-serialization"></a>Serialização de mensagem

Ao usar o protocolo padrão de saudação, comportamento de serialização saudação padrão da biblioteca de cliente .NET Olá é Olá toouse [DataContractSerializer] [ DataContractSerializer] digite tooserialize um [BrokeredMessage ] [ BrokeredMessage] instância para transporte entre a biblioteca de saudação do cliente e o serviço de barramento de serviço do hello. Ao usar o modo de transporte do AMQP Olá, biblioteca de saudação do cliente usa o sistema de tipos do AMQP Olá para a serialização de saudação [mensagens orientadas] [ BrokeredMessage] em uma mensagem do AMQP. Essa serialização permite Olá mensagem toobe recebida e interpretada por um aplicativo que provavelmente esteja em execução em uma plataforma diferente, por exemplo, um aplicativo Java que usa Olá API JMS tooaccess barramento de serviço.

Quando você cria um [BrokeredMessage] [ BrokeredMessage] instância, você pode fornecer um objeto .NET como um tooserve de construtor do parâmetro toohello como corpo da saudação de mensagem de saudação. Para objetos que podem ser mapeadas tooAMQP os tipos primitivos, corpo Olá é serializado em tipos de dados do AMQP. Se o objeto de saudação não pode ser mapeado diretamente em um tipo primitivo do AMQP ou seja, um tipo personalizado definido pelo aplicativo hello e, em seguida, objeto Olá é serializado usando Olá [DataContractSerializer][DataContractSerializer], e Olá serializado bytes são enviados em uma mensagem de dados do AMQP.

interoperabilidade de toofacilitate com clientes não .NET, use somente tipos .NET que podem ser serializados diretamente em tipos do AMQP para o corpo de saudação de mensagem de saudação. Olá a tabela a seguir fornece detalhes sobre os tipos e Olá correspondente mapeamento toohello AMQP sistema de tipo.

| Tipo de objeto de corpo .NET | Tipo do AMQP mapeado | Tipo de seção de corpo do AMQP |
| --- | --- | --- |
| bool |Booliano |Valor do AMQP |
| byte |ubyte |Valor do AMQP |
| ushort |ushort |Valor do AMQP |
| uint |uint |Valor do AMQP |
| ulong |ulong |Valor do AMQP |
| sbyte |byte |Valor do AMQP |
| short |short |Valor do AMQP |
| int |int |Valor do AMQP |
| longo |longo |Valor do AMQP |
| flutuante |flutuante |Valor do AMQP |
| double |double |Valor do AMQP |
| decimal |decimal128 |Valor do AMQP |
| char |char |Valor do AMQP |
| DateTime |timestamp |Valor do AMQP |
| Guid |uuid |Valor do AMQP |
| byte[] |binário |Valor do AMQP |
| string |string |Valor do AMQP |
| System.Collections.IList |list |Valor do AMQP: itens contidos na coleção de saudação só podem ser aqueles definidos nesta tabela. |
| System.Array |array |Valor do AMQP: itens contidos na coleção de saudação só podem ser aqueles definidos nesta tabela. |
| System.Collections.IDictionary |map |Valor do AMQP: itens contidos na coleção de saudação só podem ser aqueles definidos nesta tabela. Observação: somente as chaves de cadeia de caracteres têm suporte. |
| Uri |Descritas a cadeia de caracteres (consulte Olá a tabela a seguir) |Valor do AMQP |
| Datetimeoffset |Longo descrito (consulte Olá a tabela a seguir) |Valor do AMQP |
| TimeSpan |Longo descrito (veja a seguir Olá) |Valor do AMQP |
| Fluxo |binário |Dados do AMQP (podem ser múltiplos). as seções de dados de saudação contêm bytes brutos do hello lidos do objeto de fluxo de saudação. |
| Outro Objeto |binário |Dados do AMQP (podem ser múltiplos). Contém o binário Olá serializado do objeto Olá que usa Olá DataContractSerializer ou um serializador fornecido pelo aplicativo hello. |

| Tipo .NET | Tipo descrito do AMQP mapeado | Observações |
| --- | --- | --- |
| Uri |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |URI.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Recursos sem suporte, restrições e diferenças de comportamento

Olá recursos do hello API .NET do barramento de serviço a seguir não é suportado atualmente ao usar o AMQP:

* Transações
* Enviar por meio de destino da transferência

Também há algumas pequenas diferenças no comportamento de saudação do hello API .NET do barramento de serviço ao usar AMQP, toohello em comparação com o protocolo de padrão:

* Olá [OperationTimeout] [ OperationTimeout] propriedade será ignorada.
* `MessageReceiver.Receive(TimeSpan.Zero)` é implementado como `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Concluindo a mensagens com tokens de bloqueio pode ser feita apenas por receptores de mensagens de saudação que inicialmente receberam mensagens de saudação.

## <a name="controlling-amqp-protocol-settings"></a>Controlando configurações do protocolo AMQP

Olá [APIs .NET](/dotnet/api/) expor várias configurações toocontrol Olá comportamento de saudação protocolo AMQP:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: controles Olá crédito inicial aplicado tooa link. saudação padrão é 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: controles Olá tamanho máximo do AMQP quadro oferecido durante a negociação de saudação em tempo de abertura da conexão. padrão de saudação é 65.536 bytes.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: se transferências batchable, esse valor determina o atraso máximo de saudação para envio de disposições. Herdado pelos remetentes/destinatários por padrão. Remetente/destinatário individual pode substituir o padrão de saudação, que é 20 milissegundos.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: controla se as conexões do AMQP são estabelecidas por uma conexão SSL. saudação padrão é **true**.

## <a name="next-steps"></a>Próximas etapas

Pronto toolearn mais? Visite Olá links a seguir:

* [Visão geral do Barramento de Serviço para AMQP]
* [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]
* [AMQP no Barramento de Serviço para Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Visão geral do Barramento de Serviço para AMQP]: service-bus-amqp-overview.md
[Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP no Barramento de Serviço para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
