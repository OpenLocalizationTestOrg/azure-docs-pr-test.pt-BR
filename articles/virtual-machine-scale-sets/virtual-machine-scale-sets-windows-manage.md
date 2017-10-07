---
title: "aaaManage VMs em um conjunto de escala de máquinas virtuais | Microsoft Docs"
description: "Gerenciar máquinas virtuais em um conjunto de escala de máquina virtual usando o Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Gerenciar máquinas virtuais em um conjunto de dimensionamento de máquinas virtuais
Use tarefas Olá neste artigo as máquinas virtuais toomanage em seu conjunto de escala de máquinas virtuais.

A maioria das tarefas de saudação que envolvem o gerenciamento de uma máquina virtual em um conjunto de escala exige que você saiba Olá ID da instância de máquina Olá que você deseja toomanage. Você pode usar [Gerenciador de recursos do Azure](https://resources.azure.com) toofind Olá ID da instância de uma máquina virtual em um conjunto de escala. Você também usar o Gerenciador de recursos tooverify Olá status Olá tarefas que você concluir.

Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.

## <a name="display-information-about-a-scale-set"></a>Exibir informações sobre um conjunto de dimensionamento
Você pode obter informações gerais sobre um conjunto de escala, que também é chamado tooas Olá exibição da instância. Ou, você pode obter informações mais específicas, como informações sobre os recursos de saudação no conjunto de escala de saudação.

Substitua Olá valores com nome hello ou seu grupo de recursos e a escala definida e, em seguida, execute o comando de saudação entre aspas:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Ele retorna algo semelhante a:

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas. Substituir  *#*  com o identificador de instância de saudação da máquina virtual de saudação que você deseja obter informações de tooget e, em seguida, executá-lo:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

É retornado algo semelhante a este exemplo:

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Iniciar uma máquina virtual em um conjunto de escala
Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas. Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toostart e, em seguida, executá-lo:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

No Gerenciador de recursos, podemos ver que o status de saudação da instância de saudação é **executando**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Você pode iniciar todas as máquinas virtuais de saudação em escala Olá definida por não usar o parâmetro - InstanceId de hello.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Parar uma máquina virtual em um conjunto de escala
Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas. Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toostop e, em seguida, executá-lo:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

No Gerenciador de recursos, podemos ver que o status de saudação da instância de saudação é **desalocada**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop uma máquina virtual e não desalocá-lo, use o parâmetro de StayProvisioned - Olá. Você pode parar todas as máquinas virtuais de saudação em Olá definido por não usar o parâmetro - InstanceId de hello.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Reiniciar uma máquina virtual em um conjunto de escala
Substitua saudação valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas. Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toorestart e, em seguida, executá-lo:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Você pode reiniciar todas as máquinas virtuais de saudação em Olá definido por não usar o parâmetro - InstanceId de hello.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Remover uma máquina virtual de um conjunto de escala
Substitua saudação valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas. Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja tooremove e, em seguida, executá-lo:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Você pode remover o conjunto de escalas da máquina virtual Olá todos de uma vez por não usar o parâmetro - InstanceId de hello.

## <a name="change-hello-capacity-of-a-scale-set"></a>Capacidade de saudação de alteração de um conjunto de escala
Você pode adicionar ou remover as máquinas virtuais, alterando a capacidade de saudação do conjunto de saudação. Obter conjunto de escala de saudação que você deseja toochange, conjunto Olá capacidade toowhat desejar toobe e, em seguida, atualizar o conjunto de escala de saudação com a nova capacidade de saudação. Esses comandos, substitua Olá valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Se você estiver removendo as máquinas virtuais do conjunto de escala hello, máquinas virtuais de saudação com ids de mais altos de saudação são removidas primeiro.

