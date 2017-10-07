---
title: "exceções de retransmissão aaaAzure e como tooresolve-los | Microsoft Docs"
description: "Obter uma lista de exceções de retransmissão do Azure e ações sugeridas, você pode tomar toohelp resolvê-los."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Exceções de Retransmissão do Azure

Este artigo lista algumas exceções que podem ser geradas por Olá APIs de retransmissão do Azure. Essa referência é toochange de assunto, portanto, verifique as atualizações.

## <a name="exception-categories"></a>Categorias de exceções

Olá retransmissão APIs geram exceções que podem entrar Olá categorias a seguir. Ações sugeridas que você pode seguir toohelp resolva exceções Olá estão listadas também.

*   **Erro de codificação do usuário**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Ação geral**: tente toofix código de saudação antes de continuar.
*   **Erro de instalação/configuração**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Ação geral**: examine sua configuração. Se necessário, altere a configuração de saudação.
*   **Exceções temporárias**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Ação geral**: repita a operação de saudação ou notificar os usuários.
*   **Outras exceções**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Ação geral**: tipo de exceção toohello específico. Consulte a tabela Olá Olá seção a seguir. 

## <a name="exception-types"></a>Tipos de exceção

Olá tabela a seguir lista os tipos de exceção mensagens e suas causas. Ele também observa sugeridas ações toohelp resolva exceções hello.

| **Tipo de exceção** | **Descrição** | **Ação sugerida** | **Observação sobre repetição automática ou imediata** |
| --- | --- | --- | --- |
| [Tempo limite](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Olá servidor não respondeu toohello solicitado operação dentro de saudação especificado tempo, o que é controlado pelo [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Olá servidor pode ter concluído Olá operação solicitada. Isso pode acontecer devido a toonetwork ou outros atrasos de infraestrutura. |Verifique o estado do sistema Olá para manter a consistência e, em seguida, tentar novamente, se necessário. Veja [TimeoutException](#timeoutexception). |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [Operação inválida](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Olá solicitou uma operação de usuário não é permitida no servidor de saudação ou serviço. Consulte a mensagem de exceção Olá para obter detalhes. |Verifique o código hello e documentação de saudação. Certifique-se de que Olá solicitou a operação é válida. |Tentar novamente não ajudará. |
| [Operação cancelada](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Uma tentativa for feita tooinvoke uma operação em um objeto que já foi fechado, anulada ou descartado. Em casos raros, a transação de ambiente Olá já foi descartada. |Verifique o código de hello e verifique se que ele não invocar operações em um objeto descartado. |Tentar novamente não ajudará. |
| [Acesso não autorizado](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto não foi possível adquirir um token, Olá token é inválido ou Olá token não contém Olá declarações necessárias tooperform Olá operação. |Verifique se que esse provedor de token Olá é criado com valores corretos hello. Verifique a configuração de saudação do hello serviço de controle de acesso. |Repetição pode ajudar em alguns casos. Adicione toocode de lógica de repetição. |
| [Exceção de Argumento](https://msdn.microsoft.com/library/system.argumentexception.aspx),<br /> [Argumento Nulo](https://msdn.microsoft.com/library/system.argumentnullexception.aspx),<br />[Argumento fora do intervalo](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Um ou mais dos seguintes Olá ocorreu:<br />Um ou mais método de toohello de argumentos fornecidos são inválidos.<br /> Olá URI fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) contém um ou mais segmentos de caminho.<br />o esquema de URI Olá fornecido muito[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [criar](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) é inválido. <br />o valor da propriedade Olá é maior do que 32 KB. |Verifique o código de chamada hello e certifique-se de argumentos Olá estão corretos. |Tentar novamente não ajudará. |
| [Servidor ocupado](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Serviço não é capaz de tooprocess Olá solicitação no momento. |cliente Olá pode aguardar um período de tempo e repita a operação de saudação. |Olá cliente pode novamente após um intervalo específico. Se um resultados da repetição em uma exceção diferente, verifique o comportamento de repetição de saudação dessa exceção. |
| [Cota excedida](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |saudação de entidade de mensagens atingiu seu tamanho máximo permitido. |Crie espaço na entidade Olá recebendo mensagens da entidade hello ou seus subfilas. Confira [QuotaExceededException](#quotaexceededexception). |Pode ajudar a repetição se as mensagens foram removidas do hello enquanto isso. |
| [Tamanho da mensagem excedido](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Conteúdo de uma mensagem excede o limite de 256 KB de saudação. Observe que limite de 256 KB Olá Olá tamanho total de mensagens. Olá tamanho total de mensagens pode incluir propriedades do sistema e qualquer sobrecarga de Microsoft .NET. |Reduzir o tamanho de saudação da carga de mensagem de saudação e repita a operação de saudação. |Tentar novamente não ajudará. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que uma cota para uma entidade específica foi excedida.

Para retransmissão, essa exceção encapsula Olá [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), que indica o número máximo Olá de ouvintes foi excedido para este ponto de extremidade. Isso é indicado na Olá **MaximumListenersPerEndpoint** valor de mensagem de exceção de saudação.

## <a name="timeoutexception"></a>TimeoutException
Um [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que uma operação iniciada pelo usuário está demorando mais que o tempo limite da operação hello. 

Verifique o valor Olá Olá [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) propriedade. Atingir esse limite também pode causar uma [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Para a Retransmissão, você poderá receber exceções de tempo limite ao abrir pela primeira vez uma conexão de remetente de retransmissão. Há duas causas comuns para essa exceção:

*   Olá [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valor pode ser muito pequeno (se até mesmo em uma fração de segundo).
* Um ouvinte de retransmissão local pode ficar sem resposta (ou ele pode encontrar problemas de regras de firewall que proíbem ouvintes de aceitar novas conexões de cliente) e hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valor é menor que cerca de 20 segundos.

Exemplo:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Causas comuns
Há duas causas comuns para esse erro:

*   **Configuração incorreta**
    
    tempo limite da operação Olá pode ser muito pequeno para a condição operacional hello. valor padrão Olá Olá tempo limite da operação no SDK do cliente Olá é 60 segundos. Verifique toosee se o valor de saudação em seu código é definido toosomething muito pequeno. Observe que condição hello e uso de CPU da rede Olá pode afetar Olá tempo de uma operação toocomplete. É uma boa ideia não tooset Olá operação timeout tooa valor muito pequeno.
*   **Erro de serviço transitório**

    Ocasionalmente, Olá serviço de retransmissão pode enfrentar atrasos no processamento de solicitações. Isso pode acontecer, por exemplo, durante períodos de tráfego intenso. Se isso ocorrer, repita a operação após um atraso até que a operação de saudação for bem-sucedida. Se hello mesma operação continua toofail após várias tentativas, verifique Olá [site de status do serviço do Azure](https://azure.microsoft.com/status/) toosee se há interrupções no serviço conhecidos.

## <a name="next-steps"></a>Próximas etapas
* [Perguntas frequentes sobre Retransmissão do Azure](relay-faq.md)
* [Criar um namespace de retransmissão](relay-create-namespace-portal.md)
* [Introdução à Retransmissão do Azure e .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução à Retransmissão do Azure e Nó](relay-hybrid-connections-node-get-started.md)

