---
title: "Visão geral da arquitetura de processamento de mensagens do Barramento de Serviço do Azure | Microsoft Docs"
description: "Descreve a arquitetura de processamento de mensagens do Barramento de Serviço do Azure."
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
ms.date: 12/21/2017
ms.author: sethm
ms.openlocfilehash: c3bf541c14e6d869f77ca7d7a6e520bd3489fcad
ms.sourcegitcommit: 6f33adc568931edf91bfa96abbccf3719aa32041
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="service-bus-architecture"></a>Arquitetura do Barramento de Serviço

Este artigo descreve a arquitetura de processamento de mensagens do [Barramento de Serviço do Azure](https://azure.microsoft.com/services/service-bus/).

## <a name="service-bus-scale-units"></a>Unidades de escala do Barramento de Serviço

O Barramento de Serviço é organizado por *unidades de escala*. Uma unidade de escala é uma unidade de implantação que contém todos os componentes necessários para executar o serviço. Cada região implanta uma ou mais unidades de escala do Barramento de Serviço.

Um namespace de Barramento de Serviço é mapeado para uma unidade de escala. A unidade de escala trata todos os tipos de entidade do Barramento de Serviço (filas, tópicos, assinaturas). Uma unidade de escala do Barramento de Serviço consiste nos seguintes componentes:

* **Um conjunto de nós de gateway.** Os nós de gateway autenticam solicitações de entrada. Cada nó de gateway tem um endereço IP público.
* **Um conjunto de nós do agente de mensagens.** Os nós do agente de mensagens processam solicitações referentes às entidades de mensagens.
* **Um repositório de gateway.** O repositório de gateway mantém os dados para cada entidade definida nessa unidade de escala. O repositório de gateway é implementado sobre uma instância do Banco de Dados SQL.
* **Múltiplos repositórios de mensagens.** Repositórios de mensagens mantêm as mensagens de todas as filas, tópicos e assinaturas que são definidas na unidade de escala. Eles também contêm todos os dados de assinatura. A menos que o [particionamento de entidades de mensagens](service-bus-partitioning.md) esteja habilitado, uma fila ou tópico é mapeado para um repositório de mensagens. As assinaturas são armazenadas no mesmo repositório de mensagens que o tópico pai. Com exceção do [Sistema de Mensagens Premium](service-bus-premium-messaging.md) do Barramento de Serviço, os repositórios de mensagens são implementados sobre instâncias do [Banco de Dados SQL](https://azure.microsoft.com/services/sql-database/).

## <a name="containers"></a>Contêineres

Cada entidade de mensagens é atribuída a um contêiner específico. Um contêiner é um constructo lógico que utiliza um repositório de mensagens para todos os dados relevantes para esse contêiner. Cada contêiner é atribuído a um nó do agente de mensagens. Normalmente, há mais contêineres que nós do agente de mensagens. Portanto, cada nó do agente de mensagens carrega diversos contêineres. A distribuição de contêineres para um nó do agente de mensagens é organizada de modo que todos os nós do agende de mensagens sejam carregados igualmente. Se o padrão de carga mudar (por exemplo, um dos contêineres ficar muito ocupado) ou se um nó do agente de mensagens ficar indisponível temporariamente, os contêineres serão redistribuídos entre os nós de agente de mensagens.

## <a name="processing-of-incoming-messaging-requests"></a>Processamento de mensagens de solicitações de entrada

Quando um cliente envia uma solicitação ao Barramento de Serviço, o balanceador de carga do Azure direciona para qualquer um de nós do gateway. O nó do gateway autoriza a solicitação. Se a solicitação for referente a uma entidade de mensagens (fila, tópico, assinatura), o nó do gateway busca a entidade no repositório de gateway e determina em qual repositório de mensagens a entidade está localizada. Depois, ele procura qual nó do agente de mensagens está servindo o contêiner e envia a solicitação para esse nó. O nó do agente de mensagens processa a solicitação e atualiza o estado da entidade no repositório do contêiner. O nó do agente de mensagens, em seguida, envia a resposta de volta ao nó do gateway, que envia uma resposta apropriada para o cliente que emitiu a solicitação original.

![Processamento de mensagens de solicitações de entrada](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você leu uma visão geral da arquitetura do Barramento de Serviço, consulte os seguintes links para obter mais informações:

* [Visão geral de mensagens do Barramento de Serviço](service-bus-messaging-overview.md)
* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)


