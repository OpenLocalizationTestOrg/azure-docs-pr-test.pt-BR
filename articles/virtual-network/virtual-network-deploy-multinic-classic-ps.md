---
title: "Criar uma VM (Clássica) com diversas NICs - Azure PowerShell | Microsoft Docs"
description: "Saiba como criar uma VM (Clássica) com diversas NICs usando o PowerShell."
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
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="3b59a-103">Criar uma VM (Clássica) com diversas NICs usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b59a-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="3b59a-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias interfaces de rede (NICs) para cada uma de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="3b59a-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="3b59a-105">Várias NICs permitem a separação dos tipos de tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="3b59a-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="3b59a-106">Por exemplo, uma NIC pode se comunicar com a Internet, enquanto outra se comunica apenas com recursos internos que não estão conectados à Internet.</span><span class="sxs-lookup"><span data-stu-id="3b59a-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="3b59a-107">A capacidade de separar o tráfego de rede entre as várias NICs é necessária para vários dispositivos de rede virtual, como a entrega de aplicativos e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="3b59a-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b59a-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3b59a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3b59a-109">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="3b59a-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="3b59a-110">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="3b59a-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3b59a-111">Saiba como executar essas etapas usando o [modelo de implantação do Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3b59a-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="3b59a-112">As etapas a seguir usam um grupo de recursos chamado *IaaSStory* para os servidores Web e o grupo de recursos e *IaaSStory-BackEnd* para os servidores DB.</span><span class="sxs-lookup"><span data-stu-id="3b59a-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b59a-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b59a-113">Prerequisites</span></span>

<span data-ttu-id="3b59a-114">Antes de criar os servidores DB, você precisa criar o grupo de recursos *IaaSStory* com todos os recursos necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="3b59a-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="3b59a-115">Para criar esses recursos, conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="3b59a-116">Crie uma rede virtual seguindo as etapas no artigo [Criar uma rede virtual](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3b59a-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="3b59a-117">Criar VMs de back-end</span><span class="sxs-lookup"><span data-stu-id="3b59a-117">Create the back-end VMs</span></span>
<span data-ttu-id="3b59a-118">As VMs de back-end dependem da criação dos seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="3b59a-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="3b59a-119">**Sub-rede de back-end**.</span><span class="sxs-lookup"><span data-stu-id="3b59a-119">**Backend subnet**.</span></span> <span data-ttu-id="3b59a-120">Os servidores de banco de dados serão parte de uma sub-rede separada, para segregar o tráfego.</span><span class="sxs-lookup"><span data-stu-id="3b59a-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="3b59a-121">O script a seguir espera que essa sub-rede exista em uma vnet chamada *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="3b59a-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="3b59a-122">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="3b59a-122">**Storage account for data disks**.</span></span> <span data-ttu-id="3b59a-123">Para obter um melhor desempenho, os discos de dados dos servidores de banco de dados usam a tecnologia SDD (unidade de estado sólido), que requer uma conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="3b59a-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="3b59a-124">Verifique se o local do Azure no qual você vai implantar é compatível com o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="3b59a-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="3b59a-125">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="3b59a-125">**Availability set**.</span></span> <span data-ttu-id="3b59a-126">Todos os servidores de banco de dados são adicionados a um conjunto de disponibilidade único, para garantir que pelo menos uma das VMs está ativa e em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="3b59a-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="3b59a-127">Etapa 1 – Iniciar o script</span><span class="sxs-lookup"><span data-stu-id="3b59a-127">Step 1 - Start your script</span></span>
<span data-ttu-id="3b59a-128">Baixe o script completo do PowerShell usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="3b59a-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="3b59a-129">Realize os procedimentos abaixo para alterar o script para funcionar em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3b59a-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="3b59a-130">Altere os valores das variáveis a seguir com base no grupo de recursos existente implantado acima, no tópico [Pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="3b59a-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="3b59a-131">Altere os valores das variáveis a seguir de acordo com os valores que deseja usar na implantação do back-end.</span><span class="sxs-lookup"><span data-stu-id="3b59a-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="3b59a-132">Etapa 2 – Criar recursos necessários para as VMs</span><span class="sxs-lookup"><span data-stu-id="3b59a-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="3b59a-133">Você precisa criar um novo serviço de nuvem e conta de armazenamento para os discos de dados para todas as VMs.</span><span class="sxs-lookup"><span data-stu-id="3b59a-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="3b59a-134">Você também precisa especificar uma imagem e uma conta de administrador local para as VMs.</span><span class="sxs-lookup"><span data-stu-id="3b59a-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="3b59a-135">Para criar esses recursos, siga estes etapas:</span><span class="sxs-lookup"><span data-stu-id="3b59a-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="3b59a-136">Crie um novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="3b59a-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="3b59a-137">Crie uma nova conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="3b59a-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="3b59a-138">Defina a conta de armazenamento criada acima como a conta de armazenamento para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3b59a-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="3b59a-139">Selecione uma imagem para a VM.</span><span class="sxs-lookup"><span data-stu-id="3b59a-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="3b59a-140">Defina as credenciais da conta de administrador local.</span><span class="sxs-lookup"><span data-stu-id="3b59a-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="3b59a-141">Etapa 3 - Criar VMs</span><span class="sxs-lookup"><span data-stu-id="3b59a-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="3b59a-142">Você deve usar um loop para criar várias VMs desejadas e para criar as NICs e VMs necessárias dentro do loop.</span><span class="sxs-lookup"><span data-stu-id="3b59a-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="3b59a-143">Para criar as NICs e VMs, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3b59a-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="3b59a-144">Inicie um loop `for` para repetir os comandos para criar uma VM e duas NICs, quantas vezes forem necessárias, com base no valor da variável `$numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="3b59a-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="3b59a-145">Crie um objeto `VMConfig` que especifica a imagem, o tamanho e o conjunto de disponibilidade da VM.</span><span class="sxs-lookup"><span data-stu-id="3b59a-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="3b59a-146">Provisione a VM como uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="3b59a-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="3b59a-147">Defina a NIC padrão e atribua um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="3b59a-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="3b59a-148">Adicione uma segunda NIC para cada VM.</span><span class="sxs-lookup"><span data-stu-id="3b59a-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="3b59a-149">Crie discos de dados para cada VM.</span><span class="sxs-lookup"><span data-stu-id="3b59a-149">Create to data disks for each VM.</span></span>

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

7. <span data-ttu-id="3b59a-150">Crie cada VM e encerre o loop.</span><span class="sxs-lookup"><span data-stu-id="3b59a-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="3b59a-151">Etapa 4 – Executar o script</span><span class="sxs-lookup"><span data-stu-id="3b59a-151">Step 4 - Run the script</span></span>
<span data-ttu-id="3b59a-152">Agora que você baixou e alterou o script de acordo com suas necessidades, execute o script para criar VMs do banco de dados de back-end com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="3b59a-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="3b59a-153">Salve seu script e execute-o no prompt de comando do **PowerShell** ou **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="3b59a-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="3b59a-154">A saída inicial será exibida, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3b59a-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="3b59a-155">Preencha as informações necessárias na solicitação de credenciais e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b59a-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="3b59a-156">A saída abaixo é retornada.</span><span class="sxs-lookup"><span data-stu-id="3b59a-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
