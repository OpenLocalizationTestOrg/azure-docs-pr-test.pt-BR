---
title: "aaaTroubleshoot com relatórios de integridade do sistema | Microsoft Docs"
description: "Descreve os relatórios de integridade Olá enviados pelos componentes do Azure Service Fabric e seu uso para solução de problemas de cluster ou problemas de aplicativos."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="d2142-103">Usar tootroubleshoot de relatórios de integridade do sistema</span><span class="sxs-lookup"><span data-stu-id="d2142-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="d2142-104">Relatório do Azure Service Fabric componentes imediato saudação em todas as entidades no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="d2142-105">Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) cria e exclui entidades com base em relatórios de saudação do sistema.</span><span class="sxs-lookup"><span data-stu-id="d2142-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="d2142-106">Ele também os organiza em uma hierarquia que captura interações de entidade.</span><span class="sxs-lookup"><span data-stu-id="d2142-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="d2142-107">conceitos relacionados à integridade toounderstand, leia mais em [modelo de integridade da malha do serviço](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2142-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="d2142-108">Os relatórios de integridade do sistema fornecem visibilidade da funcionalidade do cluster e de aplicativos e sinalizam problemas por meio da integridade.</span><span class="sxs-lookup"><span data-stu-id="d2142-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="d2142-109">Para aplicativos e serviços, relatórios de integridade do sistema, verifique se que entidades foram implementadas e estão funcionando corretamente da saudação perspectiva do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2142-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="d2142-110">relatórios de saudação não fornecem nenhum monitoramento de integridade de lógica de negócios de saudação do serviço hello ou detecção de processos travados.</span><span class="sxs-lookup"><span data-stu-id="d2142-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="d2142-111">Serviços de usuário podem enriquecer os dados de integridade de saudação com lógica de tootheir específicos de informações.</span><span class="sxs-lookup"><span data-stu-id="d2142-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="d2142-112">Relatórios de integridade watchdogs são visíveis apenas *depois* componentes do sistema Olá criam uma entidade.</span><span class="sxs-lookup"><span data-stu-id="d2142-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="d2142-113">Quando uma entidade é excluída, o repositório de integridade Olá exclui automaticamente todos os relatórios de integridade associados a ele.</span><span class="sxs-lookup"><span data-stu-id="d2142-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="d2142-114">Olá mesmo é verdadeiro quando é criada uma nova instância da entidade de saudação (por exemplo, uma nova instância de réplica com monitoração de estado de serviço persistente é criada).</span><span class="sxs-lookup"><span data-stu-id="d2142-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="d2142-115">Todos os relatórios associados a instância antiga Olá são excluídos e limpos do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="d2142-116">Olá relatórios de componente do sistema são identificados pela origem hello, que inicia com hello "**System.**"</span><span class="sxs-lookup"><span data-stu-id="d2142-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="d2142-117">prefixo.</span><span class="sxs-lookup"><span data-stu-id="d2142-117">prefix.</span></span> <span data-ttu-id="d2142-118">Watchdogs não podem usar o hello mesmo prefixo para suas fontes, como relatórios com parâmetros inválidos são rejeitados.</span><span class="sxs-lookup"><span data-stu-id="d2142-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="d2142-119">Vamos examinar alguns relatórios toounderstand que faz com que elas e como toocorrect Olá possíveis problemas que eles representam.</span><span class="sxs-lookup"><span data-stu-id="d2142-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="d2142-120">Service Fabric continua tooadd relatórios sobre as condições de interesse que melhorar a visibilidade sobre o que está acontecendo no aplicativo e o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="d2142-121">Os relatórios existentes também podem ser aprimorados com mais detalhes toohelp solucionar problema hello mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="d2142-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="d2142-122">Relatórios de integridade do sistema de cluster</span><span class="sxs-lookup"><span data-stu-id="d2142-122">Cluster system health reports</span></span>
<span data-ttu-id="d2142-123">entidade de integridade do cluster Olá é criada automaticamente no repositório de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="d2142-124">Se tudo funcionar corretamente, ele não terá um relatório do sistema.</span><span class="sxs-lookup"><span data-stu-id="d2142-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="d2142-125">Perda de ambiente</span><span class="sxs-lookup"><span data-stu-id="d2142-125">Neighborhood loss</span></span>
<span data-ttu-id="d2142-126">**System.Federation** relata um erro quando detecta uma perda de ambiente.</span><span class="sxs-lookup"><span data-stu-id="d2142-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="d2142-127">relatório de saudação for de nós individuais e Olá a ID do nó está incluída no nome da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="d2142-128">Se um ambiente é perdido no anel de malha do serviço inteiro hello, normalmente, haverá dois eventos (ambos os lados do relatório de intervalo de saudação).</span><span class="sxs-lookup"><span data-stu-id="d2142-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="d2142-129">Se houver mais perdas de ambiente, haverá mais eventos.</span><span class="sxs-lookup"><span data-stu-id="d2142-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="d2142-130">relatório de Olá Especifica o tempo limite de concessão global hello como tempo de saudação toolive.</span><span class="sxs-lookup"><span data-stu-id="d2142-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="d2142-131">relatório de saudação é reenviado cada metade da duração de tempo de vida de saudação de como condição Olá permanece ativa.</span><span class="sxs-lookup"><span data-stu-id="d2142-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="d2142-132">evento de saudação é removido automaticamente quando ela expirar.</span><span class="sxs-lookup"><span data-stu-id="d2142-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="d2142-133">Remova ao comportamento expirado garante que relatório Olá é limpos do repositório de integridade Olá corretamente, mesmo se o nó reporting hello está inativo.</span><span class="sxs-lookup"><span data-stu-id="d2142-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="d2142-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="d2142-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="d2142-135">**Propriedade**: começa com **Ambiente** e inclui informações sobre o nó</span><span class="sxs-lookup"><span data-stu-id="d2142-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="d2142-136">**Próximas etapas**: investigar por que o ambiente de saudação for perdido (por exemplo, verificar Olá comunicação entre nós de cluster).</span><span class="sxs-lookup"><span data-stu-id="d2142-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="d2142-137">Relatórios de integridade do sistema de nó</span><span class="sxs-lookup"><span data-stu-id="d2142-137">Node system health reports</span></span>
<span data-ttu-id="d2142-138">**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="d2142-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="d2142-139">Cada nó deve ter um relatório de System.FM mostrando seu estado.</span><span class="sxs-lookup"><span data-stu-id="d2142-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="d2142-140">entidades de nó Olá são removidas quando o estado do nó Olá é removido (consulte [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="d2142-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="d2142-141">Nó ativo/inativo</span><span class="sxs-lookup"><span data-stu-id="d2142-141">Node up/down</span></span>
<span data-ttu-id="d2142-142">System.FM informa como Okey ao nó Olá une anel hello (estiver em execução).</span><span class="sxs-lookup"><span data-stu-id="d2142-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="d2142-143">Ele relata um erro ao nó Olá entregas de anel hello (ele estiver inativo, seja para atualizar ou simplesmente porque ele falhou).</span><span class="sxs-lookup"><span data-stu-id="d2142-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="d2142-144">hierarquia de integridade Olá criada pelo repositório de integridade Olá age em entidades implantadas em correlação com relatórios de nó System.FM.</span><span class="sxs-lookup"><span data-stu-id="d2142-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="d2142-145">Ele considera nó Olá virtual pai de todas as entidades implantados.</span><span class="sxs-lookup"><span data-stu-id="d2142-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="d2142-146">entidades Olá implantado nesse nó são expostas por meio de consultas se o nó Olá é relatada como backup por System.FM, com hello mesmo a instância como instância Olá associada com entidades de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="d2142-147">Ao System.FM relatórios a nó hello está desligado ou reiniciado (uma nova instância), repositório de integridade Olá limpa automaticamente entidades Olá implantado que podem existir somente Olá para baixo de nó ou na instância anterior de saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="d2142-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d2142-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d2142-149">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-149">**Property**: State</span></span>
* <span data-ttu-id="d2142-150">**Próximas etapas**: se o nó de saudação está inativo para uma atualização, ele deve voltar depois que ele foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="d2142-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="d2142-151">Nesse caso, o estado de integridade de saudação deve alternar tooOK back.</span><span class="sxs-lookup"><span data-stu-id="d2142-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="d2142-152">Se o nó de saudação não voltar ou falhar, problema de saudação precisa de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="d2142-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="d2142-153">Olá exemplo a seguir mostra Olá System.FM evento com um estado de integridade de Okey para o nó de:</span><span class="sxs-lookup"><span data-stu-id="d2142-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="d2142-154">Expiração de certificado</span><span class="sxs-lookup"><span data-stu-id="d2142-154">Certificate expiration</span></span>
<span data-ttu-id="d2142-155">**System.FabricNode** relata um aviso quando certificados usados por nó Olá estão prestes a expirar.</span><span class="sxs-lookup"><span data-stu-id="d2142-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="d2142-156">Há três certificados por nó: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="d2142-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="d2142-157">Quando a expiração de saudação é pelo menos duas semanas, o estado de integridade de relatório de saudação é Okey.</span><span class="sxs-lookup"><span data-stu-id="d2142-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="d2142-158">Quando a expiração Olá estiver dentro de duas semanas, o tipo de relatório de saudação é um aviso.</span><span class="sxs-lookup"><span data-stu-id="d2142-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="d2142-159">TTL desses eventos é infinito, e eles são removidos quando sai de um nó de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="d2142-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="d2142-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="d2142-161">**Propriedade**: começa com **certificado** e contém mais informações sobre o tipo de certificado Olá</span><span class="sxs-lookup"><span data-stu-id="d2142-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="d2142-162">**Próximas etapas**: atualizar certificados de saudação se eles estiverem perto da expiração.</span><span class="sxs-lookup"><span data-stu-id="d2142-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="d2142-163">Violação da capacidade de carga</span><span class="sxs-lookup"><span data-stu-id="d2142-163">Load capacity violation</span></span>
<span data-ttu-id="d2142-164">Olá balanceador de carga de malha do serviço relata um aviso quando detecta uma violação de capacidade do nó.</span><span class="sxs-lookup"><span data-stu-id="d2142-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="d2142-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d2142-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d2142-166">**Propriedade**: começa com **Capacity**</span><span class="sxs-lookup"><span data-stu-id="d2142-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="d2142-167">**Próximas etapas**: seleção fornecido capacidade atual de métricas e exibição Olá no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="d2142-168">Relatórios de integridade do sistema de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2142-168">Application system health reports</span></span>
<span data-ttu-id="d2142-169">**System.CM**, que representa o serviço de Gerenciador de Cluster de hello, Olá autoridade que gerencia informações sobre um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2142-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="d2142-170">Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-170">State</span></span>
<span data-ttu-id="d2142-171">System.CM informa como Okey quando o aplicativo hello foi criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="d2142-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="d2142-172">Ele informa repositório de integridade hello quando o aplicativo hello foi excluído, para que ele pode ser removido do repositório.</span><span class="sxs-lookup"><span data-stu-id="d2142-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="d2142-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="d2142-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="d2142-174">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-174">**Property**: State</span></span>
* <span data-ttu-id="d2142-175">**Próximas etapas**: se o aplicativo hello foi criado ou atualizado, ele deve incluir o relatório de integridade do Gerenciador de Cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="d2142-176">Caso contrário, verifique o estado de saudação do aplicativo hello emitindo uma consulta (por exemplo, Olá cmdlet do PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="d2142-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="d2142-177">Olá exemplo a seguir mostra o evento de estado Olá em hello **fabric: / WordCount** aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d2142-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="d2142-178">Relatórios de integridade do sistema de serviço</span><span class="sxs-lookup"><span data-stu-id="d2142-178">Service system health reports</span></span>
<span data-ttu-id="d2142-179">**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre os serviços.</span><span class="sxs-lookup"><span data-stu-id="d2142-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="d2142-180">Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-180">State</span></span>
<span data-ttu-id="d2142-181">System.FM informa como Okey quando Olá serviço foi criado.</span><span class="sxs-lookup"><span data-stu-id="d2142-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="d2142-182">Ele exclui entidade saudação do repositório de integridade hello quando o serviço de saudação foi excluído.</span><span class="sxs-lookup"><span data-stu-id="d2142-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="d2142-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d2142-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d2142-184">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-184">**Property**: State</span></span>

<span data-ttu-id="d2142-185">Olá exemplo a seguir mostra o evento de estado Olá no serviço de saudação **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="d2142-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="d2142-186">Erro de correlação de serviço</span><span class="sxs-lookup"><span data-stu-id="d2142-186">Service correlation error</span></span>
<span data-ttu-id="d2142-187">**System.PLB** relata um erro quando detecta que um toobe serviço correlacionada com outro serviço de atualização cria uma cadeia de afinidade.</span><span class="sxs-lookup"><span data-stu-id="d2142-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="d2142-188">relatório de saudação é limpo quando ocorre a atualização bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d2142-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="d2142-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d2142-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d2142-190">**Propriedade**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="d2142-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="d2142-191">**Próximas etapas**: seleção Olá correlacionados descrições de serviços.</span><span class="sxs-lookup"><span data-stu-id="d2142-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="d2142-192">Relatórios de integridade do sistema de partição</span><span class="sxs-lookup"><span data-stu-id="d2142-192">Partition system health reports</span></span>
<span data-ttu-id="d2142-193">**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre partições de serviço.</span><span class="sxs-lookup"><span data-stu-id="d2142-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="d2142-194">Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-194">State</span></span>
<span data-ttu-id="d2142-195">System.FM informa como Okey quando a partição Olá foi criada e está íntegra.</span><span class="sxs-lookup"><span data-stu-id="d2142-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="d2142-196">Ele exclui entidade saudação do repositório de integridade hello quando Olá partição será excluída.</span><span class="sxs-lookup"><span data-stu-id="d2142-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="d2142-197">Se a partição Olá está abaixo da contagem de réplica mínimo hello, ele relata um erro.</span><span class="sxs-lookup"><span data-stu-id="d2142-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="d2142-198">Se Olá partição não está abaixo da contagem de réplica mínimo hello, mas está abaixo da contagem de réplica de destino hello, ele relata um aviso.</span><span class="sxs-lookup"><span data-stu-id="d2142-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="d2142-199">Se a partição de saudação está em perda de quorum, System.FM relata um erro.</span><span class="sxs-lookup"><span data-stu-id="d2142-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="d2142-200">Outros eventos importantes incluem um aviso quando a reconfiguração de saudação leva mais tempo do que o esperado e quando a compilação Olá demora mais do que o esperado.</span><span class="sxs-lookup"><span data-stu-id="d2142-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="d2142-201">tempos de saudação esperado para compilação hello e reconfiguração são configuráveis com base em cenários de serviço.</span><span class="sxs-lookup"><span data-stu-id="d2142-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="d2142-202">Por exemplo, se um serviço tem um terabyte de estado, como o banco de dados SQL, compilação Olá leva mais tempo do que para um serviço com uma pequena quantidade de estado.</span><span class="sxs-lookup"><span data-stu-id="d2142-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="d2142-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d2142-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d2142-204">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-204">**Property**: State</span></span>
* <span data-ttu-id="d2142-205">**Próximas etapas**: se o estado de integridade de saudação não for Okey, é possível que algumas réplicas não foram criado, aberto ou promovida tooprimary ou secundário corretamente.</span><span class="sxs-lookup"><span data-stu-id="d2142-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="d2142-206">Em muitos casos, Olá principal causa é um bug de serviço no hello aberta ou na implementação de função de alteração.</span><span class="sxs-lookup"><span data-stu-id="d2142-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="d2142-207">saudação de exemplo a seguir mostra uma partição íntegra:</span><span class="sxs-lookup"><span data-stu-id="d2142-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="d2142-208">Olá exemplo a seguir mostra a integridade saudação de uma partição que está abaixo da contagem de réplica de destino.</span><span class="sxs-lookup"><span data-stu-id="d2142-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="d2142-209">Olá próxima etapa é tooget Olá descrição da partição, que mostra como estiver configurado: **MinReplicaSetSize** é três e **TargetReplicaSetSize** é sete.</span><span class="sxs-lookup"><span data-stu-id="d2142-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="d2142-210">Em seguida, obter o número de Olá de nós no cluster Olá: cinco.</span><span class="sxs-lookup"><span data-stu-id="d2142-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="d2142-211">Portanto nesse caso, duas réplicas não podem ser armazenadas porque o número de destino de saudação de réplicas é maior do que o número de saudação de nós disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d2142-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="replica-constraint-violation"></a><span data-ttu-id="d2142-212">Violação da restrição de réplica</span><span class="sxs-lookup"><span data-stu-id="d2142-212">Replica constraint violation</span></span>
<span data-ttu-id="d2142-213">**System.PLB** relata um aviso se detectar uma violação de restrição de réplica e não puder posicionar todas as réplicas da partição.</span><span class="sxs-lookup"><span data-stu-id="d2142-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="d2142-214">detalhes do relatório Olá mostram quais restrições e propriedades de evitar que o posicionamento de réplica de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="d2142-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d2142-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d2142-216">**Propriedade**: começa com **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="d2142-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="d2142-217">Relatórios de integridade do sistema de réplica</span><span class="sxs-lookup"><span data-stu-id="d2142-217">Replica system health reports</span></span>
<span data-ttu-id="d2142-218">**System.RA**, que representa o componente do agente de reconfiguração Olá, é a autoridade de saudação para estado da réplica hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="d2142-219">Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-219">State</span></span>
<span data-ttu-id="d2142-220">**System.RA** relata Okey quando Olá réplica foi criada.</span><span class="sxs-lookup"><span data-stu-id="d2142-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="d2142-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="d2142-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="d2142-222">**Propriedade**: Estado</span><span class="sxs-lookup"><span data-stu-id="d2142-222">**Property**: State</span></span>

<span data-ttu-id="d2142-223">saudação de exemplo a seguir mostra uma réplica íntegra:</span><span class="sxs-lookup"><span data-stu-id="d2142-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="d2142-224">Status aberto da réplica</span><span class="sxs-lookup"><span data-stu-id="d2142-224">Replica open status</span></span>
<span data-ttu-id="d2142-225">Descrição de saudação deste relatório de integridade contém a hora de início da saudação (Coordinated Universal Time) quando chamada Olá API foi chamada.</span><span class="sxs-lookup"><span data-stu-id="d2142-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="d2142-226">**System.RA** relata um aviso se a réplica de saudação abrir demora mais do que o período Olá configurado (padrão: 30 minutos).</span><span class="sxs-lookup"><span data-stu-id="d2142-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="d2142-227">Se Olá API afeta a disponibilidade do serviço, o relatório de saudação é emitido muito mais rápido (um intervalo configurável, com um padrão de 30 segundos).</span><span class="sxs-lookup"><span data-stu-id="d2142-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="d2142-228">medida de tempo de saudação inclui tempo Olá para o replicador de saudação aberto e o serviço de Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="d2142-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="d2142-229">Olá tooOK de alterações de propriedade se abrir Olá completa.</span><span class="sxs-lookup"><span data-stu-id="d2142-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="d2142-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="d2142-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="d2142-231">**Propriedade**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="d2142-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="d2142-232">**Próximas etapas**: se o estado de integridade de saudação não for Okey, investigue por que a réplica de saudação abrir demora mais do que esperado.</span><span class="sxs-lookup"><span data-stu-id="d2142-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="d2142-233">Chamada à API para serviço lento</span><span class="sxs-lookup"><span data-stu-id="d2142-233">Slow service API call</span></span>
<span data-ttu-id="d2142-234">**System.RAP** e **System.Replicator** relatar um aviso se um código de serviço chamada toohello usuário demora mais do que o tempo de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="d2142-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="d2142-235">Aviso de saudação é limpo quando Olá chamada é concluída.</span><span class="sxs-lookup"><span data-stu-id="d2142-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="d2142-236">**SourceId**: System.RAP ou System.Replicator</span><span class="sxs-lookup"><span data-stu-id="d2142-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="d2142-237">**Propriedade**: nome de saudação da API lenta hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="d2142-238">Descrição de saudação fornece mais detalhes sobre a saudação de tempo Olá API foi pendente.</span><span class="sxs-lookup"><span data-stu-id="d2142-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="d2142-239">**Próximas etapas**: investigar por que a chamada de saudação demora mais do que esperado.</span><span class="sxs-lookup"><span data-stu-id="d2142-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="d2142-240">saudação de exemplo a seguir mostra uma partição em perda de quorum e Olá investigação etapas feitas toofigure o motivo.</span><span class="sxs-lookup"><span data-stu-id="d2142-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="d2142-241">Uma das réplicas de saudação tem um estado de integridade de aviso, para que você obtenha sua integridade.</span><span class="sxs-lookup"><span data-stu-id="d2142-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="d2142-242">Ele mostra que operação de serviço Olá leva mais tempo do que o esperado, um evento relatado pelo System.RAP.</span><span class="sxs-lookup"><span data-stu-id="d2142-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="d2142-243">Depois que essas informações são recebidas, o hello próxima etapa é toolook no código de serviço hello e investigar existe.</span><span class="sxs-lookup"><span data-stu-id="d2142-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="d2142-244">Nesse caso, Olá **RunAsync** implementação de serviço com monitoração de estado Olá lança uma exceção sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="d2142-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="d2142-245">réplicas de saudação são Reciclando, talvez você não veja todas as réplicas em estado de aviso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="d2142-246">Você pode tentar novamente obter estado de integridade de saudação e examinar as diferenças na ID de réplica hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="d2142-247">Em certos casos, repetições Olá podem fornecer pistas.</span><span class="sxs-lookup"><span data-stu-id="d2142-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="d2142-248">Quando você inicia o aplicativo com defeito hello sob depurador Olá, o windows de eventos de diagnóstico de saudação mostram exceção de saudação do RunAsync:</span><span class="sxs-lookup"><span data-stu-id="d2142-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="d2142-250">Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="d2142-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="d2142-251">Fila de replicação cheia</span><span class="sxs-lookup"><span data-stu-id="d2142-251">Replication queue full</span></span>
<span data-ttu-id="d2142-252">**System.Replicator** relata um aviso quando a fila de replicação hello está cheia.</span><span class="sxs-lookup"><span data-stu-id="d2142-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="d2142-253">Em Olá primário, fila de replicação normalmente fica cheio porque uma ou mais réplicas secundárias são operações tooacknowledge lenta.</span><span class="sxs-lookup"><span data-stu-id="d2142-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="d2142-254">Em Olá secundário, isso geralmente acontece quando o serviço hello está lenta tooapply Olá operações.</span><span class="sxs-lookup"><span data-stu-id="d2142-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="d2142-255">Aviso de saudação é limpo quando a fila de saudação não esteja mais cheio.</span><span class="sxs-lookup"><span data-stu-id="d2142-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="d2142-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="d2142-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="d2142-257">**Propriedade**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, dependendo da função de réplica Olá</span><span class="sxs-lookup"><span data-stu-id="d2142-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="d2142-258">Operações de Nomeação lentas</span><span class="sxs-lookup"><span data-stu-id="d2142-258">Slow Naming operations</span></span>
<span data-ttu-id="d2142-259">**System.NamingService** relata a integridade na réplica primária quando uma operação de nomenclatura demora mais do que o aceitável.</span><span class="sxs-lookup"><span data-stu-id="d2142-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="d2142-260">Exemplos de operações de Nomeação: [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) ou [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="d2142-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="d2142-261">Mais métodos podem ser encontrados em FabricClient, por exemplo, em [métodos de gerenciamento do serviço](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou [métodos de gerenciamento de propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="d2142-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="d2142-262">Olá Naming service resolve local tooa do serviço de nomes de cluster hello e permite que propriedades e nomes de serviço toomanage de usuários.</span><span class="sxs-lookup"><span data-stu-id="d2142-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="d2142-263">É um serviço persistentes particionado pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2142-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="d2142-264">Uma das partições Olá representa Olá proprietário da autoridade, que contém metadados sobre todos os nomes de serviço de malha e serviços.</span><span class="sxs-lookup"><span data-stu-id="d2142-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="d2142-265">nomes de Service Fabric do Hello são mapeadas toodifferent partições, chamadas partições do proprietário do nome, portanto, o serviço de saudação extensível.</span><span class="sxs-lookup"><span data-stu-id="d2142-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="d2142-266">Leia mais sobre o [Serviço de nomeação](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="d2142-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="d2142-267">Quando uma operação de nomenclatura leva mais tempo do que o esperado, operação Olá será sinalizada com um relatório de aviso em Olá *réplica primária do hello nomear a partição de serviço que serve a operação de saudação*.</span><span class="sxs-lookup"><span data-stu-id="d2142-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="d2142-268">Se a operação de saudação for concluída com êxito, hello aviso está desmarcado.</span><span class="sxs-lookup"><span data-stu-id="d2142-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="d2142-269">Se a conclusão da operação de saudação com um erro, o relatório de integridade Olá inclui detalhes sobre o erro hello.</span><span class="sxs-lookup"><span data-stu-id="d2142-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="d2142-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="d2142-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="d2142-271">**Propriedade**: começa com o prefixo **Duration_** e identifica a operação lenta hello e o nome de malha do serviço Olá quais Olá operação é aplicada.</span><span class="sxs-lookup"><span data-stu-id="d2142-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="d2142-272">Por exemplo, se criar um serviço na malha de nome: / MyApp/MyService leva muito tempo, a propriedade de saudação é Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="d2142-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="d2142-273">Função de toohello sol pontos de saudação partição de nomenclatura para o nome e a operação.</span><span class="sxs-lookup"><span data-stu-id="d2142-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="d2142-274">**Próximas etapas**: seleção por Olá nomenclatura operação falha.</span><span class="sxs-lookup"><span data-stu-id="d2142-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="d2142-275">Cada operação pode ter causas raiz diferentes.</span><span class="sxs-lookup"><span data-stu-id="d2142-275">Each operation can have different root causes.</span></span> <span data-ttu-id="d2142-276">Por exemplo, excluir o serviço pode estar preso em um nó, porque o host de aplicativo hello fica falhando em um nó devido tooa bug de usuário no código de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="d2142-277">saudação de exemplo a seguir mostra uma operação de criação do serviço.</span><span class="sxs-lookup"><span data-stu-id="d2142-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="d2142-278">operação de saudação demorou mais do que a duração de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="d2142-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="d2142-279">AO tentar novamente e envia tooNO de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d2142-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="d2142-280">Nenhuma operação última Olá concluída com tempo limite.</span><span class="sxs-lookup"><span data-stu-id="d2142-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="d2142-281">Nesse caso, hello mesma réplica é a principal para Olá sol e nenhuma função.</span><span class="sxs-lookup"><span data-stu-id="d2142-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="d2142-282">Relatórios de integridade do sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="d2142-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="d2142-283">**System.Hosting** é Olá autoridade em entidades implantadas.</span><span class="sxs-lookup"><span data-stu-id="d2142-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="d2142-284">Ativação</span><span class="sxs-lookup"><span data-stu-id="d2142-284">Activation</span></span>
<span data-ttu-id="d2142-285">System.Hosting informa como Okey quando um aplicativo foi ativado com êxito no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="d2142-286">Caso contrário, ele relata um erro.</span><span class="sxs-lookup"><span data-stu-id="d2142-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="d2142-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-288">**Propriedade**: ativação, incluindo a versão de distribuição Olá</span><span class="sxs-lookup"><span data-stu-id="d2142-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="d2142-289">**Próximas etapas**: se o aplicativo hello não está íntegro, investigar por que a ativação de saudação falhou.</span><span class="sxs-lookup"><span data-stu-id="d2142-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="d2142-290">saudação de ativação bem-sucedida do exemplo mostra a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2142-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="d2142-291">Baixar</span><span class="sxs-lookup"><span data-stu-id="d2142-291">Download</span></span>
<span data-ttu-id="d2142-292">**System.Hosting** relata um erro se o download do pacote de aplicativo hello falhar.</span><span class="sxs-lookup"><span data-stu-id="d2142-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="d2142-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-294">**Propriedade**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="d2142-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="d2142-295">**Próximas etapas**: investigar por que o download de saudação falhou no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="d2142-296">Relatórios de integridade do sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="d2142-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="d2142-297">**System.Hosting** é Olá autoridade em entidades implantadas.</span><span class="sxs-lookup"><span data-stu-id="d2142-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="d2142-298">Ativação do pacote de serviço</span><span class="sxs-lookup"><span data-stu-id="d2142-298">Service package activation</span></span>
<span data-ttu-id="d2142-299">System.Hosting informa como Okey se a ativação do pacote de serviço Olá no nó de saudação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d2142-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="d2142-300">Caso contrário, ele relata um erro.</span><span class="sxs-lookup"><span data-stu-id="d2142-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="d2142-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-302">**Propriedade**: ativação</span><span class="sxs-lookup"><span data-stu-id="d2142-302">**Property**: Activation</span></span>
* <span data-ttu-id="d2142-303">**Próximas etapas**: investigar por que a ativação de saudação falhou.</span><span class="sxs-lookup"><span data-stu-id="d2142-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="d2142-304">Ativação do pacote de códigos</span><span class="sxs-lookup"><span data-stu-id="d2142-304">Code package activation</span></span>
<span data-ttu-id="d2142-305">**System.Hosting** informa como Okey para cada pacote de código se saudação de ativação é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d2142-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="d2142-306">Se a ativação Olá falhar, ele relata um aviso como configurado.</span><span class="sxs-lookup"><span data-stu-id="d2142-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="d2142-307">Se **CodePackage** falhar tooactivate ou termina com um erro maior Olá configurado **CodePackageHealthErrorThreshold**, hospedagem relata um erro.</span><span class="sxs-lookup"><span data-stu-id="d2142-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="d2142-308">Se um pacote de serviço contiver vários pacotes de código, um relatório de ativação será gerado para cada um.</span><span class="sxs-lookup"><span data-stu-id="d2142-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="d2142-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-310">**Propriedade**: prefixo de saudação usa **CodePackageActivation** e contém o nome de saudação do pacote de códigos hello e ponto de entrada hello como  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint** * (por exemplo, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="d2142-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="d2142-311">Registro do tipo de serviço</span><span class="sxs-lookup"><span data-stu-id="d2142-311">Service type registration</span></span>
<span data-ttu-id="d2142-312">**System.Hosting** informa como Okey se o tipo de serviço Olá foi registrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d2142-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="d2142-313">Ele relata um erro se Olá registro não foi feito no tempo (configurado usando **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="d2142-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="d2142-314">Se Olá runtime estiver fechada, o tipo de serviço Olá é cancelar o registro do nó de saudação e hospedagem relata um aviso.</span><span class="sxs-lookup"><span data-stu-id="d2142-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="d2142-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-316">**Propriedade**: prefixo de saudação usa **ServiceTypeRegistration** e contém o nome do tipo de serviço de saudação (por exemplo, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="d2142-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="d2142-317">saudação de exemplo a seguir mostra um pacote de serviço implantado Íntegro:</span><span class="sxs-lookup"><span data-stu-id="d2142-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="d2142-318">Baixar</span><span class="sxs-lookup"><span data-stu-id="d2142-318">Download</span></span>
<span data-ttu-id="d2142-319">**System.Hosting** relata um erro se o download do pacote de serviço Olá falhar.</span><span class="sxs-lookup"><span data-stu-id="d2142-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="d2142-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-321">**Propriedade**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="d2142-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="d2142-322">**Próximas etapas**: investigar por que o download de saudação falhou no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="d2142-323">Validação da atualização</span><span class="sxs-lookup"><span data-stu-id="d2142-323">Upgrade validation</span></span>
<span data-ttu-id="d2142-324">**System.Hosting** relata um erro se houver falha na validação durante a atualização de saudação ou se hello atualização falha no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2142-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="d2142-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d2142-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d2142-326">**Propriedade**: prefixo de saudação usa **FabricUpgradeValidation** e contém a versão de atualização de saudação</span><span class="sxs-lookup"><span data-stu-id="d2142-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="d2142-327">**Descrição**: pontos toohello erro</span><span class="sxs-lookup"><span data-stu-id="d2142-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2142-328">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2142-328">Next steps</span></span>
[<span data-ttu-id="d2142-329">Como exibir relatórios de integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2142-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="d2142-330">Como tooreport e verificação de integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="d2142-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="d2142-331">Monitorar e diagnosticar serviços localmente</span><span class="sxs-lookup"><span data-stu-id="d2142-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="d2142-332">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d2142-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

