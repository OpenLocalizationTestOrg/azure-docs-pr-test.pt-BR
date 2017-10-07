---
title: Perguntas frequentes sobre Hubs de evento de aaaAzure | Microsoft Docs
description: Perguntas frequentes (FAQs) sobre os Hubs de Eventos do Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Perguntas frequentes sobre os Hubs de Eventos

## <a name="general"></a>Geral

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Qual é a diferença de saudação entre camadas padrão e Hubs de eventos Basic?

a camada padrão Olá de Hubs de eventos do Azure fornece recursos além do que está disponível na camada básica hello. Olá recursos a seguir está incluído com o padrão:
* Maior retenção de evento
* Conexões orientadas adicionais, com uma taxa excedente mais de número Olá incluído
* Mais de um único Grupo de consumidores
* [Captura](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Para obter mais informações sobre os preços de camadas, incluindo dedicado de Hubs de evento, consulte Olá [detalhes de preços de Hubs de eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>O que são unidades de produtividade dos Hubs de Eventos?

Você selecionar unidades de taxa de transferência de Hubs de eventos, por meio do portal do Azure de saudação ou modelos do Gerenciador de recursos de Hubs de eventos. Unidades de taxa de transferência aplicam tooall hubs de eventos em um namespace de Hubs de eventos, e cada unidade de taxa de transferência permite Olá namespace toohello recursos a seguir:

* Too1 MB por segundo de eventos de entrada (eventos enviados para um hub de eventos), mas não há mais de 1000 eventos de entrada, operações de gerenciamento ou controle de chamadas de API por segundo.
* Too2 MB por segundo de eventos de saída (eventos consumidos a partir de um hub de eventos).
* A too84 GB de armazenamento de eventos (suficiente para o período de retenção de 24 horas da saudação).

Unidades de taxa de transferência dos Hubs de eventos são cobradas por hora, com base no número máximo de saudação de unidades selecionadas durante a saudação fornecida hora.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Como os limites de unidades de produtividade dos Hubs de Eventos são aplicados?
Se taxa de transferência de entrada total Olá ou a taxa de eventos de entrada total Olá em todos os hubs de eventos em um namespace exceder provisões para unidade de taxa de transferência agregada Olá, os remetentes são limitados e receberão erros indicando que cota de entrada hello foi excedida.

Se taxa de transferência de saída total hello ou a taxa de saída Olá total de eventos em todos os hubs de evento em um namespace exceder provisões para unidade de taxa de transferência agregada hello, receptores são limitados e receberão erros indicando a que cota de saída que Olá foi excedida. Cotas de entrada e saída são aplicadas separadamente para que nenhum remetente pode causar tooslow de consumo de eventos para baixo, nem um destinatário pode evitar eventos sejam enviadas em um hub de eventos.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>Há um limite no número de saudação de unidades de taxa de transferência que podem ser selecionadas?
Há uma cota padrão de 20 unidades de produtividade por namespace. Você pode solicitar uma cota maior de unidades de produtividade preenchendo um tíquete de suporte. Além do limite de unidade 20 de taxa de transferência hello, os pacotes estão disponíveis em unidades de taxa de transferência de 20 e 100. Observe que o uso de mais de 20 unidades de taxa de transferência remove Olá capacidade toochange Olá inúmeros unidades de taxa de transferência sem um tíquete de suporte de arquivamento.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>É possível usar um único toosend de conexão AMQP e receber vários dos hubs de eventos?
Sim, contanto que todos os hubs de evento Olá estão em Olá mesmo namespace.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>O que é o período de retenção máximo de saudação de eventos?
O nível Standard dos Hubs de Eventos atualmente dão suporte a um período de retenção máximo de 7 dias. Observe que os Hubs de Eventos não são destinados a funcionarem como um armazenamento de dados permanente. Períodos de retenção superiores a 24 horas destinam-se para cenários em que é conveniente tooreplay um evento de fluxo em Olá mesmos sistemas; Por exemplo, tootrain ou verificar um novo modelo de aprendizado de máquina nos dados existentes. Se você precisa de mensagem de retenção além de 7 dias, habilitando [Hubs de evento captura](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) em seu evento hub extrai dados de saudação da sua conta de armazenamento do toohello de hub de eventos ou a conta de serviço do Azure Data Lake de sua escolha. A habilitação da Captura incorrerá em uma cobrança de acordo com a Unidade de Produtividade adquirida.

### <a name="where-is-azure-event-hubs-available"></a>Onde os Hubs de Eventos do Azure estão disponíveis?
Os Hubs de Eventos do Azure está disponível em todas as regiões do Azure com suporte. Para obter uma lista, visite Olá [regiões do Azure](https://azure.microsoft.com/regions/) página.  

## <a name="best-practices"></a>Práticas recomendadas

### <a name="how-many-partitions-do-i-need"></a>De quantas partições preciso?
Por favor, tenha em mente que Olá contagem de partições em um hub de eventos não pode ser modificada após a instalação. Com isso em mente, é importante toothink sobre quantas partições você precisa antes de começar. 

Hubs de eventos é projetado tooallow leitor uma única partição por grupo de consumidores. Na maioria dos casos de uso, a configuração padrão de saudação quatro partições é suficiente. Se você estiver procurando tooscale o processamento de eventos, convém tooconsider adicionando partições adicionais. Não há nenhum limite de taxa de transferência específico em uma partição, mas a taxa de transferência agregada no seu namespace Olá é limitada pelo número de saudação de unidades de taxa de transferência. Conforme você aumenta o número de saudação de unidades de taxa de transferência no seu namespace, talvez você queira partições adicionais tooallow leitores simultâneos tooachieve seu próprios taxa de transferência máxima.

No entanto, se você tiver um modelo no qual seu aplicativo tem uma partição específica de tooa de afinidade, aumentar o número de saudação de partições pode não ser tooyou qualquer benefício. Para obter mais informações sobre isso, consulte [disponibilidade e consistência](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Preços

### <a name="where-can-i-find-more-pricing-information"></a>Onde posso encontrar mais informações sobre preços?
Para obter informações completas sobre os preços de Hubs de eventos, consulte Olá [detalhes de preços de Hubs de eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>Há um custo para a retenção de eventos de Hubs de Eventos por mais de 24 horas?
camada Standard de Hubs de eventos Olá permitir retenção de mensagem períodos mais de 24 horas, para um máximo de 7 dias. Se o tamanho de saudação do número total de saudação de eventos armazenados exceder o limite de armazenamento Olá para número de saudação de unidades de taxa de transferência selecionadas (84 GB por unidade de taxa de transferência), tamanho de saudação que excede o limite de saudação é cobrado nos Olá publicado taxa de armazenamento de BLOBs do Azure. limite de armazenamento de saudação em cada unidade de taxa de transferência abrange todos os custos de armazenamento para períodos de retenção de 24 horas (saudação padrão) mesmo se a unidade de taxa de transferência de saudação seja usada até o limite máximo de entrada de toohello.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Como os Olá tamanho de armazenamento de Hubs de eventos é calculado e cobrado?
tamanho total de saudação de todos os eventos armazenados, incluindo eventuais sobrecargas internas para cabeçalhos de eventos ou estruturas de armazenamento de disco em todos os hubs de eventos, é medido durante o dia de saudação. No final de saudação do dia hello, tamanho do armazenamento de pico de saudação é calculado. o limite de armazenamento diário Olá é calculado com base no número mínimo de saudação de unidades de taxa de transferência que foram selecionados durante o dia de saudação (cada unidade de taxa de transferência fornece um limite de 84 GB). Se excede o tamanho total Olá Olá calculado diariamente. limite de armazenamento, armazenamento em excesso Olá é cobrado usando as taxas de armazenamento de BLOBs do Azure (em Olá **armazenamento localmente redundante** taxa).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Como os eventos de entrada de Hubs de Eventos são calculados?
Cada evento enviado hub de eventos tooan contará como uma mensagem faturável. Um *eventos de entrada* é definido como uma unidade de dados é menor ou igual too64 KB. Qualquer evento que é menor ou igual a too64 KB de tamanho é considerado toobe um evento faturável. Se o evento Olá for maior que 64 KB, o número de saudação de eventos faturáveis é calculado de acordo com o tamanho do evento toohello, em múltiplos de 64 KB. Por exemplo, um evento de 8 KB enviado toohello hub de eventos é cobrado como um evento, mas uma mensagem de 96 KB enviada toohello hub de eventos é cobrada como dois eventos.

Eventos consumidos a partir de um hub de eventos, bem como as operações de gerenciamento e chamadas de controle, como pontos de verificação, não são contados como eventos de entrada faturáveis, mas se acumulam o limite de unidade de taxa de transferência toohello.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Encargos de conexão orientadas se aplicam a Hubs tooEvent?
Encargos de Conexão se aplicam somente quando Olá protocolo AMQP é usado. Não há nenhum encargos de conexão para enviar eventos usando HTTP, independentemente do número de saudação do envio de sistemas ou dispositivos. Se você planejar toouse AMQP (por exemplo, tooachieve mais eficiente eventos streaming ou tooenable a comunicação bidirecional em cenários de comando e controle de IoT), consulte Olá [informações sobre preços de Hubs de eventos](https://azure.microsoft.com/pricing/details/event-hubs/) página para obter detalhes sobre como número de conexões é incluído em cada camada de serviço.

### <a name="how-is-event-hubs-capture-billed"></a>Como a Captura de Hubs de Eventos é cobrada?
Captura é habilitada quando qualquer hub de eventos no namespace Olá tem a opção de captura Olá habilitada. A Captura de Hubs de Eventos é cobrada por hora de acordo com a Unidade de Produtividade comprada. Como Olá contagem de unidades de taxa de transferência está aumentando ou diminuindo, Hubs de evento captura cobrança reflete essas alterações em incrementos de hora inteira. Para obter mais informações sobre a cobrança da Captura de Hubs de Eventos, confira [informações de preços de Hubs de Eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>Será eu cobrado por conta de armazenamento Olá que selecionar para Hubs de evento captura?
A Captura usa uma conta de armazenamento fornecida quando habilitado em um Hub de Eventos. Como esta é sua conta de armazenamento, as alterações para essa configuração são cobrada tooyour assinatura do Azure.

## <a name="quotas"></a>Cotas

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Existe alguma cota associada aos Hubs de Eventos?
Para obter uma lista de todas as cotas de Hubs de Eventos, consulte [cotas](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>O que são exceções Olá geradas por Hubs de eventos e suas ações sugeridas?
Para obter uma lista de exceções possíveis dos Hubs de Eventos, confira [Visão geral das exceções](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Logs de diagnóstico
Hubs de evento oferece suporte a dois tipos de [logs de diagnóstico](event-hubs-diagnostic-logs.md) -logs de erros de captura e logs operacionais - que são representados em json e podem ser ativados por meio de Olá portal do Azure.

### <a name="support-and-sla"></a>Suporte e SLA
O suporte técnico para Hubs de eventos está disponível por meio de saudação [fóruns da comunidade](https://social.msdn.microsoft.com/forums/azure/home). O suporte para gerenciamento de assinaturas e cobranças é fornecido sem custo adicional.

toolearn mais sobre nosso SLA, consulte Olá [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/) página.

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
