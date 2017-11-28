---
title: "Redefinir um tooreestablish de gateway de VPN do Azure túneis IPsec | Microsoft Docs"
description: "Este artigo o orienta por meio da redefinição os túneis do IPsec de tooreestablish Gateway de VPN do Azure. artigo Olá aplica gateways tooVPN Olá clássico e modelos de implantação do Gerenciador de recursos de saudação."
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
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="4fe14-104">Redefinir um Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="4fe14-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="4fe14-105">Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="4fe14-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="4fe14-106">Nessa situação, os seus dispositivos VPN local são todos funcionando corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4fe14-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="4fe14-107">Este artigo ajuda-o a redefinir o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="4fe14-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="4fe14-108">O que acontece durante uma redefinição?</span><span class="sxs-lookup"><span data-stu-id="4fe14-108">What happens during a reset?</span></span>

<span data-ttu-id="4fe14-109">Um gateway de VPN é composto de duas instâncias de VM em execução em uma configuração de modo em espera ativo.</span><span class="sxs-lookup"><span data-stu-id="4fe14-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="4fe14-110">Quando você redefinir o gateway hello, ela reinicia gateway Olá, e, em seguida, Olá reaplica entre locais tooit configurações.</span><span class="sxs-lookup"><span data-stu-id="4fe14-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="4fe14-111">gateway Olá mantém o endereço IP público Olá já possui.</span><span class="sxs-lookup"><span data-stu-id="4fe14-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="4fe14-112">Isso significa que você não precisará configuração do roteador tooupdate Olá VPN com um novo endereço IP público para o gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe14-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="4fe14-113">Quando você emitir o gateway de Olá Olá comando tooreset, instância ativa atual de saudação do gateway de VPN do Azure Olá é reinicializada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="4fe14-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="4fe14-114">Haverá uma breve interrupção durante o failover de saudação do hello instância ativa (que está sendo reinicializado), instância de toohello em espera.</span><span class="sxs-lookup"><span data-stu-id="4fe14-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="4fe14-115">intervalo de saudação deve ser menor que um minuto.</span><span class="sxs-lookup"><span data-stu-id="4fe14-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="4fe14-116">Se a conexão de saudação não é restaurado após a primeira reinicialização do hello, problema Olá mesmo comando novamente tooreboot instância VM segundo hello (Olá novo active gateway).</span><span class="sxs-lookup"><span data-stu-id="4fe14-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="4fe14-117">Se duas reinicializações de saudação tooback back solicitada, haverá um pouco maior período em que as duas instâncias VM (ativas e em espera) estão sendo reinicializadas.</span><span class="sxs-lookup"><span data-stu-id="4fe14-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="4fe14-118">Isso fará com que um intervalo mais conectividade VPN hello, backup too2 too4 minutos para reinicializações de saudação toocomplete VMs.</span><span class="sxs-lookup"><span data-stu-id="4fe14-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="4fe14-119">Depois de duas reinicializações, se você ainda tiver problemas de conectividade entre locais, abra uma solicitação de suporte de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe14-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="4fe14-120"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4fe14-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="4fe14-121">Antes de redefinir o gateway, verifique se itens importantes Olá listados abaixo para cada túnel VPN IPsec Site a Site (S2S).</span><span class="sxs-lookup"><span data-stu-id="4fe14-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="4fe14-122">Qualquer incompatibilidade nos itens Olá resulta em Desconectar Olá de túneis de VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="4fe14-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="4fe14-123">Verificar e corrigir configurações de saudação para seu local e gateways de VPN do Azure evita que você reinicializações desnecessárias e interrupções de Olá outras conexões de trabalho em gateways de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fe14-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="4fe14-124">Verifique se Olá itens a seguir antes de redefinir o gateway:</span><span class="sxs-lookup"><span data-stu-id="4fe14-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="4fe14-125">Olá IP Internet endereços (VIPs) para o gateway de VPN do Azure ambos hello e Olá gateway VPN estão configurados corretamente em ambas as políticas hello Azure e hello local VPN ao local.</span><span class="sxs-lookup"><span data-stu-id="4fe14-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="4fe14-126">chave pré-compartilhada Olá deve ser Olá mesmo em gateways VPN do Azure e no local.</span><span class="sxs-lookup"><span data-stu-id="4fe14-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="4fe14-127">Se você aplicar configuração do IPsec/IKE específica, como criptografia, algoritmos de hash e PFS (sigilo), certifique-se de ambos hello Azure e gateways de VPN local têm Olá mesmas configurações.</span><span class="sxs-lookup"><span data-stu-id="4fe14-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="4fe14-128"><a name="portal"></a>Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fe14-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="4fe14-129">Você pode redefinir um gateway de VPN do Gerenciador de recursos usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe14-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="4fe14-130">Se você quiser tooreset um gateway clássico, consulte Olá [PowerShell](#resetclassic) etapas.</span><span class="sxs-lookup"><span data-stu-id="4fe14-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="4fe14-131">Modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4fe14-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="4fe14-132">Olá abrir [portal do Azure](https://portal.azure.com) e navegue gateway de rede virtual do Gerenciador de recursos do toohello que você deseja tooreset.</span><span class="sxs-lookup"><span data-stu-id="4fe14-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="4fe14-133">Na folha de saudação para gateway de rede virtual Olá, clique em 'Redefinir'.</span><span class="sxs-lookup"><span data-stu-id="4fe14-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Folha Redefinir Gateway de VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="4fe14-135">Na saudação redefinir folha, clique em Olá **redefinir** botão.</span><span class="sxs-lookup"><span data-stu-id="4fe14-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="4fe14-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fe14-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="4fe14-137">Modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4fe14-137">Resource Manager deployment model</span></span>

<span data-ttu-id="4fe14-138">Olá cmdlet para redefinir um gateway é **AzureRmVirtualNetworkGateway redefinição**.</span><span class="sxs-lookup"><span data-stu-id="4fe14-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="4fe14-139">Antes de executar uma redefinição, verifique se você tem a versão mais recente de saudação do hello [cmdlets do PowerShell do Gerenciador de recursos](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="4fe14-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="4fe14-140">Olá, exemplo a seguir redefine um gateway de rede virtual denominado VNet1GW no grupo de recursos de TestRG1 hello:</span><span class="sxs-lookup"><span data-stu-id="4fe14-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="4fe14-141">Resultado:</span><span class="sxs-lookup"><span data-stu-id="4fe14-141">Result:</span></span>

<span data-ttu-id="4fe14-142">Quando você receber um resultado de retorno, você pode presumir Olá redefinição de gateway foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4fe14-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="4fe14-143">No entanto, há nada no resultado de retorno de saudação que indica explicitamente que redefinem Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4fe14-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="4fe14-144">Se você quiser toolook perto na Olá histórico toosee exatamente quando redefinir gateway Olá ocorreu, você pode exibir essas informações no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4fe14-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4fe14-145">No portal de hello, navegue até muito**'GatewayName' -> integridade do recurso**.</span><span class="sxs-lookup"><span data-stu-id="4fe14-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="4fe14-146"><a name="resetclassic"></a> Modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="4fe14-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="4fe14-147">Olá cmdlet para redefinir um gateway é **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="4fe14-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="4fe14-148">Antes de executar uma redefinição, verifique se você tem a versão mais recente de saudação do hello [cmdlets do PowerShell de gerenciamento de serviço (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="4fe14-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="4fe14-149">Olá, exemplo a seguir redefine gateway Olá para uma rede virtual denominada "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="4fe14-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="4fe14-150">Resultado:</span><span class="sxs-lookup"><span data-stu-id="4fe14-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="4fe14-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4fe14-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="4fe14-152">gateway tooreset Olá Olá use [vnet-gateway de rede az redefinir](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando.</span><span class="sxs-lookup"><span data-stu-id="4fe14-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="4fe14-153">Olá, exemplo a seguir redefine um gateway de rede virtual denominado VNet5GW no grupo de recursos de TestRG5 hello:</span><span class="sxs-lookup"><span data-stu-id="4fe14-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="4fe14-154">Resultado:</span><span class="sxs-lookup"><span data-stu-id="4fe14-154">Result:</span></span>

<span data-ttu-id="4fe14-155">Quando você receber um resultado de retorno, você pode presumir Olá redefinição de gateway foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4fe14-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="4fe14-156">No entanto, há nada no resultado de retorno de saudação que indica explicitamente que redefinem Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4fe14-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="4fe14-157">Se você quiser toolook perto na Olá histórico toosee exatamente quando redefinir gateway Olá ocorreu, você pode exibir essas informações no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4fe14-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4fe14-158">No portal de hello, navegue até muito**'GatewayName' -> integridade do recurso**.</span><span class="sxs-lookup"><span data-stu-id="4fe14-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
