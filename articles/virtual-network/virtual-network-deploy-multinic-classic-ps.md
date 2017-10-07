---
title: "aaaCreate uma VM (clássico) com várias NICs - PowerShell do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM (clássico) com várias placas de rede usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="8182d-103">Criar uma VM (Clássica) com diversas NICs usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="8182d-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="8182d-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8182d-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="8182d-105">Várias NICs permitem a separação dos tipos de tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="8182d-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="8182d-106">Por exemplo, um que NIC pode se comunicar com hello Internet, enquanto o outro se comunica apenas com recursos internos não conectado toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="8182d-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="8182d-107">tráfego de rede de tooseparate Olá capacidade para várias NICs é necessário para muitos dispositivos de rede virtual, como fornecimento de aplicativos e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="8182d-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8182d-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8182d-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8182d-109">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8182d-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8182d-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8182d-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8182d-111">Saiba como tooperform essas etapas usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8182d-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="8182d-112">Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8182d-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8182d-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8182d-113">Prerequisites</span></span>

<span data-ttu-id="8182d-114">Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="8182d-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="8182d-115">toocreate esses recursos, completos Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8182d-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="8182d-116">Criar uma rede virtual, seguindo as etapas de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-netcfg-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8182d-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="8182d-117">Criar hello VMs de back-end</span><span class="sxs-lookup"><span data-stu-id="8182d-117">Create hello back-end VMs</span></span>
<span data-ttu-id="8182d-118">Olá que VMs de back-end dependem de criação de saudação do hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8182d-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="8182d-119">**Sub-rede de back-end**.</span><span class="sxs-lookup"><span data-stu-id="8182d-119">**Backend subnet**.</span></span> <span data-ttu-id="8182d-120">servidores de banco de dados de saudação farão parte de uma sub-rede separada, toosegregate tráfego.</span><span class="sxs-lookup"><span data-stu-id="8182d-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="8182d-121">script de saudação abaixo espera tooexist essa sub-rede em uma rede virtual denominada *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="8182d-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="8182d-122">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="8182d-122">**Storage account for data disks**.</span></span> <span data-ttu-id="8182d-123">Para obter melhor desempenho, os discos de dados Olá em servidores de banco de dados de saudação usará tecnologia SSD (unidade) de estado sólido, que requer uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="8182d-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="8182d-124">Verifique se Olá local do Azure que você implantar o armazenamento do premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="8182d-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="8182d-125">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="8182d-125">**Availability set**.</span></span> <span data-ttu-id="8182d-126">Todos os servidores de banco de dados serão adicionados tooa único conjunto de disponibilidade, tooensure pelo menos uma das VMs hello está em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="8182d-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="8182d-127">Etapa 1 – Iniciar o script</span><span class="sxs-lookup"><span data-stu-id="8182d-127">Step 1 - Start your script</span></span>
<span data-ttu-id="8182d-128">Você pode baixar o script do PowerShell completo Olá usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="8182d-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="8182d-129">Siga as próximas etapas, Olá toochange Olá script toowork em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8182d-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="8182d-130">Alterar valores de saudação das variáveis de saudação abaixo com base em seu grupo de recursos existente implantado acima em [pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="8182d-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="8182d-131">Alterar Olá valores de variáveis de saudação abaixo com base nos valores hello, você deseja toouse para sua implantação de back-end.</span><span class="sxs-lookup"><span data-stu-id="8182d-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="8182d-132">Etapa 2 – Criar recursos necessários para as VMs</span><span class="sxs-lookup"><span data-stu-id="8182d-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="8182d-133">É necessário toocreate um novo serviço de nuvem e um armazenamento de conta Olá para discos de dados para todas as VMs.</span><span class="sxs-lookup"><span data-stu-id="8182d-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="8182d-134">Você também precisará toospecify uma imagem e uma conta de administrador local para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="8182d-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="8182d-135">concluir a esses recursos, toocreate Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8182d-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="8182d-136">Crie um novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="8182d-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="8182d-137">Crie uma nova conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="8182d-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="8182d-138">Conta de armazenamento de saudação conjunto criada acima como conta de armazenamento atual Olá para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8182d-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="8182d-139">Selecione uma imagem de VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="8182d-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="8182d-140">Defina credenciais de conta de administrador local hello.</span><span class="sxs-lookup"><span data-stu-id="8182d-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="8182d-141">Etapa 3 - Criar VMs</span><span class="sxs-lookup"><span data-stu-id="8182d-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="8182d-142">Você precisa toouse toocreate um loop, como várias VMs conforme desejar e criar hello necessário de NICs e VMs em loop hello.</span><span class="sxs-lookup"><span data-stu-id="8182d-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="8182d-143">Olá toocreate NICs e VMs, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8182d-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="8182d-144">Iniciar um `for` saudação do loop toorepeat comandos toocreate uma VM e duas NICs de quantas vezes forem necessárias, com base no valor de saudação do hello `$numberOfVMs` variável.</span><span class="sxs-lookup"><span data-stu-id="8182d-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="8182d-145">Criar um `VMConfig` objeto especificando Olá imagem, tamanho e conjunto de disponibilidade para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8182d-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="8182d-146">Saudação de provisionar a VM como uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="8182d-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="8182d-147">Defina o padrão de saudação NIC e atribuir a ele um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="8182d-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="8182d-148">Adicione uma segunda NIC para cada VM.</span><span class="sxs-lookup"><span data-stu-id="8182d-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="8182d-149">Crie discos toodata para cada VM.</span><span class="sxs-lookup"><span data-stu-id="8182d-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="8182d-150">Crie cada VM e o loop de saudação do end.</span><span class="sxs-lookup"><span data-stu-id="8182d-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="8182d-151">Etapa 4: executar o script de saudação</span><span class="sxs-lookup"><span data-stu-id="8182d-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="8182d-152">Agora que você baixou e alterado Olá baseado no script em suas necessidades, runt banco de dados de back-end do toocreate Olá VMs com várias NICs do script.</span><span class="sxs-lookup"><span data-stu-id="8182d-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="8182d-153">Salve o script e executá-lo da saudação **PowerShell** prompt de comando, ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="8182d-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="8182d-154">Você verá uma saída de inicial hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8182d-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="8182d-155">Preencha as informações de saudação necessárias no prompt de credenciais hello e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8182d-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="8182d-156">saída de Hello abaixo é retornada.</span><span class="sxs-lookup"><span data-stu-id="8182d-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
