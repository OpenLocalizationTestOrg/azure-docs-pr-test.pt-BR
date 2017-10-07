---
title: "aaaAzure híbrida benefício de usar para o Windows Server e Windows Client | Microsoft Docs"
description: "Saiba como toomaximize seu toobring benefícios de garantia de Software do Windows local tooAzure de licenças"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="26a40-103">Benefício de Uso Híbrido do Azure para o Windows Server e o Windows Client</span><span class="sxs-lookup"><span data-stu-id="26a40-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="26a40-104">Para clientes com Software Assurance, o benefício de uso do Azure híbrido permite toouse suas licenças de cliente Windows Server e Windows de local e executadas máquinas virtuais do Windows no Azure a um custo reduzido.</span><span class="sxs-lookup"><span data-stu-id="26a40-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="26a40-105">O Benefício de Uso Híbrido do Azure para o Windows Server inclui o Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="26a40-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="26a40-106">O Benefício de Uso Híbrido do Azure para o Windows Client inclui o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="26a40-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="26a40-107">Para obter mais informações, consulte Olá [página de licenciamento do benefício de uso do Azure híbrido](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="26a40-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="26a40-108">Azure híbrido Use benefícios para o cliente do Windows está atualmente em visualização usando imagem Olá Windows 10 em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="26a40-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="26a40-109">Somente clientes Enterprise com o Windows 10 Enterprise E3/E5 por usuário ou o Windows VDA por usuário (Licenças de Assinatura de Usuário ou Licenças de Assinatura de Usuário Complementares) (“Licenças Aplicáveis”) são qualificados.</span><span class="sxs-lookup"><span data-stu-id="26a40-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="26a40-110">Maneiras toouse benefício de uso do Azure híbrido</span><span class="sxs-lookup"><span data-stu-id="26a40-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="26a40-111">Há duas maneiras diferentes toodeploy VMs do Windows com hello benefício de uso do Azure híbrido:</span><span class="sxs-lookup"><span data-stu-id="26a40-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="26a40-112">Você pode implantar VMs das [imagens específicas do Marketplace](#deploy-a-vm-using-the-azure-marketplace) que são pré-configuradas com o benefício de uso do Azure Hybrid – Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="26a40-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="26a40-113">Você pode [carregar uma VM personalizada](#upload-a-windows-vhd) e [implantar usando um modelo do Resource Manager](#deploy-a-vm-via-resource-manager) ou [do Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="26a40-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="26a40-114">Implantar uma VM usando hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="26a40-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="26a40-115">Imagens a seguir estão disponíveis no hello Marketplace pré-configurado com o benefício de uso do Azure híbrido: Windows Server 2016, o Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="26a40-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="26a40-116">Essas imagens podem ser implantadas diretamente de saudação portal do Azure, modelos do Gerenciador de recursos ou do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="26a40-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="26a40-117">Você pode implantar essas imagens diretamente do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26a40-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="26a40-118">Para uso em modelos do Gerenciador de recursos e com o Azure PowerShell, exiba a lista de saudação de imagens da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="26a40-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="26a40-119">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="26a40-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="26a40-120">2016-Datacenter versão 2016.127.20170406 ou superior</span><span class="sxs-lookup"><span data-stu-id="26a40-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="26a40-121">2012-R2-Datacenter versão 4.127.20170406 ou superior</span><span class="sxs-lookup"><span data-stu-id="26a40-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="26a40-122">2012-Datacenter versão 3.127.20170406 ou superior</span><span class="sxs-lookup"><span data-stu-id="26a40-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="26a40-123">2008-R2-SP1 versão 2.127.20170406 ou superior</span><span class="sxs-lookup"><span data-stu-id="26a40-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="26a40-124">Para Windows Client:</span><span class="sxs-lookup"><span data-stu-id="26a40-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="26a40-125">Carregar um VHD do Windows Server</span><span class="sxs-lookup"><span data-stu-id="26a40-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="26a40-126">toodeploy uma VM do Windows Server no Azure, você primeiro precisa toocreate um VHD que contém seu build do Windows base.</span><span class="sxs-lookup"><span data-stu-id="26a40-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="26a40-127">Esse VHD deve estar preparado adequadamente por meio de Sysprep antes de carregá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="26a40-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="26a40-128">Você pode [Leia mais sobre o processo do Sysprep e os requisitos de VHD de saudação](upload-generalized-managed.md) e [suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="26a40-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="26a40-129">Faça backup Olá VM antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="26a40-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="26a40-130">Verifique se você tem [mais recente do PowerShell do Azure instalado e configurado hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26a40-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="26a40-131">Depois de preparar o VHD, carregar conta de armazenamento do Azure Olá VHD tooyour usando Olá `Add-AzureRmVhd` cmdlet da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="26a40-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="26a40-132">O Microsoft SQL Server, SharePoint Server e Dynamics também podem utilizar o licenciamento Software Assurance.</span><span class="sxs-lookup"><span data-stu-id="26a40-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="26a40-133">Você ainda precisa imagem de servidor do Windows hello tooprepare instalando os componentes do aplicativo e fornecendo as chaves de licença adequadamente, em seguida, carregar Olá tooAzure de imagem de disco.</span><span class="sxs-lookup"><span data-stu-id="26a40-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="26a40-134">Examine a documentação apropriada Olá para executar o Sysprep com seu aplicativo, como [considerações sobre a instalação do SQL Server usando Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) ou [montar uma imagem de referência do SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="26a40-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="26a40-135">Você também pode ler mais sobre [Olá VHD tooAzure processo de carregamento](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="26a40-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="26a40-136">Implantar uma VM por meio de um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26a40-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="26a40-137">Nos modelos do Resource Manager, um parâmetro adicional para `licenseType` pode ser especificado.</span><span class="sxs-lookup"><span data-stu-id="26a40-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="26a40-138">Você pode ler mais sobre a [criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="26a40-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="26a40-139">Uma vez que o VHD carregado tooAzure, edite é o tipo de licença do Gerenciador de recursos modelo tooinclude hello como parte da saudação provedor de computação e implantar o modelo como normal:</span><span class="sxs-lookup"><span data-stu-id="26a40-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="26a40-140">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="26a40-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="26a40-141">Para o cliente do Windows toouse com a imagem do Azure Marketplace só:</span><span class="sxs-lookup"><span data-stu-id="26a40-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="26a40-142">Implantar uma VM por meio do início rápido do PowerShell</span><span class="sxs-lookup"><span data-stu-id="26a40-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="26a40-143">Ao implantar a VM do Windows Server por meio do PowerShell, você tem um parâmetro adicional para `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="26a40-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="26a40-144">Uma vez que o VHD carregado tooAzure, criar uma VM usando `New-AzureRmVM` e especificar o tipo de licenciamento de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="26a40-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="26a40-145">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="26a40-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="26a40-146">Para o cliente do Windows toouse com a imagem do Azure Marketplace só:</span><span class="sxs-lookup"><span data-stu-id="26a40-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="26a40-147">Você pode [ler uma explicação mais detalhada sobre como implantar uma VM no Azure por meio do PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) abaixo ou leitura um guia mais descritivo Olá diferentes etapas muito[criar uma VM do Windows usando o Gerenciador de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26a40-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="26a40-148">Verifique se que a VM está utilizando o benefício de licenciamento Olá</span><span class="sxs-lookup"><span data-stu-id="26a40-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="26a40-149">Depois de implantar sua VM por meio de saudação do PowerShell ou método de implantação do Gerenciador de recursos, verificar o tipo de licença de saudação com `Get-AzureRmVM` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="26a40-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="26a40-150">saudação de saída é similar toohello exemplo a seguir para o Windows Server:</span><span class="sxs-lookup"><span data-stu-id="26a40-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="26a40-151">Essa saída contrasta com hello que seguir VM implantada sem licenciamento benefício de uso do Azure híbrido, como uma VM implantada diretamente da saudação Galeria do Azure:</span><span class="sxs-lookup"><span data-stu-id="26a40-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="26a40-152">Passo a passo detalhado de implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="26a40-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="26a40-153">a seguir Olá detalhadas Mostrar de etapas do PowerShell uma implantação completa de uma VM.</span><span class="sxs-lookup"><span data-stu-id="26a40-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="26a40-154">Você pode ler mais contexto como cmdlets real toohello e componentes diferentes, que está sendo criados no [criar uma VM do Windows usando o Gerenciador de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26a40-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="26a40-155">Você passa pela criação de seu grupo de recursos, da conta de armazenamento e da rede virtual e, por fim, define e crie sua VM.</span><span class="sxs-lookup"><span data-stu-id="26a40-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="26a40-156">Primeiro, obtenha credenciais com segurança, defina um local e o nome do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="26a40-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="26a40-157">Criar um IP público:</span><span class="sxs-lookup"><span data-stu-id="26a40-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="26a40-158">Defina sua sub-rede, NIC e VNET:</span><span class="sxs-lookup"><span data-stu-id="26a40-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="26a40-159">Nomeie sua VM e crie uma configuração da VM:</span><span class="sxs-lookup"><span data-stu-id="26a40-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="26a40-160">Defina seu sistema operacional:</span><span class="sxs-lookup"><span data-stu-id="26a40-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="26a40-161">Adicione seu toohello NIC VM:</span><span class="sxs-lookup"><span data-stu-id="26a40-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="26a40-162">Defina Olá toouse de conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="26a40-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="26a40-163">Carregar o VHD, adequadamente preparado e anexar tooyour VM para uso:</span><span class="sxs-lookup"><span data-stu-id="26a40-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="26a40-164">Finalmente, crie sua VM e definir Olá tipo tooutilize benefício de uso do Azure híbrido de licenciamento:</span><span class="sxs-lookup"><span data-stu-id="26a40-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="26a40-165">Para Windows Server:</span><span class="sxs-lookup"><span data-stu-id="26a40-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="26a40-166">Implantar um conjunto de dimensionamento de máquinas virtuais por meio do modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="26a40-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="26a40-167">Nos modelos do Gerenciador de Recursos VMSS, um parâmetro adicional para `licenseType` deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="26a40-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="26a40-168">Você pode ler mais sobre a [criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="26a40-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="26a40-169">Editar a propriedade de licenseType saudação do Gerenciador de recursos modelo tooinclude como parte do virtualMachineProfile do conjunto de escala hello e implantar o modelo como normal - consulte o exemplo a seguir usando a imagem do Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="26a40-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="26a40-170">O suporte para implantação de um conjunto de dimensionamento da máquina virtual com benefícios AHUB por meio do PowerShell e de outras ferramentas de SDK está disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="26a40-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="26a40-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26a40-171">Next steps</span></span>
<span data-ttu-id="26a40-172">Leia mais sobre o [Licenciamento do Benefício de Uso Híbrido do Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="26a40-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="26a40-173">Saiba mais sobre como [usar os modelos do Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26a40-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="26a40-174">Saiba mais sobre [benefício de usar híbrido do Azure e o Azure Site Recovery fazem migração tooAzure de aplicativos ainda mais econômica](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="26a40-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
