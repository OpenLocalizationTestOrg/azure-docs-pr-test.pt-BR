---
title: "aaaCreate uma máquina Virtual do SQL Server no Azure PowerShell (clássico) | Microsoft Docs"
description: "Fornece etapas e scripts do PowerShell para criar uma VM do Azure com imagens da galeria de máquinas virtuais do SQL Server. Este tópico usa o modo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="0fc57-104">Provisionar uma máquina virtual do SQL Server usando o Azure PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="0fc57-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="0fc57-105">Este artigo fornece etapas para como toocreate uma máquina de virtual do SQL Server no Azure usando Olá cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fc57-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0fc57-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0fc57-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0fc57-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="0fc57-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0fc57-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fc57-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="0fc57-109">Para a versão do Gerenciador de recursos de saudação deste tópico, consulte [provisionar uma máquina virtual do SQL Server usando o Gerenciador de recursos do Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="0fc57-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="0fc57-110">Instalar e configurar o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0fc57-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="0fc57-111">Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fc57-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="0fc57-112">[Baixe e instale os comandos do PowerShell do Azure mais recentes Olá](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0fc57-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="0fc57-113">Inicie o Windows PowerShell e conectá-lo tooyour assinatura do Azure com hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="0fc57-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="0fc57-114">Determinar o região de destino do Azure</span><span class="sxs-lookup"><span data-stu-id="0fc57-114">Determine your target Azure region</span></span>

<span data-ttu-id="0fc57-115">A máquina virtual do SQL Server será hospedada em um serviço de nuvem que reside em uma região específica do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc57-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="0fc57-116">Olá etapas a seguir ajudam você toodetermine sua região, a conta de armazenamento e o serviço de nuvem que será usado para o restante de saudação do tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fc57-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="0fc57-117">Determine o Datacenter Olá que você deseja toouse toohost VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fc57-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="0fc57-118">saudação de comando do PowerShell a seguir exibe uma lista de nomes de região disponível.</span><span class="sxs-lookup"><span data-stu-id="0fc57-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="0fc57-119">Depois de identificar o local preferencial, definir uma variável denominada **$dcLocation** toothat região.</span><span class="sxs-lookup"><span data-stu-id="0fc57-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="0fc57-120">Por exemplo, Olá conjuntos Olá região muito de comando a seguir "Leste dos Estados Unidos":</span><span class="sxs-lookup"><span data-stu-id="0fc57-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="0fc57-121">Definir a assinatura e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0fc57-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="0fc57-122">Determine Olá assinatura do Azure que você usará para a máquina virtual da nova hello.</span><span class="sxs-lookup"><span data-stu-id="0fc57-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="0fc57-123">Atribuir o toohello de assinatura do Azure de destino **$subscr** variável.</span><span class="sxs-lookup"><span data-stu-id="0fc57-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="0fc57-124">Em seguida, defina isso como sua assinatura atual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc57-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="0fc57-125">Verifique se há contas de armazenamento existentes.</span><span class="sxs-lookup"><span data-stu-id="0fc57-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="0fc57-126">Olá, script a seguir exibe todas as contas de armazenamento que existem em sua região escolhida:</span><span class="sxs-lookup"><span data-stu-id="0fc57-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="0fc57-127">Se você precisar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento de todas as minúsculas com o comando Olá novo AzureStorageAccount como Olá exemplo a seguir:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="0fc57-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="0fc57-128">Atribuir Olá destino armazenamento conta nome toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="0fc57-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="0fc57-129">Em seguida, use **Set-AzureSubscription** tooset Olá assinatura e a conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="0fc57-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="0fc57-130">Selecione uma imagem de máquina virtual do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0fc57-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="0fc57-131">Descobrir a lista de saudação de imagens de máquinas virtuais do SQL Server disponíveis na Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fc57-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="0fc57-132">Todas essas imagens têm uma propriedade **ImageFamily** que começa com "SQL".</span><span class="sxs-lookup"><span data-stu-id="0fc57-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="0fc57-133">consulta a seguir de saudação exibe Olá imagem família disponível tooyou com o SQL Server pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="0fc57-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="0fc57-134">Quando você encontrar família de imagem de máquina virtual hello, pode haver várias imagens publicadas nesta família.</span><span class="sxs-lookup"><span data-stu-id="0fc57-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="0fc57-135">Script a seguir de saudação do uso toofind hello mais recente publicada imagem nome da máquina virtual para sua família de imagem selecionada (como **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="0fc57-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="0fc57-136">Criar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="0fc57-136">Create hello virtual machine</span></span>

<span data-ttu-id="0fc57-137">Finalmente, crie a máquina virtual de saudação com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0fc57-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="0fc57-138">Criar uma nuvem toohost serviço Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="0fc57-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="0fc57-139">Observe que também é possível toouse um serviço de nuvem existente em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0fc57-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="0fc57-140">Criar uma nova variável **$svcname** com o nome curto de Olá Olá do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0fc57-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="0fc57-141">Especifique o nome da máquina virtual hello e um tamanho.</span><span class="sxs-lookup"><span data-stu-id="0fc57-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="0fc57-142">Para obter mais informações sobre tamanhos de máquina virtual, consulte [Tamanhos de Máquina Virtual para o Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc57-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="0fc57-143">Especifique a senha e a conta de administrador local hello.</span><span class="sxs-lookup"><span data-stu-id="0fc57-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="0fc57-144">Execute Olá máquina virtual do script toocreate Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fc57-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="0fc57-145">Para explicação adicional e opções de configuração, consulte Olá **criar o conjunto de comandos** seção [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc57-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="0fc57-146">Exemplo de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc57-146">Example PowerShell script</span></span>

<span data-ttu-id="0fc57-147">Olá, script a seguir fornece um exemplo de um script completo que cria um **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2** máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0fc57-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="0fc57-148">Se você usar esse script, você deve personalizar variáveis inicial hello, com base em etapas de saudação anterior neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0fc57-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="0fc57-149">Conectar-se à área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="0fc57-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="0fc57-150">Crie arquivos RDP de saudação em toolaunch de pasta de documentos do usuário atual Olá instalação de toocomplete essas máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="0fc57-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="0fc57-151">No diretório de documentos hello, inicie o arquivo RDP de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fc57-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="0fc57-152">Conecte-se com o nome de usuário de administrador hello e a senha fornecidos anteriormente (por exemplo, se seu nome de usuário foi VMAdmin, especifique "\VMAdmin" como usuário hello e fornecer a senha de saudação).</span><span class="sxs-lookup"><span data-stu-id="0fc57-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="0fc57-153">Configuração de saudação completa de saudação máquina do SQL Server para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="0fc57-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="0fc57-154">Depois de fazer logon na máquina toohello com área de trabalho remota, configurar o SQL Server com base nas instruções de saudação em [etapas para configurar a conectividade do SQL Server em uma VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="0fc57-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc57-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fc57-155">Next steps</span></span>

<span data-ttu-id="0fc57-156">Você pode encontrar instruções adicionais para o provisionamento de máquinas virtuais com o PowerShell Olá [documentação de máquinas virtuais](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc57-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="0fc57-157">Em muitos casos, a saudação próxima etapa é toomigrate toothis seus bancos de dados nova VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fc57-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="0fc57-158">Para obter diretrizes de migração do banco de dados, consulte [migrando um banco de dados tooSQL Server em uma VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fc57-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="0fc57-159">Se você também está interessado em usar Olá toocreate portal do Azure máquinas virtuais do SQL, consulte [provisionar uma máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0fc57-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="0fc57-160">Observe que esse tutorial Olá que aborda a que você por meio do portal Olá cria VMs usando Olá modelo recomendado do Gerenciador de recursos, em vez de um modelo clássico Olá usado neste tópico do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fc57-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="0fc57-161">Além de recursos de toothese, é recomendável que você examine [outros tópicos relacionados toorunning do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0fc57-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
