---
title: aaaHow toocreate imagens de VM do Windows Azure com Packer | Microsoft Docs
description: "Saiba como imagens de toocreate Packer toouse de máquinas virtuais do Windows no Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="3bbee-103">Como as imagens de máquina virtual do toouse Packer toocreate Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="3bbee-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="3bbee-104">Cada máquina virtual (VM) no Azure é criada a partir de uma imagem que define hello distribuição do Windows e a versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3bbee-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="3bbee-105">As imagens podem incluir configurações e aplicativos pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="3bbee-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="3bbee-106">Hello Azure Marketplace fornece muitas imagens primeira e terceiro para o sistema operacional mais comuns e ambientes de aplicativo, ou você pode criar suas próprias necessidades de tooyour personalizadas de imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3bbee-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="3bbee-107">Este artigo detalha como toouse Olá abrir a ferramenta de origem [Packer](https://www.packer.io/) toodefine e criar imagens personalizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="3bbee-108">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbee-108">Create Azure resource group</span></span>
<span data-ttu-id="3bbee-109">Durante o processo de compilação hello, Packer cria temporários recursos do Azure, ele cria a VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="3bbee-110">toocapture que a VM de origem para uso como uma imagem, você deve definir um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3bbee-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="3bbee-111">Hello saída do processo de compilação Packer Olá é armazenada no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3bbee-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="3bbee-112">Crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3bbee-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="3bbee-113">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="3bbee-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="3bbee-114">Criar as credenciais do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbee-114">Create Azure credentials</span></span>
<span data-ttu-id="3bbee-115">O Packer se autentica no Azure usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3bbee-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="3bbee-116">Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Packer.</span><span class="sxs-lookup"><span data-stu-id="3bbee-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="3bbee-117">Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbee-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="3bbee-118">Criar um serviço principal com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) e atribuir permissões para toocreate principal do serviço hello e gerenciar recursos com [AzureRmRoleAssignment novo](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="3bbee-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="3bbee-119">tooauthenticate tooAzure, você também precisa tooobtain suas IDs de locatário e assinatura do Azure com [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="3bbee-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="3bbee-120">Você pode usar essas duas IDs na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="3bbee-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="3bbee-121">Definir modelo do Packer</span><span class="sxs-lookup"><span data-stu-id="3bbee-121">Define Packer template</span></span>
<span data-ttu-id="3bbee-122">toobuild imagens, criar um modelo como um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="3bbee-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="3bbee-123">No modelo de hello, definir construtores e provisioners realizarem Olá real do processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="3bbee-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="3bbee-124">Packer tem um [provedor do Azure](https://www.packer.io/docs/builders/azure.html) que permite a você toodefine Azure recursos, como credenciais do serviço principal do hello criados no hello anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="3bbee-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="3bbee-125">Crie um arquivo chamado *windows.json* e colar Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3bbee-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="3bbee-126">Insira seus próprios valores para os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="3bbee-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="3bbee-127">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3bbee-127">Parameter</span></span>                           | <span data-ttu-id="3bbee-128">Onde tooobtain</span><span class="sxs-lookup"><span data-stu-id="3bbee-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="3bbee-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="3bbee-129">*client_id*</span></span>                         | <span data-ttu-id="3bbee-130">Exiba a ID da entidade de serviço com `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="3bbee-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="3bbee-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="3bbee-131">*client_secret*</span></span>                     | <span data-ttu-id="3bbee-132">Senha especificada em `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="3bbee-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="3bbee-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="3bbee-133">*tenant_id*</span></span>                         | <span data-ttu-id="3bbee-134">Saída do comando `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="3bbee-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="3bbee-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="3bbee-135">*subscription_id*</span></span>                   | <span data-ttu-id="3bbee-136">Saída do comando `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="3bbee-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="3bbee-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="3bbee-137">*object_id*</span></span>                         | <span data-ttu-id="3bbee-138">Exiba a ID de objeto da entidade de serviço com `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="3bbee-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="3bbee-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="3bbee-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="3bbee-140">Nome do grupo de recursos que você criou na etapa primeiro Olá</span><span class="sxs-lookup"><span data-stu-id="3bbee-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="3bbee-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="3bbee-141">*managed_image_name*</span></span>                | <span data-ttu-id="3bbee-142">Nome de imagem de disco gerenciado Olá criado</span><span class="sxs-lookup"><span data-stu-id="3bbee-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="3bbee-143">Este modelo cria uma VM do Windows Server 2016, instala o IIS e generaliza Olá VM com Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3bbee-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="3bbee-144">Criar uma imagem do Packer</span><span class="sxs-lookup"><span data-stu-id="3bbee-144">Build Packer image</span></span>
<span data-ttu-id="3bbee-145">Se ainda não tiver instalado em seu computador local, de Packer [siga as instruções de instalação do hello Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="3bbee-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="3bbee-146">Crie imagem Olá especificando seu Packer arquivo de modelo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3bbee-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="3bbee-147">Um exemplo da saída de hello de saudação anterior comandos é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3bbee-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="3bbee-148">Levará alguns minutos para saudação de toobuild Packer VM, execute provisioners Olá e limpar Olá implantação.</span><span class="sxs-lookup"><span data-stu-id="3bbee-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="3bbee-149">Criar uma VM com base em uma Imagem do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbee-149">Create VM from Azure Image</span></span>
<span data-ttu-id="3bbee-150">Definir um administrador de nome de usuário e senha para Olá VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="3bbee-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="3bbee-151">Agora você pode criar uma VM com base na Imagem com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3bbee-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="3bbee-152">Olá, exemplo a seguir cria uma VM denominada *myVM* de *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="3bbee-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="3bbee-153">Ele usa Olá toocreate de alguns minutos VM.</span><span class="sxs-lookup"><span data-stu-id="3bbee-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="3bbee-154">Testar a VM e o IIS</span><span class="sxs-lookup"><span data-stu-id="3bbee-154">Test VM and IIS</span></span>
<span data-ttu-id="3bbee-155">Obter o endereço IP público de saudação da VM com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="3bbee-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="3bbee-156">Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="3bbee-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="3bbee-157">Você pode inserir o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="3bbee-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Site do IIS padrão](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="3bbee-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3bbee-159">Next steps</span></span>
<span data-ttu-id="3bbee-160">Neste exemplo, você usou Packer toocreate uma imagem de VM com o IIS já está instalado.</span><span class="sxs-lookup"><span data-stu-id="3bbee-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="3bbee-161">Você pode usar esta imagem VM junto com a implantação fluxos de trabalho existentes, como toodeploy tooVMs seu aplicativo criado a partir de saudação imagem com Team Services, Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="3bbee-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="3bbee-162">Para obter outros modelos de exemplo do Packer para outras distribuições do Windows, consulte [este repositório GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="3bbee-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>