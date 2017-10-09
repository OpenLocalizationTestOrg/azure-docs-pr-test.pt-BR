---
title: "Instâncias de contêiner aaaAzure e a coordenação de contêiner"
description: "Entender como as Instâncias de Contêiner do Azure interagem com orquestradores de contêiner"
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
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Instâncias de Contêiner do Azure e orquestradores de contêiner

Devido ao seu tamanho reduzido e a orientação a aplicativos, os contêineres são adequados para ambientes de entrega com agilidade e arquiteturas baseadas em microsserviço. tarefa de saudação de automatizar e gerenciar um grande número de contêineres e como eles interagem é conhecida como *orquestração*. Orchestrators contêiner populares incluem Kubernetes, DC/OS e Docker Swarm, que estão disponíveis no hello [serviço de contêiner do Azure](https://docs.microsoft.com/azure/container-service/).

Instâncias de contêiner do Azure fornece algumas Olá básico de funcionalidades de plataformas de orquestração do agendamento, mas ele não aborda os serviços de valor mais alto Olá que essas plataformas fornecem e podem realmente ser complementares com eles. Este artigo descreve o escopo de saudação do lida com instâncias de contêiner do Azure e quanto orchestrators de contêiner podem interagir com ele.

## <a name="traditional-orchestration"></a>Orquestração tradicional

a definição padrão Olá de orquestração inclui Olá tarefas a seguir:

- **Agendando**: uma imagem de contêiner e uma solicitação de recurso, localize uma máquina adequada no contêiner toorun hello.
- **Afinidade/Antiafinidade**: especificar que um conjunto de contêineres devem ser executados próximo uns aos outros (para desempenho) ou suficientemente distantes (para disponibilidade).
- **Monitoramento de integridade**: inspecionar falhas de contêiner e automaticamente reagendá-los.
- **Failover**: controlar o que está em execução em cada computador e reagendar contêineres de nós de toohealthy máquinas com falha.
- **Dimensionamento**: Adicionar ou remover a demanda de toomatch de instâncias de contêiner, manual ou automaticamente.
- **Rede**: forneça uma rede de sobreposição para coordenar contêineres toocommunicate em vários computadores de host.
- **Descoberta do serviço**: habilitar toolocate contêineres uns aos outros automaticamente mesmo quando eles se mover entre computadores host e alteram os endereços IP.
- **Coordenada atualizações de aplicativo**: gerenciar aplicativo de contêiner atualizações tooavoid de tempo de inatividade e habilitar a reversão se algo der errado.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orquestração com Instâncias de Contêiner do Azure: uma abordagem em camadas

Instâncias de contêiner do Azure permite tooorchestration uma abordagem em camadas, fornecendo todos Olá agendamento e recursos de gerenciamento necessários toorun um único contêiner, permitindo orchestrator tarefas de contêiner de várias plataformas toomanage sobre ele.

Como todos Olá infra-estrutura subjacente para instâncias de contêiner é gerenciado pelo Azure, uma plataforma orchestrator não precisa tooconcern se encontrar uma máquina de host apropriado no qual toorun um único contêiner. elasticidade de saudação da nuvem de saudação garante que um está sempre disponível. Em vez disso, o orchestrator Olá pode se concentrarem em tarefas de Olá que simplificam o desenvolvimento de saudação do contêiner várias arquiteturas, incluindo dimensionamento e upgrades coordenados.



## <a name="potential-scenarios"></a>Cenários possíveis

Embora a integração do orquestrador com as Instâncias de Contêiner do Azure ainda seja recente, estimamos que alguns ambientes diferentes podem surgir:

### <a name="orchestration-of-container-instances-exclusively"></a>Orquestração de instâncias de contêiner de maneira exclusiva

Porque eles iniciar rapidamente e cobrar pelo Olá segundo, um ambiente com base exclusivamente em instâncias de contêiner do Azure oferece iniciado Olá tooget de maneira mais rápida e toodeal com cargas de trabalho altamente variáveis.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinação de Instâncias de Contêiner e Contêineres em Máquinas Virtuais

Demoradas, cargas de trabalho estáveis, orquestrar contêineres em um cluster de máquinas virtuais dedicadas geralmente será mais baratas do que contêineres em execução Olá mesmo com instâncias de contêiner. No entanto, instâncias de contêiner oferecer uma ótima solução para expandir e reduzir seu toodeal capacidade total com picos de curta duração ou inesperados no uso rapidamente. Em vez de dimensionar número Olá de máquinas virtuais em cluster, em seguida, implantar contêineres adicionais para as máquinas, Olá orchestrator pode agendar recipientes adicionais hello, usando as instâncias de contêiner e excluí-los quando eles são simplesmente nenhum mais necessários.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Exemplo de implementação: conector de Instâncias de Contêiner do Azure para Kubernetes

toodemonstrate como integrar plataformas de orquestração de contêiner com instâncias de contêiner do Azure, começamos criando uma [conector de exemplo para Kubernetes][aci-connector-k8s]. 

Olá conector para Kubernetes imita Olá [kubelet] [ kubelet-doc] registrando como um nó com capacidade ilimitada e expedir a criação de saudação do [compartimentos] [ pod-doc] como grupos de contêineres em instâncias de contêiner do Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Conectores para outros orchestrators podem ser criados da mesma forma integrada com simplicidade de gerenciar contêineres em instâncias de contêiner do Azure e capacidade de saudação de toocombine de primitivos de plataforma do orchestrator Olá API com velocidade de saudação.

> [!WARNING]
> Olá conector ACI é Kubernetes *experimental* e não deve ser usada na produção.

## <a name="next-steps"></a>Próximas etapas

Criar o primeiro contêiner com instâncias de contêiner do Azure usando Olá [guia de início rápido](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/