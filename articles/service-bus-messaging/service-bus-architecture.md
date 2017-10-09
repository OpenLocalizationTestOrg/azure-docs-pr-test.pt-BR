---
title: "Visão geral da arquitetura de processamento de mensagens de barramento de serviço de aaaAzure | Microsoft Docs"
description: "Descreve a arquitetura de processamento de mensagem de saudação do barramento de serviço do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Arquitetura do Barramento de Serviço
Este artigo descreve a arquitetura de processamento de mensagem de saudação do barramento de serviço do Azure.

## <a name="service-bus-scale-units"></a>Unidades de escala do Barramento de Serviço
O Barramento de Serviço é organizado por *unidades de escala*. Uma unidade de escala é uma unidade de implantação e contém todas as componentes necessários Olá execução de serviço. Cada região implanta uma ou mais unidades de escala do Barramento de Serviço.

Um namespace de barramento de serviço é a unidade de escala de tooa mapeada. unidade de escala Olá trata todos os tipos de entidades do Service Bus (filas, tópicos, assinaturas). Uma unidade de escala de barramento de serviço consiste em Olá componentes a seguir:

* **Um conjunto de nós de gateway.** Os nós de gateway autenticam solicitações de entrada. Cada nó de gateway tem um endereço IP público.
* **Um conjunto de nós do agente de mensagens.** Os nós do agente de mensagens processam solicitações referentes às entidades de mensagens.
* **Um repositório de gateway.** repositório de gateway Olá contém os dados de saudação para cada entidade definida nesta unidade de escala. armazenamento de gateway de saudação é implementado na parte superior de um banco de dados do SQL Azure.
* **Múltiplos repositórios de mensagens.** Repositórios de mensagens guardar mensagens de saudação de todas as filas, tópicos e assinaturas que são definidas nesta unidade de escala. Eles também contêm todos os dados de assinatura. A menos que [particionando entidades de mensagens](service-bus-partitioning.md) está habilitado, uma fila ou tópico é o repositório de mensagens tooone mapeada. As assinaturas são armazenadas no hello mesmo repositório de mensagens como seu tópico pai. Exceto para o barramento de serviço [sistema de mensagens Premium](service-bus-premium-messaging.md), repositórios de mensagens de saudação são implementados sobre bancos de dados do SQL Azure.

## <a name="containers"></a>Contêineres
Cada entidade de mensagens é atribuída a um contêiner específico. Um contêiner é um constructo lógico que usa exatamente um toostore mensagens do repositório de dados relevantes para esse contêiner. Cada contêiner é atribuído tooa nó do agente de mensagens. Normalmente, há mais contêineres que nós do agente de mensagens. Portanto, cada nó do agente de mensagens carrega diversos contêineres. distribuição de saudação do nó do agente contêineres tooa mensagens é organizada de modo que todos os nós de broker mensagens são igualmente carregados. Se alterações de padrão de carga hello (por exemplo, uma saudação contêineres obtém muito ocupado) ou se um nó do agente de mensagens fica temporariamente indisponível, Olá contêineres são redistribuídos entre nós do agente de mensagens de saudação.

## <a name="processing-of-incoming-messaging-requests"></a>Processamento de mensagens de solicitações de entrada
Quando um cliente envia uma solicitação tooService barramento, balanceador de carga do Azure Olá encaminha tooany de nós de gateway hello. nó de gateway Olá autoriza a solicitação de saudação. Se a solicitação de saudação se refere a uma entidade de mensagens (fila, tópico, assinatura), o nó de gateway de Olá procura entidade Olá no repositório de gateway hello e determina em qual saudação do repositório de mensagens entidade está localizada. Em seguida, pesquisa a qual nó broker mensagens atualmente está servindo a esse contêiner e envia Olá solicitação toothat nó do agente de mensagens. nó do agente de mensagens de saudação processa a solicitação de saudação e atualiza o estado da entidade Olá no repositório de contêiner de saudação. Olá, em seguida, o nó do agente de mensagens envia Olá resposta toohello back gateway nó, que envia um resposta apropriada ao cliente toohello back solicitação original Olá emitidos.

![Processamento de mensagens de solicitações de entrada](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Próximas etapas
Agora que você leu uma visão geral da arquitetura do barramento de serviço, visite Olá links para obter mais informações a seguir:

* [Visão geral de mensagens do Barramento de Serviço](service-bus-messaging-overview.md)
* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Uma solução de mensagens na fila usando filas do Barramento de Serviço](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


