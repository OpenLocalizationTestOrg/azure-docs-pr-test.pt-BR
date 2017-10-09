---
title: "aaaCreate uma VM (clássico) com várias NICs - 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM (clássico) com várias NICs usando hello Azure interface de linha de comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="6a4c3-103">Criar uma VM (clássico) com várias NICs usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6a4c3-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="6a4c3-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="6a4c3-105">Várias NICs permitem a separação dos tipos de tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="6a4c3-106">Por exemplo, um que NIC pode se comunicar com hello Internet, enquanto o outro se comunica apenas com recursos internos não conectado toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="6a4c3-107">tráfego de rede de tooseparate Olá capacidade para várias NICs é necessário para muitos dispositivos de rede virtual, como fornecimento de aplicativos e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a4c3-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6a4c3-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6a4c3-109">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6a4c3-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6a4c3-111">Saiba como tooperform essas etapas usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6a4c3-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="6a4c3-112">Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a4c3-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a4c3-113">Prerequisites</span></span>
<span data-ttu-id="6a4c3-114">Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="6a4c3-115">toocreate esses recursos, completos Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="6a4c3-116">Criar uma rede virtual, seguindo as etapas de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="6a4c3-117">Olá back-end de implantar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="6a4c3-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="6a4c3-118">Olá que VMs de back-end dependem de criação de saudação do hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a4c3-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="6a4c3-119">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-119">**Storage account for data disks**.</span></span> <span data-ttu-id="6a4c3-120">Para obter melhor desempenho, os discos de dados Olá em servidores de banco de dados de saudação usará tecnologia SSD (unidade) de estado sólido, que requer uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="6a4c3-121">Verifique se Olá local do Azure que você implantar o armazenamento do premium toosupport.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="6a4c3-122">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-122">**NICs**.</span></span> <span data-ttu-id="6a4c3-123">Cada VM tem duas NICs, uma para acesso ao banco de dados e outra para gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="6a4c3-124">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-124">**Availability set**.</span></span> <span data-ttu-id="6a4c3-125">Todos os servidores de banco de dados serão adicionados tooa único conjunto de disponibilidade, tooensure pelo menos uma das VMs hello está em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="6a4c3-126">Etapa 1 – Iniciar o script</span><span class="sxs-lookup"><span data-stu-id="6a4c3-126">Step 1 - Start your script</span></span>
<span data-ttu-id="6a4c3-127">Você pode baixar o script de bash completo Olá usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="6a4c3-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="6a4c3-128">Olá concluir etapas toochange Olá script toowork em seu ambiente a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a4c3-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="6a4c3-129">Alterar valores de saudação das variáveis de saudação abaixo com base em seu grupo de recursos existente implantado acima em [pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6a4c3-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="6a4c3-130">Alterar Olá valores de variáveis de saudação abaixo com base nos valores hello, você deseja toouse para sua implantação de back-end.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="6a4c3-131">Etapa 2 – Criar recursos necessários para as VMs</span><span class="sxs-lookup"><span data-stu-id="6a4c3-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="6a4c3-132">Crie um novo serviço de nuvem para todas as VMs de back-end.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="6a4c3-133">Aviso uso Olá Olá `$backendCSName` variável do nome de grupo de recurso Olá, e `$location` para Olá região do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="6a4c3-134">Crie uma conta de armazenamento premium para Olá SO e toobe de discos de dados usados por suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="6a4c3-135">Etapa 3 - Criar VMs com várias NICs</span><span class="sxs-lookup"><span data-stu-id="6a4c3-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="6a4c3-136">Iniciar um loop toocreate várias VMs, com base em Olá `numberOfVMs` variáveis.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="6a4c3-137">Para cada VM, especifique o nome de saudação e endereço IP de cada Olá duas NICs.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="6a4c3-138">Crie hello VM.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-138">Create hello VM.</span></span> <span data-ttu-id="6a4c3-139">Observe o uso de saudação do hello `--nic-config` parâmetro, que contém uma lista de todas as NICs com nome, a sub-rede e o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="6a4c3-140">Para cada VM, crie dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="6a4c3-141">Etapa 4: executar o script de saudação</span><span class="sxs-lookup"><span data-stu-id="6a4c3-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="6a4c3-142">Agora que você baixou e alterado script hello com base em suas necessidades, executadas Olá Olá de toocreate script final VMs de banco de dados com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="6a4c3-143">Salve seu script e execute-o em seu terminal **Bash** .</span><span class="sxs-lookup"><span data-stu-id="6a4c3-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="6a4c3-144">Você verá uma saída de inicial hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="6a4c3-145">Após alguns minutos, execução Olá terminará e você verá restante Olá Olá saída conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6a4c3-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
