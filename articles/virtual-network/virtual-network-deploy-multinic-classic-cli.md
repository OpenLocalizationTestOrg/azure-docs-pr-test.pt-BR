---
title: "Criar uma VM (Clássica) com várias NICs - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como criar uma VM (Clássica) com várias placas de rede usando a CLI (interface de linha de comando) do Azure 1.0."
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
ms.openlocfilehash: b62421b7289650818748d0016dccfdf42ef0a768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="fae64-103">Criar uma VM (Clássica) com várias NICs usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fae64-103">Create a VM (Classic) with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="fae64-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias interfaces de rede (NICs) para cada uma de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="fae64-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="fae64-105">Várias NICs permitem a separação dos tipos de tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="fae64-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="fae64-106">Por exemplo, uma NIC pode se comunicar com a Internet, enquanto outra se comunica apenas com recursos internos que não estão conectados à Internet.</span><span class="sxs-lookup"><span data-stu-id="fae64-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="fae64-107">A capacidade de separar o tráfego de rede entre as várias NICs é necessária para vários dispositivos de rede virtual, como a entrega de aplicativos e soluções de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="fae64-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fae64-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fae64-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fae64-109">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="fae64-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="fae64-110">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="fae64-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fae64-111">Saiba como executar essas etapas usando o [modelo de implantação do Resource Manager](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fae64-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="fae64-112">As etapas a seguir usam um grupo de recursos chamado *IaaSStory* para os servidores Web e o grupo de recursos e *IaaSStory-BackEnd* para os servidores DB.</span><span class="sxs-lookup"><span data-stu-id="fae64-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fae64-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fae64-113">Prerequisites</span></span>
<span data-ttu-id="fae64-114">Antes de criar os servidores DB, você precisa criar o grupo de recursos *IaaSStory* com todos os recursos necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="fae64-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="fae64-115">Para criar esses recursos, conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="fae64-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="fae64-116">Criar uma rede virtual, seguindo as etapas do artigo [Criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fae64-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-the-back-end-vms"></a><span data-ttu-id="fae64-117">Implantar VMs de back-end</span><span class="sxs-lookup"><span data-stu-id="fae64-117">Deploy the back-end VMs</span></span>
<span data-ttu-id="fae64-118">As VMs de back-end dependem da criação dos seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="fae64-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="fae64-119">**Conta de armazenamento para discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="fae64-119">**Storage account for data disks**.</span></span> <span data-ttu-id="fae64-120">Para obter um melhor desempenho, os discos de dados dos servidores de banco de dados usam a tecnologia SDD (unidade de estado sólido), que requer uma conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="fae64-120">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="fae64-121">Verifique se o local do Azure no qual você vai implantar é compatível com o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="fae64-121">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="fae64-122">**NICs**.</span><span class="sxs-lookup"><span data-stu-id="fae64-122">**NICs**.</span></span> <span data-ttu-id="fae64-123">Cada VM tem duas NICs, uma para acesso ao banco de dados e outra para gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="fae64-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="fae64-124">**Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="fae64-124">**Availability set**.</span></span> <span data-ttu-id="fae64-125">Todos os servidores de banco de dados são adicionados a um conjunto de disponibilidade único, para garantir que pelo menos uma das VMs está ativa e em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="fae64-125">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="fae64-126">Etapa 1 – Iniciar o script</span><span class="sxs-lookup"><span data-stu-id="fae64-126">Step 1 - Start your script</span></span>
<span data-ttu-id="fae64-127">Você pode baixar o script bash completo usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="fae64-127">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="fae64-128">Realize as seguintes etapas para alterar o script para funcionar em seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="fae64-128">Complete the following steps to change the script to work in your environment:</span></span>

1. <span data-ttu-id="fae64-129">Altere os valores das variáveis a seguir com base no grupo de recursos existente implantado acima, no tópico [Pré-requisitos](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="fae64-129">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="fae64-130">Altere os valores das variáveis a seguir de acordo com os valores que deseja usar na implantação do back-end.</span><span class="sxs-lookup"><span data-stu-id="fae64-130">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="fae64-131">Etapa 2 – Criar recursos necessários para as VMs</span><span class="sxs-lookup"><span data-stu-id="fae64-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="fae64-132">Crie um novo serviço de nuvem para todas as VMs de back-end.</span><span class="sxs-lookup"><span data-stu-id="fae64-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="fae64-133">Observe o uso da variável `$backendCSName` para o nome do grupo de recursos e `$location` para a região do Azure.</span><span class="sxs-lookup"><span data-stu-id="fae64-133">Notice the use of the `$backendCSName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="fae64-134">Crie uma conta de armazenamento Premium para o sistema operacional e discos de dados a ser usada por suas VMs.</span><span class="sxs-lookup"><span data-stu-id="fae64-134">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="fae64-135">Etapa 3 - Criar VMs com várias NICs</span><span class="sxs-lookup"><span data-stu-id="fae64-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="fae64-136">Inicie um loop para criar várias VMs, com base em variáveis `numberOfVMs` .</span><span class="sxs-lookup"><span data-stu-id="fae64-136">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="fae64-137">Para cada VM, especifique o nome e o endereço IP de cada uma das duas NICs.</span><span class="sxs-lookup"><span data-stu-id="fae64-137">For each VM, specify the name and IP address of each of the two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="fae64-138">Crie a VM.</span><span class="sxs-lookup"><span data-stu-id="fae64-138">Create the VM.</span></span> <span data-ttu-id="fae64-139">Observe o uso do parâmetro `--nic-config` , que contém uma lista de todas as NICs com nome, sub-rede e endereço IP.</span><span class="sxs-lookup"><span data-stu-id="fae64-139">Notice the usage of the `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

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

4. <span data-ttu-id="fae64-140">Para cada VM, crie dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="fae64-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="fae64-141">Etapa 4 – Executar o script</span><span class="sxs-lookup"><span data-stu-id="fae64-141">Step 4 - Run the script</span></span>
<span data-ttu-id="fae64-142">Agora que você baixou e alterou o script de acordo com suas necessidades, execute o script para criar VMs do banco de dados de back-end com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="fae64-142">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="fae64-143">Salve seu script e execute-o em seu terminal **Bash** .</span><span class="sxs-lookup"><span data-stu-id="fae64-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="fae64-144">A saída inicial será exibida, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="fae64-144">You will see the initial output, as shown below.</span></span>

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

2. <span data-ttu-id="fae64-145">Depois de alguns minutos, a execução será encerrada e você verá o restante da saída conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fae64-145">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>

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
