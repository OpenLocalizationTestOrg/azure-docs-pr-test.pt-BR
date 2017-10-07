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
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Como tooset IP privado estático interno de endereço usando o PowerShell (clássico)
Na maioria dos casos, você não precisará toospecify um endereço IP interno estático para sua máquina virtual. As VMs de uma rede virtual receberão automaticamente endereço IP interno de um intervalo especificado por você. Mas, em alguns casos, a especificação de um endereço IP estático para uma determinada VM fará sentido. Por exemplo, se sua VM for contínuo toorun DNS ou será um controlador de domínio. Um endereço IP interno estático permanece com hello VM até mesmo por meio de um estado de interrupção/desprovisionamento. 

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações usam Olá [modelo de implantação do Gerenciador de recursos](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Como tooverify se um endereço IP específico está disponível
tooverify se hello endereço IP *10.0.0.7* está disponível em uma rede virtual denominada *TestVnet*, execute Olá comando PowerShell a seguir e verifique se o valor de saudação para *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Se você quiser que o comando de saudação tootest acima em um ambiente seguro siga as diretrizes de saudação em [criar uma rede virtual (clássica)](virtual-networks-create-vnet-classic-pportal.md) toocreate uma rede virtual denominada *TestVnet* e certifique-se de que ele usa Olá  *10.0.0.0/8* espaço de endereço.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Como toospecify um endereço IP interno estático ao criar uma VM
Olá script do PowerShell abaixo cria um novo serviço de nuvem chamado *TestService*, em seguida, recupera uma imagem do Azure e cria uma VM denominada *TestVM* em Olá novo serviço de nuvem usando a imagem Olá recuperado, conjuntos de Olá toobe VM em uma sub-rede denominada *Subnet-1*e define *10.0.0.7* como um endereço IP interno estático para Olá VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Como tooretrieve internas informações de IP estático para uma máquina virtual
tooview Olá internas informações de IP estático para Olá VM criada com o script de saudação acima, execute Olá comando PowerShell a seguir e observar os valores hello para *IpAddress*:

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Como tooremove um endereço IP interno estático de uma VM
tooremove Olá IP interno estático adicionado toohello VM no script de saudação acima, execute Olá comando PowerShell a seguir:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Como tooadd uma tooan IP interno estático VM existente
tooadd um toohello IP interno estático VM criada usando o script hello acima runt comando a seguir:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Próximas etapas
[IP Reservado](virtual-networks-reserved-public-ip.md)

[IP Público em Nível de Instância (ILPIP)](virtual-networks-instance-level-public-ip.md)

[APIs REST com IP Reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx)

