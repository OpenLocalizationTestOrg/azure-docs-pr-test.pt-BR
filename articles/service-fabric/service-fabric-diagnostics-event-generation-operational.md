---
title: aaaAzure Service Fabric operacional Channel | Microsoft Docs
description: Lista abrangente dos logs gerados em clusters de canal operacionais do Azure Service Fabric hello.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Canal operacional 

canal operacional Olá consiste em logs de alto nível ações executadas pelo serviço de malha em seus nós e o cluster. Quando "diagnóstico" está habilitado para um cluster, Olá agente de diagnóstico do Azure é implantado em seu cluster e é por padrão configurado tooread em logs do canal operacional hello. Leia mais sobre como configurar Olá [agente de diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md) toomodify configuração de diagnóstico de saudação do toopick seu cluster mais logs ou contadores de desempenho. 

## <a name="operational-channel-logs"></a>Logs do canal operacional 

Aqui está uma lista abrangente dos logs fornecidos pela malha do serviço no canal operacional hello. 

| EventId | Nome | Origem (Tarefa) | Nível |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informativo |
| 25621 | NodeOpenedSuccess | FabricNode | Informativo |
| 25622 | NodeOpenedFailed | FabricNode | Informativo |
| 25623 | NodeClosing | FabricNode | Informativo |
| 25624 | NodeClosed | FabricNode | Informativo |
| 25625 | NodeAborting | FabricNode | Informativo |
| 25626 | NodeAborted | FabricNode | Informativo |
| 29627 | ClusterUpgradeStart | CM | Informativo |
| 29628 | ClusterUpgradeComplete | CM | Informativo |
| 29629 | ClusterUpgradeRollback | CM | Informativo |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informativo |
| 29631 | ClusterUpgradeDomainComplete | CM | Informativo |
| 23074 | ContainerActivated | Hosting | Informativo |
| 23075 | ContainerDeactivated | Hosting | Informativo |
| 29620 | ApplicationCreated | CM | Informativo |
| 29621 | ApplicationUpgradeStart | CM | Informativo |
| 29622 | ApplicationUpgradeComplete | CM | Informativo |
| 29623 | ApplicationUpgradeRollback | CM | Informativo |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informativo |
| 29625 | ApplicationDeleted | CM | Informativo |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informativo |
| 18566 | ServiceCreated | FM | Informativo |
| 18567 | ServiceDeleted | FM | Informativo |

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre geral [geração de eventos no nível de plataforma Olá](service-fabric-diagnostics-event-generation-infra.md) na malha do serviço
* Modificando o [diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md) configuração toocollect mais logs
* [Configurar o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee o canal operacional logs
