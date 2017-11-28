---
title: "conjunto de escala de uma máquina virtual do Azure aaaCreate | Microsoft Docs"
description: "Crie e implante um conjunto de dimensionamento de máquinas virtuais Linux ou Windows do Azure com a CLI do Azure, o PowerShell, um modelo ou o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="4ac27-103">Criar e implantar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="4ac27-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="4ac27-104">Conjuntos de escala de máquinas virtuais tornam mais fácil para você toodeploy e gerenciam máquinas virtuais idênticas como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="4ac27-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="4ac27-105">Os conjuntos de dimensionamento fornecem uma camada de computação altamente escalonável e personalizável para aplicativos de hiperescala e suporte a imagens da plataforma Windows, imagens da plataforma Linux, imagens personalizadas e extensões.</span><span class="sxs-lookup"><span data-stu-id="4ac27-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="4ac27-106">Para obter mais informações sobre conjuntos de dimensionamento, consulte [Conjuntos de dimensionamento de máquinas virtuais](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="4ac27-107">Este tutorial mostra como toocreate uma escala de máquina virtual configurada **sem** usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac27-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="4ac27-108">Para obter informações sobre como toouse Olá portal do Azure, consulte [como toocreate uma escala de máquina virtual definido com hello portal do Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="4ac27-109">Para saber mais sobre os recursos do Azure Resource Manager, confira [Azure Resource Manager vs. Implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="4ac27-110">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="4ac27-110">Sign in tooAzure</span></span>

<span data-ttu-id="4ac27-111">Se você estiver usando uma escala de toocreate 2.0 do CLI do Azure ou o Azure PowerShell definida, é necessário primeiro toosign tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="4ac27-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="4ac27-112">Para obter mais informações sobre como tooinstall, configurar e entre em tooAzure com CLI do Azure ou o PowerShell, consulte [guia de Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) ou [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ac27-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="4ac27-113">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4ac27-113">Create a resource group</span></span>

<span data-ttu-id="4ac27-114">É necessário primeiro toocreate um grupo de recursos que o conjunto de escala de máquina virtual hello está associado.</span><span class="sxs-lookup"><span data-stu-id="4ac27-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="4ac27-115">Criar com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac27-115">Create from Azure CLI</span></span>

<span data-ttu-id="4ac27-116">Com a CLI do Azure, você pode criar um conjunto de dimensionamento de máquinas virtuais com esforço mínimo.</span><span class="sxs-lookup"><span data-stu-id="4ac27-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="4ac27-117">Se você omitir valores padrão, eles serão fornecidos para você.</span><span class="sxs-lookup"><span data-stu-id="4ac27-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="4ac27-118">Por exemplo, se você não especificar as informações de rede virtual, uma rede virtual será criada para você.</span><span class="sxs-lookup"><span data-stu-id="4ac27-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="4ac27-119">Se você omitir Olá partes a seguir, são criadas para você:</span><span class="sxs-lookup"><span data-stu-id="4ac27-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="4ac27-120">Um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="4ac27-120">A load balancer</span></span>
- <span data-ttu-id="4ac27-121">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="4ac27-121">A virtual network</span></span>
- <span data-ttu-id="4ac27-122">Um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="4ac27-122">A public IP address</span></span>

<span data-ttu-id="4ac27-123">Ao escolher hello imagem da máquina virtual que você deseja toouse no conjunto de escalas da máquina virtual hello, você tem algumas opções:</span><span class="sxs-lookup"><span data-stu-id="4ac27-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="4ac27-124">URN</span><span class="sxs-lookup"><span data-stu-id="4ac27-124">URN</span></span>  
<span data-ttu-id="4ac27-125">Identificador de saudação de um recurso:</span><span class="sxs-lookup"><span data-stu-id="4ac27-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="4ac27-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="4ac27-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="4ac27-127">Alias do URN</span><span class="sxs-lookup"><span data-stu-id="4ac27-127">URN alias</span></span>  
<span data-ttu-id="4ac27-128">nome amigável de saudação de um URN:</span><span class="sxs-lookup"><span data-stu-id="4ac27-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="4ac27-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="4ac27-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="4ac27-130">ID de recurso personalizado</span><span class="sxs-lookup"><span data-stu-id="4ac27-130">Custom resource id</span></span>  
<span data-ttu-id="4ac27-131">Olá caminho tooan recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="4ac27-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="4ac27-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="4ac27-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="4ac27-133">Recurso da Web</span><span class="sxs-lookup"><span data-stu-id="4ac27-133">Web resource</span></span>  
<span data-ttu-id="4ac27-134">Olá caminho tooan URI HTTP:</span><span class="sxs-lookup"><span data-stu-id="4ac27-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="4ac27-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="4ac27-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="4ac27-136">Você pode encontrar a lista de imagens disponíveis com `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="4ac27-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="4ac27-137">toocreate definido de uma escala de máquina virtual, você deve especificar o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4ac27-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="4ac27-138">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4ac27-138">Resource group</span></span> 
- <span data-ttu-id="4ac27-139">Nome</span><span class="sxs-lookup"><span data-stu-id="4ac27-139">Name</span></span>
- <span data-ttu-id="4ac27-140">Imagem do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="4ac27-140">Operating system image</span></span>
- <span data-ttu-id="4ac27-141">Informações de autenticação</span><span class="sxs-lookup"><span data-stu-id="4ac27-141">Authentication information</span></span> 
 
<span data-ttu-id="4ac27-142">saudação de exemplo a seguir cria um conjunto de escala básica da máquina virtual (esta etapa pode levar alguns minutos).</span><span class="sxs-lookup"><span data-stu-id="4ac27-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="4ac27-143">Depois que o comando Olá é concluído, você terá a escala de máquina virtual definido criado.</span><span class="sxs-lookup"><span data-stu-id="4ac27-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="4ac27-144">Endereço IP de saudação tooget da máquina virtual de saudação talvez seja necessário para que você possa conectar tooit.</span><span class="sxs-lookup"><span data-stu-id="4ac27-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="4ac27-145">Você pode obter muitas informações diferentes sobre a máquina virtual de saudação (incluindo o endereço IP de saudação) com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ac27-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="4ac27-146">Criar com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ac27-146">Create from PowerShell</span></span>

<span data-ttu-id="4ac27-147">O PowerShell é mais complicado toouse de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac27-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="4ac27-148">Enquanto a CLI do Azure fornece padrões para recursos relacionados à rede (balanceadores de carga, endereços IP e redes virtuais), isso não ocorre com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ac27-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="4ac27-149">Referenciar uma imagem com o PowerShell também é um pouco mais complicado.</span><span class="sxs-lookup"><span data-stu-id="4ac27-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="4ac27-150">Você pode obter imagens com hello cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ac27-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="4ac27-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="4ac27-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="4ac27-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="4ac27-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="4ac27-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="4ac27-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="4ac27-154">Olá cmdlets trabalho pode ser usado na sequência.</span><span class="sxs-lookup"><span data-stu-id="4ac27-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="4ac27-155">Aqui está um exemplo de como tooget todas as imagens para Olá **Oeste dos EUA 2** região com um publicador que tem o nome da saudação **microsoft** nele.</span><span class="sxs-lookup"><span data-stu-id="4ac27-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="4ac27-156">fluxo de trabalho Olá para a criação de um conjunto de escala de máquina virtual é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4ac27-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="4ac27-157">Crie um objeto de configuração que contém informações sobre o conjunto de escala hello.</span><span class="sxs-lookup"><span data-stu-id="4ac27-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="4ac27-158">Imagem de sistema operacional base Olá de referência.</span><span class="sxs-lookup"><span data-stu-id="4ac27-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="4ac27-159">Definir as configurações do sistema operacional Olá: autenticação, o prefixo do nome VM e o usuário/senha.</span><span class="sxs-lookup"><span data-stu-id="4ac27-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="4ac27-160">Configurar a rede.</span><span class="sxs-lookup"><span data-stu-id="4ac27-160">Configure networking.</span></span>
5. <span data-ttu-id="4ac27-161">Crie conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ac27-161">Create hello scale set.</span></span>

<span data-ttu-id="4ac27-162">Este exemplo cria um conjunto de dimensionamento básico de duas instâncias para um computador com o Windows Server 2016 instalado.</span><span class="sxs-lookup"><span data-stu-id="4ac27-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="4ac27-163">Usar uma imagem de máquina virtual personalizada</span><span class="sxs-lookup"><span data-stu-id="4ac27-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="4ac27-164">Se você estiver criando uma escala de conjunto de sua própria imagem personalizada, em vez de fazer referência a uma imagem de máquina virtual da Galeria hello, Olá _AzureRmVmssStorageProfile conjunto_ comando teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4ac27-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="4ac27-165">Criar usando um modelo</span><span class="sxs-lookup"><span data-stu-id="4ac27-165">Create from a template</span></span>

<span data-ttu-id="4ac27-166">Você pode implantar um conjunto de dimensionamento de máquinas virtuais usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ac27-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="4ac27-167">Você pode criar seu próprio modelo ou usar um de saudação [repositório de modelos](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="4ac27-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="4ac27-168">Esses modelos podem ser implantados diretamente tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac27-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="4ac27-169">toocreate seu próprio modelo, você cria um arquivo de texto JSON.</span><span class="sxs-lookup"><span data-stu-id="4ac27-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="4ac27-170">Para obter informações gerais sobre como toocreate e personalizar um modelo, consulte [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4ac27-171">Um modelo de exemplo está disponível [no GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="4ac27-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="4ac27-172">Para obter mais informações sobre como toocreate e usar esse exemplo, consulte [conjunto de escala viável mínimo](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="4ac27-173">Criar com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ac27-173">Create from Visual Studio</span></span>

<span data-ttu-id="4ac27-174">Com o Visual Studio, você pode criar um projeto do grupo de recursos do Azure e adicionar que modelo tooit do conjunto de uma escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4ac27-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="4ac27-175">Você pode escolher se deseja tooimport do GitHub ou hello Galeria de aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac27-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="4ac27-176">Um script de implantação do PowerShell também é gerado para você.</span><span class="sxs-lookup"><span data-stu-id="4ac27-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="4ac27-177">Para obter mais informações, consulte [como toocreate uma escala de máquina virtual definido com o Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="4ac27-178">Criar a partir de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4ac27-178">Create from hello Azure portal</span></span>

<span data-ttu-id="4ac27-179">Olá portal do Azure fornece uma maneira conveniente tooquickly criar um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="4ac27-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="4ac27-180">Para obter mais informações, consulte [como toocreate uma escala de máquina virtual definido com hello portal do Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ac27-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ac27-181">Next steps</span></span>

<span data-ttu-id="4ac27-182">Saiba mais sobre [discos de dados](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="4ac27-183">Saiba como muito[gerenciar seus aplicativos](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ac27-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
