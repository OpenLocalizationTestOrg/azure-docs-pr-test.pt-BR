---
title: Eventos agendados para VMs do Windows no Azure | Microsoft Docs
description: "Agendado eventos usando o serviço de metadados do Azure para em suas máquinas virtuais do Windows."
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
ms.openlocfilehash: 7198fa8d1a512d10ca7022078aa2ea7bde3a4c02
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="d8585-103">Serviço de Metadados do Azure: Eventos Agendados (versão prévia) para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="d8585-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="d8585-104">As visualizações são disponibilizadas a você se concordar com os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="d8585-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="d8585-105">Para obter mais informações, consulte [Termos de Uso Complementares do Microsoft Azure para Visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="d8585-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="d8585-106">Eventos Agendados é um dos subserviços no Serviço de Metadados do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8585-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="d8585-107">Ele responsável por identificar informações sobre eventos futuros (por exemplo, reiniciar) para que seu aplicativo possa se preparar para eles e limitar a interrupção.</span><span class="sxs-lookup"><span data-stu-id="d8585-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="d8585-108">Estão disponíveis para todos os tipos de Máquina Virtual do Azure, incluindo PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="d8585-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="d8585-109">Os Eventos Agendados fornecem seu tempo de Máquina Virtual para executar tarefas preventivas, de modo a minimizar o efeito de um evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="d8585-110">Os eventos agendados estão disponíveis para Linux e VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="d8585-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="d8585-111">Para saber mais sobre os Eventos Agendados no Linux, confira [Eventos agendados para VMs do Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="d8585-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="d8585-112">Por que Eventos Agendados?</span><span class="sxs-lookup"><span data-stu-id="d8585-112">Why Scheduled Events?</span></span>

<span data-ttu-id="d8585-113">Com os Eventos Agendados é possível tomar medidas para limitar o impacto da manutenção iniciada na plataforma ou ações iniciadas pelo usuário em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d8585-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="d8585-114">Cargas de trabalho de várias instâncias, que usam técnicas de replicação para manter o estado, podem estar vulneráveis a interrupções que ocorrem em diversas instâncias.</span><span class="sxs-lookup"><span data-stu-id="d8585-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="d8585-115">Tais interrupções podem resultar em tarefas caras (por exemplo, recompilação de índices) ou até mesmo na perda de uma réplica.</span><span class="sxs-lookup"><span data-stu-id="d8585-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="d8585-116">Em muitos outros casos, a disponibilidade geral do serviço pode ser melhorada ao executar uma sequência de desligamento normal, como concluir (ou cancelar) transações em andamento, reatribuir tarefas a outras VMs no cluster (failover manual) ou remover a Máquina Virtual de um pool de balanceador de carga de rede.</span><span class="sxs-lookup"><span data-stu-id="d8585-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="d8585-117">Há casos em que a notificação de um administrador sobre um evento futuro ou o registro desse evento ajudam a melhorar a capacidade de manutenção de aplicativos hospedados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d8585-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="d8585-118">O Serviço de Metadados do Azure revela Eventos Agendados nos seguintes casos de uso:</span><span class="sxs-lookup"><span data-stu-id="d8585-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="d8585-119">Manutenção iniciada na plataforma (por exemplo, distribuição do sistema operacional do Host)</span><span class="sxs-lookup"><span data-stu-id="d8585-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="d8585-120">Chamadas iniciadas pelo usuário (por exemplo, o usuário reinicia ou reimplanta uma VM)</span><span class="sxs-lookup"><span data-stu-id="d8585-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="d8585-121">Noções básicas</span><span class="sxs-lookup"><span data-stu-id="d8585-121">The basics</span></span>  

<span data-ttu-id="d8585-122">O Serviço de Metadados do Azure expõe informações sobre a execução de Máquinas Virtuais usando um Ponto de Extremidade REST acessível de dentro da VM.</span><span class="sxs-lookup"><span data-stu-id="d8585-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="d8585-123">As informações estão disponíveis por meio de um IP não roteável para que ele não seja exposto fora da VM.</span><span class="sxs-lookup"><span data-stu-id="d8585-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="d8585-124">Escopo</span><span class="sxs-lookup"><span data-stu-id="d8585-124">Scope</span></span>
<span data-ttu-id="d8585-125">Eventos agendados são exibidos para todas as máquinas virtuais em um serviço de nuvem ou para todas as máquinas virtuais em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d8585-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="d8585-126">Como resultado, você deve verificar o campo `Resources` no evento para identificar quais VMs serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="d8585-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="d8585-127">Descoberta do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="d8585-127">Discovering the endpoint</span></span>
<span data-ttu-id="d8585-128">No caso em que uma máquina virtual é criada em uma VNet (Rede Virtual), o serviço de metadados está disponível a partir de um IP não roteável estático, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="d8585-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="d8585-129">Se a Máquina Virtual não for criada em uma Rede Virtual, casos padrão para serviços de nuvem e VMs clássicas, uma lógica adicional será necessária para descobrir o ponto de extremidade a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="d8585-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="d8585-130">Consulte esse exemplo para saber como [descobrir o ponto de extremidade do host](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="d8585-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="d8585-131">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="d8585-131">Versioning</span></span> 
<span data-ttu-id="d8585-132">O Serviço de Metadados de Instância tem controle de versão.</span><span class="sxs-lookup"><span data-stu-id="d8585-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="d8585-133">As versões são obrigatórias e a versão atual é `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="d8585-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d8585-134">Versões de visualização anteriores de eventos agendados compatíveis {mais recentes} como a api-version.</span><span class="sxs-lookup"><span data-stu-id="d8585-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="d8585-135">Esse formato não é mais suportado e será substituído no futuro.</span><span class="sxs-lookup"><span data-stu-id="d8585-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="d8585-136">Uso de cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="d8585-136">Using headers</span></span>
<span data-ttu-id="d8585-137">Ao consultar o Serviço de Metadados você deverá fornecer o cabeçalho `Metadata: true` para garantir que a solicitação não foi redirecionada de forma involuntária.</span><span class="sxs-lookup"><span data-stu-id="d8585-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="d8585-138">Habilitar Eventos Agendados</span><span class="sxs-lookup"><span data-stu-id="d8585-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="d8585-139">Na primeira vez em que fizer uma solicitação de eventos programados, o Azure habilitará implicitamente o recurso em sua Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d8585-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="d8585-140">Como resultado, você deve esperar um atraso na resposta em sua primeira chamada de até dois minutos.</span><span class="sxs-lookup"><span data-stu-id="d8585-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="d8585-141">Manutenção iniciada pelo usuário</span><span class="sxs-lookup"><span data-stu-id="d8585-141">User initiated maintenance</span></span>
<span data-ttu-id="d8585-142">A manutenção de máquinas virtuais iniciada pelo usuário pelo portal do Azure, API, CLI ou PowerShell resulta em um evento agendado.</span><span class="sxs-lookup"><span data-stu-id="d8585-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="d8585-143">Isso permite que você teste a lógica de preparação de manutenção em seu aplicativo e permite que seu aplicativo se prepare para manutenção iniciada pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="d8585-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="d8585-144">Reiniciar uma máquina virtual agendará um evento com tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="d8585-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="d8585-145">Reimplantar uma máquina virtual agendará um evento com tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="d8585-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d8585-146">No momento, no máximo 10 operações de manutenção iniciadas pelo usuário podem ser agendadas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d8585-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="d8585-147">Esse limite será aliviado antes da disponibilidade geral de Eventos Agendados.</span><span class="sxs-lookup"><span data-stu-id="d8585-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="d8585-148">A manutenção iniciada pelo usuário que resulta em Eventos Agendados no momento não é configurável.</span><span class="sxs-lookup"><span data-stu-id="d8585-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="d8585-149">A capacidade de configuração está prevista para uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="d8585-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="d8585-150">Usando a API</span><span class="sxs-lookup"><span data-stu-id="d8585-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="d8585-151">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="d8585-151">Query for events</span></span>
<span data-ttu-id="d8585-152">Você pode consultar Eventos agendados realizando a chamada a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8585-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="d8585-153">Uma resposta contém uma matriz de eventos agendados.</span><span class="sxs-lookup"><span data-stu-id="d8585-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="d8585-154">Uma matriz vazia significa que não há eventos agendados no momento.</span><span class="sxs-lookup"><span data-stu-id="d8585-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="d8585-155">No caso de haver eventos agendados, a resposta contém uma matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="d8585-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="d8585-156">Propriedades do evento</span><span class="sxs-lookup"><span data-stu-id="d8585-156">Event properties</span></span>
|<span data-ttu-id="d8585-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d8585-157">Property</span></span>  |  <span data-ttu-id="d8585-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="d8585-158">Description</span></span> |
| - | - |
| <span data-ttu-id="d8585-159">EventId</span><span class="sxs-lookup"><span data-stu-id="d8585-159">EventId</span></span> | <span data-ttu-id="d8585-160">Identificador global exclusivo para esse evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="d8585-161">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d8585-161">Example:</span></span> <br><ul><li><span data-ttu-id="d8585-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="d8585-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="d8585-163">EventType</span><span class="sxs-lookup"><span data-stu-id="d8585-163">EventType</span></span> | <span data-ttu-id="d8585-164">Impacto desse evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="d8585-165">Valores:</span><span class="sxs-lookup"><span data-stu-id="d8585-165">Values:</span></span> <br><ul><li> <span data-ttu-id="d8585-166">`Freeze`: a máquina virtual está agendada para pausar por alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="d8585-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="d8585-167">A CPU é suspensa, mas não há nenhum impacto na memória, em arquivos abertos ou em conexões de rede.</span><span class="sxs-lookup"><span data-stu-id="d8585-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="d8585-168">`Reboot`: a Máquina Virtual está agendada para reiniciar (a memória é apagada).</span><span class="sxs-lookup"><span data-stu-id="d8585-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="d8585-169">`Redeploy`: a Máquina Virtual está agendada para ser movida para outro nó (os discos efêmeros são perdidos).</span><span class="sxs-lookup"><span data-stu-id="d8585-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="d8585-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d8585-170">ResourceType</span></span> | <span data-ttu-id="d8585-171">Tipo de recurso que esse evento impacta.</span><span class="sxs-lookup"><span data-stu-id="d8585-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="d8585-172">Valores:</span><span class="sxs-lookup"><span data-stu-id="d8585-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="d8585-173">Recursos</span><span class="sxs-lookup"><span data-stu-id="d8585-173">Resources</span></span>| <span data-ttu-id="d8585-174">Lista de recursos que esse evento impacta.</span><span class="sxs-lookup"><span data-stu-id="d8585-174">List of resources this event impacts.</span></span> <span data-ttu-id="d8585-175">Isso é garantido para conter máquinas de no máximo um [Domínio de Atualização](manage-availability.md), mas pode não conter todas as máquinas no UD.</span><span class="sxs-lookup"><span data-stu-id="d8585-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="d8585-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d8585-176">Example:</span></span> <br><ul><li> <span data-ttu-id="d8585-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="d8585-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="d8585-178">Status do evento</span><span class="sxs-lookup"><span data-stu-id="d8585-178">Event Status</span></span> | <span data-ttu-id="d8585-179">Status desse evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-179">Status of this event.</span></span> <br><br> <span data-ttu-id="d8585-180">Valores:</span><span class="sxs-lookup"><span data-stu-id="d8585-180">Values:</span></span> <ul><li><span data-ttu-id="d8585-181">`Scheduled`: esse evento está agendado para iniciar após o tempo especificado na propriedade `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="d8585-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="d8585-182">`Started`: esse evento foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="d8585-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="d8585-183">Não `Completed` status semelhante já foi fornecido; o evento não será mais retornado quando o evento for concluído.</span><span class="sxs-lookup"><span data-stu-id="d8585-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="d8585-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="d8585-184">NotBefore</span></span>| <span data-ttu-id="d8585-185">Tempo após o qual esse evento poderá começar.</span><span class="sxs-lookup"><span data-stu-id="d8585-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="d8585-186">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d8585-186">Example:</span></span> <br><ul><li> <span data-ttu-id="d8585-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="d8585-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="d8585-188">Agendamento do evento</span><span class="sxs-lookup"><span data-stu-id="d8585-188">Event scheduling</span></span>
<span data-ttu-id="d8585-189">Cada evento é agendado uma quantidade mínima de tempo no futuro com base no tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="d8585-190">Esse tempo é refletido na propriedades `NotBefore` de um evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="d8585-191">EventType</span><span class="sxs-lookup"><span data-stu-id="d8585-191">EventType</span></span>  | <span data-ttu-id="d8585-192">Aviso mínimo</span><span class="sxs-lookup"><span data-stu-id="d8585-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="d8585-193">Congelamento</span><span class="sxs-lookup"><span data-stu-id="d8585-193">Freeze</span></span>| <span data-ttu-id="d8585-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="d8585-194">15 minutes</span></span> |
| <span data-ttu-id="d8585-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="d8585-195">Reboot</span></span> | <span data-ttu-id="d8585-196">15 minutos</span><span class="sxs-lookup"><span data-stu-id="d8585-196">15 minutes</span></span> |
| <span data-ttu-id="d8585-197">Reimplantar</span><span class="sxs-lookup"><span data-stu-id="d8585-197">Redeploy</span></span> | <span data-ttu-id="d8585-198">10 minutos</span><span class="sxs-lookup"><span data-stu-id="d8585-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="d8585-199">Como iniciar um evento</span><span class="sxs-lookup"><span data-stu-id="d8585-199">Starting an event</span></span> 

<span data-ttu-id="d8585-200">Após a descoberta de um evento futuro e concluído sua lógica de desligamento normal, você poderá aprovar o evento pendente fazendo uma chamada `POST` para o serviço de metadados com `EventId`.</span><span class="sxs-lookup"><span data-stu-id="d8585-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="d8585-201">Isso indica para o Azure que ele pode encurtar o tempo mínimo de notificação (quando possível).</span><span class="sxs-lookup"><span data-stu-id="d8585-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="d8585-202">Reconhecer um evento permite que o evento prossiga para todos `Resources` no evento, e não apenas a máquina virtual que reconhece o evento.</span><span class="sxs-lookup"><span data-stu-id="d8585-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="d8585-203">Portanto, é possível eleger um líder para coordenar o reconhecimento, que pode ser tão simples como a primeira máquina no campo `Resources`.</span><span class="sxs-lookup"><span data-stu-id="d8585-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="d8585-204">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8585-204">PowerShell sample</span></span> 

<span data-ttu-id="d8585-205">O exemplo a seguir consulta o serviço de metadados para eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="d8585-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


## <a name="c-sample"></a><span data-ttu-id="d8585-206">Exemplo de C\#</span><span class="sxs-lookup"><span data-stu-id="d8585-206">C\# sample</span></span> 

<span data-ttu-id="d8585-207">O exemplo a seguir é de um cliente simples que se comunica com o serviço de metadados.</span><span class="sxs-lookup"><span data-stu-id="d8585-207">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="d8585-208">Os Eventos Agendados podem ser representados utilizando as seguintes estruturas de dados:</span><span class="sxs-lookup"><span data-stu-id="d8585-208">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="d8585-209">O exemplo a seguir consulta o serviço de metadados para eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="d8585-209">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

## <a name="python-sample"></a><span data-ttu-id="d8585-210">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="d8585-210">Python sample</span></span> 

<span data-ttu-id="d8585-211">O exemplo a seguir consulta o serviço de metadados para eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="d8585-211">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d8585-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8585-212">Next steps</span></span> 

- <span data-ttu-id="d8585-213">Leia mais sobre as API disponíveis no [serviço Metadados da Instância](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="d8585-213">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="d8585-214">Saiba mais sobre a [manutenção planejada para máquinas virtuais do Windows no Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="d8585-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

