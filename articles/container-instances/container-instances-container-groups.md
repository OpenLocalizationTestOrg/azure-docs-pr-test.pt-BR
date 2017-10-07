---
title: "aaaAzure grupos de contêineres de instâncias de contêiner"
description: "Entenda como funcionam os grupos de contêineres em Instâncias de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Grupos de contêineres em Instâncias de Contêiner do Azure

o recurso de nível superior Olá em instâncias de contêiner do Azure é um grupo de contêiner. Este artigo descreve quais são os grupos de contêineres e quais tipos de cenários que eles permitem.

## <a name="how-a-container-group-works"></a>Como um grupo de contêineres funciona

Um contêiner de grupo é uma coleção de contêineres que seja agendados em Olá mesmo host de máquina e compartilhar um ciclo de vida, a rede local e volumes de armazenamento. É o conceito de toohello semelhantes de um *pod* na [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Olá diagrama a seguir mostra um exemplo de um grupo de contêiner que inclui vários contêineres.

![Exemplo de grupos de contêineres][container-groups-example]

Observe que:

- grupo de saudação está agendado em uma máquina de host único.
- grupo de saudação expõe um único endereço IP público, com uma porta exposto.
- grupo de saudação é composto por dois contêineres. Um contêiner de escuta na porta 80, enquanto outros Olá escuta na porta 5000.
- grupo de saudação inclui dois compartilhamentos de arquivos do Azure como montagem de volume e cada contêiner monta uma saudação compartilhamentos localmente.

### <a name="networking"></a>Rede

Grupos de contêineres compartilham um endereço IP e um namespace de porta nesse endereço IP. tooenable clientes externos tooreach um contêiner no grupo hello, você deve expor porta Olá no endereço IP hello e do contêiner de saudação. Como contêineres no grupo Olá compartilham um namespace de porta, não há suporte para mapeamento de porta. Contêineres dentro de um grupo podem acessar uns aos outros por meio de localhost em Olá portas que eles têm expostos, mesmo se essas portas não estiverem expostas externamente no endereço IP do grupo de saudação.

### <a name="storage"></a>Armazenamento

Você pode especificar volumes externo toomount dentro de um grupo de contêiner. Você pode mapear os volumes para caminhos específicos dentro de contêineres de saudação individuais em um grupo.

## <a name="common-scenarios"></a>Cenários comuns

Contêiner de vários grupos são úteis nos casos em que você deseja toodivide a uma única tarefa funcional em um pequeno número de imagens de contêiner, que podem ser entregues por equipes diferentes e têm requisitos de recursos separado. Os exemplos de uso podem incluir:

- Um contêiner de aplicativo e um contêiner de log. contêiner de log Olá coleta logs de saudação e saída de métricas por aplicativo principal hello e os grava armazenamento toolong prazo.
- Um aplicativo e um contêiner de monitoramento. Olá monitoramento contêiner periodicamente faz um tooensure de aplicativo solicitação toohello que ele está em execução e respondendo corretamente e emite um alerta se não for.
- Um contêiner que atende a um aplicativo web e um contêiner de extrair o conteúdo mais recente de saudação do controle de origem.

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[implantar um grupo de vários contêiner](container-instances-multi-container-group.md) com um modelo do Gerenciador de recursos do Azure.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png