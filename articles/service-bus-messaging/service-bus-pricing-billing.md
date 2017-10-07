---
title: "preços e faturamento do barramento do aaaService | Microsoft Docs"
description: "Visão geral da estrutura de preços de Barramento de Serviço."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Barramento de Serviço, preços e cobrança
O Barramento de Serviço é oferecido nas camadas Basic, Standard e [Premium](service-bus-premium-messaging.md). É possível escolher uma camada de serviço para cada namespace de serviço do Barramento de Serviço criado por você, e essa seleção de camada aplica-se a todas as entidades criadas dentro desse namespace.

> [!NOTE]
> Para obter informações detalhadas sobre os preços de barramento de serviço atual, consulte Olá [página de preços do Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)e hello [perguntas frequentes sobre o barramento de serviço](service-bus-faq.md#pricing).
>
>

Barramento de serviço usa Olá dois medidores para filas e tópicos/assinaturas a seguir:

1. **Operações de sistema de mensagens**: definido como chamadas à API em pontos de extremidade de serviço de fila ou tópico/assinatura. Esse medidor substituirá as mensagens enviadas ou recebidas como a unidade principal Olá de uso faturável para filas e tópicos/assinaturas.
2. **Conexões agenciadas**: definido como o número máximo de saudação de conexões persistentes abertas em relação a filas, tópicos ou assinaturas durante um período de amostragem de uma hora fornecida. Esse medidor será aplicado apenas na camada padrão do hello, no qual você pode abrir conexões adicionais (anteriormente, as conexões eram too100 limitado por fila/tópico/assinatura) para uma taxa nominal por conexão.

Olá **padrão** camada introduz níveis de preços para operações realizadas com filas e tópicos/assinaturas, resultando em descontos com base no volume de % too80 em níveis mais altos de uso hello. Também há uma taxa básica de camada padrão de US $10 por mês, que permite que você tooperform backup too12.5 milhão de operações por mês sem custo adicional.

Olá **Premium** camada fornece isolamento de recursos na camada de CPU e memória Olá para que cada carga de trabalho do cliente é executada em isolamento. Esse contêiner de recurso é chamado de *unidade do sistema de mensagens*. Cada namespace premium é alocado para pelo menos uma unidade do sistema de mensagens. Você pode adquirir 1, 2 ou 4 unidades do sistema de mensagens para cada namespace Premium do Barramento de serviço. Uma única carga de trabalho ou uma entidade pode abranger várias unidades de sistema de mensagens e número de saudação de unidades de sistema de mensagens pode ser alterado conforme o desejado, embora a cobrança é em encargos de taxa de 24 horas ou diária. resultado de saudação é desempenho previsível e reproduzível para sua solução com base no barramento de serviço. Esse desempenho não é apenas o mais previsível e disponível, mas também o mais rápido.

Observe que a taxa básica de camada padrão Olá é cobrada apenas uma vez por mês por assinatura do Azure. Isso significa que, depois de criar um namespace de barramento de serviço de nível único padrão, será possível toocreate quantos namespaces padrão adicionais que você desejar na mesma assinatura do Azure, sem incorrer em adicionais encargos de base.

Olá [preços de barramento de serviço](https://azure.microsoft.com/pricing/details/service-bus/) tabela resume as diferenças funcionais da saudação entre as camadas Basic, Standard e Premium Olá.

## <a name="messaging-operations"></a>Operações de sistema de mensagens
Como parte do novo modelo de preços de hello, cobrança por filas e tópicos/assinaturas está mudando. Essas entidades são mais por mensagem toobilling por operação. Uma "operação" refere-se a chamada de tooany API feita em relação a um ponto de extremidade de serviço fila ou tópico/assinatura. Isso inclui operações de gerenciamento, envio/recebimento e estado da sessão.

| Tipo de operação | Descrição |
| --- | --- |
| Gerenciamento |Criar, ler, atualizar, excluir (CRUD) em relação a filas ou tópicos/assinaturas. |
| Mensagens |Enviando e recebendo mensagens com filas ou tópicos/assinaturas. |
| Estado de sessão |Obter ou definir o estado de sessão em uma fila ou tópico/assinatura. |

Para obter detalhes de custo, consulte preços Olá listados em Olá [preços de barramento de serviço](https://azure.microsoft.com/pricing/details/service-bus/) página.

## <a name="brokered-connections"></a>Conexões orientadas
*Conexões agenciadas* acomodam padrões de uso do cliente que envolvem um grande número de remetentes/destinatários “persistentemente conectados” em filas, tópicos ou assinaturas. Remetentes/destinatários persistentemente conectados são aqueles que se conectam com AMQP ou HTTP diferente com tempo limite de recebimento diferente de zero (por exemplo, sondagem longa de HTTP). Remetentes e receptores HTTP com um tempo limite imediato não geram conexões orientadas.

Para cotas de conexão e outros limites de serviço, consulte Olá [cotas de barramento de serviço](service-bus-quotas.md) artigo.

camada padrão Olá remove o limite de conexão orientadas por namespace hello e contagens de uso de agregação conexão orientadas por Olá assinatura do Azure. Para obter mais informações, consulte Olá [conexões Agenciadas](https://azure.microsoft.com/pricing/details/service-bus/) tabela.

> [!NOTE]
> 1000 conexões agenciadas são incluídos com a camada de mensagens padrão hello (por meio de taxa básica de saudação) e podem ser compartilhados entre todas as filas, tópicos e assinaturas de assinatura do Azure Olá associado.
>
>

<br />

> [!NOTE]
> A cobrança é baseada no número de pico de saudação de conexões simultâneas e é dividida Pro hora com base nas 744 horas por mês.
>
>

| Camada Premium |
| --- |
| Conexões agenciadas não serão cobrados na camada de Premium Olá. |

Para obter mais informações sobre conexões agenciadas, consulte Olá [perguntas frequentes sobre](#faq) seção mais adiante neste tópico.

## <a name="faq"></a>Perguntas frequentes

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>O que são conexões orientadas e como serei cobrado para elas?
Uma conexão agenciada é definido como um dos seguintes hello:

1. Uma conexão AMQP de uma fila do barramento de serviço do cliente tooa ou tópico/assinatura.
2. Uma chamada HTTP tooreceive uma mensagem de uma fila que tem um valor de tempo limite de recebimento maior que zero ou um tópico do barramento de serviço.

Encargos de barramento de serviço para o número de pico de saudação de conexões agenciadas simultâneas que excedem a saudação incluídos quantidade (1000 na camada padrão Olá). Picos são medidos por hora, divididos pelas 744 horas em um mês e acrescentados ao período de cobrança mensal de saudação. Quantidade Olá incluída (1000 conexões agenciadas por mês) é aplicada no final de saudação do período de cobrança Olá em relação a soma de saudação do hello rateado picos de hora em hora.

Por exemplo:

1. Cada um dos 10.000 dispositivos se conecta por meio de uma única conexão AMQP e recebe comandos de um tópico do Barramento de Serviço. Olá dispositivos as enviam eventos de telemetria tooan Hub de eventos. Se todos os dispositivos se conectarem 12 horas por dia, Olá encargos de conexão a seguir se aplicam (em adição tooany outras cobranças de tópico do barramento de serviço): 10.000 conexões * 12 horas * 31 dias / 744 = 5000 conexões agenciadas. Após a provisão mensal de saudação de 1000 conexões agenciadas, você será cobrado por 4000 conexões agenciadas, a taxa de saudação de US $0,03 por conexão agenciada, totalizando US $120.
2. 10.000 dispositivos recebem mensagens de uma fila do Barramento de Serviço por meio de HTTP, especificando um tempo limite diferente de zero. Se todos os dispositivos se conectarem 12 horas por dia, você verá Olá encargos de conexão a seguir (em adição tooany outros encargos de barramento de serviço): 10.000 conexões HTTP receber * 12 horas por dia * 31 dias / 744 horas = 5000 conexões agenciadas.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Encargos de conexão orientadas são aplicáveis tooqueues e tópicos/assinaturas?
Sim. Não há nenhum encargos de conexão para enviar eventos usando HTTP, independentemente do número de saudação do envio de sistemas ou dispositivos. O recebimento de eventos com HTTP usando um tempo limite maior que zero, às vezes chamado de "sondagem longa", gera encargos de conexão gerenciada. As conexões AMQP geram cobranças de conexão orientadas independentemente conexões Olá estão sendo usado toosend ou receberam. Observe que são permitidas 100 conexões orientadas gratuitamente em um namespace da camada Basic. Também, este é o número máximo de saudação de conexões agenciadas permitidas para Olá assinatura do Azure. Olá a primeiro 1000 conexões agenciadas em todos os namespaces padrão em uma assinatura do Azure são incluídas sem custo adicional (além da taxa básica de saudação). Como essas provisões são suficientes toocover muitos serviços para cenários de mensagens, geralmente encargos de conexão orientadas somente ficarão relevantes se você planejar toouse AMQP ou HTTP sondagem longa com um grande número de clientes. Por exemplo, tooachieve mais eficiente eventos streaming ou habilitar comunicação bidirecional com muitos dispositivos ou instâncias do aplicativo.

## <a name="next-steps"></a>Próximas etapas
* Para obter detalhes completos sobre preços de barramento de serviço, consulte Olá [página de preços de barramento de serviço](https://azure.microsoft.com/pricing/details/service-bus/).
* Consulte Olá [perguntas frequentes sobre o barramento de serviço](service-bus-faq.md#pricing) para alguns frequentes sobre preços e faturamento do barramento do serviço.

[Azure portal]: https://portal.azure.com
