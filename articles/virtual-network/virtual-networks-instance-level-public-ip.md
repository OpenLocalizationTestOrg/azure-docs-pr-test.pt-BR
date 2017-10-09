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
# <a name="instance-level-public-ip-classic-overview"></a>Visão geral de IP público em nível de instância (Clássico)
Uma instância de IP público nível (ILPIP) é um endereço IP público que você pode atribuir diretamente tooa instância de função VM ou serviços de nuvem, em vez de serviço de nuvem toohello que sua instância de função ou máquina virtual residem em. Um ILPIP não substituir Olá Olá IP virtual (VIP) atribuído tooyour serviço de nuvem. Em vez disso, ele é um endereço IP adicional que você pode usar tooconnect diretamente tooyour VM ou instância de função.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda a criação de VMs por meio do Resource Manager. Certifique-se de que você entenda como os [endereços IP](virtual-network-ip-addresses-overview-classic.md) funcionam no Azure.

![Diferença entre ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Conforme mostrado na Figura 1, o serviço de nuvem Olá é acessado usando um VIP, durante a saudação VMs individuais normalmente são acessadas usando o VIP:&lt;número da porta&gt;. Atribuindo um tooa ILPIP VM específica, que a VM pode ser acessado diretamente usando o endereço IP.

Quando você cria um serviço de nuvem no Azure, os registros DNS A correspondentes são criados automaticamente serviço de toohello tooallow acesso através de um nome de domínio totalmente qualificado (FQDN), em vez de usar o VIP real hello. Olá mesmo processo ocorre para um ILPIP, permitindo acesso toohello VM ou instância de função pelo FQDN em vez da saudação ILPIP. Por exemplo, se você criar um serviço de nuvem chamado *contosoadservice*, e você configurar uma função web chamada *contosoweb* com duas instâncias, os registros de saudação do Azure registra seguindo um para instâncias de saudação:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Você pode atribuir apenas um ILPIP para cada VM ou instância de função. Você pode usar o ILPIPs too5 por assinatura. Não há suporte para ILPIPs em VMs com várias NICs.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Por que solicitar um ILPIP?
Se você quiser toobe capaz de tooconnect tooyour VM ou instância de função por um endereço IP atribuído diretamente tooit, em vez de usar nuvem Olá serviço VIP:&lt;número da porta&gt;, solicitar um ILPIP para sua VM ou sua instância de função.

* **FTP ativo** -atribuindo um tooa ILPIP VM, ela pode receber tráfego em qualquer porta. Pontos de extremidade não são necessários para Olá tooreceive o tráfego de VM.  Consulte (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Visão geral do protocolo FTP] para obter detalhes sobre o protocolo de saudação FTP.
* **IP de saída** - o tráfego de saída provenientes de saudação VM é mapeado toohello ILPIP como origem hello e Olá ILPIP identifica entidades de tooexternal Olá VM.

> [!NOTE]
> Olá anterior, um endereço ILPIP era chamado tooas um endereço IP (PIP).
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Gerenciar um ILPIP de uma VM
Olá tarefas a seguir permitem que você toocreate, atribuir e remover ILPIPs de VMs:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Como toorequest um ILPIP durante a criação da VM usando o PowerShell
saudação de script do PowerShell a seguir cria um serviço de nuvem chamado *FTPService*, recupera uma imagem do Azure, cria uma VM denominada *FTPInstance* usando a imagem Olá recuperado, define Olá VM toouse um ILPIP e adiciona um novo serviço de saudação VM toohello:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Como obter informações de ILPIP tooretrieve para uma máquina virtual
Olá tooview informações ILPIP para Olá VM criada com o script anterior do hello, execute Olá comando PowerShell a seguir e observar os valores hello para *PublicIPAddress* e *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Saída esperada:
 
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

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Como tooremove uma ILPIP de uma VM
Olá tooremove ILPIP adicionados toohello VM Olá anterior execução de script, Olá comando PowerShell a seguir:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Como tooadd uma tooan ILPIP VM existente
tooadd toohello um ILPIP VM criada usando o script de saudação anterior, execute Olá comando a seguir:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Gerenciar um ILPIP de uma instância de função dos Serviços de Nuvem

tooadd uma instância de função de serviços de nuvem do ILPIP tooa, Olá concluir as etapas a seguir:

1. Baixar arquivo. cscfg de saudação para serviço de nuvem Olá Concluindo Olá as etapas em Olá [como serviços em nuvem tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.
2. Arquivo. cscfg de atualização de saudação adicionando Olá `InstanceAddress` elemento. Olá, exemplo a seguir adiciona um ILPIP denominado *MyPublicIP* tooa instância de função chamada *WebRole1*: 

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
3. Carregar arquivo. cscfg de saudação para serviço de nuvem Olá Concluindo Olá as etapas em Olá [como serviços em nuvem tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.

## <a name="next-steps"></a>Próximas etapas
* Entender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implantação clássico hello.
* Saiba mais sobre [IPs reservados](virtual-networks-reserved-public-ip.md).
