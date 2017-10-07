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
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Criar uma VM (Clássica) com diversas NICs usando PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais. Várias NICs permitem a separação dos tipos de tráfego entre NICs. Por exemplo, um que NIC pode se comunicar com hello Internet, enquanto o outro se comunica apenas com recursos internos não conectado toohello da Internet. tráfego de rede de tooseparate Olá capacidade para várias NICs é necessário para muitos dispositivos de rede virtual, como fornecimento de aplicativos e soluções de otimização de WAN.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como tooperform essas etapas usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.

## <a name="prerequisites"></a>Pré-requisitos

Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário. toocreate esses recursos, completos Olá etapas a seguir. Criar uma rede virtual, seguindo as etapas de Olá Olá [criar uma rede virtual](virtual-networks-create-vnet-classic-netcfg-ps.md) artigo.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Criar hello VMs de back-end
Olá que VMs de back-end dependem de criação de saudação do hello recursos a seguir:

* **Sub-rede de back-end**. servidores de banco de dados de saudação farão parte de uma sub-rede separada, toosegregate tráfego. script de saudação abaixo espera tooexist essa sub-rede em uma rede virtual denominada *WTestVnet*.
* **Conta de armazenamento para discos de dados**. Para obter melhor desempenho, os discos de dados Olá em servidores de banco de dados de saudação usará tecnologia SSD (unidade) de estado sólido, que requer uma conta de armazenamento premium. Verifique se Olá local do Azure que você implantar o armazenamento do premium toosupport.
* **Conjunto de disponibilidade**. Todos os servidores de banco de dados serão adicionados tooa único conjunto de disponibilidade, tooensure pelo menos uma das VMs hello está em execução durante a manutenção.

### <a name="step-1---start-your-script"></a>Etapa 1 – Iniciar o script
Você pode baixar o script do PowerShell completo Olá usado [aqui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Siga as próximas etapas, Olá toochange Olá script toowork em seu ambiente.

1. Alterar valores de saudação das variáveis de saudação abaixo com base em seu grupo de recursos existente implantado acima em [pré-requisitos](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Alterar Olá valores de variáveis de saudação abaixo com base nos valores hello, você deseja toouse para sua implantação de back-end.

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Etapa 2 – Criar recursos necessários para as VMs
É necessário toocreate um novo serviço de nuvem e um armazenamento de conta Olá para discos de dados para todas as VMs. Você também precisará toospecify uma imagem e uma conta de administrador local para Olá VMs. concluir a esses recursos, toocreate Olá seguintes etapas:

1. Crie um novo serviço de nuvem

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Crie uma nova conta de armazenamento Premium.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Conta de armazenamento de saudação conjunto criada acima como conta de armazenamento atual Olá para sua assinatura.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Selecione uma imagem de VM de saudação.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Defina credenciais de conta de administrador local hello.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Etapa 3 - Criar VMs
Você precisa toouse toocreate um loop, como várias VMs conforme desejar e criar hello necessário de NICs e VMs em loop hello. Olá toocreate NICs e VMs, execute Olá etapas a seguir.

1. Iniciar um `for` saudação do loop toorepeat comandos toocreate uma VM e duas NICs de quantas vezes forem necessárias, com base no valor de saudação do hello `$numberOfVMs` variável.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Criar um `VMConfig` objeto especificando Olá imagem, tamanho e conjunto de disponibilidade para Olá VM.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Saudação de provisionar a VM como uma VM do Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Defina o padrão de saudação NIC e atribuir a ele um endereço IP estático.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Adicione uma segunda NIC para cada VM.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Crie discos toodata para cada VM.

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

7. Crie cada VM e o loop de saudação do end.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Etapa 4: executar o script de saudação
Agora que você baixou e alterado Olá baseado no script em suas necessidades, runt banco de dados de back-end do toocreate Olá VMs com várias NICs do script.

1. Salve o script e executá-lo da saudação **PowerShell** prompt de comando, ou **PowerShell ISE**. Você verá uma saída de inicial hello, conforme mostrado abaixo.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Preencha as informações de saudação necessárias no prompt de credenciais hello e clique em **Okey**. saída de Hello abaixo é retornada.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
