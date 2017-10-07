---
title: "Verifique se o tráfego aaaVerify com fluxo de IP de Inspetor de rede do Azure - REST | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="c60f0-103">Verifique se o tráfego é permitido ou negado com a verificação de fluxo de IP, um componente do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="c60f0-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c60f0-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c60f0-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="c60f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c60f0-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="c60f0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c60f0-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="c60f0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c60f0-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="c60f0-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="c60f0-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="c60f0-109">Fluxo IP, verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c60f0-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="c60f0-110">validação de saudação pode ser executada para o tráfego de entrada ou saído.</span><span class="sxs-lookup"><span data-stu-id="c60f0-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="c60f0-111">Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou back-end.</span><span class="sxs-lookup"><span data-stu-id="c60f0-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="c60f0-112">Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="c60f0-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="c60f0-113">Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="c60f0-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c60f0-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c60f0-114">Before you begin</span></span>

<span data-ttu-id="c60f0-115">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c60f0-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="c60f0-116">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="c60f0-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c60f0-117">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="c60f0-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c60f0-118">Cenário</span><span class="sxs-lookup"><span data-stu-id="c60f0-118">Scenario</span></span>

<span data-ttu-id="c60f0-119">Esse cenário usa IP fluxo verificar tooverify se uma máquina virtual pode se comunicar tooanother máquina pela porta 443.</span><span class="sxs-lookup"><span data-stu-id="c60f0-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="c60f0-120">Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="c60f0-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="c60f0-121">toolearn mais sobre o fluxo de IP verificar, visite [fluxo IP verificar a visão geral](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c60f0-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="c60f0-122">Nesse cenário, você irá:</span><span class="sxs-lookup"><span data-stu-id="c60f0-122">In this scenario, you:</span></span>

* <span data-ttu-id="c60f0-123">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c60f0-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="c60f0-124">Chamar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="c60f0-124">Call IP flow verify</span></span>
* <span data-ttu-id="c60f0-125">Verificar os resultados</span><span class="sxs-lookup"><span data-stu-id="c60f0-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c60f0-126">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="c60f0-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="c60f0-127">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c60f0-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="c60f0-128">Execute Olá tooreturn de script a seguir em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c60f0-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="c60f0-129">Olá código a seguir precisa de valores para variáveis de saudação:</span><span class="sxs-lookup"><span data-stu-id="c60f0-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="c60f0-130">**subscriptionId** -Olá toouse de Id de assinatura.</span><span class="sxs-lookup"><span data-stu-id="c60f0-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="c60f0-131">**resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c60f0-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="c60f0-132">as informações necessárias Hello são id de saudação em tipo hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="c60f0-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="c60f0-133">resultados de saudação devem ser semelhante toohello exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c60f0-133">hello results should be similar toohello following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="c60f0-134">Chamar a Verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="c60f0-134">Call IP flow Verify</span></span>

<span data-ttu-id="c60f0-135">Olá, exemplo a seguir cria um solicitação tooverify Olá o tráfego para uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="c60f0-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="c60f0-136">resposta de saudação retorna se Olá tráfego é permitido ou se Olá tráfego é negado.</span><span class="sxs-lookup"><span data-stu-id="c60f0-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="c60f0-137">Se o tráfego é negado a que ele também retorna quais blocos de regra Olá tráfego.</span><span class="sxs-lookup"><span data-stu-id="c60f0-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="c60f0-138">Fluxo IP verificar requer que o recurso VM hello está alocado.</span><span class="sxs-lookup"><span data-stu-id="c60f0-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="c60f0-139">script Hello requer recursos Olá Id de uma máquina virtual e de uma placa de interface de rede na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c60f0-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="c60f0-140">Esses valores são fornecidos pelo Olá precede a saída.</span><span class="sxs-lookup"><span data-stu-id="c60f0-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="c60f0-141">Para todos os demais de Inspetor de rede chamadas Olá nome do grupo de recursos na solicitação Olá que URI é hello aquele que contém a instância do observador de rede hello, não recursos Olá estiver executando ações de diagnóstico de saudação em.</span><span class="sxs-lookup"><span data-stu-id="c60f0-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a><span data-ttu-id="c60f0-142">Entendendo os resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="c60f0-142">Understanding hello results</span></span>

<span data-ttu-id="c60f0-143">resposta de saudação que voltar informa se o tráfego de saudação é permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="c60f0-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="c60f0-144">resposta de saudação semelhante a um Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c60f0-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="c60f0-145">**Permitido**</span><span class="sxs-lookup"><span data-stu-id="c60f0-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="c60f0-146">**Negado**</span><span class="sxs-lookup"><span data-stu-id="c60f0-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="c60f0-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c60f0-147">Next steps</span></span>

<span data-ttu-id="c60f0-148">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn mais sobre grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="c60f0-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












