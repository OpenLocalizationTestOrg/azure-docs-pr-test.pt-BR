---
title: "Atualização de aplicativos: parâmetros de atualização | Microsoft Docs"
description: "Descreve os parâmetros relacionados tooupgrading um aplicativo de malha do serviço, incluindo integridade verificações de políticas e tooperform tooautomatically desfazer Olá atualização."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Parâmetros de atualização de aplicativo
Este artigo descreve Olá vários parâmetros que se aplicam durante a saudação atualizar de um aplicativo do Azure Service Fabric. parâmetros de saudação incluem nome hello e versão do aplicativo hello. São botões que controlam o tempo limite de saudação e verificações de integridade que são aplicadas durante a atualização de saudação e especificam políticas Olá que devem ser aplicadas quando uma atualização falhar.

<br>

| Parâmetro | Descrição |
| --- | --- |
| ApplicationName |Nome do aplicativo hello que está sendo atualizado. Exemplos: fabric:/VisualObjects, fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |versão de saudação do tipo de aplicativo Olá Olá destinos de atualização. |
| FailureAction |ação de saudação realizada pela malha do serviço quando ocorre falha na atualização de saudação. aplicativo Hello pode ser revertido versão de pré-atualização toohello (reversão) ou atualização Olá pode ser interrompida no domínio de atualização atual hello. No último caso de Olá, modo de atualização de saudação também é alterado tooManual. Os valores permitidos são Manual e Reversão. |
| HealthCheckWaitDurationSec |Olá toowait de tempo (em segundos) depois da atualização de saudação foi concluída no domínio de atualização de saudação antes do Service Fabric avalia a integridade de saudação do aplicativo hello. Esta duração também pode ser considerada como tempo de saudação que um aplicativo deve estar em execução antes que possa ser considerado íntegro. Se a verificação de integridade Olá passa, o processo de atualização de saudação passa toohello próximo domínio de atualização.  Se a verificação de integridade de saudação falhar, o Service Fabric aguarda um intervalo (Olá UpgradeHealthCheckInterval) antes de tentar novamente a verificação de integridade de saudação novamente até Olá que healthcheckretrytimeout for atingido. valor saudação padrão e recomendado é 0 segundos. |
| HealthCheckRetryTimeoutSec |duração da saudação (em segundos) que Service Fabric continua a avaliação de integridade tooperform antes de declarar atualização hello como falha. padrão de saudação é 600 segundos. Esta duração é iniciada depois que a HealthCheckWaitDuration for atingida. Neste HealthCheckRetryTimeout Service Fabric pode executar diversas verificações de integridade do aplicativo hello. valor padrão de saudação é de 10 minutos e deve ser personalizada adequadamente para seu aplicativo. |
| HealthCheckStableDurationSec |Olá tooverify duração (em segundos) que o aplicativo hello está estável antes de mover toohello próximo domínio de atualização ou concluir Olá atualização. A duração da espera é alterações tooprevent usado detectado de integridade logo após a verificação de integridade de saudação. valor padrão de saudação é de 120 segundos e deve ser personalizada adequadamente para seu aplicativo. |
| UpgradeDomainTimeoutSec |Tempo máximo (em segundos) para atualizar um único domínio de atualização. Se esse tempo limite for atingido, atualização hello interrompe e continua com base na configuração de saudação para UpgradeFailureAction. saudação padrão valor nunca é (infinito) e devem ser personalizados adequadamente para seu aplicativo. |
| UpgradeTimeout |Um tempo limite (em segundos) que se aplica a atualização inteira hello. Se esse tempo limite for atingido, Olá atualização para e UpgradeFailureAction é acionado. saudação padrão valor nunca é (infinito) e devem ser personalizados adequadamente para seu aplicativo. |
| UpgradeHealthCheckInterval |frequência de Olá Olá status de integridade é verificada. Este parâmetro é especificado em Olá Olá seção ClusterManager *cluster* *manifesto*e não é especificado como parte do cmdlet atualização hello. valor padrão de saudação é 60 segundos. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Avaliação de integridade do serviço durante a atualização do aplicativo
<br>
critérios de avaliação de integridade de saudação são opcionais. Se os critérios de avaliação de integridade de saudação não são especificados quando uma atualização é iniciada, o Service Fabric usa diretivas de integridade do aplicativo hello especificadas no hello ApplicationManifest.xml da instância de aplicativo hello.

<br>

| Parâmetro | Descrição |
| --- | --- |
| ConsiderWarningAsError |O valor padrão é Falso. Trate eventos de integridade de aviso de Olá para o aplicativo hello como erros ao avaliar a integridade de saudação do aplicativo hello durante a atualização. Por padrão, do Service Fabric não avalia falhas de toobe de eventos de integridade de aviso (erros), para que atualização Olá pode continuar mesmo se há eventos de aviso. |
| MaxPercentUnhealthyDeployedApplications |O valor padrão e recomendado é 0. Especifique o número máximo de saudação dos aplicativos implantados (consulte Olá [seção integridade](service-fabric-health-introduction.md)) que pode ser não íntegro, antes de aplicativo hello é considerado não íntegro e falhar Olá atualização. Esse parâmetro define a integridade do aplicativo hello no nó hello e ajuda a detectar problemas durante a atualização. Normalmente, as réplicas de saudação do aplicativo hello obtém toohello com balanceamento de carga outro nó, o que permite Olá aplicativo tooappear íntegro, permitindo Olá tooproceed de atualização. Especificando uma integridade MaxPercentUnhealthyDeployedApplications rígida, Service Fabric pode detectar um problema com o pacote de aplicativo hello rapidamente e ajudar a produzir uma falha de atualização rápida. |
| MaxPercentUnhealthyServices |O valor padrão e recomendado é 0. Especifique o número máximo de saudação de serviços na instância de aplicativo hello que pode ser problemáticos antes de aplicativo hello é considerado não íntegro e Falha na atualização de saudação. |
| MaxPercentUnhealthyPartitionsPerService |O valor padrão e recomendado é 0. Especifique o número máximo de saudação de partições em um serviço que pode ser não-íntegro, antes que o serviço de saudação é considerado não íntegro. |
| MaxPercentUnhealthyReplicasPerPartition |O valor padrão e recomendado é 0. Especifique o número máximo de saudação de réplicas de partição pode ser não-íntegro antes da partição de saudação é considerada não íntegro. |
| UpgradeReplicaSetCheckTimeout |**Serviço sem monitoração de estado**– em um único domínio de atualização do Service Fabric tenta tooensure que instâncias adicionais do serviço de saudação do estão disponíveis. Se contagem de instâncias de destino Olá for mais de um, o Service Fabric aguarda toobe em mais de uma instância disponível, o valor de tempo limite máximo de tooa. Esse tempo limite é especificado usando a propriedade de UpgradeReplicaSetCheckTimeout hello. Se o tempo limite de saudação expirar, Service Fabric prossegue com atualização hello, independentemente do número de saudação de instâncias de serviço. Se a contagem de instâncias de destino Olá é um, Service Fabric não espera e imediatamente continua com a atualização de saudação. **Serviço com monitoração de estado**– em um único domínio de atualização do Service Fabric tenta tooensure que Olá réplica conjunto tem um quorum. Service Fabric aguarda um toobe de quorum disponível, o valor de tempo limite máximo de tooa (especificado pela propriedade de UpgradeReplicaSetCheckTimeout Olá). Se o tempo limite de saudação expirar, Service Fabric prossegue com atualização hello, independentemente de quorum. Essa configuração está definida como nunca (infinito) durante o roll forward e 900 segundos durante a reversão. |
| ForceRestart |Se você atualizar uma configuração ou o pacote de dados sem atualizar o código de serviço hello, serviço de saudação é reiniciado somente se Olá /forcerestart propriedade é definida tootrue. Quando Olá atualização for concluída, o Service Fabric notifica serviço Olá um novo pacote de configuração ou o pacote de dados está disponível. serviço de saudação é responsável por aplicar as alterações de saudação. Se necessário, o serviço Olá pode reiniciar em si. |

<br>
<br>
Olá MaxPercentUnhealthyServices, MaxPercentUnhealthyPartitionsPerService e MaxPercentUnhealthyReplicasPerPartition critérios podem ser especificados por tipo de serviço para uma instância do aplicativo. Definir esses parâmetros por serviço permite que um toocontain diferentes para serviços de aplicativo tipos com políticas de avaliação diferentes. Por exemplo, um tipo de serviço de gateway sem monitoração de estado pode ter um MaxPercentUnhealthyPartitionsPerService que é diferente de um tipo de serviço de mecanismo com monitoração de estado para uma determinada instância de aplicativo.

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

A [Atualização do aplicativo usando a CLI do Service Fabric no Linux](service-fabric-application-lifecycle-sfctl.md#upgrade-application) orienta você ao longo de uma atualização de aplicativo usando a CLI do Service Fabric.

[Atualizar seu aplicativo usando o plug-in Eclipse do Service Fabric](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).
