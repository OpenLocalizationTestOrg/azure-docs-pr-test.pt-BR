---
title: "IP privado interno estático – VM do Azure – Clássico"
description: "Noções básicas sobre IPs estáticos internos (DIPs) e como gerenciá-los"
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="1cf35-103">Como definir um endereço IP privado interno estático usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="1cf35-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="1cf35-104">Na maioria dos casos, você não precisará especificar um endereço IP interno estático para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1cf35-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="1cf35-105">As VMs de uma rede virtual receberão automaticamente endereço IP interno de um intervalo especificado por você.</span><span class="sxs-lookup"><span data-stu-id="1cf35-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="1cf35-106">Mas, em alguns casos, a especificação de um endereço IP estático para uma determinada VM fará sentido.</span><span class="sxs-lookup"><span data-stu-id="1cf35-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="1cf35-107">Por exemplo, se a sua VM se destinar à execução de DNS ou a ser um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="1cf35-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="1cf35-108">Um endereço IP interno estático permanece com a VM mesmo em um estado de interrupção/desprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="1cf35-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1cf35-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1cf35-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1cf35-110">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="1cf35-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="1cf35-111">A Microsoft recomenda que a maioria das implantações novas use o [modelo de implantação do Gerenciador de Recursos](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1cf35-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="1cf35-112">Você pode verificar se um endereço IP específico está disponível</span><span class="sxs-lookup"><span data-stu-id="1cf35-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="1cf35-113">Para verificar se o endereço IP *10.0.0.7* está disponível em uma VNet *TestVnet*, execute o seguinte comando do PowerShell e verifique o valor de *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="1cf35-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="1cf35-114">Se você quiser testar o comando acima em um ambiente seguro, siga as diretrizes em [Criar uma rede virtual (clássica)](virtual-networks-create-vnet-classic-pportal.md) para criar uma rede virtual denominada *TestVnet* e verificar se ela usa o espaço de endereço *10.0.0.0/8*.</span><span class="sxs-lookup"><span data-stu-id="1cf35-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="1cf35-115">Como especificar um endereço IP interno estático ao criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1cf35-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="1cf35-116">O script do PowerShell abaixo cria um novo serviço de nuvem chamado *TestService* e, em seguida, recupera uma imagem do Azure e cria uma VM denominada *TestVM* no novo serviço de nuvem usando a imagem recuperada, define a VM em uma sub-rede denominada *Subnet-1* e define *10.0.0.7* como um endereço IP interno estático para a VM:</span><span class="sxs-lookup"><span data-stu-id="1cf35-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="1cf35-117">Como recuperar informações de IP interno estático para uma VM</span><span class="sxs-lookup"><span data-stu-id="1cf35-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="1cf35-118">Para exibir as informações do IP interno estático da VM criado com o script acima, execute o seguinte comando do PowerShell e observe os valores de *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="1cf35-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="1cf35-119">Como remover um endereço IP interno estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="1cf35-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="1cf35-120">Para remover o IP interno estático adicionado à VM no script acima, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1cf35-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="1cf35-121">Como adicionar um IP interno estático a uma VM existente</span><span class="sxs-lookup"><span data-stu-id="1cf35-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="1cf35-122">Para adicionar um IP interno estático à VM criada usando o script acima, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1cf35-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="1cf35-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1cf35-123">Next steps</span></span>
[<span data-ttu-id="1cf35-124">IP Reservado</span><span class="sxs-lookup"><span data-stu-id="1cf35-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="1cf35-125">IP Público em Nível de Instância (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="1cf35-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="1cf35-126">APIs REST com IP Reservado</span><span class="sxs-lookup"><span data-stu-id="1cf35-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

