---
title: "endereços de IP público (clássico) aaaAzure nível de instância | Microsoft Docs"
description: "Entender os endereços de IP (ILPIP) de público com nível de instância e como toomanage-los usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="c3b17-103">Visão geral de IP público em nível de instância (Clássico)</span><span class="sxs-lookup"><span data-stu-id="c3b17-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="c3b17-104">Uma instância de IP público nível (ILPIP) é um endereço IP público que você pode atribuir diretamente tooa instância de função VM ou serviços de nuvem, em vez de serviço de nuvem toohello que sua instância de função ou máquina virtual residem em.</span><span class="sxs-lookup"><span data-stu-id="c3b17-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="c3b17-105">Um ILPIP não substituir Olá Olá IP virtual (VIP) atribuído tooyour serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c3b17-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="c3b17-106">Em vez disso, ele é um endereço IP adicional que você pode usar tooconnect diretamente tooyour VM ou instância de função.</span><span class="sxs-lookup"><span data-stu-id="c3b17-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3b17-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3b17-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="c3b17-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c3b17-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="c3b17-109">A Microsoft recomenda a criação de VMs por meio do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c3b17-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="c3b17-110">Certifique-se de que você entenda como os [endereços IP](virtual-network-ip-addresses-overview-classic.md) funcionam no Azure.</span><span class="sxs-lookup"><span data-stu-id="c3b17-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Diferença entre ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="c3b17-112">Conforme mostrado na Figura 1, o serviço de nuvem Olá é acessado usando um VIP, durante a saudação VMs individuais normalmente são acessadas usando o VIP:&lt;número da porta&gt;.</span><span class="sxs-lookup"><span data-stu-id="c3b17-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="c3b17-113">Atribuindo um tooa ILPIP VM específica, que a VM pode ser acessado diretamente usando o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="c3b17-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="c3b17-114">Quando você cria um serviço de nuvem no Azure, os registros DNS A correspondentes são criados automaticamente serviço de toohello tooallow acesso através de um nome de domínio totalmente qualificado (FQDN), em vez de usar o VIP real hello.</span><span class="sxs-lookup"><span data-stu-id="c3b17-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="c3b17-115">Olá mesmo processo ocorre para um ILPIP, permitindo acesso toohello VM ou instância de função pelo FQDN em vez da saudação ILPIP.</span><span class="sxs-lookup"><span data-stu-id="c3b17-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="c3b17-116">Por exemplo, se você criar um serviço de nuvem chamado *contosoadservice*, e você configurar uma função web chamada *contosoweb* com duas instâncias, os registros de saudação do Azure registra seguindo um para instâncias de saudação:</span><span class="sxs-lookup"><span data-stu-id="c3b17-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="c3b17-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="c3b17-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="c3b17-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="c3b17-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="c3b17-119">Você pode atribuir apenas um ILPIP para cada VM ou instância de função.</span><span class="sxs-lookup"><span data-stu-id="c3b17-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="c3b17-120">Você pode usar o ILPIPs too5 por assinatura.</span><span class="sxs-lookup"><span data-stu-id="c3b17-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="c3b17-121">Não há suporte para ILPIPs em VMs com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="c3b17-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="c3b17-122">Por que solicitar um ILPIP?</span><span class="sxs-lookup"><span data-stu-id="c3b17-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="c3b17-123">Se você quiser toobe capaz de tooconnect tooyour VM ou instância de função por um endereço IP atribuído diretamente tooit, em vez de usar nuvem Olá serviço VIP:&lt;número da porta&gt;, solicitar um ILPIP para sua VM ou sua instância de função.</span><span class="sxs-lookup"><span data-stu-id="c3b17-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="c3b17-124">**FTP ativo** -atribuindo um tooa ILPIP VM, ela pode receber tráfego em qualquer porta.</span><span class="sxs-lookup"><span data-stu-id="c3b17-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="c3b17-125">Pontos de extremidade não são necessários para Olá tooreceive o tráfego de VM.</span><span class="sxs-lookup"><span data-stu-id="c3b17-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="c3b17-126">Consulte (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Visão geral do protocolo FTP] para obter detalhes sobre o protocolo de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="c3b17-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="c3b17-127">**IP de saída** - o tráfego de saída provenientes de saudação VM é mapeado toohello ILPIP como origem hello e Olá ILPIP identifica entidades de tooexternal Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c3b17-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="c3b17-128">Olá anterior, um endereço ILPIP era chamado tooas um endereço IP (PIP).</span><span class="sxs-lookup"><span data-stu-id="c3b17-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="c3b17-129">Gerenciar um ILPIP de uma VM</span><span class="sxs-lookup"><span data-stu-id="c3b17-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="c3b17-130">Olá tarefas a seguir permitem que você toocreate, atribuir e remover ILPIPs de VMs:</span><span class="sxs-lookup"><span data-stu-id="c3b17-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="c3b17-131">Como toorequest um ILPIP durante a criação da VM usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3b17-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="c3b17-132">saudação de script do PowerShell a seguir cria um serviço de nuvem chamado *FTPService*, recupera uma imagem do Azure, cria uma VM denominada *FTPInstance* usando a imagem Olá recuperado, define Olá VM toouse um ILPIP e adiciona um novo serviço de saudação VM toohello:</span><span class="sxs-lookup"><span data-stu-id="c3b17-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="c3b17-133">Como obter informações de ILPIP tooretrieve para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c3b17-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="c3b17-134">Olá tooview informações ILPIP para Olá VM criada com o script anterior do hello, execute Olá comando PowerShell a seguir e observar os valores hello para *PublicIPAddress* e *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="c3b17-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="c3b17-135">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="c3b17-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="c3b17-136">Como tooremove uma ILPIP de uma VM</span><span class="sxs-lookup"><span data-stu-id="c3b17-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="c3b17-137">Olá tooremove ILPIP adicionados toohello VM Olá anterior execução de script, Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3b17-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="c3b17-138">Como tooadd uma tooan ILPIP VM existente</span><span class="sxs-lookup"><span data-stu-id="c3b17-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="c3b17-139">tooadd toohello um ILPIP VM criada usando o script de saudação anterior, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3b17-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="c3b17-140">Gerenciar um ILPIP de uma instância de função dos Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="c3b17-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="c3b17-141">tooadd uma instância de função de serviços de nuvem do ILPIP tooa, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3b17-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="c3b17-142">Baixar arquivo. cscfg de saudação para serviço de nuvem Olá Concluindo Olá as etapas em Olá [como serviços em nuvem tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.</span><span class="sxs-lookup"><span data-stu-id="c3b17-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="c3b17-143">Arquivo. cscfg de atualização de saudação adicionando Olá `InstanceAddress` elemento.</span><span class="sxs-lookup"><span data-stu-id="c3b17-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="c3b17-144">Olá, exemplo a seguir adiciona um ILPIP denominado *MyPublicIP* tooa instância de função chamada *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="c3b17-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="c3b17-145">Carregar arquivo. cscfg de saudação para serviço de nuvem Olá Concluindo Olá as etapas em Olá [como serviços em nuvem tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.</span><span class="sxs-lookup"><span data-stu-id="c3b17-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3b17-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3b17-146">Next steps</span></span>
* <span data-ttu-id="c3b17-147">Entender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c3b17-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="c3b17-148">Saiba mais sobre [IPs reservados](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c3b17-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
