---
title: "Solucionar problemas com relatórios de integridade do sistema | Microsoft Docs"
description: "Descreve os relatórios de integridade enviados por componentes do Service Fabric do Azure e seu uso para solucionar problemas de cluster ou de aplicativos."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="5b616-103">Usar relatórios de integridade do sistema para solução de problemas</span><span class="sxs-lookup"><span data-stu-id="5b616-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="5b616-104">Os componentes do Service Fabric apresentam relatórios de integridade prontos para uso sobre todas as entidades.</span><span class="sxs-lookup"><span data-stu-id="5b616-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="5b616-105">O [repositório de integridade](service-fabric-health-introduction.md#health-store) cria e exclui entidades baseado nos relatórios do sistema.</span><span class="sxs-lookup"><span data-stu-id="5b616-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="5b616-106">Ele também os organiza em uma hierarquia que captura interações de entidade.</span><span class="sxs-lookup"><span data-stu-id="5b616-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="5b616-107">Leia mais sobre o [Modelo de Integridade do Service Fabric](service-fabric-health-introduction.md)para entender os conceitos relacionados à integridade.</span><span class="sxs-lookup"><span data-stu-id="5b616-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="5b616-108">Os relatórios de integridade do sistema fornecem visibilidade da funcionalidade do cluster e de aplicativos e sinalizam problemas por meio da integridade.</span><span class="sxs-lookup"><span data-stu-id="5b616-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="5b616-109">Para aplicativos e serviços, os relatórios de integridade do sistema verificam se as entidades são implementadas e estão se comportando corretamente da perspectiva do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b616-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="5b616-110">Os relatórios não fornecem monitoramento de integridade da lógica de negócios do serviço nem detecção de processos travados.</span><span class="sxs-lookup"><span data-stu-id="5b616-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="5b616-111">Os serviços de usuário podem enriquecer os dados de integridade com informações específicas à respectiva lógica.</span><span class="sxs-lookup"><span data-stu-id="5b616-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="5b616-112">Os relatórios de integridade dos watchdogs ficam visíveis somente *depois* que os componentes do sistema criam uma entidade.</span><span class="sxs-lookup"><span data-stu-id="5b616-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="5b616-113">Quando uma entidade é excluída, o repositório de integridade exclui automaticamente todos os relatórios de integridade associados a ela.</span><span class="sxs-lookup"><span data-stu-id="5b616-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="5b616-114">O mesmo acontece quando uma nova instância da entidade é criada (por exemplo, uma nova instância de réplica do serviço com estado persistente é criada).</span><span class="sxs-lookup"><span data-stu-id="5b616-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="5b616-115">Todos os relatórios associados à instância antiga são excluídos e removidos do repositório.</span><span class="sxs-lookup"><span data-stu-id="5b616-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="5b616-116">Os relatórios de componentes do sistema são identificados por sua origem, que começa com o prefixo "**System.**"</span><span class="sxs-lookup"><span data-stu-id="5b616-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="5b616-117">prefixo.</span><span class="sxs-lookup"><span data-stu-id="5b616-117">prefix.</span></span> <span data-ttu-id="5b616-118">Os watchdogs não podem usar o mesmo prefixo para suas origens, pois os relatórios com parâmetros inválidos são rejeitados.</span><span class="sxs-lookup"><span data-stu-id="5b616-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="5b616-119">Vamos examinar alguns relatórios do sistema para entender o que os dispara e como corrigir possíveis problemas que eles representam.</span><span class="sxs-lookup"><span data-stu-id="5b616-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="5b616-120">O Service Fabric continua adicionando relatórios sobre condições de interesse que melhoram a visibilidade do que está acontecendo no cluster e no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5b616-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="5b616-121">Os relatórios existentes também podem ser aprimorados com mais detalhes para ajudar a solucionar o problema mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="5b616-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="5b616-122">Relatórios de integridade do sistema de cluster</span><span class="sxs-lookup"><span data-stu-id="5b616-122">Cluster system health reports</span></span>
<span data-ttu-id="5b616-123">A entidade de integridade do cluster é criada automaticamente no repositório de integridade.</span><span class="sxs-lookup"><span data-stu-id="5b616-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="5b616-124">Se tudo funcionar corretamente, ele não terá um relatório do sistema.</span><span class="sxs-lookup"><span data-stu-id="5b616-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="5b616-125">Perda de ambiente</span><span class="sxs-lookup"><span data-stu-id="5b616-125">Neighborhood loss</span></span>
<span data-ttu-id="5b616-126">**System.Federation** relata um erro quando detecta uma perda de ambiente.</span><span class="sxs-lookup"><span data-stu-id="5b616-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="5b616-127">O relatório tem origem em nós individuais e a ID do nó é incluída no nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="5b616-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="5b616-128">Caso haja uma perda de ambiente em todo o anel do Service Fabric, geralmente podemos esperar dois eventos (ambos os lados da lacuna serão relatados).</span><span class="sxs-lookup"><span data-stu-id="5b616-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="5b616-129">Se houver mais perdas de ambiente, haverá mais eventos.</span><span class="sxs-lookup"><span data-stu-id="5b616-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="5b616-130">O relatório especifica o tempo limite de concessão global como o tempo de vida útil.</span><span class="sxs-lookup"><span data-stu-id="5b616-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="5b616-131">O relatório é enviado novamente a cada metade da duração do tempo de vida útil, desde que a condição permaneça ativa.</span><span class="sxs-lookup"><span data-stu-id="5b616-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="5b616-132">O evento é removido automaticamente quando expira.</span><span class="sxs-lookup"><span data-stu-id="5b616-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="5b616-133">Remover o comportamento expirado garante que o relatório será removido do repositório de integridade corretamente, mesmo que o nó de relatório esteja inativo.</span><span class="sxs-lookup"><span data-stu-id="5b616-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="5b616-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="5b616-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="5b616-135">**Propriedade**: começa com **Ambiente** e inclui informações sobre o nó</span><span class="sxs-lookup"><span data-stu-id="5b616-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="5b616-136">**Próximas etapas**: investigue por que o ambiente foi perdido (por exemplo, verifique a comunicação entre os nós do cluster).</span><span class="sxs-lookup"><span data-stu-id="5b616-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="5b616-137">Relatórios de integridade do sistema de nó</span><span class="sxs-lookup"><span data-stu-id="5b616-137">Node system health reports</span></span>
<span data-ttu-id="5b616-138">**System.FM**, que representa o serviço Gerenciador de Failover, é a autoridade que gerencia informações sobre nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="5b616-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="5b616-139">Cada nó deve ter um relatório de System.FM mostrando seu estado.</span><span class="sxs-lookup"><span data-stu-id="5b616-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="5b616-140">As entidades de nó são removidas quando o estado do nó é removido (veja [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="5b616-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="5b616-141">Nó ativo/inativo</span><span class="sxs-lookup"><span data-stu-id="5b616-141">Node up/down</span></span>
<span data-ttu-id="5b616-142">System.FM relata OK quando o nó ingressa no anel (está em execução).</span><span class="sxs-lookup"><span data-stu-id="5b616-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="5b616-143">Ele relata um erro quando o nó é removido do anel (ele está desativado, seja para atualização ou simplesmente porque falhou).</span><span class="sxs-lookup"><span data-stu-id="5b616-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="5b616-144">A hierarquia de integridade criada pelo repositório de integridade age nas entidades implantadas em correlação com relatórios de nó do System.FM.</span><span class="sxs-lookup"><span data-stu-id="5b616-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="5b616-145">Ela considera o nó como um pai virtual de todas as entidades implantadas.</span><span class="sxs-lookup"><span data-stu-id="5b616-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="5b616-146">As entidades implantadas nesse nó serão expostas por meio de consultas se o nó for reportado como ativo pelo System.FM, com a mesma instância que aquela associada às entidades.</span><span class="sxs-lookup"><span data-stu-id="5b616-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="5b616-147">Quando System.FM relata o nó inativo ou reiniciado (nova instância), o repositório de integridade remove automaticamente as entidades implantadas que podem existir apenas no nó inativo ou na instância anterior do nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="5b616-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5b616-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5b616-149">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-149">**Property**: State</span></span>
* <span data-ttu-id="5b616-150">**Próximas etapas**: se o nó estiver inativo para uma atualização, ele deverá aparecer novamente depois que for atualizado.</span><span class="sxs-lookup"><span data-stu-id="5b616-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="5b616-151">Nesse caso, o estado de integridade deve ser alternado de volta para OK.</span><span class="sxs-lookup"><span data-stu-id="5b616-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="5b616-152">Se o nó não voltar ou falhar, será preciso investigar mais.</span><span class="sxs-lookup"><span data-stu-id="5b616-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="5b616-153">O exemplo a seguir mostra o evento System.FM com estado de integridade OK para o nó ativo:</span><span class="sxs-lookup"><span data-stu-id="5b616-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="5b616-154">Expiração de certificado</span><span class="sxs-lookup"><span data-stu-id="5b616-154">Certificate expiration</span></span>
<span data-ttu-id="5b616-155">**System.FabricNode** relata um aviso quando os certificados usados pelo nó estão prestes a expirar.</span><span class="sxs-lookup"><span data-stu-id="5b616-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="5b616-156">Há três certificados por nó: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="5b616-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="5b616-157">Quando falta pelo menos duas semanas para expirar, o estado de integridade do relatório é OK.</span><span class="sxs-lookup"><span data-stu-id="5b616-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="5b616-158">Quando a expiração é dentro de duas semanas, o tipo de relatório é um aviso.</span><span class="sxs-lookup"><span data-stu-id="5b616-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="5b616-159">O tempo de vida útil desses eventos é infinito; eles são removidos quando um nó deixa o cluster.</span><span class="sxs-lookup"><span data-stu-id="5b616-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="5b616-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="5b616-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="5b616-161">**Propriedade**: começa com **Certificate** e contém mais informações sobre o tipo de certificado</span><span class="sxs-lookup"><span data-stu-id="5b616-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="5b616-162">**Próximas etapas**: atualize os certificados se eles estiverem prestes a expirar.</span><span class="sxs-lookup"><span data-stu-id="5b616-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="5b616-163">Violação da capacidade de carga</span><span class="sxs-lookup"><span data-stu-id="5b616-163">Load capacity violation</span></span>
<span data-ttu-id="5b616-164">O Service Fabric Load Balancer relata um aviso quando detecta uma violação da capacidade do nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="5b616-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5b616-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5b616-166">**Propriedade**: começa com **Capacity**</span><span class="sxs-lookup"><span data-stu-id="5b616-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="5b616-167">**Próximas etapas**: verifique as métricas fornecidas e exiba a capacidade atual do nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="5b616-168">Relatórios de integridade do sistema de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5b616-168">Application system health reports</span></span>
<span data-ttu-id="5b616-169">**System.CM**, que representa o serviço do Gerenciador de Cluster, é a autoridade que gerencia as informações sobre um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5b616-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="5b616-170">Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-170">State</span></span>
<span data-ttu-id="5b616-171">System.CM relata OK quando o aplicativo é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="5b616-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="5b616-172">Ele informa ao repositório de integridade quando o aplicativo é excluído para que este possa ser removido do repositório.</span><span class="sxs-lookup"><span data-stu-id="5b616-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="5b616-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="5b616-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="5b616-174">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-174">**Property**: State</span></span>
* <span data-ttu-id="5b616-175">**Próximas etapas**: se o aplicativo tiver sido criado ou atualizado, ele deverá incluir o relatório de integridade do Gerenciador de Cluster.</span><span class="sxs-lookup"><span data-stu-id="5b616-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="5b616-176">Caso contrário, verifique o estado do aplicativo emitindo uma consulta (por exemplo, o cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName*** do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5b616-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="5b616-177">O exemplo a seguir mostra o evento de estado no aplicativo **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="5b616-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="5b616-178">Relatórios de integridade do sistema de serviço</span><span class="sxs-lookup"><span data-stu-id="5b616-178">Service system health reports</span></span>
<span data-ttu-id="5b616-179">**System.FM**, que representa o serviço do Gerenciador de Failover, é a autoridade que gerencia as informações sobre serviços.</span><span class="sxs-lookup"><span data-stu-id="5b616-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="5b616-180">Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-180">State</span></span>
<span data-ttu-id="5b616-181">System.FM relata OK quando o serviço é criado.</span><span class="sxs-lookup"><span data-stu-id="5b616-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="5b616-182">Ele exclui a entidade do repositório de integridade quando o serviço é excluído.</span><span class="sxs-lookup"><span data-stu-id="5b616-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="5b616-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5b616-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5b616-184">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-184">**Property**: State</span></span>

<span data-ttu-id="5b616-185">O exemplo a seguir mostra o evento de estado no serviço **fabric:/WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="5b616-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="5b616-186">Erro de correlação de serviço</span><span class="sxs-lookup"><span data-stu-id="5b616-186">Service correlation error</span></span>
<span data-ttu-id="5b616-187">**System.PLB** relata um erro ao detectar que a atualização de um serviço a ser correlacionado com outro serviço cria uma cadeia de afinidade.</span><span class="sxs-lookup"><span data-stu-id="5b616-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="5b616-188">O relatório é limpo quando a atualização é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5b616-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="5b616-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5b616-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5b616-190">**Propriedade**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="5b616-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="5b616-191">**Próximas etapas**: verifique as descrições de serviços correlacionadas.</span><span class="sxs-lookup"><span data-stu-id="5b616-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="5b616-192">Relatórios de integridade do sistema de partição</span><span class="sxs-lookup"><span data-stu-id="5b616-192">Partition system health reports</span></span>
<span data-ttu-id="5b616-193">**System.FM**, que representa o serviço do Gerenciador de Failover, é a autoridade que gerencia as informações sobre partições de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="5b616-194">Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-194">State</span></span>
<span data-ttu-id="5b616-195">System.FM relata OK quando a partição é criada e está íntegra.</span><span class="sxs-lookup"><span data-stu-id="5b616-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="5b616-196">Ele exclui a entidade do repositório de integridade quando a partição é excluída.</span><span class="sxs-lookup"><span data-stu-id="5b616-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="5b616-197">Se a partição estiver abaixo da contagem mínima de réplica, ela relatará um erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="5b616-198">Se a partição não estiver abaixo da contagem mínima de réplica, mas estiver abaixo da contagem de réplica de destino, ele relatará um aviso.</span><span class="sxs-lookup"><span data-stu-id="5b616-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="5b616-199">Se a partição estiver na perda de quórum, o System.FM relatará um erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="5b616-200">Outros eventos importantes incluem avisos quando a reconfiguração demorar mais que o esperado e quando a compilação demorar mais que o esperado.</span><span class="sxs-lookup"><span data-stu-id="5b616-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="5b616-201">Os tempos esperados para compilação ou reconfiguração podem ser configurados baseados nos cenários de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="5b616-202">Por exemplo, se um serviço tem um terabyte de estado, como o Banco de Dados SQL, criá-lo demora mais do que demoraria para um serviço com uma pequena quantidade de estado.</span><span class="sxs-lookup"><span data-stu-id="5b616-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="5b616-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5b616-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5b616-204">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-204">**Property**: State</span></span>
* <span data-ttu-id="5b616-205">**Próximas etapas**: se o estado de integridade não está OK, é possível que algumas réplicas não tenham sido criadas, abertas ou promovidas para o primário ou secundário corretamente.</span><span class="sxs-lookup"><span data-stu-id="5b616-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="5b616-206">Em muitos casos, a causa raiz é um bug de serviço na implementação da função de abertura ou de alteração.</span><span class="sxs-lookup"><span data-stu-id="5b616-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="5b616-207">O exemplo a seguir mostra uma partição íntegra:</span><span class="sxs-lookup"><span data-stu-id="5b616-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="5b616-208">O exemplo a seguir mostra a integridade de uma partição que está abaixo da contagem de réplica de destino.</span><span class="sxs-lookup"><span data-stu-id="5b616-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="5b616-209">A etapa seguinte é obter a descrição da partição, que mostra como ela é configurada: **MinReplicaSetSize** é três e **TargetReplicaSetSize** é sete.</span><span class="sxs-lookup"><span data-stu-id="5b616-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="5b616-210">Em seguida, obtenha o número de nós no cluster: cinco.</span><span class="sxs-lookup"><span data-stu-id="5b616-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="5b616-211">Nesse caso, portanto, duas réplicas não podem ser colocadas porque o número de réplicas de destino é maior do que o número de nós disponíveis.</span><span class="sxs-lookup"><span data-stu-id="5b616-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="5b616-212">Violação da restrição de réplica</span><span class="sxs-lookup"><span data-stu-id="5b616-212">Replica constraint violation</span></span>
<span data-ttu-id="5b616-213">**System.PLB** relata um aviso se detectar uma violação de restrição de réplica e não puder posicionar todas as réplicas da partição.</span><span class="sxs-lookup"><span data-stu-id="5b616-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="5b616-214">Os detalhes do relatório mostram quais restrições e propriedades impedem o posicionamento da réplica.</span><span class="sxs-lookup"><span data-stu-id="5b616-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="5b616-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5b616-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5b616-216">**Propriedade**: começa com **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="5b616-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="5b616-217">Relatórios de integridade do sistema de réplica</span><span class="sxs-lookup"><span data-stu-id="5b616-217">Replica system health reports</span></span>
<span data-ttu-id="5b616-218">**System.RA**, que representa o componente do agente de reconfiguração, é a autoridade do estado da réplica.</span><span class="sxs-lookup"><span data-stu-id="5b616-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="5b616-219">Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-219">State</span></span>
<span data-ttu-id="5b616-220">**System.RA** relata OK quando a réplica é criada.</span><span class="sxs-lookup"><span data-stu-id="5b616-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="5b616-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5b616-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5b616-222">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="5b616-222">**Property**: State</span></span>

<span data-ttu-id="5b616-223">O exemplo a seguir mostra uma réplica íntegra:</span><span class="sxs-lookup"><span data-stu-id="5b616-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="5b616-224">Status aberto da réplica</span><span class="sxs-lookup"><span data-stu-id="5b616-224">Replica open status</span></span>
<span data-ttu-id="5b616-225">A descrição desse relatório de integridade contém a hora de início (UTC) da chamada à API invocada.</span><span class="sxs-lookup"><span data-stu-id="5b616-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="5b616-226">**System.RA** relatará um aviso se a réplica aberta demorar mais que o período configurado (padrão: 30 minutos).</span><span class="sxs-lookup"><span data-stu-id="5b616-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="5b616-227">Quando a API afeta a disponibilidade do serviço, o relatório é emitido muito mais rapidamente (intervalo configurável, padrão de 30 segundos).</span><span class="sxs-lookup"><span data-stu-id="5b616-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="5b616-228">O tempo medido inclui o tempo necessário para abrir o replicador e abrir o serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="5b616-229">A propriedade muda para OK quando a abertura é concluída.</span><span class="sxs-lookup"><span data-stu-id="5b616-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="5b616-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5b616-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5b616-231">**Propriedade**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="5b616-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="5b616-232">**Próximas etapas**: se o estado de integridade não estiver OK, investigue o motivo pelo qual a réplica aberta demora mais que o esperado.</span><span class="sxs-lookup"><span data-stu-id="5b616-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="5b616-233">Chamada à API para serviço lento</span><span class="sxs-lookup"><span data-stu-id="5b616-233">Slow service API call</span></span>
<span data-ttu-id="5b616-234">**System.RAP** e **System.Replicator** relatarão um aviso se uma chamada para o código do serviço do usuário demorar mais que o tempo configurado.</span><span class="sxs-lookup"><span data-stu-id="5b616-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="5b616-235">Esse status é removido quando a chamada é concluída.</span><span class="sxs-lookup"><span data-stu-id="5b616-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="5b616-236">**SourceId**: System.RAP ou System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5b616-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="5b616-237">**Propriedade**: o nome da API lenta.</span><span class="sxs-lookup"><span data-stu-id="5b616-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="5b616-238">A descrição fornece mais detalhes sobre o tempo em que a API esteve pendente.</span><span class="sxs-lookup"><span data-stu-id="5b616-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="5b616-239">**Próximas etapas**: investigue o motivo pelo qual a chamada demora mais que o esperado.</span><span class="sxs-lookup"><span data-stu-id="5b616-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="5b616-240">O exemplo a seguir mostra uma partição na perda de quórum e as etapas de investigação realizadas para entender o motivo.</span><span class="sxs-lookup"><span data-stu-id="5b616-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="5b616-241">Uma das réplicas tem o estado de integridade de aviso; portanto, obtemos sua integridade.</span><span class="sxs-lookup"><span data-stu-id="5b616-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="5b616-242">Ele mostra que a operação do serviço demora mais que o esperado, um evento relatado por System.RAP.</span><span class="sxs-lookup"><span data-stu-id="5b616-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="5b616-243">Depois que a informação é recebida, a próxima etapa será examinar o código de serviço e investigá-lo.</span><span class="sxs-lookup"><span data-stu-id="5b616-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="5b616-244">Nesse caso, a implementação de **RunAsync** do serviço com estado gera uma exceção sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="5b616-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="5b616-245">As réplicas são recicladas, de modo que você não pode ver nenhuma réplica no estado de aviso.</span><span class="sxs-lookup"><span data-stu-id="5b616-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="5b616-246">Você pode tentar novamente obter o estado de integridade e examinar as diferenças na ID de réplica.</span><span class="sxs-lookup"><span data-stu-id="5b616-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="5b616-247">Em alguns casos, as novas tentativas podem lhe dar pistas.</span><span class="sxs-lookup"><span data-stu-id="5b616-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="5b616-248">Ao iniciar o aplicativo com defeito no depurador, as janelas Eventos de Diagnóstico mostram a exceção lançada por RunAsync:</span><span class="sxs-lookup"><span data-stu-id="5b616-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="5b616-250">Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="5b616-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="5b616-251">Fila de replicação cheia</span><span class="sxs-lookup"><span data-stu-id="5b616-251">Replication queue full</span></span>
<span data-ttu-id="5b616-252">**System.Replicator** relata um aviso quando a fila de replicação está cheia.</span><span class="sxs-lookup"><span data-stu-id="5b616-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="5b616-253">Na réplica primária, a fila de replicação normalmente fica cheia porque uma ou mais réplicas secundárias são lentas confirmar as operações.</span><span class="sxs-lookup"><span data-stu-id="5b616-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="5b616-254">No local secundário, isso geralmente acontece quando o serviço está lento para aplicar as operações.</span><span class="sxs-lookup"><span data-stu-id="5b616-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="5b616-255">O aviso será removido quando a fila não estiver mais cheia.</span><span class="sxs-lookup"><span data-stu-id="5b616-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="5b616-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5b616-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="5b616-257">**Propriedade**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, dependendo da função da réplica</span><span class="sxs-lookup"><span data-stu-id="5b616-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="5b616-258">Operações de Nomeação lentas</span><span class="sxs-lookup"><span data-stu-id="5b616-258">Slow Naming operations</span></span>
<span data-ttu-id="5b616-259">**System.NamingService** relata a integridade na réplica primária quando uma operação de nomenclatura demora mais do que o aceitável.</span><span class="sxs-lookup"><span data-stu-id="5b616-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="5b616-260">Exemplos de operações de Nomeação: [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) ou [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="5b616-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="5b616-261">Mais métodos podem ser encontrados em FabricClient, por exemplo, em [métodos de gerenciamento do serviço](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou [métodos de gerenciamento de propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="5b616-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="5b616-262">O serviço de nomenclatura resolve nomes de serviço para um local no cluster e permite aos usuários gerenciar propriedades e nomes de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="5b616-263">É um serviço persistentes particionado pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b616-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="5b616-264">Uma das partições representa o proprietário da autoridade, que contém metadados sobre todos os nomes e serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5b616-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="5b616-265">Os nomes do Service Fabric são mapeados para partições diferentes, chamadas de partições de Proprietário de Nome, assim, o serviço é extensível.</span><span class="sxs-lookup"><span data-stu-id="5b616-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="5b616-266">Leia mais sobre o [Serviço de nomeação](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="5b616-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="5b616-267">Quando uma operação de nomeação leva mais tempo do que o esperado, a operação é sinalizada com um relatório de Aviso na *réplica primária da partição de serviço de nomeação que atende à operação*.</span><span class="sxs-lookup"><span data-stu-id="5b616-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="5b616-268">Se a operação for concluída com êxito, o Aviso será limpo.</span><span class="sxs-lookup"><span data-stu-id="5b616-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="5b616-269">Se a operação for concluída com um erro, o relatório de integridade incluirá detalhes sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="5b616-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="5b616-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="5b616-271">**Propriedade**: começa com o prefixo **Duration_** e identifica a operação lenta e o nome do Service Fabric em que a operação é aplicada.</span><span class="sxs-lookup"><span data-stu-id="5b616-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="5b616-272">Por exemplo, se a criação de um serviço em name fabric: /MyApp/MyService levar muito tempo, a propriedade será Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="5b616-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="5b616-273">AO aponta para a função da partição de nomeação para esse nome e a operação.</span><span class="sxs-lookup"><span data-stu-id="5b616-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="5b616-274">**Próximas etapas**: verifique por que a operação de nomeação falha.</span><span class="sxs-lookup"><span data-stu-id="5b616-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="5b616-275">Cada operação pode ter causas raiz diferentes.</span><span class="sxs-lookup"><span data-stu-id="5b616-275">Each operation can have different root causes.</span></span> <span data-ttu-id="5b616-276">Por exemplo, a exclusão de serviço pode estar bloqueado em um nó porque o host do aplicativo falha em um nó devido a um bug de usuário no código de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="5b616-277">O exemplo a seguir mostra uma operação de criação de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b616-277">The following example shows a create service operation.</span></span> <span data-ttu-id="5b616-278">A operação demorou mais do que a duração configurada.</span><span class="sxs-lookup"><span data-stu-id="5b616-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="5b616-279">AO tenta novamente e envia o trabalho para NO.</span><span class="sxs-lookup"><span data-stu-id="5b616-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="5b616-280">NO concluiu a última operação com Tempo limite.</span><span class="sxs-lookup"><span data-stu-id="5b616-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="5b616-281">Nesse caso, a mesma réplica é primária para as funções AO e NO.</span><span class="sxs-lookup"><span data-stu-id="5b616-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="5b616-282">Relatórios de integridade do sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="5b616-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="5b616-283">**System.Hosting** é a autoridade nas entidades implantadas.</span><span class="sxs-lookup"><span data-stu-id="5b616-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="5b616-284">Ativação</span><span class="sxs-lookup"><span data-stu-id="5b616-284">Activation</span></span>
<span data-ttu-id="5b616-285">System.Hosting relata OK quando um aplicativo é ativado com êxito no nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="5b616-286">Caso contrário, ele relata um erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5b616-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-288">**Propriedade**: ativação, incluindo a versão de distribuição</span><span class="sxs-lookup"><span data-stu-id="5b616-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="5b616-289">**Próximas etapas**: se o aplicativo não estiver íntegro, investigue o motivo pelo qual a ativação falhou.</span><span class="sxs-lookup"><span data-stu-id="5b616-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="5b616-290">O exemplo a seguir mostra uma ativação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="5b616-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5b616-291">Baixar</span><span class="sxs-lookup"><span data-stu-id="5b616-291">Download</span></span>
<span data-ttu-id="5b616-292">**System.Hosting** relatará um erro se o download do pacote de aplicativos falhar.</span><span class="sxs-lookup"><span data-stu-id="5b616-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="5b616-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-294">**Propriedade**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5b616-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5b616-295">**Próximas etapas**: investigue o motivo pelo qual o download falhou no nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="5b616-296">Relatórios de integridade do sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="5b616-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="5b616-297">**System.Hosting** é a autoridade nas entidades implantadas.</span><span class="sxs-lookup"><span data-stu-id="5b616-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="5b616-298">Ativação do pacote de serviço</span><span class="sxs-lookup"><span data-stu-id="5b616-298">Service package activation</span></span>
<span data-ttu-id="5b616-299">System.Hosting relatará OK se a ativação do pacote de serviço no nó for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5b616-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="5b616-300">Caso contrário, ele relata um erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5b616-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-302">**Propriedade**: ativação</span><span class="sxs-lookup"><span data-stu-id="5b616-302">**Property**: Activation</span></span>
* <span data-ttu-id="5b616-303">**Próximas etapas**: investigue o motivo pelo qual a ativação falhou.</span><span class="sxs-lookup"><span data-stu-id="5b616-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="5b616-304">Ativação do pacote de códigos</span><span class="sxs-lookup"><span data-stu-id="5b616-304">Code package activation</span></span>
<span data-ttu-id="5b616-305">**System.Hosting** relatará OK para cada pacote de códigos se a ativação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5b616-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="5b616-306">Se houver falha na ativação, ele relatará um aviso conforme configurado.</span><span class="sxs-lookup"><span data-stu-id="5b616-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="5b616-307">Se **CodePackage** falhar em ativar ou terminar com um erro maior que o **CodePackageHealthErrorThreshold** configurado, a hospedagem relatará um erro.</span><span class="sxs-lookup"><span data-stu-id="5b616-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="5b616-308">Se um pacote de serviço contiver vários pacotes de código, um relatório de ativação será gerado para cada um.</span><span class="sxs-lookup"><span data-stu-id="5b616-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="5b616-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-310">**Propriedade**: usa o prefixo **CodePackageActivation** e contém o nome do pacote de códigos e o ponto de entrada como **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (por exemplo, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="5b616-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="5b616-311">Registro do tipo de serviço</span><span class="sxs-lookup"><span data-stu-id="5b616-311">Service type registration</span></span>
<span data-ttu-id="5b616-312">**System.Hosting** relatará OK se o tipo de serviço for registrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="5b616-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="5b616-313">Ele relatará um erro se o registro não foi feito pontualmente (conforme configurado usando **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="5b616-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="5b616-314">Se o tempo de execução estiver fechado, o tipo de serviço não estará registrado no nó e Hospedagem relatará um aviso.</span><span class="sxs-lookup"><span data-stu-id="5b616-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="5b616-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-316">**Propriedade**: usa o prefixo **ServiceTypeRegistration** e contém o nome do tipo de serviço (por exemplo, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="5b616-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="5b616-317">O exemplo a seguir mostra um pacote de serviço íntegro implantado:</span><span class="sxs-lookup"><span data-stu-id="5b616-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5b616-318">Baixar</span><span class="sxs-lookup"><span data-stu-id="5b616-318">Download</span></span>
<span data-ttu-id="5b616-319">**System.Hosting** relatará um erro se o download do pacote de serviço falhar.</span><span class="sxs-lookup"><span data-stu-id="5b616-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="5b616-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-321">**Propriedade**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5b616-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5b616-322">**Próximas etapas**: investigue o motivo pelo qual o download falhou no nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="5b616-323">Validação da atualização</span><span class="sxs-lookup"><span data-stu-id="5b616-323">Upgrade validation</span></span>
<span data-ttu-id="5b616-324">**System.Hosting** relatará um erro se a validação durante a atualização falhar ou se a atualização falhar no nó.</span><span class="sxs-lookup"><span data-stu-id="5b616-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="5b616-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5b616-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5b616-326">**Propriedade**: usa o prefixo **FabricUpgradeValidation** e contém a versão de atualização</span><span class="sxs-lookup"><span data-stu-id="5b616-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="5b616-327">**Descrição**: aponta para o erro encontrado</span><span class="sxs-lookup"><span data-stu-id="5b616-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b616-328">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b616-328">Next steps</span></span>
[<span data-ttu-id="5b616-329">Como exibir relatórios de integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b616-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="5b616-330">Como relatar e verificar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="5b616-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="5b616-331">Monitorar e diagnosticar serviços localmente</span><span class="sxs-lookup"><span data-stu-id="5b616-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="5b616-332">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5b616-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

