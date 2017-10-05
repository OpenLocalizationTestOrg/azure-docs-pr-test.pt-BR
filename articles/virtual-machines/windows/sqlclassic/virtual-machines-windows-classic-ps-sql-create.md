---
title: "Criar uma máquina virtual do SQL Server no Azure PowerShell (Clássico) | Microsoft Docs"
description: "Fornece etapas e scripts do PowerShell para criar uma VM do Azure com imagens da galeria de máquinas virtuais do SQL Server. Este tópico usa o modo de implantação clássico."
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
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="ff7a5-104">Provisionar uma máquina virtual do SQL Server usando o Azure PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="ff7a5-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="ff7a5-105">Este artigo fornece as etapas para a criação de uma máquina virtual do SQL Server no Azure usando os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ff7a5-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff7a5-107">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ff7a5-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="ff7a5-109">Para obter a versão do Resource Manager desse tópico, consulte [Provisionar uma máquina virtual do SQL Server usando o Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="ff7a5-110">Instalar e configurar o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ff7a5-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="ff7a5-111">Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="ff7a5-112">[Baixe e instale os comandos mais recentes do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="ff7a5-113">Em seguida, conecte o Windows PowerShell à sua assinatura do Azure usando o comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="ff7a5-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="ff7a5-114">Determinar o região de destino do Azure</span><span class="sxs-lookup"><span data-stu-id="ff7a5-114">Determine your target Azure region</span></span>

<span data-ttu-id="ff7a5-115">A máquina virtual do SQL Server será hospedada em um serviço de nuvem que reside em uma região específica do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="ff7a5-116">As etapas a seguir ajudam a determinar sua região, a conta de armazenamento e o serviço de nuvem que será usado para o restante do tutorial.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="ff7a5-117">Determine o data center que você deseja usar para hospedar a VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="ff7a5-118">O comando do PowerShell a seguir exibe uma lista de nomes de região disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="ff7a5-119">Depois de identificar seu local preferido, defina uma variável chamada **$dcLocation** para essa região.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="ff7a5-120">Por exemplo, o comando a seguir define a região como "Leste dos EUA":</span><span class="sxs-lookup"><span data-stu-id="ff7a5-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="ff7a5-121">Definir a assinatura e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ff7a5-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="ff7a5-122">Determine a assinatura do Azure que você usará para a nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="ff7a5-123">Atribua sua assinatura de destino do Azure à variável **$subscr** .</span><span class="sxs-lookup"><span data-stu-id="ff7a5-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="ff7a5-124">Em seguida, defina isso como sua assinatura atual do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="ff7a5-125">Verifique se há contas de armazenamento existentes.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="ff7a5-126">O script a seguir exibe todas as contas de armazenamento existentes em sua região escolhida:</span><span class="sxs-lookup"><span data-stu-id="ff7a5-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="ff7a5-127">Se precisar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento com todas as letras minúsculas usando o comando New-AzureStorageAccount, como mostra o seguinte exemplo: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="ff7a5-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="ff7a5-128">Atribua o nome da conta de armazenamento de destino para **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="ff7a5-129">Em seguida, use **Set-AzureSubscription** para definir a assinatura e a conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="ff7a5-130">Selecione uma imagem de máquina virtual do SQL Server</span><span class="sxs-lookup"><span data-stu-id="ff7a5-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="ff7a5-131">Descubra a lista de imagens de máquinas virtuais do SQL Server disponíveis na Galeria.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="ff7a5-132">Todas essas imagens têm uma propriedade **ImageFamily** que começa com "SQL".</span><span class="sxs-lookup"><span data-stu-id="ff7a5-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="ff7a5-133">A consulta a seguir exibe a família de imagens disponível com o SQL Server pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="ff7a5-134">Quando você encontrar a família de imagens da máquina virtual, talvez existam várias imagens publicadas nessa família.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="ff7a5-135">Use o script a seguir para localizar o nome de imagem de máquina virtual publicado recentemente para sua família de imagens selecionada (por exemplo, **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="ff7a5-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="ff7a5-136">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ff7a5-136">Create the virtual machine</span></span>

<span data-ttu-id="ff7a5-137">Por fim, crie a máquina virtual com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ff7a5-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="ff7a5-138">Crie um serviço de nuvem para hospedar a nova VM.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="ff7a5-139">Observe que também é possível usar um serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="ff7a5-140">Crie uma nova variável **$svcname** com o nome curto do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="ff7a5-141">Especifique o nome e o tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="ff7a5-142">Para obter mais informações sobre tamanhos de máquina virtual, consulte [Tamanhos de Máquina Virtual para o Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="ff7a5-143">Especifique a conta de administrador local e a senha.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="ff7a5-144">Execute o script a seguir para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="ff7a5-145">Para obter explicações adicionais e outras opções de configuração, consulte a seção **Criar o conjunto de comandos** em [Usar o Azure PowerShell para criar e pré-configurar as Máquinas Virtuais baseadas no Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="ff7a5-146">Exemplo de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff7a5-146">Example PowerShell script</span></span>

<span data-ttu-id="ff7a5-147">O script a seguir fornece um exemplo de um script completo que cria uma máquina virtual **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2** .</span><span class="sxs-lookup"><span data-stu-id="ff7a5-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="ff7a5-148">Se você usar esse script, personalize as variáveis iniciais com base nas etapas anteriores deste tópico.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="ff7a5-149">Conectar-se à área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="ff7a5-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="ff7a5-150">Crie os arquivos RDP na pasta de documentos do usuário atual para iniciar essas máquinas virtuais e concluir a instalação:</span><span class="sxs-lookup"><span data-stu-id="ff7a5-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="ff7a5-151">No diretório de documentos, inicie o arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="ff7a5-152">Conecte-se com o nome de usuário e a senha de administrador fornecidos anteriormente (por exemplo, se o nome de usuário era VMAdmin, especifique "\VMAdmin" como o usuário e forneça a senha).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="ff7a5-153">Concluir a configuração da Máquina do SQL Server para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="ff7a5-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="ff7a5-154">Depois de fazer logon no computador com a área de trabalho remota, configure o SQL Server com base nas instruções em [Etapas para configurar a conectividade do SQL Server em uma VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7a5-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff7a5-155">Next steps</span></span>

<span data-ttu-id="ff7a5-156">Encontre mais instruções para o provisionamento de máquinas virtuais com o PowerShell na [documentação das máquinas virtuais](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="ff7a5-157">Em muitos casos, a próxima etapa é migrar os bancos de dados para essa nova VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="ff7a5-158">Para obter orientações sobre a migração de banco de dados, veja [Migrando um banco de dados para o SQL Server em uma VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="ff7a5-159">Se você também estiver interessado em usar o Portal do Azure para criar Máquinas Virtuais do SQL, veja [Provisionar uma máquina virtual do SQL Server no Portal do Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="ff7a5-160">Observe que o tutorial que orienta você sobre o portal cria máquinas virtuais usando o modelo recomendado do Gerenciador de Recursos, em vez do modelo clássico usado neste tópico do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff7a5-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="ff7a5-161">Além desses recursos, recomendamos ver [outros tópicos relacionados à execução do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff7a5-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
