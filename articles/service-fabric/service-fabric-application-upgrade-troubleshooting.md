---
title: "atualizações de aplicativo aaaTroubleshooting | Microsoft Docs"
description: "Este artigo aborda alguns problemas comuns em torno de atualização de um aplicativo de malha do serviço e como tooresolve-los."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a>Solucionar problemas de atualizações de aplicativo
Este artigo aborda alguns dos problemas comuns de saudação em torno de atualizar um aplicativo do Azure Service Fabric e como tooresolve-los.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Solucionar problemas de atualização de um aplicativo com falha
Quando uma atualização falhar, saída Olá Olá **Get-ServiceFabricApplicationUpgrade** comando contém informações adicionais de depuração falha hello.  Olá lista a seguir especifica como as informações adicionais de saudação podem ser usadas:

1. Identifique o tipo de falha de saudação.
2. Identificar o motivo da falha hello.
3. Isolar um ou mais componentes com falha para saber mais.

Essas informações estão disponíveis quando o Service Fabric detecta a falha de saudação independentemente de se hello **FailureAction** está de volta tooroll ou suspender atualização hello.

### <a name="identify-hello-failure-type"></a>Identificar o tipo de falha de saudação
Na saída de saudação do **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica Olá carimbo de hora (UTC) em que uma falha de atualização foi detectada pela malha do serviço e  **FailureAction** foi disparado. **Motivo da falha** identifica um dos três possíveis causas de alto nível de falha de saudação:

1. UpgradeDomainTimeout - indica que um determinado domínio de atualização demorou muito toocomplete e **UpgradeDomainTimeout** expirou.
2. OverallUpgradeTimeout - indica que Olá geral da atualização demorou muito toocomplete e **UpgradeTimeout** expirou.
3. Verificação de integridade - indica que, depois de atualizar um domínio de atualização, aplicativo hello permaneceu não íntegro de acordo com o toohello especificado diretivas de integridade e **HealthCheckRetryTimeout** expirou.

Essas entradas só aparecem na saída de hello quando atualização Olá falha e começa a reversão. Informações adicionais são exibidas, dependendo do tipo de saudação de falha de saudação.

### <a name="investigate-upgrade-timeouts"></a>Investigar tempos limite de atualização
As falhas de tempo de execução de atualização são geralmente causadas por problemas de disponibilidade do serviço. saída de Hello este parágrafo a seguir é típica de atualizações de onde réplicas do serviço ou instâncias falharem toostart na nova versão do código Olá. Olá **UpgradeDomainProgressAtFailure** campo captura um instantâneo de qualquer trabalho de atualização pendente no momento de saudação da falha.

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

Neste exemplo, Olá Falha na atualização no domínio de atualização *MYUD1* e duas partições (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) foram presos. partições de saudação foram presos porque Olá runtime foi réplicas primárias tooplace não é possível (*WaitForPrimaryPlacement*) em nós de destino *Node1* e *Nó4*.

Olá **Get-ServiceFabricNode** comando pode ser usado tooverify que esses dois nós estão no domínio de atualização *MYUD1*. Olá *UpgradePhase* diz *PostUpgradeSafetyCheck*, o que significa que essas verificações de segurança estão ocorrendo depois que todos os nós no domínio de atualização Olá concluída a atualização. Todas essas informações pontos tooa possível problema com a nova versão Olá Olá do código do aplicativo. problemas mais comuns de saudação são erros de serviço em Olá aberta ou caminhos de código tooprimary promoção.

Um *UpgradePhase* de *PreUpgradeSafetyCheck* significa que houve problemas de preparação de domínio de atualização de saudação antes que ela foi executada. Nesse caso, problemas mais comuns de saudação são erros de serviço em Olá feche ou rebaixamento de caminhos de código principal.

Olá atual **UpgradeState** é *RollingBackCompleted*, de modo de atualização original Olá deve ter sido realizada com uma reversão **FailureAction**, que automaticamente reversão da atualização Olá em caso de falha. Se a atualização original Olá foi executada com um manual **FailureAction**, atualização de saudação em vez disso, será um tooallow estado suspenso ao vivo de depuração de aplicativo hello.

### <a name="investigate-health-check-failures"></a>Investigar falhas de verificação de integridade
As falhas de verificação de integridade podem ser acionadas por vários problemas que podem ocorrer depois que todos os nós em um domínio de atualização terminam a atualização e passam por todas as verificações de segurança. saída de Hello este parágrafo a seguir é típica de uma falha na atualização devido toofailed verificações de integridade. Olá **UnhealthyEvaluations** campo captura um instantâneo das verificações de integridade falhou em tempo de saudação da atualização Olá toohello especificado de acordo com [política de integridade](service-fabric-health-introduction.md).

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

Primeiro investigar falhas de verificação de integridade requer uma compreensão Olá Service Fabric do modelo de integridade. Mas mesmo sem tal uma compreensão detalhada, podemos ver que os dois serviços estão íntegros: *fabric: / DemoApp/Svc3* e *fabric: / DemoApp/Svc2*, juntamente com os relatórios de integridade de erro hello ("InjectedFault "nesse caso). Neste exemplo, duas de quatro serviços são não íntegros, que está abaixo do objectivo do saudação padrão de 0% não íntegro (*MaxPercentUnhealthyServices*).

Olá atualização foi suspenso após a falha, especificando um **FailureAction** de manual quando iniciar Olá atualização. Esse modo permite que nós tooinvestigate Olá ao vivo sistema em estado de falha de saudação antes de realizar qualquer ação adicional.

### <a name="recover-from-a-suspended-upgrade"></a>Recuperar de uma atualização suspensa
Com uma reversão **FailureAction**, não há nenhuma recuperação é necessária, já que a atualização de saudação reverte automaticamente após a falha. Com uma **FailureAction**manual, há várias opções de recuperação:

1.  disparar uma reversão
2. Prossiga com o restante da saudação de atualização de saudação manualmente
3. Olá retomar monitorado atualização

Olá **ServiceFabricApplicationRollback início** comando pode ser usado em qualquer toostart tempo Revertendo aplicativo hello. Depois que o comando Olá retorna com êxito, solicitação de reversão Olá foi registrada no sistema de saudação e inicia logo depois.

Olá **Resume-ServiceFabricApplicationUpgrade** comando pode ser usado tooproceed pelo restante Olá Olá atualizar manualmente, um domínio de atualização por vez. Nesse modo, as verificações de segurança só são executadas pelo sistema de saudação. Nenhuma outra verificação de integridade é executada. Este comando só pode ser usado quando hello *UpgradeState* mostra *RollingForwardPending*, que significa que esse domínio de atualização atual Olá terminou de atualizar mas hello lado um não foi iniciado (pendente).

Olá **ServiceFabricApplicationUpgrade atualização** comando pode ser usado tooresume Olá monitorado atualização com verificações de integridade e segurança que está sendo executada.

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

atualização Olá continua no domínio de atualização Olá onde ele foi suspenso pela última vez e use Olá mesmo atualizar parâmetros e políticas de integridade como antes. Se necessário, qualquer um dos parâmetros de atualização de hello e diretivas de integridade mostradas Olá precede a saída pode ser alterado no hello mesmo comando quando sair da atualização de saudação. Neste exemplo, a atualização Olá foi retomada no modo monitorado, com parâmetros de saudação e políticas de integridade Olá inalteradas.

## <a name="further-troubleshooting"></a>Solução de problemas adicionais
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Malha do serviço não é seguir Olá especificado diretivas de integridade
Possível causa 1:

Service Fabric converte todas as porcentagens em números reais de entidades (por exemplo, réplicas, partições e serviços) para avaliação de integridade e sempre é arredondado para cima toowhole entidades. Por exemplo, se hello máximo *MaxPercentUnhealthyReplicasPerPartition* % 21 e há cinco réplicas, e a malha do serviço permite que até tootwo réplicas (ou seja,`Math.Ceiling (5*0.21)`). Portanto, as políticas de integridade devem ser definidas adequadamente.

Possível causa 2:

as políticas de integridade são especificadas em termos de percentuais do total de serviço e não em instâncias de serviço específicas. Por exemplo, antes de uma atualização, se um aplicativo tem quatro instâncias A, B, C e D, de serviço onde o serviço D não está íntegro, mas com aplicativos de toohello pouco impacto. Queremos Olá tooignore conhecido não íntegro serviço D durante a parâmetro hello atualização e defina *MaxPercentUnhealthyServices* toobe 25%, supondo que somente A, B e C necessário toobe íntegro.

No entanto, durante a atualização de saudação D pode se tornar íntegra enquanto C se torna não íntegro. atualização Olá ainda terá sucesso porque somente 25% dos serviços de saudação estão em estado íntegro. No entanto, pode resultar em erros inesperados devido tooC sendo inesperadamente não íntegros, em vez de D. Nessa situação, D deve ser modelada como um tipo de serviço diferente de A, B e C. Como diretivas de integridade são especificadas por tipo de serviço, limites de porcentagem Íntegro diferentes podem ser aplicadas toodifferent serviços. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Eu não especificou uma diretiva de integridade para a atualização do aplicativo, mas a atualização Olá ainda falha por algum tempos limite que eu nunca especificado
Quando as políticas de integridade não são fornecidas toohello solicitação de atualização, eles são tirados Olá *ApplicationManifest.xml* da versão atual do aplicativo hello. Por exemplo, se você estiver atualizando X aplicativo versão 1.0 tooversion 2.0, diretivas de integridade do aplicativo especificadas para a versão 1.0 são usadas. Se uma política de integridade de diferentes deve ser usada para atualização hello, política de saudação precisa toobe especificado como parte da chamada à API atualização aplicativo hello. Olá especificadas como parte da chamada de API de saudação de políticas se aplicam somente durante a atualização de saudação. Após a conclusão da atualização hello, políticas de saudação especificadas na Olá *ApplicationManifest.xml* são usados.

### <a name="incorrect-time-outs-are-specified"></a>Os tempos limite incorretos estão especificados
Você pode já ter se perguntado sobre o que acontece quando os tempos limite são definidos de forma inconsistente. Por exemplo, você pode ter um *UpgradeTimeout* que é menor que Olá *UpgradeDomainTimeout*. resposta de saudação é que um erro será retornado. Os erros são retornados se hello *UpgradeDomainTimeout* é menor do que a soma de saudação do *HealthCheckWaitDuration* e *HealthCheckRetryTimeout*, ou se  *UpgradeDomainTimeout* é menor do que a soma de saudação do *HealthCheckWaitDuration* e *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Minhas atualizações estão demorando muito
tempo de saudação para uma atualização toocomplete depende Olá verificações de integridade e o tempo limite especificado. Verificações de integridade e tempos limite depende de quanto tempo toocopy, implanta e estabilizar aplicativo hello. Muita agressividade com tempos limite pode significar mais atualizações com falha e, portanto, recomendamos um início mais conservador com tempos limites mais longos.

Aqui está um atualizador rápido sobre como os tempos limite de saudação interage com tempos de atualização de saudação:

A atualização de um domínio de atualização não pode ser concluída mais rapidamente do que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

A falha de atualização não pode ocorrer mais rápido do que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Olá tempo de atualização para um domínio de atualização é limitado pelo *UpgradeDomainTimeout*.  Se *HealthCheckRetryTimeout* e *HealthCheckStableDuration* são diferentes de zero e integridade de saudação do aplicativo hello mantém alternar, em seguida, a atualização Olá eventualmente expira em  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* inicia a contagem regressiva uma vez Olá atualização para o domínio de atualização atual Olá começa.

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).
