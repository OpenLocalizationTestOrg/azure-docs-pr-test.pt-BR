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
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="6f16c-103">Solucionar problemas de atualizações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="6f16c-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="6f16c-104">Este artigo aborda alguns dos problemas comuns de saudação em torno de atualizar um aplicativo do Azure Service Fabric e como tooresolve-los.</span><span class="sxs-lookup"><span data-stu-id="6f16c-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="6f16c-105">Solucionar problemas de atualização de um aplicativo com falha</span><span class="sxs-lookup"><span data-stu-id="6f16c-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="6f16c-106">Quando uma atualização falhar, saída Olá Olá **Get-ServiceFabricApplicationUpgrade** comando contém informações adicionais de depuração falha hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="6f16c-107">Olá lista a seguir especifica como as informações adicionais de saudação podem ser usadas:</span><span class="sxs-lookup"><span data-stu-id="6f16c-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="6f16c-108">Identifique o tipo de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f16c-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="6f16c-109">Identificar o motivo da falha hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="6f16c-110">Isolar um ou mais componentes com falha para saber mais.</span><span class="sxs-lookup"><span data-stu-id="6f16c-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="6f16c-111">Essas informações estão disponíveis quando o Service Fabric detecta a falha de saudação independentemente de se hello **FailureAction** está de volta tooroll ou suspender atualização hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="6f16c-112">Identificar o tipo de falha de saudação</span><span class="sxs-lookup"><span data-stu-id="6f16c-112">Identify hello failure type</span></span>
<span data-ttu-id="6f16c-113">Na saída de saudação do **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica Olá carimbo de hora (UTC) em que uma falha de atualização foi detectada pela malha do serviço e  **FailureAction** foi disparado.</span><span class="sxs-lookup"><span data-stu-id="6f16c-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="6f16c-114">**Motivo da falha** identifica um dos três possíveis causas de alto nível de falha de saudação:</span><span class="sxs-lookup"><span data-stu-id="6f16c-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="6f16c-115">UpgradeDomainTimeout - indica que um determinado domínio de atualização demorou muito toocomplete e **UpgradeDomainTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="6f16c-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="6f16c-116">OverallUpgradeTimeout - indica que Olá geral da atualização demorou muito toocomplete e **UpgradeTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="6f16c-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="6f16c-117">Verificação de integridade - indica que, depois de atualizar um domínio de atualização, aplicativo hello permaneceu não íntegro de acordo com o toohello especificado diretivas de integridade e **HealthCheckRetryTimeout** expirou.</span><span class="sxs-lookup"><span data-stu-id="6f16c-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="6f16c-118">Essas entradas só aparecem na saída de hello quando atualização Olá falha e começa a reversão.</span><span class="sxs-lookup"><span data-stu-id="6f16c-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="6f16c-119">Informações adicionais são exibidas, dependendo do tipo de saudação de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f16c-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="6f16c-120">Investigar tempos limite de atualização</span><span class="sxs-lookup"><span data-stu-id="6f16c-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="6f16c-121">As falhas de tempo de execução de atualização são geralmente causadas por problemas de disponibilidade do serviço.</span><span class="sxs-lookup"><span data-stu-id="6f16c-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="6f16c-122">saída de Hello este parágrafo a seguir é típica de atualizações de onde réplicas do serviço ou instâncias falharem toostart na nova versão do código Olá.</span><span class="sxs-lookup"><span data-stu-id="6f16c-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="6f16c-123">Olá **UpgradeDomainProgressAtFailure** campo captura um instantâneo de qualquer trabalho de atualização pendente no momento de saudação da falha.</span><span class="sxs-lookup"><span data-stu-id="6f16c-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

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

<span data-ttu-id="6f16c-124">Neste exemplo, Olá Falha na atualização no domínio de atualização *MYUD1* e duas partições (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) foram presos.</span><span class="sxs-lookup"><span data-stu-id="6f16c-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="6f16c-125">partições de saudação foram presos porque Olá runtime foi réplicas primárias tooplace não é possível (*WaitForPrimaryPlacement*) em nós de destino *Node1* e *Nó4*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="6f16c-126">Olá **Get-ServiceFabricNode** comando pode ser usado tooverify que esses dois nós estão no domínio de atualização *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="6f16c-127">Olá *UpgradePhase* diz *PostUpgradeSafetyCheck*, o que significa que essas verificações de segurança estão ocorrendo depois que todos os nós no domínio de atualização Olá concluída a atualização.</span><span class="sxs-lookup"><span data-stu-id="6f16c-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="6f16c-128">Todas essas informações pontos tooa possível problema com a nova versão Olá Olá do código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6f16c-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="6f16c-129">problemas mais comuns de saudação são erros de serviço em Olá aberta ou caminhos de código tooprimary promoção.</span><span class="sxs-lookup"><span data-stu-id="6f16c-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="6f16c-130">Um *UpgradePhase* de *PreUpgradeSafetyCheck* significa que houve problemas de preparação de domínio de atualização de saudação antes que ela foi executada.</span><span class="sxs-lookup"><span data-stu-id="6f16c-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="6f16c-131">Nesse caso, problemas mais comuns de saudação são erros de serviço em Olá feche ou rebaixamento de caminhos de código principal.</span><span class="sxs-lookup"><span data-stu-id="6f16c-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="6f16c-132">Olá atual **UpgradeState** é *RollingBackCompleted*, de modo de atualização original Olá deve ter sido realizada com uma reversão **FailureAction**, que automaticamente reversão da atualização Olá em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="6f16c-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="6f16c-133">Se a atualização original Olá foi executada com um manual **FailureAction**, atualização de saudação em vez disso, será um tooallow estado suspenso ao vivo de depuração de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="6f16c-134">Investigar falhas de verificação de integridade</span><span class="sxs-lookup"><span data-stu-id="6f16c-134">Investigate health check failures</span></span>
<span data-ttu-id="6f16c-135">As falhas de verificação de integridade podem ser acionadas por vários problemas que podem ocorrer depois que todos os nós em um domínio de atualização terminam a atualização e passam por todas as verificações de segurança.</span><span class="sxs-lookup"><span data-stu-id="6f16c-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="6f16c-136">saída de Hello este parágrafo a seguir é típica de uma falha na atualização devido toofailed verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="6f16c-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="6f16c-137">Olá **UnhealthyEvaluations** campo captura um instantâneo das verificações de integridade falhou em tempo de saudação da atualização Olá toohello especificado de acordo com [política de integridade](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f16c-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="6f16c-138">Primeiro investigar falhas de verificação de integridade requer uma compreensão Olá Service Fabric do modelo de integridade.</span><span class="sxs-lookup"><span data-stu-id="6f16c-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="6f16c-139">Mas mesmo sem tal uma compreensão detalhada, podemos ver que os dois serviços estão íntegros: *fabric: / DemoApp/Svc3* e *fabric: / DemoApp/Svc2*, juntamente com os relatórios de integridade de erro hello ("InjectedFault "nesse caso).</span><span class="sxs-lookup"><span data-stu-id="6f16c-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="6f16c-140">Neste exemplo, duas de quatro serviços são não íntegros, que está abaixo do objectivo do saudação padrão de 0% não íntegro (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="6f16c-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="6f16c-141">Olá atualização foi suspenso após a falha, especificando um **FailureAction** de manual quando iniciar Olá atualização.</span><span class="sxs-lookup"><span data-stu-id="6f16c-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="6f16c-142">Esse modo permite que nós tooinvestigate Olá ao vivo sistema em estado de falha de saudação antes de realizar qualquer ação adicional.</span><span class="sxs-lookup"><span data-stu-id="6f16c-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="6f16c-143">Recuperar de uma atualização suspensa</span><span class="sxs-lookup"><span data-stu-id="6f16c-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="6f16c-144">Com uma reversão **FailureAction**, não há nenhuma recuperação é necessária, já que a atualização de saudação reverte automaticamente após a falha.</span><span class="sxs-lookup"><span data-stu-id="6f16c-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="6f16c-145">Com uma **FailureAction**manual, há várias opções de recuperação:</span><span class="sxs-lookup"><span data-stu-id="6f16c-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="6f16c-146">disparar uma reversão</span><span class="sxs-lookup"><span data-stu-id="6f16c-146">trigger a rollback</span></span>
2. <span data-ttu-id="6f16c-147">Prossiga com o restante da saudação de atualização de saudação manualmente</span><span class="sxs-lookup"><span data-stu-id="6f16c-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="6f16c-148">Olá retomar monitorado atualização</span><span class="sxs-lookup"><span data-stu-id="6f16c-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="6f16c-149">Olá **ServiceFabricApplicationRollback início** comando pode ser usado em qualquer toostart tempo Revertendo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="6f16c-150">Depois que o comando Olá retorna com êxito, solicitação de reversão Olá foi registrada no sistema de saudação e inicia logo depois.</span><span class="sxs-lookup"><span data-stu-id="6f16c-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="6f16c-151">Olá **Resume-ServiceFabricApplicationUpgrade** comando pode ser usado tooproceed pelo restante Olá Olá atualizar manualmente, um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="6f16c-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="6f16c-152">Nesse modo, as verificações de segurança só são executadas pelo sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f16c-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="6f16c-153">Nenhuma outra verificação de integridade é executada.</span><span class="sxs-lookup"><span data-stu-id="6f16c-153">No more health checks are performed.</span></span> <span data-ttu-id="6f16c-154">Este comando só pode ser usado quando hello *UpgradeState* mostra *RollingForwardPending*, que significa que esse domínio de atualização atual Olá terminou de atualizar mas hello lado um não foi iniciado (pendente).</span><span class="sxs-lookup"><span data-stu-id="6f16c-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="6f16c-155">Olá **ServiceFabricApplicationUpgrade atualização** comando pode ser usado tooresume Olá monitorado atualização com verificações de integridade e segurança que está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="6f16c-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="6f16c-156">atualização Olá continua no domínio de atualização Olá onde ele foi suspenso pela última vez e use Olá mesmo atualizar parâmetros e políticas de integridade como antes.</span><span class="sxs-lookup"><span data-stu-id="6f16c-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="6f16c-157">Se necessário, qualquer um dos parâmetros de atualização de hello e diretivas de integridade mostradas Olá precede a saída pode ser alterado no hello mesmo comando quando sair da atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f16c-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="6f16c-158">Neste exemplo, a atualização Olá foi retomada no modo monitorado, com parâmetros de saudação e políticas de integridade Olá inalteradas.</span><span class="sxs-lookup"><span data-stu-id="6f16c-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="6f16c-159">Solução de problemas adicionais</span><span class="sxs-lookup"><span data-stu-id="6f16c-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="6f16c-160">Malha do serviço não é seguir Olá especificado diretivas de integridade</span><span class="sxs-lookup"><span data-stu-id="6f16c-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="6f16c-161">Possível causa 1:</span><span class="sxs-lookup"><span data-stu-id="6f16c-161">Possible Cause 1:</span></span>

<span data-ttu-id="6f16c-162">Service Fabric converte todas as porcentagens em números reais de entidades (por exemplo, réplicas, partições e serviços) para avaliação de integridade e sempre é arredondado para cima toowhole entidades.</span><span class="sxs-lookup"><span data-stu-id="6f16c-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="6f16c-163">Por exemplo, se hello máximo *MaxPercentUnhealthyReplicasPerPartition* % 21 e há cinco réplicas, e a malha do serviço permite que até tootwo réplicas (ou seja,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="6f16c-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="6f16c-164">Portanto, as políticas de integridade devem ser definidas adequadamente.</span><span class="sxs-lookup"><span data-stu-id="6f16c-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="6f16c-165">Possível causa 2:</span><span class="sxs-lookup"><span data-stu-id="6f16c-165">Possible Cause 2:</span></span>

<span data-ttu-id="6f16c-166">as políticas de integridade são especificadas em termos de percentuais do total de serviço e não em instâncias de serviço específicas.</span><span class="sxs-lookup"><span data-stu-id="6f16c-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="6f16c-167">Por exemplo, antes de uma atualização, se um aplicativo tem quatro instâncias A, B, C e D, de serviço onde o serviço D não está íntegro, mas com aplicativos de toohello pouco impacto.</span><span class="sxs-lookup"><span data-stu-id="6f16c-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="6f16c-168">Queremos Olá tooignore conhecido não íntegro serviço D durante a parâmetro hello atualização e defina *MaxPercentUnhealthyServices* toobe 25%, supondo que somente A, B e C necessário toobe íntegro.</span><span class="sxs-lookup"><span data-stu-id="6f16c-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="6f16c-169">No entanto, durante a atualização de saudação D pode se tornar íntegra enquanto C se torna não íntegro.</span><span class="sxs-lookup"><span data-stu-id="6f16c-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="6f16c-170">atualização Olá ainda terá sucesso porque somente 25% dos serviços de saudação estão em estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="6f16c-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="6f16c-171">No entanto, pode resultar em erros inesperados devido tooC sendo inesperadamente não íntegros, em vez de D. Nessa situação, D deve ser modelada como um tipo de serviço diferente de A, B e C. Como diretivas de integridade são especificadas por tipo de serviço, limites de porcentagem Íntegro diferentes podem ser aplicadas toodifferent serviços.</span><span class="sxs-lookup"><span data-stu-id="6f16c-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="6f16c-172">Eu não especificou uma diretiva de integridade para a atualização do aplicativo, mas a atualização Olá ainda falha por algum tempos limite que eu nunca especificado</span><span class="sxs-lookup"><span data-stu-id="6f16c-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="6f16c-173">Quando as políticas de integridade não são fornecidas toohello solicitação de atualização, eles são tirados Olá *ApplicationManifest.xml* da versão atual do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="6f16c-174">Por exemplo, se você estiver atualizando X aplicativo versão 1.0 tooversion 2.0, diretivas de integridade do aplicativo especificadas para a versão 1.0 são usadas.</span><span class="sxs-lookup"><span data-stu-id="6f16c-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="6f16c-175">Se uma política de integridade de diferentes deve ser usada para atualização hello, política de saudação precisa toobe especificado como parte da chamada à API atualização aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="6f16c-176">Olá especificadas como parte da chamada de API de saudação de políticas se aplicam somente durante a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f16c-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="6f16c-177">Após a conclusão da atualização hello, políticas de saudação especificadas na Olá *ApplicationManifest.xml* são usados.</span><span class="sxs-lookup"><span data-stu-id="6f16c-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="6f16c-178">Os tempos limite incorretos estão especificados</span><span class="sxs-lookup"><span data-stu-id="6f16c-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="6f16c-179">Você pode já ter se perguntado sobre o que acontece quando os tempos limite são definidos de forma inconsistente.</span><span class="sxs-lookup"><span data-stu-id="6f16c-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="6f16c-180">Por exemplo, você pode ter um *UpgradeTimeout* que é menor que Olá *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="6f16c-181">resposta de saudação é que um erro será retornado.</span><span class="sxs-lookup"><span data-stu-id="6f16c-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="6f16c-182">Os erros são retornados se hello *UpgradeDomainTimeout* é menor do que a soma de saudação do *HealthCheckWaitDuration* e *HealthCheckRetryTimeout*, ou se  *UpgradeDomainTimeout* é menor do que a soma de saudação do *HealthCheckWaitDuration* e *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="6f16c-183">Minhas atualizações estão demorando muito</span><span class="sxs-lookup"><span data-stu-id="6f16c-183">My upgrades are taking too long</span></span>
<span data-ttu-id="6f16c-184">tempo de saudação para uma atualização toocomplete depende Olá verificações de integridade e o tempo limite especificado.</span><span class="sxs-lookup"><span data-stu-id="6f16c-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="6f16c-185">Verificações de integridade e tempos limite depende de quanto tempo toocopy, implanta e estabilizar aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f16c-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="6f16c-186">Muita agressividade com tempos limite pode significar mais atualizações com falha e, portanto, recomendamos um início mais conservador com tempos limites mais longos.</span><span class="sxs-lookup"><span data-stu-id="6f16c-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="6f16c-187">Aqui está um atualizador rápido sobre como os tempos limite de saudação interage com tempos de atualização de saudação:</span><span class="sxs-lookup"><span data-stu-id="6f16c-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="6f16c-188">A atualização de um domínio de atualização não pode ser concluída mais rapidamente do que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="6f16c-189">A falha de atualização não pode ocorrer mais rápido do que *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="6f16c-190">Olá tempo de atualização para um domínio de atualização é limitado pelo *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="6f16c-191">Se *HealthCheckRetryTimeout* e *HealthCheckStableDuration* são diferentes de zero e integridade de saudação do aplicativo hello mantém alternar, em seguida, a atualização Olá eventualmente expira em  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="6f16c-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="6f16c-192">*UpgradeDomainTimeout* inicia a contagem regressiva uma vez Olá atualização para o domínio de atualização atual Olá começa.</span><span class="sxs-lookup"><span data-stu-id="6f16c-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f16c-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f16c-193">Next steps</span></span>
<span data-ttu-id="6f16c-194">[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f16c-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="6f16c-195">[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f16c-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="6f16c-196">Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="6f16c-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="6f16c-197">Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="6f16c-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="6f16c-198">Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="6f16c-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
