---
title: aaaScheduled eventos para VMs do Windows no Azure | Microsoft Docs
description: "Eventos agendados usando o serviço de metadados do Azure Olá para em suas máquinas virtuais do Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="32643-103">Serviço de Metadados do Azure: Eventos Agendados (versão prévia) para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="32643-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="32643-104">Visualizações são feitas tooyou disponível em condição de saudação concordar toohello termos de uso.</span><span class="sxs-lookup"><span data-stu-id="32643-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="32643-105">Para obter mais informações, consulte [Termos de Uso Complementares do Microsoft Azure para Visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="32643-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="32643-106">Eventos agendados é uma saudação subserviços em hello Azure metadados de serviço.</span><span class="sxs-lookup"><span data-stu-id="32643-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="32643-107">Ele responsável por identificar informações sobre eventos futuros (por exemplo, reiniciar) para que seu aplicativo possa se preparar para eles e limitar a interrupção.</span><span class="sxs-lookup"><span data-stu-id="32643-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="32643-108">Estão disponíveis para todos os tipos de Máquina Virtual do Azure, incluindo PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="32643-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="32643-109">Eventos agendados dá toominimize Olá efeito um evento de suas tarefas tooperform preventivas de tempo de máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="32643-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="32643-110">Os eventos agendados estão disponíveis para Linux e VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="32643-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="32643-111">Para saber mais sobre os Eventos Agendados no Linux, confira [Eventos agendados para VMs do Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="32643-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="32643-112">Por que Eventos Agendados?</span><span class="sxs-lookup"><span data-stu-id="32643-112">Why Scheduled Events?</span></span>

<span data-ttu-id="32643-113">Com os eventos agendados, você pode adotar medidas impacto de saudação do toolimit de plataforma intiated manutenção ou ações iniciadas pelo usuário em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="32643-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="32643-114">Cargas de trabalho de várias instâncias, que usam o estado da replicação técnicas toomaintain, podem ser vulnerável toooutages acontecendo em várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="32643-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="32643-115">Tais interrupções podem resultar em tarefas caras (por exemplo, recompilação de índices) ou até mesmo na perda de uma réplica.</span><span class="sxs-lookup"><span data-stu-id="32643-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="32643-116">Em muitos casos, hello geral disponibilidade do serviço pode ser melhorada pela execução de uma sequência de desligamento normal como concluídas (ou cancelamento) transações em andamento, reatribuindo tarefas tooother VMs no cluster hello (failover manual) ou removendo Olá Máquina virtual de um pool de Balanceador de carga de rede.</span><span class="sxs-lookup"><span data-stu-id="32643-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="32643-117">Há casos onde notificando um administrador sobre um evento futuro ou registro em log um evento ajudar a melhorar a facilidade de manutenção de saudação de aplicativos hospedados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="32643-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="32643-118">Casos de uso do Azure Metadata Service superfícies agendado eventos no seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="32643-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="32643-119">Manutenção iniciada na plataforma (por exemplo, distribuição do sistema operacional do Host)</span><span class="sxs-lookup"><span data-stu-id="32643-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="32643-120">Chamadas iniciadas pelo usuário (por exemplo, o usuário reinicia ou reimplanta uma VM)</span><span class="sxs-lookup"><span data-stu-id="32643-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="32643-121">Noções básicas de saudação</span><span class="sxs-lookup"><span data-stu-id="32643-121">hello basics</span></span>  

<span data-ttu-id="32643-122">Serviço de metadados do Azure expõe informações sobre a execução de máquinas virtuais usando um ponto de extremidade de REST podem ser acessados no hello VM.</span><span class="sxs-lookup"><span data-stu-id="32643-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="32643-123">informações de saudação estão disponíveis por meio de um IP não roteável para que ele não é exposto fora Olá VM.</span><span class="sxs-lookup"><span data-stu-id="32643-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="32643-124">Escopo</span><span class="sxs-lookup"><span data-stu-id="32643-124">Scope</span></span>
<span data-ttu-id="32643-125">Eventos agendados são tooall da superfície máquinas virtuais em um serviço de nuvem ou tooall máquinas virtuais em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="32643-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="32643-126">Como resultado, você deve verificar Olá `Resources` campo Olá evento tooidentify que máquinas virtuais serão toobe afetado.</span><span class="sxs-lookup"><span data-stu-id="32643-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="32643-127">Descobrir ponto de extremidade Olá</span><span class="sxs-lookup"><span data-stu-id="32643-127">Discovering hello endpoint</span></span>
<span data-ttu-id="32643-128">No caso de Olá onde uma máquina Virtual é criada em uma rede Virtual (VNet), o serviço de metadados de hello está disponível de um IP não roteável estático, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="32643-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="32643-129">Se Olá Máquina Virtual não é criado em uma rede Virtual, casos de padrão de saudação para serviços de nuvem e VMs clássicas, lógica adicional é necessário toodiscover toouse de ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="32643-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="32643-130">Consulte toothis exemplo toolearn como muito[descobrir o ponto de extremidade do hello host](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="32643-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="32643-131">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="32643-131">Versioning</span></span> 
<span data-ttu-id="32643-132">Olá serviço de metadados de instância é com controle de versão.</span><span class="sxs-lookup"><span data-stu-id="32643-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="32643-133">As versões são obrigatórias e Olá a versão atual é `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="32643-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="32643-134">Versões anteriores de visualização de eventos agendados suportados {mais recente} como Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="32643-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="32643-135">Esse formato não é mais suportado e será substituído em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="32643-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="32643-136">Uso de cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="32643-136">Using headers</span></span>
<span data-ttu-id="32643-137">Quando você consulta Olá Metadata Service, você deve fornecer o cabeçalho Olá `Metadata: true` solicitação de saudação tooensure não foi redirecionada acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="32643-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="32643-138">Habilitar Eventos Agendados</span><span class="sxs-lookup"><span data-stu-id="32643-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="32643-139">Olá primeira vez que você faz uma solicitação para eventos agendados, Azure implicitamente habilita Olá recurso em sua máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="32643-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="32643-140">Como resultado, você deve esperar uma resposta atrasada em sua primeira chamada do backup tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="32643-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="32643-141">Manutenção iniciada pelo usuário</span><span class="sxs-lookup"><span data-stu-id="32643-141">User initiated maintenance</span></span>
<span data-ttu-id="32643-142">Manutenção de máquinas virtuais por meio de saudação portal do Azure, API, CLI, iniciada pelo usuário ou o PowerShell resulta em um evento agendado.</span><span class="sxs-lookup"><span data-stu-id="32643-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="32643-143">Isso permite que você tootest lógica de preparação de manutenção de saudação em seu aplicativo e permite tooprepare seu aplicativo para manutenção iniciada pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="32643-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="32643-144">Reiniciar uma máquina virtual agendará um evento com tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="32643-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="32643-145">Reimplantar uma máquina virtual agendará um evento com tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="32643-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="32643-146">No momento, no máximo 10 operações de manutenção iniciadas pelo usuário podem ser agendadas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="32643-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="32643-147">Esse limite será aliviado antes da disponibilidade geral de Eventos Agendados.</span><span class="sxs-lookup"><span data-stu-id="32643-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="32643-148">A manutenção iniciada pelo usuário que resulta em Eventos Agendados no momento não é configurável.</span><span class="sxs-lookup"><span data-stu-id="32643-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="32643-149">A capacidade de configuração está prevista para uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="32643-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="32643-150">Usando a API de saudação</span><span class="sxs-lookup"><span data-stu-id="32643-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="32643-151">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="32643-151">Query for events</span></span>
<span data-ttu-id="32643-152">Você pode consultar eventos agendados simplesmente fazendo Olá seguinte chamada:</span><span class="sxs-lookup"><span data-stu-id="32643-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="32643-153">Uma resposta contém uma matriz de eventos agendados.</span><span class="sxs-lookup"><span data-stu-id="32643-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="32643-154">Uma matriz vazia significa que não há eventos agendados no momento.</span><span class="sxs-lookup"><span data-stu-id="32643-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="32643-155">No caso de Olá onde há eventos agendados, resposta Olá contém uma matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="32643-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="32643-156">Propriedades do evento</span><span class="sxs-lookup"><span data-stu-id="32643-156">Event properties</span></span>
|<span data-ttu-id="32643-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="32643-157">Property</span></span>  |  <span data-ttu-id="32643-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="32643-158">Description</span></span> |
| - | - |
| <span data-ttu-id="32643-159">EventId</span><span class="sxs-lookup"><span data-stu-id="32643-159">EventId</span></span> | <span data-ttu-id="32643-160">Identificador global exclusivo para esse evento.</span><span class="sxs-lookup"><span data-stu-id="32643-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="32643-161">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="32643-161">Example:</span></span> <br><ul><li><span data-ttu-id="32643-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="32643-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="32643-163">EventType</span><span class="sxs-lookup"><span data-stu-id="32643-163">EventType</span></span> | <span data-ttu-id="32643-164">Impacto desse evento.</span><span class="sxs-lookup"><span data-stu-id="32643-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="32643-165">Valores:</span><span class="sxs-lookup"><span data-stu-id="32643-165">Values:</span></span> <br><ul><li> <span data-ttu-id="32643-166">`Freeze`: Olá Máquina Virtual é agendado toopause por alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="32643-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="32643-167">Olá CPU está suspenso, mas não há nenhum impacto na memória, arquivos abertos ou conexões de rede.</span><span class="sxs-lookup"><span data-stu-id="32643-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="32643-168">`Reboot`: Olá Máquina Virtual está agendada para reinicialização (a memória não persistente é perdida).</span><span class="sxs-lookup"><span data-stu-id="32643-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="32643-169">`Redeploy`: Olá Máquina Virtual é agendado toomove tooanother nó (efêmeros discos são perdidos).</span><span class="sxs-lookup"><span data-stu-id="32643-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="32643-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="32643-170">ResourceType</span></span> | <span data-ttu-id="32643-171">Tipo de recurso que esse evento impacta.</span><span class="sxs-lookup"><span data-stu-id="32643-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="32643-172">Valores:</span><span class="sxs-lookup"><span data-stu-id="32643-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="32643-173">Recursos</span><span class="sxs-lookup"><span data-stu-id="32643-173">Resources</span></span>| <span data-ttu-id="32643-174">Lista de recursos que esse evento impacta.</span><span class="sxs-lookup"><span data-stu-id="32643-174">List of resources this event impacts.</span></span> <span data-ttu-id="32643-175">Isso é garantido toocontain máquinas de no máximo uma [domínio de atualização](manage-availability.md), mas não pode conter todas as máquinas no hello UD.</span><span class="sxs-lookup"><span data-stu-id="32643-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="32643-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="32643-176">Example:</span></span> <br><ul><li> <span data-ttu-id="32643-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="32643-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="32643-178">Status do evento</span><span class="sxs-lookup"><span data-stu-id="32643-178">Event Status</span></span> | <span data-ttu-id="32643-179">Status desse evento.</span><span class="sxs-lookup"><span data-stu-id="32643-179">Status of this event.</span></span> <br><br> <span data-ttu-id="32643-180">Valores:</span><span class="sxs-lookup"><span data-stu-id="32643-180">Values:</span></span> <ul><li><span data-ttu-id="32643-181">`Scheduled`: Esse evento é agendado toostart depois de tempo de saudação especificado no hello `NotBefore` propriedade.</span><span class="sxs-lookup"><span data-stu-id="32643-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="32643-182">`Started`: esse evento foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="32643-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="32643-183">Não `Completed` ou status semelhante já é fornecido; evento Olá não será retornado quando o evento de saudação é concluído.</span><span class="sxs-lookup"><span data-stu-id="32643-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="32643-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="32643-184">NotBefore</span></span>| <span data-ttu-id="32643-185">Tempo após o qual esse evento poderá começar.</span><span class="sxs-lookup"><span data-stu-id="32643-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="32643-186">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="32643-186">Example:</span></span> <br><ul><li> <span data-ttu-id="32643-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="32643-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="32643-188">Agendamento do evento</span><span class="sxs-lookup"><span data-stu-id="32643-188">Event scheduling</span></span>
<span data-ttu-id="32643-189">Cada evento é agendado uma quantidade mínima de tempo em Olá futuro com base no tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="32643-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="32643-190">Esse tempo é refletido na propriedades `NotBefore` de um evento.</span><span class="sxs-lookup"><span data-stu-id="32643-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="32643-191">EventType</span><span class="sxs-lookup"><span data-stu-id="32643-191">EventType</span></span>  | <span data-ttu-id="32643-192">Aviso mínimo</span><span class="sxs-lookup"><span data-stu-id="32643-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="32643-193">Congelamento</span><span class="sxs-lookup"><span data-stu-id="32643-193">Freeze</span></span>| <span data-ttu-id="32643-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="32643-194">15 minutes</span></span> |
| <span data-ttu-id="32643-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="32643-195">Reboot</span></span> | <span data-ttu-id="32643-196">15 minutos</span><span class="sxs-lookup"><span data-stu-id="32643-196">15 minutes</span></span> |
| <span data-ttu-id="32643-197">Reimplantar</span><span class="sxs-lookup"><span data-stu-id="32643-197">Redeploy</span></span> | <span data-ttu-id="32643-198">10 minutos</span><span class="sxs-lookup"><span data-stu-id="32643-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="32643-199">Como iniciar um evento</span><span class="sxs-lookup"><span data-stu-id="32643-199">Starting an event</span></span> 

<span data-ttu-id="32643-200">Depois que você tem conhecimento de um evento futuro e concluiu sua lógica de desligamento normal, você pode aprovar eventos pendentes Olá fazendo uma `POST` chamar o serviço de metadados toohello com hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="32643-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="32643-201">Isso indica tooAzure que ele pode diminuir notificação mínimo Olá tempo (quando for possível).</span><span class="sxs-lookup"><span data-stu-id="32643-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="32643-202">Confirmar um evento permite Olá evento tooproceed para todos os `Resources` no evento hello, não apenas Olá máquina virtual que reconhece o evento hello.</span><span class="sxs-lookup"><span data-stu-id="32643-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="32643-203">Portanto, você pode escolher tooelect uma confirmação de saudação do líder toocoordinate, que pode ser tão simple quanto a primeira máquina Olá em Olá `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="32643-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="32643-204">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="32643-204">PowerShell sample</span></span> 

<span data-ttu-id="32643-205">Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="32643-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="32643-206">Exemplo de C\#</span><span class="sxs-lookup"><span data-stu-id="32643-206">C\# sample</span></span> 

<span data-ttu-id="32643-207">Olá exemplo a seguir é de um cliente simple que se comunica com o serviço de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="32643-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="32643-208">Eventos agendados podem ser representados usando Olá estruturas de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="32643-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="32643-209">Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="32643-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="32643-210">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="32643-210">Python sample</span></span> 

<span data-ttu-id="32643-211">Olá exemplos de consultas a seguir Olá metadados de serviço para eventos agendados e aprova a cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="32643-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="32643-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32643-212">Next steps</span></span> 

- <span data-ttu-id="32643-213">Leia mais sobre Olá APIs disponíveis no hello [o serviço de metadados de instância](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="32643-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="32643-214">Saiba mais sobre a [manutenção planejada para máquinas virtuais do Windows no Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="32643-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

