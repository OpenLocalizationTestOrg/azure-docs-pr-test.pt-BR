---
title: "Solucionando problemas de atualizações de aplicativo | Microsoft Docs"
description: "Este artigo aborda alguns problemas comuns em torno da atualização de um aplicativo Service Fabric e como resolvê-los."
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
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="41205-103">Solucionar problemas de atualizações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="41205-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="41205-104">Este artigo aborda alguns dos problemas comuns na atualização de um aplicativo do Service Fabric e como resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="41205-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="41205-105">Solucionar problemas de atualização de um aplicativo com falha</span><span class="sxs-lookup"><span data-stu-id="41205-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="41205-106">Quando uma atualização falha, a saída do comando **Get-ServiceFabricApplicationUpgrade** contém informações adicionais para depurar a falha.</span><span class="sxs-lookup"><span data-stu-id="41205-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="41205-107">A lista a seguir especifica como as informações adicionais podem ser usadas:</span><span class="sxs-lookup"><span data-stu-id="41205-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="41205-108">Identificar o tipo de falha.</span><span class="sxs-lookup"><span data-stu-id="41205-108">Identify the failure type.</span></span>
2. <span data-ttu-id="41205-109">Identificar o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="41205-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="41205-110">Isolar um ou mais componentes com falha para saber mais.</span><span class="sxs-lookup"><span data-stu-id="41205-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="41205-111">Essas informações estão disponíveis quando o Service Fabric detecta a falha, independentemente de a **FailureAction** reverter ou suspender a atualização.</span><span class="sxs-lookup"><span data-stu-id="41205-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="41205-112">Identificar o tipo de falha</span><span class="sxs-lookup"><span data-stu-id="41205-112">Identify the failure type</span></span>
<span data-ttu-id="41205-113">Na saída de **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica o carimbo de hora (UTC) em que uma falha de atualização foi detectada pelo Service Fabric e **FailureAction** foi acionado.</span><span class="sxs-lookup"><span data-stu-id="41205-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="41205-114">**FailureReason** identifica uma das três possíveis causas de alto nível da falha:</span><span class="sxs-lookup"><span data-stu-id="41205-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="41205-115">UpgradeDomainTimeout: indica que um determinado domínio de atualização demorou muito para ser concluído e **UpgradeDomainTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="41205-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="41205-116">OverallUpgradeTimeout: indica que a atualização global demorou muito para ser concluída e **UpgradeTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="41205-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="41205-117">HealthCheck: indica que, após a atualização de um domínio de atualização, o aplicativo permaneceu não íntegro de acordo com as políticas de integridade especificadas e **HealthCheckRetryTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="41205-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="41205-118">Essas entradas somente são exibidas na saída quando a atualização falhar e começar a reversão.</span><span class="sxs-lookup"><span data-stu-id="41205-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="41205-119">Outras Informações são exibidas dependendo do tipo de falha.</span><span class="sxs-lookup"><span data-stu-id="41205-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="41205-120">Investigar tempos limite de atualização</span><span class="sxs-lookup"><span data-stu-id="41205-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="41205-121">As falhas de tempo de execução de atualização são geralmente causadas por problemas de disponibilidade do serviço.</span><span class="sxs-lookup"><span data-stu-id="41205-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="41205-122">A saída após este parágrafo é típica de atualizações em que as réplicas ou instâncias de serviço não são iniciadas na nova versão do código.</span><span class="sxs-lookup"><span data-stu-id="41205-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="41205-123">O campo **UpgradeDomainProgressAtFailure** captura um instantâneo de trabalhos de atualização pendentes no momento da falha.</span><span class="sxs-lookup"><span data-stu-id="41205-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

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

<span data-ttu-id="41205-124">Neste exemplo, a atualização falhou no domínio de atualização *MYUD1* e duas partições (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) foram bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="41205-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="41205-125">As partições foram bloqueadas porque o tempo de execução não pôde colocar réplicas primárias (*WaitForPrimaryPlacement*) em nós de destino *Node1* e *Node4*.</span><span class="sxs-lookup"><span data-stu-id="41205-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="41205-126">O comando **Get-ServiceFabricNode** pode ser usado para verificar se esses dois nós estão no domínio de atualização *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="41205-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="41205-127">O *UpgradePhase* diz *PostUpgradeSafetyCheck*, que significa que essas verificações de segurança estão ocorrendo depois que todos os nós no domínio de atualização concluíram a atualização.</span><span class="sxs-lookup"><span data-stu-id="41205-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="41205-128">Todas essas informações combinadas apontam para um possível problema com a nova versão do código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="41205-129">Os problemas mais comuns são erros de serviço em aberto ou promoção para caminhos de código principal.</span><span class="sxs-lookup"><span data-stu-id="41205-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="41205-130">Uma *UpgradePhase* de *PreUpgradeSafetyCheck* significa que houve problemas na preparação do domínio de atualização antes de a atualização ser executada.</span><span class="sxs-lookup"><span data-stu-id="41205-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="41205-131">Nesse caso, os problemas mais comuns são erros de serviço no fechamento ou rebaixamento de caminhos de código principal.</span><span class="sxs-lookup"><span data-stu-id="41205-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="41205-132">O **UpgradeState** atual é *RollingBackCompleted*; portanto, a atualização original deve ter sido realizada com uma reversão **FailureAction**, que automaticamente reverteu a atualização em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="41205-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="41205-133">Se a atualização original tivesse sido realizada com um **FailureAction**manual, a atualização estaria em um estado suspenso para permitir a depuração dinâmica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="41205-134">Investigar falhas de verificação de integridade</span><span class="sxs-lookup"><span data-stu-id="41205-134">Investigate health check failures</span></span>
<span data-ttu-id="41205-135">As falhas de verificação de integridade podem ser acionadas por vários problemas que podem ocorrer depois que todos os nós em um domínio de atualização terminam a atualização e passam por todas as verificações de segurança.</span><span class="sxs-lookup"><span data-stu-id="41205-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="41205-136">A saída após este parágrafo é típica de uma falha na atualização devido a falhas de verificação de integridade.</span><span class="sxs-lookup"><span data-stu-id="41205-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="41205-137">O campo **UnhealthyEvaluations** captura um instantâneo das verificações de integridade com falha no momento da atualização de acordo com a [política de integridade](service-fabric-health-introduction.md)especificada.</span><span class="sxs-lookup"><span data-stu-id="41205-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="41205-138">A investigação de falhas de verificação de integridade exige primeiro uma compreensão do modelo de integridade do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="41205-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="41205-139">Mas mesmo sem essa compreensão detalhada, podemos ver que dois serviços não estão íntegros: *fabric:/DemoApp/Svc3* e *fabric:/DemoApp/Svc2*, junto com os relatórios de integridade de erro ("InjectedFault" nesse caso).</span><span class="sxs-lookup"><span data-stu-id="41205-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="41205-140">Neste exemplo, dois de quatro serviços não estão íntegros, abaixo da meta padrão de 0% de não integridade (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="41205-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="41205-141">A atualização foi suspensa com falha, especificando um **FailureAction** manual quando iniciada a atualização.</span><span class="sxs-lookup"><span data-stu-id="41205-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="41205-142">Esse modo permite investigar o sistema dinâmico no estado de falha antes de realizar qualquer outra ação.</span><span class="sxs-lookup"><span data-stu-id="41205-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="41205-143">Recuperar de uma atualização suspensa</span><span class="sxs-lookup"><span data-stu-id="41205-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="41205-144">Com uma reversão de **FailureAction**, não há nenhuma recuperação necessária, já que a atualização é revertida automaticamente após a falha.</span><span class="sxs-lookup"><span data-stu-id="41205-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="41205-145">Com uma **FailureAction**manual, há várias opções de recuperação:</span><span class="sxs-lookup"><span data-stu-id="41205-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="41205-146">disparar uma reversão</span><span class="sxs-lookup"><span data-stu-id="41205-146">trigger a rollback</span></span>
2. <span data-ttu-id="41205-147">Continuar com o restante da atualização manualmente</span><span class="sxs-lookup"><span data-stu-id="41205-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="41205-148">Continuar a atualização monitorada</span><span class="sxs-lookup"><span data-stu-id="41205-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="41205-149">O comando **Start-ServiceFabricApplicationRollback** pode ser usado a qualquer momento para iniciar a reversão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="41205-150">Depois que o comando retornar com êxito, a solicitação de reversão foi registrada no sistema e começa em breve.</span><span class="sxs-lookup"><span data-stu-id="41205-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="41205-151">O comando **ServiceFabricApplicationUpgrade retomar** pode ser usado para percorrer o restante da atualização manualmente, um domínio de atualização de cada vez.</span><span class="sxs-lookup"><span data-stu-id="41205-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="41205-152">Nesse modo, somente verificações de segurança são executadas pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="41205-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="41205-153">Nenhuma outra verificação de integridade é executada.</span><span class="sxs-lookup"><span data-stu-id="41205-153">No more health checks are performed.</span></span> <span data-ttu-id="41205-154">Esse comando só pode ser usado quando o *UpgradeState* mostra *RollingForwardPending*, o que significa que o domínio de atualização atual concluiu a atualização, mas o próximo ainda não foi iniciado (pendente).</span><span class="sxs-lookup"><span data-stu-id="41205-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="41205-155">O comando **ServiceFabricApplicationUpgrade atualização** pode ser usado para retomar a atualização monitorada com a realização tanto da verificação de segurança quanto da de integridade.</span><span class="sxs-lookup"><span data-stu-id="41205-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="41205-156">A atualização continua no domínio de atualização no qual ela foi suspensa da última vez e usa os mesmos parâmetros de atualização e políticas de integridade de antes.</span><span class="sxs-lookup"><span data-stu-id="41205-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="41205-157">Se necessário, qualquer um dos parâmetros de atualização e políticas de integridade mostrados na saída anterior poderá ser alterado no mesmo comando ao retomar a atualização.</span><span class="sxs-lookup"><span data-stu-id="41205-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="41205-158">Neste exemplo, a atualização foi reiniciada no modo monitorado, com os parâmetros e as políticas de integridade inalteradas.</span><span class="sxs-lookup"><span data-stu-id="41205-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="41205-159">Solução de problemas adicionais</span><span class="sxs-lookup"><span data-stu-id="41205-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="41205-160">O Service Fabric não está seguindo as políticas de integridade especificadas</span><span class="sxs-lookup"><span data-stu-id="41205-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="41205-161">Possível causa 1:</span><span class="sxs-lookup"><span data-stu-id="41205-161">Possible Cause 1:</span></span>

<span data-ttu-id="41205-162">O Service Fabric converte todas as porcentagens em números reais de entidades (por exemplo, réplicas, partições e serviços) para avaliação de integridade e sempre arredonda para cima para entidades inteiras.</span><span class="sxs-lookup"><span data-stu-id="41205-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="41205-163">Por exemplo, se o máximo de *MaxPercentUnhealthyReplicasPerPartition* for 21% e houver cinco réplicas, o Service Fabric permitirá até duas réplicas não íntegras (ou seja, `Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="41205-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="41205-164">Portanto, as políticas de integridade devem ser definidas adequadamente.</span><span class="sxs-lookup"><span data-stu-id="41205-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="41205-165">Possível causa 2:</span><span class="sxs-lookup"><span data-stu-id="41205-165">Possible Cause 2:</span></span>

<span data-ttu-id="41205-166">as políticas de integridade são especificadas em termos de percentuais do total de serviço e não em instâncias de serviço específicas.</span><span class="sxs-lookup"><span data-stu-id="41205-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="41205-167">Por exemplo, antes de uma atualização, se um aplicativo tem quatro instâncias de serviço A, B, C e D, em que o serviço D não está íntegro, mas tem pouco impacto no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="41205-168">Vamos ignorar o serviço conhecido não íntegro D durante a atualização e definir o parâmetro *MaxPercentUnhealthyServices* a 25%, supondo que apenas A, B e C precisem ser íntegros.</span><span class="sxs-lookup"><span data-stu-id="41205-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="41205-169">No entanto, durante a atualização, D podem se tornar íntegro enquanto C se torna não íntegro.</span><span class="sxs-lookup"><span data-stu-id="41205-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="41205-170">A atualização ainda teria êxito porque somente 25% dos serviços não estão íntegros.</span><span class="sxs-lookup"><span data-stu-id="41205-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="41205-171">No entanto, isso poderia resultar em erros inesperados devido ao fato de C estar inesperadamente não íntegro em vez de D. Nessa situação, D deve ser modelado como um tipo diferente de serviço de A, B e C. Como as políticas de integridade são especificadas baseadas no tipo de serviço, podem ser aplicados limites de percentual de não integridade diferentes para diferentes serviços.</span><span class="sxs-lookup"><span data-stu-id="41205-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="41205-172">Eu não especifiquei uma política de integridade para a atualização do aplicativo, mas a atualização ainda falha em alguns tempos limite que nunca especifiquei</span><span class="sxs-lookup"><span data-stu-id="41205-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="41205-173">Quando as políticas de integridade não são fornecidas para a solicitação de atualização, elas são tiradas do *ApplicationManifest.xml* da versão atual do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="41205-174">Por exemplo, se você estiver atualizando o Aplicativo X da versão 1.0 para a versão 2.0, as políticas de integridade do aplicativo especificadas na versão 1.0 serão usadas.</span><span class="sxs-lookup"><span data-stu-id="41205-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="41205-175">Se uma política de integridade diferente tiver que ser usada para a atualização, a política precisa ser especificada como parte da chamada de API de atualização de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="41205-176">As políticas especificadas como parte da chamada à API somente se aplicam durante a atualização.</span><span class="sxs-lookup"><span data-stu-id="41205-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="41205-177">Depois que a atualização é concluída, as políticas especificadas no *ApplicationManifest.xml* são usadas.</span><span class="sxs-lookup"><span data-stu-id="41205-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="41205-178">Os tempos limite incorretos estão especificados</span><span class="sxs-lookup"><span data-stu-id="41205-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="41205-179">Você pode já ter se perguntado sobre o que acontece quando os tempos limite são definidos de forma inconsistente.</span><span class="sxs-lookup"><span data-stu-id="41205-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="41205-180">Por exemplo, você pode ter um *UpgradeTimeout* inferior ao *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="41205-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="41205-181">A resposta é que um erro é retornado.</span><span class="sxs-lookup"><span data-stu-id="41205-181">The answer is that an error is returned.</span></span> <span data-ttu-id="41205-182">Erros serão retornados se *UpgradeDomainTimeout* for menor do que a soma de *HealthCheckWaitDuration* e *HealthCheckRetryTimeout* ou se *UpgradeDomainTimeout* for menor do que a soma de *HealthCheckWaitDuration* e *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="41205-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="41205-183">Minhas atualizações estão demorando muito</span><span class="sxs-lookup"><span data-stu-id="41205-183">My upgrades are taking too long</span></span>
<span data-ttu-id="41205-184">O tempo para concluir uma atualização depende das verificações de integridade e dos tempos limite especificados.</span><span class="sxs-lookup"><span data-stu-id="41205-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="41205-185">Verificações de integridade e tempos limite dependem de quanto tempo demora para copiar, implantar e estabilizar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41205-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="41205-186">Muita agressividade com tempos limite pode significar mais atualizações com falha e, portanto, recomendamos um início mais conservador com tempos limites mais longos.</span><span class="sxs-lookup"><span data-stu-id="41205-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="41205-187">Eis uma recapitulação de como os tempos limite interagem com os tempos de atualização:</span><span class="sxs-lookup"><span data-stu-id="41205-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="41205-188">A atualização de um domínio de atualização não pode ser concluída mais rapidamente do que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="41205-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="41205-189">A falha de atualização não pode ocorrer mais rápido do que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="41205-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="41205-190">O tempo de atualização para um domínio de atualização é limitado pelo *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="41205-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="41205-191">Se *HealthCheckRetryTimeout* e *HealthCheckStableDuration* são diferentes de zero e a integridade do aplicativo alterna entre boa e ruim, a atualização pode esgotar o tempo limite em *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="41205-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="41205-192">*UpgradeDomainTimeout* inicia a contagem regressiva quando a atualização do domínio de atualização atual começa.</span><span class="sxs-lookup"><span data-stu-id="41205-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41205-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41205-193">Next steps</span></span>
<span data-ttu-id="41205-194">[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41205-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="41205-195">[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41205-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="41205-196">Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="41205-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="41205-197">Torne suas atualizações de aplicativo compatíveis aprendendo a usar a [Serialização de Dados](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="41205-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="41205-198">Saiba como usar a funcionalidade avançada ao atualizar seu aplicativo consultando os [Tópicos avançados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="41205-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
