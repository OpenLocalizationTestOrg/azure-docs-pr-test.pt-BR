---
title: "endereços IP privados de aaaConfigure para VMs (clássico) - PowerShell do Azure | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure máquinas virtuais (clássico) usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a><span data-ttu-id="33493-103">Configurar endereços IP particulares para uma máquina virtual (Clássica) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="33493-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="33493-104">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="33493-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="33493-105">Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="33493-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="33493-106">comandos do PowerShell de exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="33493-106">hello sample PowerShell commands below expect a simple environment already created.</span></span> <span data-ttu-id="33493-107">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="33493-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="33493-108">Como tooverify se um endereço IP específico está disponível</span><span class="sxs-lookup"><span data-stu-id="33493-108">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="33493-109">tooverify se hello endereço IP *192.168.1.101* está disponível em uma rede virtual denominada *TestVNet*, execute Olá comando PowerShell a seguir e verifique se o valor de saudação para *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="33493-109">tooverify if hello IP address *192.168.1.101* is available in a VNet named *TestVNet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

<span data-ttu-id="33493-110">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="33493-110">Expected output:</span></span>

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="33493-111">Como toospecify um particular de endereços IP estáticos ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="33493-111">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="33493-112">Olá script do PowerShell abaixo cria um novo serviço de nuvem chamado *TestService*, em seguida, recupera uma imagem do Azure, cria uma VM denominada *DNS01* Olá novo serviço de nuvem usando a imagem Olá recuperado, define Olá toobe VM em uma sub-rede denominada *front-end*e define *192.168.1.7* como um endereço IP privado estático para Olá VM:</span><span class="sxs-lookup"><span data-stu-id="33493-112">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

<span data-ttu-id="33493-113">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="33493-113">Expected output:</span></span>

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="33493-114">Como informações de uma VM de endereço de IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="33493-114">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="33493-115">tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá comando PowerShell a seguir e observe os valores hello para *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="33493-115">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name DNS01 -ServiceName TestService

<span data-ttu-id="33493-116">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="33493-116">Expected output:</span></span>

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="33493-117">Como tooremove um particular de endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="33493-117">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="33493-118">tooremove Olá endereço IP privado estático adicionados toohello VM script hello acima, Olá executar comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="33493-118">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

<span data-ttu-id="33493-119">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="33493-119">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="33493-120">Como tooadd um endereço IP privado estático endereço tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="33493-120">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="33493-121">tooadd um toohello de endereço IP de privado estático VM criada usando o script hello acima runt comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="33493-121">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

<span data-ttu-id="33493-122">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="33493-122">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a><span data-ttu-id="33493-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33493-123">Next steps</span></span>
* <span data-ttu-id="33493-124">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="33493-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="33493-125">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="33493-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="33493-126">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="33493-126">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

