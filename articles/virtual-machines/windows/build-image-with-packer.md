---
title: Como criar imagens de VM Windows do Azure com o Packer | Microsoft Docs
description: "Saiba como usar o Packer para criar imagens de máquinas virtuais Windows no Azure"
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
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="e85cd-103">Como usar o Packer para criar imagens de máquina virtual Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="e85cd-103">How to use Packer to create Windows virtual machine images in Azure</span></span>
<span data-ttu-id="e85cd-104">Cada VM (máquina virtual) no Azure é criada com base em uma imagem que define a distribuição do Windows e a versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e85cd-104">Each virtual machine (VM) in Azure is created from an image that defines the Windows distribution and OS version.</span></span> <span data-ttu-id="e85cd-105">As imagens podem incluir configurações e aplicativos pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="e85cd-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="e85cd-106">O Azure Marketplace fornece várias imagens internas e de terceiros para os ambientes de sistema operacional e de aplicativo mais comuns ou você pode criar suas próprias imagens personalizadas adequadas às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="e85cd-106">The Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="e85cd-107">Este artigo fornece detalhes sobre como usar a ferramenta de software livre [Packer](https://www.packer.io/) para definir e criar imagens personalizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="e85cd-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="e85cd-108">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e85cd-108">Create Azure resource group</span></span>
<span data-ttu-id="e85cd-109">Durante o processo de build, o Packer cria recursos temporários do Azure conforme cria a VM de origem.</span><span class="sxs-lookup"><span data-stu-id="e85cd-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="e85cd-110">Para capturar essa VM de origem para uso como uma imagem, você precisa definir um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e85cd-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="e85cd-111">A saída do processo de build do Packer é armazenada nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e85cd-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="e85cd-112">Crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e85cd-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e85cd-113">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="e85cd-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="e85cd-114">Criar as credenciais do Azure</span><span class="sxs-lookup"><span data-stu-id="e85cd-114">Create Azure credentials</span></span>
<span data-ttu-id="e85cd-115">O Packer se autentica no Azure usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e85cd-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="e85cd-116">Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Packer.</span><span class="sxs-lookup"><span data-stu-id="e85cd-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="e85cd-117">Você controla e define as permissões referentes a quais operações a entidade de serviço pode executar no Azure.</span><span class="sxs-lookup"><span data-stu-id="e85cd-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="e85cd-118">Crie uma entidade de serviço com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) e atribua permissões para a entidade de serviço criar e gerenciar recursos com [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="e85cd-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for the service principal to create and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="e85cd-119">Para se autenticar no Azure, você também precisa obter suas IDs de locatário e de assinatura do Azure com [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="e85cd-119">To authenticate to Azure, you also need to obtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="e85cd-120">Você pode usar essas duas IDs na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e85cd-120">You use these two IDs in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="e85cd-121">Definir modelo do Packer</span><span class="sxs-lookup"><span data-stu-id="e85cd-121">Define Packer template</span></span>
<span data-ttu-id="e85cd-122">Para criar imagens, você cria um modelo como um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="e85cd-122">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="e85cd-123">No modelo, você define construtores e provisionadores que executam o processo de build real.</span><span class="sxs-lookup"><span data-stu-id="e85cd-123">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="e85cd-124">O Packer tem um [provisionador do Azure](https://www.packer.io/docs/builders/azure.html) que permite definir recursos do Azure, como as credenciais da entidade de serviço criadas na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="e85cd-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="e85cd-125">Crie um arquivo chamado *windows.json* e cole o conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-125">Create a file named *windows.json* and paste the following content.</span></span> <span data-ttu-id="e85cd-126">Insira seus próprios valores para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e85cd-126">Enter your own values for the following:</span></span>

| <span data-ttu-id="e85cd-127">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e85cd-127">Parameter</span></span>                           | <span data-ttu-id="e85cd-128">Onde obter</span><span class="sxs-lookup"><span data-stu-id="e85cd-128">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="e85cd-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="e85cd-129">*client_id*</span></span>                         | <span data-ttu-id="e85cd-130">Exiba a ID da entidade de serviço com `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="e85cd-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="e85cd-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="e85cd-131">*client_secret*</span></span>                     | <span data-ttu-id="e85cd-132">Senha especificada em `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="e85cd-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="e85cd-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="e85cd-133">*tenant_id*</span></span>                         | <span data-ttu-id="e85cd-134">Saída do comando `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="e85cd-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="e85cd-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="e85cd-135">*subscription_id*</span></span>                   | <span data-ttu-id="e85cd-136">Saída do comando `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="e85cd-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="e85cd-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="e85cd-137">*object_id*</span></span>                         | <span data-ttu-id="e85cd-138">Exiba a ID de objeto da entidade de serviço com `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="e85cd-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="e85cd-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="e85cd-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="e85cd-140">Nome do grupo de recursos que você criou na primeira etapa</span><span class="sxs-lookup"><span data-stu-id="e85cd-140">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="e85cd-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="e85cd-141">*managed_image_name*</span></span>                | <span data-ttu-id="e85cd-142">Nome da imagem de disco gerenciado que é criada</span><span class="sxs-lookup"><span data-stu-id="e85cd-142">Name for the managed disk image that is created</span></span> |

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

<span data-ttu-id="e85cd-143">Este modelo cria uma VM Windows Server 2016, instala o IIS e generaliza a VM com o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e85cd-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes the VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="e85cd-144">Criar uma imagem do Packer</span><span class="sxs-lookup"><span data-stu-id="e85cd-144">Build Packer image</span></span>
<span data-ttu-id="e85cd-145">Se você ainda não tiver o Packer instalado no computador local, [siga as instruções de instalação do Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="e85cd-145">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="e85cd-146">Crie a imagem especificando o arquivo de modelo do Packer da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e85cd-146">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="e85cd-147">Um exemplo da saída dos comandos anteriores é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e85cd-147">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="e85cd-148">São necessários alguns minutos para que o Packer crie a VM, execute os provisionadores e limpe a implantação.</span><span class="sxs-lookup"><span data-stu-id="e85cd-148">It takes a few minutes for Packer to build the VM, run the provisioners, and clean up the deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="e85cd-149">Criar uma VM com base em uma Imagem do Azure</span><span class="sxs-lookup"><span data-stu-id="e85cd-149">Create VM from Azure Image</span></span>
<span data-ttu-id="e85cd-150">Defina o nome de usuário e a senha de um administrador para as VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="e85cd-150">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="e85cd-151">Agora você pode criar uma VM com base na Imagem com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e85cd-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="e85cd-152">O exemplo a seguir cria uma VM chamada *myVM* com base em *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="e85cd-152">The following example creates a VM named *myVM* from *myPackerImage*.</span></span>

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

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="e85cd-153">São necessários alguns minutos para criar a VM.</span><span class="sxs-lookup"><span data-stu-id="e85cd-153">It takes a few minutes to create the VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="e85cd-154">Testar a VM e o IIS</span><span class="sxs-lookup"><span data-stu-id="e85cd-154">Test VM and IIS</span></span>
<span data-ttu-id="e85cd-155">Obtenha os endereços IP públicos da VM com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="e85cd-155">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="e85cd-156">O exemplo a seguir obtém o endereço IP para *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e85cd-156">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="e85cd-157">Você pode inserir o endereço IP público em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="e85cd-157">You can then enter the public IP address in to a web browser.</span></span>

![Site do IIS padrão](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="e85cd-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e85cd-159">Next steps</span></span>
<span data-ttu-id="e85cd-160">Neste exemplo, você usou o Packer para criar uma imagem de VM com o IIS já instalado.</span><span class="sxs-lookup"><span data-stu-id="e85cd-160">In this example, you used Packer to create a VM image with IIS already installed.</span></span> <span data-ttu-id="e85cd-161">Use essa imagem de VM junto com os fluxos de trabalho de implantação existentes para, por exemplo, implantar o aplicativo em VMs criadas com base na Imagem com o Team Services, Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="e85cd-161">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="e85cd-162">Para obter outros modelos de exemplo do Packer para outras distribuições do Windows, consulte [este repositório GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="e85cd-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>