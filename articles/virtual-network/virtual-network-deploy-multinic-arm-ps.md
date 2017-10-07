---
title: "aaaCreate uma VM com várias NICs - PowerShell do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com várias placas de rede usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="c24d4-103">Criar uma VM com diversas NICs usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c24d4-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c24d4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c24d4-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="c24d4-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c24d4-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="c24d4-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="c24d4-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="c24d4-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="c24d4-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="c24d4-108">CLI do Azure (Clássica)</span><span class="sxs-lookup"><span data-stu-id="c24d4-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c24d4-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c24d4-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c24d4-110">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c24d4-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="c24d4-111">Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24d4-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c24d4-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c24d4-112">Prerequisites</span></span>
<span data-ttu-id="c24d4-113">Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="c24d4-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="c24d4-114">concluir a esses recursos, toocreate Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c24d4-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="c24d4-115">Navegue muito[página de modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c24d4-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c24d4-116">Na página de modelo hello, toohello à direita do **o grupo de recursos pai**, clique em **implantar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="c24d4-117">Se necessário, altere os valores de parâmetro hello, siga as etapas de Olá no grupo de recursos de saudação do hello visualização do Azure toodeploy portal.</span><span class="sxs-lookup"><span data-stu-id="c24d4-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c24d4-118">Verifique se os nomes da conta de armazenamento são exclusivos.</span><span class="sxs-lookup"><span data-stu-id="c24d4-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="c24d4-119">Você não pode ter nomes de conta de armazenamento duplicados no Azure.</span><span class="sxs-lookup"><span data-stu-id="c24d4-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="c24d4-120">Criar hello VMs de back-end</span><span class="sxs-lookup"><span data-stu-id="c24d4-120">Create hello back-end VMs</span></span>
<span data-ttu-id="c24d4-121">Olá que VMs de back-end dependem de criação de saudação do hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c24d4-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="c24d4-122">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-122">**Storage account for data disks**.</span></span> <span data-ttu-id="c24d4-123">Para obter melhor desempenho, os discos de dados Olá em servidores de banco de dados de saudação usará tecnologia SSD (unidade) de estado sólido, que requer uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="c24d4-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="c24d4-124">Verifique se Olá local do Azure que você implantar o armazenamento do premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="c24d4-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="c24d4-125">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-125">**NICs**.</span></span> <span data-ttu-id="c24d4-126">Cada VM tem duas NICs, uma para acesso ao banco de dados e outra para gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c24d4-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="c24d4-127">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-127">**Availability set**.</span></span> <span data-ttu-id="c24d4-128">Todos os servidores de banco de dados serão adicionados tooa único conjunto de disponibilidade, tooensure pelo menos uma das VMs hello está em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="c24d4-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="c24d4-129">Etapa 1 – Iniciar o script</span><span class="sxs-lookup"><span data-stu-id="c24d4-129">Step 1 - Start your script</span></span>
<span data-ttu-id="c24d4-130">Você pode baixar o script do PowerShell completo Olá usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="c24d4-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="c24d4-131">Siga as próximas etapas, Olá toochange Olá script toowork em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c24d4-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="c24d4-132">Alterar valores de saudação das variáveis de saudação abaixo com base em seu grupo de recursos existente implantado acima em [pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="c24d4-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="c24d4-133">Alterar Olá valores de variáveis de saudação abaixo com base nos valores hello, você deseja toouse para sua implantação de back-end.</span><span class="sxs-lookup"><span data-stu-id="c24d4-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="c24d4-134">Recupere recursos existentes de Olá necessários para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c24d4-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="c24d4-135">Etapa 2 – Criar recursos necessários para as VMs</span><span class="sxs-lookup"><span data-stu-id="c24d4-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="c24d4-136">Você precisa toocreate um novo grupo de recursos, uma conta de armazenamento Olá para discos de dados, e um conjunto de disponibilidade para todas as VMs.</span><span class="sxs-lookup"><span data-stu-id="c24d4-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="c24d4-137">Você também precisa de credenciais de conta de administrador local Olá para cada VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="c24d4-138">toocreate esses recursos, execute Olá seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="c24d4-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="c24d4-139">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c24d4-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="c24d4-140">Crie uma nova conta de armazenamento premium Olá grupo de recursos criado acima.</span><span class="sxs-lookup"><span data-stu-id="c24d4-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="c24d4-141">Crie um novo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c24d4-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="c24d4-142">Obtenha o administrador local Olá toobe de credenciais de conta usada para cada VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="c24d4-143">Etapa 3 – crie VMs de back-end e NICs Olá</span><span class="sxs-lookup"><span data-stu-id="c24d4-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="c24d4-144">Você precisa toouse toocreate um loop, como várias VMs conforme desejar e criar hello necessário de NICs e VMs em loop hello.</span><span class="sxs-lookup"><span data-stu-id="c24d4-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="c24d4-145">Olá toocreate NICs e VMs, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c24d4-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="c24d4-146">Iniciar um `for` saudação do loop toorepeat comandos toocreate uma VM e duas NICs de quantas vezes forem necessárias, com base no valor de saudação do hello `$numberOfVMs` variável.</span><span class="sxs-lookup"><span data-stu-id="c24d4-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="c24d4-147">Crie hello que NIC usada para acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c24d4-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="c24d4-148">Crie hello que NIC usada para acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="c24d4-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="c24d4-149">Observe como esta NIC tem um tooit NSG associado.</span><span class="sxs-lookup"><span data-stu-id="c24d4-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="c24d4-150">Criar `vmConfig` objeto.</span><span class="sxs-lookup"><span data-stu-id="c24d4-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="c24d4-151">Crie dois discos de dados por VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-151">Create two data disks per VM.</span></span> <span data-ttu-id="c24d4-152">Observe que os discos de dados Olá na conta de armazenamento premium Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c24d4-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="c24d4-153">Configure sistema operacional de saudação e toobe imagem usada para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="c24d4-154">Adicionar Olá duas NICs criadas acima toohello `vmConfig` objeto.</span><span class="sxs-lookup"><span data-stu-id="c24d4-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="c24d4-155">Criar o disco do sistema operacional hello e criar hello VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="c24d4-156">Saudação de aviso `}` terminando Olá `for` loop.</span><span class="sxs-lookup"><span data-stu-id="c24d4-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="c24d4-157">Etapa 4: executar o script de saudação</span><span class="sxs-lookup"><span data-stu-id="c24d4-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="c24d4-158">Agora que você baixou e alterado Olá baseado no script em suas necessidades, runt banco de dados de back-end do toocreate Olá VMs com várias NICs do script.</span><span class="sxs-lookup"><span data-stu-id="c24d4-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="c24d4-159">Salve o script e executá-lo da saudação **PowerShell** prompt de comando, ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="c24d4-160">Você verá uma saída de inicial hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c24d4-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="c24d4-161">Depois de alguns minutos, preencha Olá prompt de credenciais e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c24d4-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="c24d4-162">saída de Hello abaixo representa uma única VM.</span><span class="sxs-lookup"><span data-stu-id="c24d4-162">hello output below represents a single VM.</span></span> <span data-ttu-id="c24d4-163">Aviso Olá todo processo levou toocomplete 8 minutos.</span><span class="sxs-lookup"><span data-stu-id="c24d4-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
