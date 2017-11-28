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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="d5a3e-103">Gerenciar máquinas virtuais em um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d5a3e-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="d5a3e-104">Use tarefas Olá neste artigo as máquinas virtuais toomanage em seu conjunto de escala de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="d5a3e-105">A maioria das tarefas de saudação que envolvem o gerenciamento de uma máquina virtual em um conjunto de escala exige que você saiba Olá ID da instância de máquina Olá que você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="d5a3e-106">Você pode usar [Gerenciador de recursos do Azure](https://resources.azure.com) toofind Olá ID da instância de uma máquina virtual em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="d5a3e-107">Você também usar o Gerenciador de recursos tooverify Olá status Olá tarefas que você concluir.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="d5a3e-108">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="d5a3e-109">Exibir informações sobre um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="d5a3e-109">Display information about a scale set</span></span>
<span data-ttu-id="d5a3e-110">Você pode obter informações gerais sobre um conjunto de escala, que também é chamado tooas Olá exibição da instância.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="d5a3e-111">Ou, você pode obter informações mais específicas, como informações sobre os recursos de saudação no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="d5a3e-112">Substitua Olá valores com nome hello ou seu grupo de recursos e a escala definida e, em seguida, execute o comando de saudação entre aspas:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="d5a3e-113">Ele retorna algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-113">It returns something like this:</span></span>

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

<span data-ttu-id="d5a3e-114">Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="d5a3e-115">Substituir  *#*  com o identificador de instância de saudação da máquina virtual de saudação que você deseja obter informações de tooget e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="d5a3e-116">É retornado algo semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="d5a3e-117">Iniciar uma máquina virtual em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="d5a3e-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="d5a3e-118">Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="d5a3e-119">Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toostart e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="d5a3e-120">No Gerenciador de recursos, podemos ver que o status de saudação da instância de saudação é **executando**:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

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

<span data-ttu-id="d5a3e-121">Você pode iniciar todas as máquinas virtuais de saudação em escala Olá definida por não usar o parâmetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="d5a3e-122">Parar uma máquina virtual em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="d5a3e-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="d5a3e-123">Substitua saudação valores com o nome de saudação do seu conjunto de escala e o grupo de recursos entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="d5a3e-124">Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toostop e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="d5a3e-125">No Gerenciador de recursos, podemos ver que o status de saudação da instância de saudação é **desalocada**:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

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

<span data-ttu-id="d5a3e-126">toostop uma máquina virtual e não desalocá-lo, use o parâmetro de StayProvisioned - Olá.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="d5a3e-127">Você pode parar todas as máquinas virtuais de saudação em Olá definido por não usar o parâmetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="d5a3e-128">Reiniciar uma máquina virtual em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="d5a3e-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="d5a3e-129">Substitua saudação valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="d5a3e-130">Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja toorestart e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="d5a3e-131">Você pode reiniciar todas as máquinas virtuais de saudação em Olá definido por não usar o parâmetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="d5a3e-132">Remover uma máquina virtual de um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="d5a3e-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="d5a3e-133">Substitua saudação valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="d5a3e-134">Substituir  *#*  com identificador de saudação da máquina virtual de saudação que você deseja tooremove e, em seguida, executá-lo:</span><span class="sxs-lookup"><span data-stu-id="d5a3e-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="d5a3e-135">Você pode remover o conjunto de escalas da máquina virtual Olá todos de uma vez por não usar o parâmetro - InstanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="d5a3e-136">Capacidade de saudação de alteração de um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="d5a3e-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="d5a3e-137">Você pode adicionar ou remover as máquinas virtuais, alterando a capacidade de saudação do conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="d5a3e-138">Obter conjunto de escala de saudação que você deseja toochange, conjunto Olá capacidade toowhat desejar toobe e, em seguida, atualizar o conjunto de escala de saudação com a nova capacidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="d5a3e-139">Esses comandos, substitua Olá valores com o nome de saudação do seu conjunto de escala de grupo e hello recurso entre aspas.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="d5a3e-140">Se você estiver removendo as máquinas virtuais do conjunto de escala hello, máquinas virtuais de saudação com ids de mais altos de saudação são removidas primeiro.</span><span class="sxs-lookup"><span data-stu-id="d5a3e-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

