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
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Criar uma VM (clássico) com várias NICs usando Olá 1.0 da CLI do Azure

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais. Várias NICs permitem a separação dos tipos de tráfego entre NICs. Por exemplo, um que NIC pode se comunicar com hello Internet, enquanto o outro se comunica apenas com recursos internos não conectado toohello da Internet. tráfego de rede de tooseparate Olá capacidade para várias NICs é necessário para muitos dispositivos de rede virtual, como fornecimento de aplicativos e soluções de otimização de WAN.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como tooperform essas etapas usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.

## <a name="prerequisites"></a>Pré-requisitos
Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário. toocreate esses recursos, completos Olá etapas a seguir. Criar uma rede virtual, seguindo as etapas de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md) artigo.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Olá back-end de implantar máquinas virtuais
Olá que VMs de back-end dependem de criação de saudação do hello recursos a seguir:

* **Conta de armazenamento para discos de dados**. Para obter melhor desempenho, os discos de dados Olá em servidores de banco de dados de saudação usará tecnologia SSD (unidade) de estado sólido, que requer uma conta de armazenamento premium. Verifique se Olá local do Azure que você implantar o armazenamento do premium toosupport.
* **NICs**. Cada VM tem duas NICs, uma para acesso ao banco de dados e outra para gerenciamento.
* **Conjunto de disponibilidade**. Todos os servidores de banco de dados serão adicionados tooa único conjunto de disponibilidade, tooensure pelo menos uma das VMs hello está em execução durante a manutenção.

### <a name="step-1---start-your-script"></a>Etapa 1 – Iniciar o script
Você pode baixar o script de bash completo Olá usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Olá concluir etapas toochange Olá script toowork em seu ambiente a seguir:

1. Alterar valores de saudação das variáveis de saudação abaixo com base em seu grupo de recursos existente implantado acima em [pré-requisitos](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Alterar Olá valores de variáveis de saudação abaixo com base nos valores hello, você deseja toouse para sua implantação de back-end.

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Etapa 2 – Criar recursos necessários para as VMs
1. Crie um novo serviço de nuvem para todas as VMs de back-end. Aviso uso Olá Olá `$backendCSName` variável do nome de grupo de recurso Olá, e `$location` para Olá região do Azure.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Crie uma conta de armazenamento premium para Olá SO e toobe de discos de dados usados por suas máquinas virtuais.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Etapa 3 - Criar VMs com várias NICs
1. Iniciar um loop toocreate várias VMs, com base em Olá `numberOfVMs` variáveis.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Para cada VM, especifique o nome de saudação e endereço IP de cada Olá duas NICs.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Crie hello VM. Observe o uso de saudação do hello `--nic-config` parâmetro, que contém uma lista de todas as NICs com nome, a sub-rede e o endereço IP.

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

4. Para cada VM, crie dois discos de dados.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Etapa 4: executar o script de saudação
Agora que você baixou e alterado script hello com base em suas necessidades, executadas Olá Olá de toocreate script final VMs de banco de dados com várias NICs.

1. Salve seu script e execute-o em seu terminal **Bash** . Você verá uma saída de inicial hello, conforme mostrado abaixo.

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

2. Após alguns minutos, execução Olá terminará e você verá restante Olá Olá saída conforme mostrado abaixo.

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
