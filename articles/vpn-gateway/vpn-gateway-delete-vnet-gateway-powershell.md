---
title: 'Excluir um gateway de rede virtual: PowerShell: Azure Resource Manager | Microsoft Docs'
description: "Exclua um gateway de rede virtual usando o PowerShell no modelo de implantação do Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="c7051-103">Excluir um gateway de rede virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7051-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7051-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7051-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="c7051-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7051-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="c7051-106">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="c7051-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="c7051-107">Há duas abordagens diferentes que podem ser executadas quando você deseja excluir um gateway de rede virtual de uma configuração de Gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="c7051-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="c7051-108">Se você desejar excluir tudo e recomeçar, por exemplo, no caso de um ambiente de teste, poderá excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="c7051-109">Quando você exclui um grupo de recursos, isso exclui todos os recursos dentro do grupo.</span><span class="sxs-lookup"><span data-stu-id="c7051-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="c7051-110">Esse método é recomendado somente se você não deseja manter os recursos no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="c7051-111">Você não pode excluir seletivamente apenas alguns recursos usando essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="c7051-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="c7051-112">Se você quiser manter alguns dos recursos no seu grupo de recursos, a exclusão de um gateway de rede virtual se tornará um pouco mais complicada.</span><span class="sxs-lookup"><span data-stu-id="c7051-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="c7051-113">Antes de poder excluir o gateway de rede virtual, primeiro você deve excluir todos os recursos que são dependentes do gateway.</span><span class="sxs-lookup"><span data-stu-id="c7051-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="c7051-114">As etapas a que seguir dependem do tipo de conexões que você criou e os recursos dependentes de cada conexão.</span><span class="sxs-lookup"><span data-stu-id="c7051-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="c7051-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c7051-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="c7051-116">1. Baixe a versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="c7051-117">Baixe e instale a versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c7051-118">Para obter mais informações sobre como baixar e instalar os cmdlets do PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7051-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="c7051-119">2. Conectar-se à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7051-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="c7051-120">Abra o console do PowerShell e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="c7051-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="c7051-121">Use o exemplo a seguir para ajudar a se conectar:</span><span class="sxs-lookup"><span data-stu-id="c7051-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c7051-122">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="c7051-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="c7051-123">Se você tiver mais de uma assinatura, especifique a assinatura que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="c7051-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="c7051-124"><a name="S2S"></a>Excluir um Gateway de VPN site a site</span><span class="sxs-lookup"><span data-stu-id="c7051-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="c7051-125">Para excluir um gateway de rede virtual para uma configuração S2S, exclua cada recurso pertencente ao gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="c7051-126">Os recursos devem ser excluídos em uma determinada ordem devido a dependências.</span><span class="sxs-lookup"><span data-stu-id="c7051-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="c7051-127">Ao trabalhar com os exemplos abaixo, alguns dos valores devem ser especificados, enquanto outros são um resultado de saída.</span><span class="sxs-lookup"><span data-stu-id="c7051-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="c7051-128">Podemos usar os seguintes valores específicos nos exemplos para fins de demonstração:</span><span class="sxs-lookup"><span data-stu-id="c7051-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="c7051-129">Nome da VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="c7051-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="c7051-130">Nome do Grupo de Recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="c7051-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="c7051-131">Nome do gateway de rede virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="c7051-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="c7051-132">As etapas a seguir se aplicam ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="c7051-133">1. Obtenha o gateway de rede virtual que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="c7051-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="c7051-134">2. Verifique se o gateway de rede virtual tem alguma conexão.</span><span class="sxs-lookup"><span data-stu-id="c7051-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="c7051-135">3. Exclua todas as conexões.</span><span class="sxs-lookup"><span data-stu-id="c7051-135">3. Delete all connections.</span></span>

<span data-ttu-id="c7051-136">Talvez seja solicitado que você confirme a exclusão de cada uma das conexões.</span><span class="sxs-lookup"><span data-stu-id="c7051-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="c7051-137">4. Exclua o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="c7051-138">Talvez seja solicitado que você confirme a exclusão do gateway.</span><span class="sxs-lookup"><span data-stu-id="c7051-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="c7051-139">Se você tiver uma configuração de P2S nessa VNet além da configuração de S2S, a exclusão do gateway de rede virtual desconectará automaticamente todos os clientes de P2S sem aviso.</span><span class="sxs-lookup"><span data-stu-id="c7051-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="c7051-140">Neste ponto, o gateway de rede virtual foi excluído.</span><span class="sxs-lookup"><span data-stu-id="c7051-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="c7051-141">Você pode usar as próximas etapas para excluir todos os recursos que não estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="c7051-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="c7051-142">5 Exclua os gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="c7051-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="c7051-143">Obtenha a lista de gateways de rede local correspondentes.</span><span class="sxs-lookup"><span data-stu-id="c7051-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="c7051-144">Exclua os gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="c7051-144">Delete the local network gateways.</span></span> <span data-ttu-id="c7051-145">Talvez seja solicitado que você confirme a exclusão de cada um dos gateways de rede local.</span><span class="sxs-lookup"><span data-stu-id="c7051-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="c7051-146">6. Exclua os recursos do endereço IP Público.</span><span class="sxs-lookup"><span data-stu-id="c7051-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="c7051-147">Obtenha as configurações de IP do gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="c7051-148">Obtenha a lista de recursos de endereços IP Públicos usados para este gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="c7051-149">Se o gateway de rede virtual estava ativo-ativo, você verá dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="c7051-150">Exclua os recursos IP Públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="c7051-151">7. Exclua a sub-rede do gateway e defina a configuração.</span><span class="sxs-lookup"><span data-stu-id="c7051-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="c7051-152"><a name="v2v"></a>Excluir um Gateway de VPN de VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="c7051-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="c7051-153">Para excluir um gateway de rede virtual para uma configuração V2V, exclua cada recurso pertencente ao gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="c7051-154">Os recursos devem ser excluídos em uma determinada ordem devido a dependências.</span><span class="sxs-lookup"><span data-stu-id="c7051-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="c7051-155">Ao trabalhar com os exemplos abaixo, alguns dos valores devem ser especificados, enquanto outros são um resultado de saída.</span><span class="sxs-lookup"><span data-stu-id="c7051-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="c7051-156">Podemos usar os seguintes valores específicos nos exemplos para fins de demonstração:</span><span class="sxs-lookup"><span data-stu-id="c7051-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="c7051-157">Nome da VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="c7051-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="c7051-158">Nome do Grupo de Recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="c7051-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="c7051-159">Nome do gateway de rede virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="c7051-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="c7051-160">As etapas a seguir se aplicam ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="c7051-161">1. Obtenha o gateway de rede virtual que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="c7051-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="c7051-162">2. Verifique se o gateway de rede virtual tem alguma conexão.</span><span class="sxs-lookup"><span data-stu-id="c7051-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="c7051-163">Pode haver outras conexões com o gateway de rede virtual que fazem parte de um grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="c7051-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="c7051-164">Verifique se há conexões adicionais em cada grupo de recursos adicional.</span><span class="sxs-lookup"><span data-stu-id="c7051-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="c7051-165">Neste exemplo, estamos verificando se há conexões de RG2.</span><span class="sxs-lookup"><span data-stu-id="c7051-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="c7051-166">Execute isso para cada grupo de recursos que você tem e que pode ter uma conexão para o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="c7051-167">3. Obtenha a lista de conexões em ambas as direções.</span><span class="sxs-lookup"><span data-stu-id="c7051-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="c7051-168">Já que essa é uma configuração de VNet para VNet, você precisa da lista de conexões em ambas as direções.</span><span class="sxs-lookup"><span data-stu-id="c7051-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="c7051-169">Neste exemplo, estamos verificando se há conexões de RG2.</span><span class="sxs-lookup"><span data-stu-id="c7051-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="c7051-170">Execute isso para cada grupo de recursos que você tem e que pode ter uma conexão para o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="c7051-171">4. Exclua todas as conexões.</span><span class="sxs-lookup"><span data-stu-id="c7051-171">4. Delete all connections.</span></span>

<span data-ttu-id="c7051-172">Talvez seja solicitado que você confirme a exclusão de cada uma das conexões.</span><span class="sxs-lookup"><span data-stu-id="c7051-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="c7051-173">5. Exclua o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="c7051-174">Talvez seja solicitado que você confirme a exclusão de cada um dos gateways de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="c7051-175">Se você tiver configurações de P2S nas Vnets além da configuração de V2V, a exclusão dos gateways de rede virtual desconectará automaticamente todos os clientes de P2S sem aviso.</span><span class="sxs-lookup"><span data-stu-id="c7051-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="c7051-176">Neste ponto, o gateway de rede virtual foi excluído.</span><span class="sxs-lookup"><span data-stu-id="c7051-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="c7051-177">Você pode usar as próximas etapas para excluir todos os recursos que não estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="c7051-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="c7051-178">6. Exclua os recursos do endereço IP Público</span><span class="sxs-lookup"><span data-stu-id="c7051-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="c7051-179">Obtenha as configurações de IP do gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="c7051-180">Obtenha a lista de recursos de endereços IP Públicos usados para este gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="c7051-181">Se o gateway de rede virtual estava ativo-ativo, você verá dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="c7051-182">Exclua os recursos IP Públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-182">Delete the Public IP resources.</span></span> <span data-ttu-id="c7051-183">Talvez seja solicitado que você confirme a exclusão do IP público.</span><span class="sxs-lookup"><span data-stu-id="c7051-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="c7051-184">7. Exclua a sub-rede do gateway e defina a configuração.</span><span class="sxs-lookup"><span data-stu-id="c7051-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="c7051-185"><a name="deletep2s"></a>Excluir um gateway de VPN ponto a site</span><span class="sxs-lookup"><span data-stu-id="c7051-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="c7051-186">Para excluir um gateway de rede virtual de uma configuração de P2S, é necessário excluir primeiro cada recurso pertencente ao gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="c7051-187">Os recursos devem ser excluídos em uma determinada ordem devido a dependências.</span><span class="sxs-lookup"><span data-stu-id="c7051-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="c7051-188">Ao trabalhar com os exemplos abaixo, alguns dos valores devem ser especificados, enquanto outros são um resultado de saída.</span><span class="sxs-lookup"><span data-stu-id="c7051-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="c7051-189">Podemos usar os seguintes valores específicos nos exemplos para fins de demonstração:</span><span class="sxs-lookup"><span data-stu-id="c7051-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="c7051-190">Nome da VNet: VNet1</span><span class="sxs-lookup"><span data-stu-id="c7051-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="c7051-191">Nome do Grupo de Recursos: RG1</span><span class="sxs-lookup"><span data-stu-id="c7051-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="c7051-192">Nome do gateway de rede virtual: GW1</span><span class="sxs-lookup"><span data-stu-id="c7051-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="c7051-193">As etapas a seguir se aplicam ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="c7051-194">Quando você excluir o gateway de VPN, todos os clientes conectados serão desconectados da VNet sem aviso.</span><span class="sxs-lookup"><span data-stu-id="c7051-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="c7051-195">1. Obtenha o gateway de rede virtual que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="c7051-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="c7051-196">2. Exclua o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="c7051-197">Talvez seja solicitado que você confirme a exclusão de cada um dos gateways de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="c7051-198">Neste ponto, o gateway de rede virtual foi excluído.</span><span class="sxs-lookup"><span data-stu-id="c7051-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="c7051-199">Você pode usar as próximas etapas para excluir todos os recursos que não estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="c7051-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="c7051-200">3. Exclua os recursos do endereço IP Público</span><span class="sxs-lookup"><span data-stu-id="c7051-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="c7051-201">Obtenha as configurações de IP do gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="c7051-202">Obtenha a lista de endereços IP públicos usados para esse gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c7051-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="c7051-203">Se o gateway de rede virtual estava ativo-ativo, você verá dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="c7051-204">Exclua os IPs públicos.</span><span class="sxs-lookup"><span data-stu-id="c7051-204">Delete the Public IPs.</span></span> <span data-ttu-id="c7051-205">Talvez seja solicitado que você confirme a exclusão do IP público.</span><span class="sxs-lookup"><span data-stu-id="c7051-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="c7051-206">4. Exclua a sub-rede do gateway e defina a configuração.</span><span class="sxs-lookup"><span data-stu-id="c7051-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="c7051-207"><a name="delete"></a>Excluir um Gateway de VPN por meio da exclusão do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c7051-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="c7051-208">Se você não estiver preocupado em manter nenhum de seus recursos no grupo de recursos e apenas desejar recomeçar, poderá excluir um grupo de recursos inteiro.</span><span class="sxs-lookup"><span data-stu-id="c7051-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="c7051-209">Essa é uma maneira rápida de remover tudo.</span><span class="sxs-lookup"><span data-stu-id="c7051-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="c7051-210">As próximas etapas se aplicam somente ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7051-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="c7051-211">1. Obtenha uma lista de todos os grupos de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7051-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="c7051-212">2. Localize o grupo de recursos que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="c7051-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="c7051-213">Localize o grupo de recursos que você deseja excluir e exiba a lista de recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="c7051-214">Neste exemplo, o nome do grupo de recursos é RG1.</span><span class="sxs-lookup"><span data-stu-id="c7051-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="c7051-215">Modificar o exemplo para recuperar uma lista de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="c7051-216">3. Verificar os recursos na lista.</span><span class="sxs-lookup"><span data-stu-id="c7051-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="c7051-217">Quando a lista for retornada, examine-a para verificar que você deseja excluir todos os recursos no grupo, bem como o grupo de recursos em si.</span><span class="sxs-lookup"><span data-stu-id="c7051-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="c7051-218">Se desejar manter alguns dos recursos no grupo de recursos, use as etapas das seções anteriores deste artigo para excluir o gateway.</span><span class="sxs-lookup"><span data-stu-id="c7051-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="c7051-219">4. Exclua o grupo de recursos e os recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="c7051-220">Para excluir o grupo de recursos e todos os recursos contidos nele, modifique o exemplo e execute-o.</span><span class="sxs-lookup"><span data-stu-id="c7051-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="c7051-221">5. Verifique o status.</span><span class="sxs-lookup"><span data-stu-id="c7051-221">5. Check the status.</span></span>

<span data-ttu-id="c7051-222">Leva algum tempo para o Azure excluir todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="c7051-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="c7051-223">Você pode verificar o status do seu grupo de recursos usando esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7051-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="c7051-224">O resultado retornado mostra 'Êxito'.</span><span class="sxs-lookup"><span data-stu-id="c7051-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```