---
title: aaaScheduler alta disponibilidade e confiabilidade
description: Alta disponibilidade e confiabilidade do Agendador
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a>Alta disponibilidade e confiabilidade do Agendador
## <a name="azure-scheduler-high-availability"></a>Alta disponibilidade do Agendador do Azure
Como um núcleo de serviços da plataforma Azure, o Agendador do Azure é altamente disponível e possui implantação do serviço de redundância geográfica e replicação geográfica regional do trabalho.

### <a name="geo-redundant-service-deployment"></a>Implantação de serviço com redundância geográfica
O Agendador do Azure está disponível por meio de saudação da interface do usuário em quase todas as regiões geográficas que estão atualmente no Azure. Olá lista de regiões em que o Agendador do Azure está disponível no é [listados aqui](https://azure.microsoft.com/regions/#services). Se um data center em uma região hospedada fique indisponível, os recursos de failover de saudação do Agendador do Azure são que o serviço de saudação esteja disponível em outro data center.

### <a name="geo-regional-job-replication"></a>Replicação geográfica regional de trabalho
Não só é Olá front-end de disponível para solicitações de gerenciamento, mas seu trabalho também é replicado geograficamente o Agendador do Azure. Quando houver uma interrupção em uma região, o Agendador do Azure faz failover e garante que trabalho Olá seja executado em outro data center na região emparelhada hello.

Por exemplo, se você tiver criado um trabalho no Centro Sul dos EUA, o Agendador do Azure replica automaticamente esse trabalho no Centro Norte dos EUA. Quando há uma falha no Centro Sul dos EUA, o Agendador do Azure garante que o trabalho Olá é executado a partir do Centro Norte dos EUA. 

![][1]

Como resultado, o Agendador do Azure garante que os dados permanecerão em Olá mesma região geográfica maior no caso de uma falha do Azure. Como resultado, é necessário duplicar a trabalho tooadd apenas alta disponibilidade – o Agendador do Azure fornece automaticamente os recursos de alta disponibilidade para seus trabalhos.

## <a name="azure-scheduler-reliability"></a>Confiabilidade do Agendador do Azure
O Agendador do Azure garante sua própria alta disponibilidade e adota uma abordagem diferente trabalhos criados pelo toouser. Por exemplo, seu trabalho pode invocar um ponto de extremidade HTTP que não está disponível. O Agendador do Azure, mesmo assim, tenta tooexecute seu trabalho com êxito, fornecendo opções alternativas toodeal com falha. O Agendador do Azure faz isso de duas maneiras:

### <a name="configurable-retry-policy-via-retrypolicy"></a>Política de repetição configurável via "retryPolicy"
O Agendador do Azure permite que você tooconfigure uma política de repetição. Por padrão, se um trabalho falhar, o Agendador tenta trabalho hello mais novamente quatro vezes, em intervalos de 30 segundos. É possível reconfigurar essa repetição política toobe mais agressiva (por exemplo, dez vezes, em intervalos de 30 segundos) ou menos rígida (por exemplo, duas vezes, em intervalos diários.)

Como um exemplo de quando isso pode ajudar, você pode criar um trabalho que é executado uma vez por semana e invoca um ponto de extremidade HTTP. Se o ponto de extremidade Olá HTTP estiver inativo por algumas horas quando o trabalho for executado, não convém toowait uma semana mais Olá trabalho toorun novamente desde que o mesmo Olá política de repetição padrão falhará. Nesses casos, você pode reconfigurar Olá tooretry de política de repetição padrão a cada três horas (por exemplo) em vez da cada 30 segundos.

toolearn como tooconfigure uma política de repetição, consulte muito[retryPolicy](scheduler-concepts-terms.md#retrypolicy).

### <a name="alternate-endpoint-configurability-via-erroraction"></a>Capacidade de configuração de ponto de extremidade alternativo via "errorAction"
Se o ponto de extremidade de destino de saudação do seu trabalho do Agendador do Azure permanecer inacessível, o Agendador do Azure reverterá toohello alternativo ponto de extremidade de tratamento de erros após sua política de repetição. Se um ponto de extremidade de tratamento de erro alternativo for configurado, o Agendador do Azure o chama. Com um ponto de extremidade alternativo, seus próprios trabalhos ficam altamente disponíveis em face de saudação da falha.

Por exemplo, no diagrama abaixo, a saudação do Agendador do Azure segue sua política de repetição toohit um serviço web de Nova York. Depois de falhas de tentativas de Olá, ele verifica se há uma alternativa. Em seguida, prossegue e começa a fazer solicitações toohello alternativo com hello mesmo política de repetição.

![][2]

Observe que Olá a mesma política de repetição se aplica a ação original do tooboth hello e ação alternativa de erro de saudação. Tipo de ação é também possível toohave Olá alternativa de erro da ação ser diferente do tipo da ação principal hello. Por exemplo, enquanto a ação principal Olá pode invocar um ponto de extremidade HTTP, uma ação de erro Olá pode ser uma fila de armazenamento, a fila do barramento de serviço ou a ação de tópico do barramento de serviço que faz log de erros.

toolearn como tooconfigure um ponto de extremidade alternativo, consulte muito[errorAction](scheduler-concepts-terms.md#action-and-erroraction).

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Agendador do Azure](scheduler-concepts-terms.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Limites, padrões e códigos de erro do Agendador do Azure](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
