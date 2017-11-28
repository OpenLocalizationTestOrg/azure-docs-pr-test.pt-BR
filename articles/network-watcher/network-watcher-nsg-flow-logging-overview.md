---
title: "log de tooflow aaaIntroduction para grupos de segurança de rede com o observador de rede do Azure | Microsoft Docs"
description: "Esta página explica como o fluxo NSG toouse registra um recurso do observador de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="40c17-103">Registro em log tooflow de Introdução para grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="40c17-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="40c17-104">Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="40c17-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="40c17-105">Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="40c17-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![visão geral dos logs de fluxo][1]

<span data-ttu-id="40c17-107">Enquanto o fluxo de logs de grupos de segurança de rede de destino, elas não são exibidas Olá mesmo como Olá outros logs.</span><span class="sxs-lookup"><span data-stu-id="40c17-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="40c17-108">Logs de fluxo são armazenados apenas dentro de uma conta de armazenamento e o seguinte caminho de log Olá conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="40c17-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="40c17-109">Olá mesmas políticas de retenção como visto em outros logs aplicam logs de tooflow.</span><span class="sxs-lookup"><span data-stu-id="40c17-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="40c17-110">Logs de tem uma política de retenção pode ser definida de dias de too365 de 1 dia.</span><span class="sxs-lookup"><span data-stu-id="40c17-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="40c17-111">Se uma política de retenção não for definida, Olá logs são mantidos indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="40c17-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="40c17-112">Arquivo de log</span><span class="sxs-lookup"><span data-stu-id="40c17-112">Log file</span></span>

<span data-ttu-id="40c17-113">Os logs de fluxo têm várias propriedades.</span><span class="sxs-lookup"><span data-stu-id="40c17-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="40c17-114">Olá lista a seguir é uma lista de propriedades de saudação que são retornados dentro do log de fluxo NSG hello:</span><span class="sxs-lookup"><span data-stu-id="40c17-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="40c17-115">**tempo** - hora em que o evento Olá foi registrado</span><span class="sxs-lookup"><span data-stu-id="40c17-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="40c17-116">**systemId** - a ID do recurso Grupo de Segurança da Rede.</span><span class="sxs-lookup"><span data-stu-id="40c17-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="40c17-117">**categoria** -categoria de saudação do evento Olá, é sempre ser NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="40c17-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="40c17-118">**ResourceID** -Olá Id de saudação NSG recurso</span><span class="sxs-lookup"><span data-stu-id="40c17-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="40c17-119">**operationName** - é sempre NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="40c17-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="40c17-120">**propriedades** -uma coleção de propriedades de fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="40c17-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="40c17-121">**Versão** -número de versão do esquema de evento do fluxo de Log Olá</span><span class="sxs-lookup"><span data-stu-id="40c17-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="40c17-122">**flows** - uma coleção de fluxos.</span><span class="sxs-lookup"><span data-stu-id="40c17-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="40c17-123">Essa propriedade tem várias entradas para diferentes regras</span><span class="sxs-lookup"><span data-stu-id="40c17-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="40c17-124">**regra** -regra para qual Olá fluxos são listados</span><span class="sxs-lookup"><span data-stu-id="40c17-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="40c17-125">**flows** - uma coleção de fluxos</span><span class="sxs-lookup"><span data-stu-id="40c17-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="40c17-126">**Mac** -Olá endereço MAC de hello NIC para Olá VM em que o fluxo de saudação foi coletado</span><span class="sxs-lookup"><span data-stu-id="40c17-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="40c17-127">**flowTuples** -uma cadeia de caracteres que contém várias propriedades de tupla de fluxo de saudação em formato separado por vírgulas</span><span class="sxs-lookup"><span data-stu-id="40c17-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="40c17-128">**Carimbo de hora** -este valor é o carimbo de hora de saudação do quando fluxo Olá ocorreu no formato de ÉPOCA do UNIX</span><span class="sxs-lookup"><span data-stu-id="40c17-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="40c17-129">**IP de origem** - Olá IP de origem</span><span class="sxs-lookup"><span data-stu-id="40c17-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="40c17-130">**Destino IP** -Olá IP de destino</span><span class="sxs-lookup"><span data-stu-id="40c17-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="40c17-131">**Porta de origem** - Olá porta de origem</span><span class="sxs-lookup"><span data-stu-id="40c17-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="40c17-132">**Porta de destino** -Olá porta de destino</span><span class="sxs-lookup"><span data-stu-id="40c17-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="40c17-133">**Protocolo** -Olá protocolo de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c17-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="40c17-134">Os valores válidos são **T** para TCP e **U** para UDP</span><span class="sxs-lookup"><span data-stu-id="40c17-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="40c17-135">**Fluxo de tráfego** -Olá a direção do fluxo de tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c17-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="40c17-136">Os valores válidos são **I** para entrada e **O** para saída.</span><span class="sxs-lookup"><span data-stu-id="40c17-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="40c17-137">**Traffic** - se o tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="40c17-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="40c17-138">Os valores válidos são **A** para permitido e **D** para negado.</span><span class="sxs-lookup"><span data-stu-id="40c17-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="40c17-139">a seguir Olá é um exemplo de um fluxo de log.</span><span class="sxs-lookup"><span data-stu-id="40c17-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="40c17-140">Como você pode ver, há vários registros que siga a lista de propriedades de saudação descrita em Olá anterior seção.</span><span class="sxs-lookup"><span data-stu-id="40c17-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="40c17-141">Os valores na propriedade de flowTuples Olá são uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="40c17-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="40c17-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40c17-142">Next steps</span></span>

<span data-ttu-id="40c17-143">Saiba como tooenable fluxo registra visitando [log habilitando fluxo](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40c17-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="40c17-144">Saiba mais sobre o log de NSG visitando [Log Analytics para os grupos de segurança da rede (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="40c17-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="40c17-145">Descubra se o tráfego é permitido ou negado em uma VM visitando [Examinar o tráfego com a verificação de fluxo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="40c17-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

