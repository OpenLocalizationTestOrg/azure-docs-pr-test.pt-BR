---
title: "aaaStatic interno clássico IP - VM do Azure - privado"
description: "Noções básicas sobre os IPs estáticos internos (DIPs) e como toomanage-los"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="e6477-103">Como tooset IP privado estático interno de endereço usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="e6477-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="e6477-104">Na maioria dos casos, você não precisará toospecify um endereço IP interno estático para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e6477-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="e6477-105">As VMs de uma rede virtual receberão automaticamente endereço IP interno de um intervalo especificado por você.</span><span class="sxs-lookup"><span data-stu-id="e6477-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="e6477-106">Mas, em alguns casos, a especificação de um endereço IP estático para uma determinada VM fará sentido.</span><span class="sxs-lookup"><span data-stu-id="e6477-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="e6477-107">Por exemplo, se sua VM for contínuo toorun DNS ou será um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="e6477-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="e6477-108">Um endereço IP interno estático permanece com hello VM até mesmo por meio de um estado de interrupção/desprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="e6477-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e6477-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e6477-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e6477-110">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="e6477-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e6477-111">A Microsoft recomenda que mais novas implantações usam Olá [modelo de implantação do Gerenciador de recursos](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e6477-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="e6477-112">Como tooverify se um endereço IP específico está disponível</span><span class="sxs-lookup"><span data-stu-id="e6477-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="e6477-113">tooverify se hello endereço IP *10.0.0.7* está disponível em uma rede virtual denominada *TestVnet*, execute Olá comando PowerShell a seguir e verifique se o valor de saudação para *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="e6477-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="e6477-114">Se você quiser que o comando de saudação tootest acima em um ambiente seguro siga as diretrizes de saudação em [criar uma rede virtual (clássica)](virtual-networks-create-vnet-classic-pportal.md) toocreate uma rede virtual denominada *TestVnet* e certifique-se de que ele usa Olá  *10.0.0.0/8* espaço de endereço.</span><span class="sxs-lookup"><span data-stu-id="e6477-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="e6477-115">Como toospecify um endereço IP interno estático ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="e6477-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="e6477-116">Olá script do PowerShell abaixo cria um novo serviço de nuvem chamado *TestService*, em seguida, recupera uma imagem do Azure e cria uma VM denominada *TestVM* em Olá novo serviço de nuvem usando a imagem Olá recuperado, conjuntos de Olá toobe VM em uma sub-rede denominada *Subnet-1*e define *10.0.0.7* como um endereço IP interno estático para Olá VM:</span><span class="sxs-lookup"><span data-stu-id="e6477-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="e6477-117">Como tooretrieve internas informações de IP estático para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e6477-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="e6477-118">tooview Olá internas informações de IP estático para Olá VM criada com o script de saudação acima, execute Olá comando PowerShell a seguir e observar os valores hello para *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="e6477-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="e6477-119">Como tooremove um endereço IP interno estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="e6477-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="e6477-120">tooremove Olá IP interno estático adicionado toohello VM no script de saudação acima, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6477-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="e6477-121">Como tooadd uma tooan IP interno estático VM existente</span><span class="sxs-lookup"><span data-stu-id="e6477-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="e6477-122">tooadd um toohello IP interno estático VM criada usando o script hello acima runt comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6477-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e6477-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6477-123">Next steps</span></span>
[<span data-ttu-id="e6477-124">IP Reservado</span><span class="sxs-lookup"><span data-stu-id="e6477-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="e6477-125">IP Público em Nível de Instância (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="e6477-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="e6477-126">APIs REST com IP Reservado</span><span class="sxs-lookup"><span data-stu-id="e6477-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

