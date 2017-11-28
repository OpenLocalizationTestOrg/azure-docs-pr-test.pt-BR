---
title: aaaCheck conectividade com o observador de rede do Azure - PowerShell | Microsoft Docs
description: "Esta página explica como tootest conectividade com o observador de rede usando o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="ecb0d-103">Verificar a conectividade com o Observador de Rede do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecb0d-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ecb0d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ecb0d-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="ecb0d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecb0d-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="ecb0d-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ecb0d-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="ecb0d-107">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="ecb0d-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="ecb0d-108">Saiba como toouse tooverify de conectividade se uma conexão TCP direto de tooa uma máquina virtual que recebe o ponto de extremidade pode ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ecb0d-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ecb0d-109">Before you begin</span></span>

<span data-ttu-id="ecb0d-110">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecb0d-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="ecb0d-111">Uma instância do observador de rede na região Olá deseja toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="ecb0d-112">Conectividade de toocheck de máquinas virtuais com.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="ecb0d-113">A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ecb0d-114">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="ecb0d-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="ecb0d-115">Registrar o recurso de visualização de saudação</span><span class="sxs-lookup"><span data-stu-id="ecb0d-115">Register hello preview capability</span></span>

<span data-ttu-id="ecb0d-116">Conectividade está atualmente em visualização pública, toouse esse recurso que é necessário toobe registrado.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="ecb0d-117">toodo, Olá execução do PowerShell exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecb0d-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="ecb0d-118">tooverify Olá o registro foi bem-sucedido, execute Olá Powershell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecb0d-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="ecb0d-119">Se o recurso de saudação foi registrado corretamente, saída de hello deve corresponder a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="ecb0d-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="ecb0d-120">Verifique a conectividade tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="ecb0d-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="ecb0d-121">Este exemplo verifica a máquina de virtual de destino conectividade tooa pela porta 80.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="ecb0d-122">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ecb0d-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="ecb0d-123">Resposta</span><span class="sxs-lookup"><span data-stu-id="ecb0d-123">Response</span></span>

<span data-ttu-id="ecb0d-124">saudação de resposta a seguir é do exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="ecb0d-125">Essa resposta, Olá `ConnectionStatus` é **inacessível**.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="ecb0d-126">Você pode ver que todos os Olá investigações enviadas com falha.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="ecb0d-127">conectividade Olá falha no dispositivo virtual Olá vencimento tooa configurada pelo usuário `NetworkSecurityRule` chamado **UserRule_Port80**, configurado tooblock o tráfego de entrada na porta 80.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="ecb0d-128">Essas informações podem ser usadas tooresearch problemas de conexão.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-128">This information can be used tooresearch connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="ecb0d-129">Validar problemas de roteamento</span><span class="sxs-lookup"><span data-stu-id="ecb0d-129">Validate routing issues</span></span>

<span data-ttu-id="ecb0d-130">exemplo Hello verifica a conectividade entre uma máquina virtual e um ponto de extremidade remoto.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="ecb0d-131">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ecb0d-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="ecb0d-132">Resposta</span><span class="sxs-lookup"><span data-stu-id="ecb0d-132">Response</span></span>

<span data-ttu-id="ecb0d-133">Em Olá exemplo a seguir, Olá `ConnectionStatus` é mostrado como **inacessível**.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="ecb0d-134">Em Olá `Hops` detalhes, você pode ver em `Issues` que o tráfego de saudação foi bloqueado devido tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="ecb0d-135">Verificar a latência de site</span><span class="sxs-lookup"><span data-stu-id="ecb0d-135">Check website latency</span></span>

<span data-ttu-id="ecb0d-136">Olá exemplo verifica Olá conectividade tooa site a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="ecb0d-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ecb0d-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="ecb0d-138">Resposta</span><span class="sxs-lookup"><span data-stu-id="ecb0d-138">Response</span></span>

<span data-ttu-id="ecb0d-139">Olá resposta a seguir, você pode ver Olá `ConnectionStatus` mostra como **alcançável**.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="ecb0d-140">Quando uma conexão é bem-sucedida, os valores de latência são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="ecb0d-141">Verifique o ponto de extremidade de armazenamento de tooa conectividade</span><span class="sxs-lookup"><span data-stu-id="ecb0d-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="ecb0d-142">saudação de exemplo a seguir testa a conectividade de saudação de uma conta de armazenamento de blog de tooa de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="ecb0d-143">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ecb0d-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="ecb0d-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="ecb0d-144">Response</span></span>

<span data-ttu-id="ecb0d-145">Olá json a seguir é de resposta de exemplo hello de executar o cmdlet anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="ecb0d-146">Como o destino de saudação estiver acessível, Olá `ConnectionStatus` propriedade mostra como **alcançável**.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="ecb0d-147">São fornecidos detalhes de Olá relativos ao número de saudação do blob de armazenamento saltos tooreach necessário hello e latência.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="ecb0d-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecb0d-148">Next steps</span></span>

<span data-ttu-id="ecb0d-149">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ecb0d-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="ecb0d-150">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="ecb0d-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














