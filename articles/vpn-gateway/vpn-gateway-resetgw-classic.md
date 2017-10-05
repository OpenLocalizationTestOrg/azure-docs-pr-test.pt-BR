---
title: "Redefinir um gateway de VPN do Azure para restabelecer túneis IPsec | Microsoft Docs"
description: "Este artigo orienta você pela redefinição de seu Gateway de VPN do Azure para reestabelecer os túneis IPsec. O artigo se aplica a gateways de VPN tanto nos modelos de implantação clássicos quanto nos modelos de implantação do Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="09502-104">Redefinir um Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="09502-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="09502-105">Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="09502-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="09502-106">Nessa situação, os dispositivos VPN locais estão funcionando corretamente, mas não são capazes de estabelecer túneis IPsec com os gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="09502-107">Este artigo ajuda-o a redefinir o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="09502-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="09502-108">O que acontece durante uma redefinição?</span><span class="sxs-lookup"><span data-stu-id="09502-108">What happens during a reset?</span></span>

<span data-ttu-id="09502-109">Um gateway de VPN é composto de duas instâncias de VM em execução em uma configuração de modo em espera ativo.</span><span class="sxs-lookup"><span data-stu-id="09502-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="09502-110">Quando você redefine o gateway, ele reinicializa o gateway e aplica novamente as configurações entre instalações a ele.</span><span class="sxs-lookup"><span data-stu-id="09502-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="09502-111">O gateway mantém o endereço IP público que já tem.</span><span class="sxs-lookup"><span data-stu-id="09502-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="09502-112">Isso significa que você não precisa atualizar a configuração do roteador VPN com um novo endereço IP público do gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="09502-113">Ao emitir o comando para redefinir o gateway, a instância ativa atual do gateway de VPN do Azure é imediatamente reiniciada.</span><span class="sxs-lookup"><span data-stu-id="09502-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="09502-114">Haverá um breve intervalo durante o failover da instância ativa (que está sendo reinicializada) à instância em espera.</span><span class="sxs-lookup"><span data-stu-id="09502-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="09502-115">O intervalo deve ser menor que um minuto.</span><span class="sxs-lookup"><span data-stu-id="09502-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="09502-116">Se a conexão não é restaurada após a primeira reinicialização, execute o mesmo comando novamente para reiniciar a segunda instância VM (o novo gateway ativo).</span><span class="sxs-lookup"><span data-stu-id="09502-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="09502-117">Se as duas reinicializações são solicitadas uma após a outra, haverá um período um pouco mais longo durante o qual as duas instâncias da VM (ativas e em espera) estão sendo reinicializadas.</span><span class="sxs-lookup"><span data-stu-id="09502-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="09502-118">Isso causará um intervalo maior na conectividade VPN, exigindo até 2 a 4 minutos para que as VMs concluam as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="09502-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="09502-119">Após duas reinicializações, se você ainda estiver tendo problemas de conectividade entre instalações, abra uma solicitação de suporte no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="09502-120"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="09502-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="09502-121">Antes de redefinir o gateway, verifique os principais itens listados abaixo para cada túnel VPN Site a Site (S2S) de IPsec.</span><span class="sxs-lookup"><span data-stu-id="09502-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="09502-122">Qualquer incompatibilidade nos itens resultará na desconexão de túneis VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="09502-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="09502-123">Verificar e corrigir as configurações para seus gateways de VPN do Azure e locais faz com que você evite reinicializações desnecessárias e interrupções para as outras conexões de trabalho nos gateways.</span><span class="sxs-lookup"><span data-stu-id="09502-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="09502-124">Verifique os itens a seguir antes de redefinir seu gateway:</span><span class="sxs-lookup"><span data-stu-id="09502-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="09502-125">Os VIPs (endereços IP da Internet) para o gateway de VPN do Azure e o gateway de VPN local estão configurados corretamente em ambas a políticas de VPN do Azure e de VPN local.</span><span class="sxs-lookup"><span data-stu-id="09502-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="09502-126">A chave pré-compartilhada deve ser a mesma em ambos o gateway de VPN do Azure e o gateway de VPN local.</span><span class="sxs-lookup"><span data-stu-id="09502-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="09502-127">Se você aplicar a configuração de IPsec/IKE específica, como criptografia, algoritmos de hash e PFS (Perfect Forward Secrecy), verifique se que o gateway de VPN do Azure e o gateway de VPN local têm as mesmas configurações.</span><span class="sxs-lookup"><span data-stu-id="09502-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="09502-128"><a name="portal"></a>Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="09502-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="09502-129">Você pode redefinir um gateway de VPN do Resource Manager usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="09502-130">Se você quiser redefinir um gateway clássico, veja as etapas [PowerShell](#resetclassic).</span><span class="sxs-lookup"><span data-stu-id="09502-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="09502-131">Modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="09502-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="09502-132">Abra o [Portal do Azure](https://portal.azure.com) e navegue até o gateway de rede virtual do Gerenciador de Recursos que deseja redefinir.</span><span class="sxs-lookup"><span data-stu-id="09502-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="09502-133">Na folha do gateway de rede virtual, clique em "Redefinir".</span><span class="sxs-lookup"><span data-stu-id="09502-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Folha Redefinir Gateway de VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="09502-135">Na folha Redefinir, clique no botão **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="09502-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="09502-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="09502-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="09502-137">Modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="09502-137">Resource Manager deployment model</span></span>

<span data-ttu-id="09502-138">O cmdlet para redefinição de um gateway é **Reset-AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="09502-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="09502-139">Antes de realizar uma redefinição, certifique-se de possui a última versão dos [cmdlets do Resource Manager PowerShell ](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="09502-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="09502-140">O exemplo a seguir redefine um gateway de rede virtual nomeado VNet1GW no grupo de recursos TestRG1:</span><span class="sxs-lookup"><span data-stu-id="09502-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="09502-141">Resultado:</span><span class="sxs-lookup"><span data-stu-id="09502-141">Result:</span></span>

<span data-ttu-id="09502-142">Ao receber um resultado de retorno, você poderá assumir que a redefinição do gateway foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="09502-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="09502-143">No entanto, não há nada no resultado de retorno que indica explicitamente que a redefinição foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="09502-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="09502-144">Caso queira analisar detalhadamente o histórico para visualizar exatamente quando ocorreu a redefinição do gateway, é possível visualizar essas informações no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09502-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09502-145">No portal, navegue até **'GatewayName' -> Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="09502-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="09502-146"><a name="resetclassic"></a> Modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="09502-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="09502-147">O cmdlet para redefinição de um gateway é **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="09502-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="09502-148">Antes de realizar uma redefinição, certifique-se de que possui a última versão dos [cmdlets do PowerShell do Gerenciamento de Serviços (SM) ](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="09502-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="09502-149">O exemplo a seguir redefine o gateway para uma rede virtual nomeada "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="09502-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="09502-150">Resultado:</span><span class="sxs-lookup"><span data-stu-id="09502-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="09502-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09502-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="09502-152">Para redefinir o gateway, utilize o comando [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset).</span><span class="sxs-lookup"><span data-stu-id="09502-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="09502-153">O exemplo a seguir redefine um gateway de rede virtual nomeado VNet5GW no grupo de recursos TestRG5:</span><span class="sxs-lookup"><span data-stu-id="09502-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="09502-154">Resultado:</span><span class="sxs-lookup"><span data-stu-id="09502-154">Result:</span></span>

<span data-ttu-id="09502-155">Ao receber um resultado de retorno, você poderá assumir que a redefinição do gateway foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="09502-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="09502-156">No entanto, não há nada no resultado de retorno que indica explicitamente que a redefinição foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="09502-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="09502-157">Caso queira analisar detalhadamente o histórico para visualizar exatamente quando ocorreu a redefinição do gateway, é possível visualizar essas informações no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09502-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09502-158">No portal, navegue até **'GatewayName' -> Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="09502-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>