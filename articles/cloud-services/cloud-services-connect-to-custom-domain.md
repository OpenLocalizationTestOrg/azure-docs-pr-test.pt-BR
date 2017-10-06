---
title: "aaaConnect tooa um serviço de nuvem controlador de domínio personalizado | Microsoft Docs"
description: "Saiba como tooconnect web/trabalhador funções tooa personalizados domínio de AD usando o PowerShell e a extensão de domínio do AD"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Conectando a funções de serviços de nuvem do Azure tooa personalizado controlador de domínio do AD hospedado no Azure
Primeiro iremos definir a uma Rede Virtual (VNet) no Azure. Em seguida, adicionaremos um toohello rede virtual do controlador de domínio do Active Directory (hospedada em uma máquina Virtual do Azure). Em seguida, podemos adicionar toohello de funções de serviço de nuvem existente criado previamente VNet e conectá-los toohello controlador de domínio.

Antes de começar, algumas das coisas tookeep em mente:

1. Este tutorial usa o PowerShell, portanto, verifique se você tiver o Azure PowerShell instalado e pronto toogo. tooget ajuda a configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
2. Suas instâncias de controlador de domínio do AD e a função Web/trabalho necessário toobe em Olá VNet.

Siga este guia passo a passo e se você tiver problemas, faça um comentário final Olá Olá artigo. Alguém irá contatá-tooyou (Sim, podemos ler comentários).

Olá rede que é referenciado pelo serviço de nuvem Olá deve ser um **rede virtual clássica**.

## <a name="create-a-virtual-network"></a>Criar uma rede virtual
Você pode criar uma rede Virtual no Azure usando Olá portal do Azure ou o PowerShell. Para este tutorial, usaremos o PowerShell. toocreate usando uma rede Virtual hello Azure portal, consulte [criar rede Virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Criar uma Máquina Virtual
Depois de concluir a configuração de rede Virtual de saudação, você precisará toocreate um controlador de domínio do AD. Para este tutorial, vamos configurar um controlador de domínio do AD em uma máquina virtual do Azure.

toodo isso, crie uma máquina virtual por meio do PowerShell usando Olá comandos a seguir:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Promover o controlador de domínio de tooa de máquina Virtual
Olá tooconfigure Máquina Virtual como um controlador de domínio do AD, será necessário toolog em toohello VM e configurá-lo.

toolog em toohello VM, você pode obter o arquivo RDP de saudação por meio do PowerShell, use Olá comandos a seguir:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Quando você estiver entrado toohello VM, configurar sua máquina Virtual como um controlador de domínio do AD pelo seguinte guia passo a passo de saudação em [como tooset seu controlador de domínio do AD do cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Adicionar sua rede Virtual de toohello do serviço de nuvem
Em seguida, você precisa tooadd seu toohello de implantação do serviço de nuvem nova rede virtual. toodo isso, modifique o cscfg do serviço de nuvem adicionando Olá seções relevantes tooyour cscfg usando o Visual Studio ou Olá editor de sua escolha.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

Em seguida compilar o projeto de serviços de nuvem e implantá-lo tooAzure. tooget ajuda com a implantação de seu tooAzure de pacote de serviços de nuvem, consulte [como tooCreate e implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Conecte-se o seu domínio de toohello funções web/de trabalho
Quando seu projeto de serviço de nuvem é implantado no Azure, conecte-se o domínio de toohello AD personalizado de instâncias de função usando Olá extensão de domínio do AD. Olá tooadd implantação dos serviços de nuvem existente extensão de domínio do AD tooyour e ingressar no domínio personalizado hello, execute Olá comandos do PowerShell a seguir:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

E isso é tudo.

Os serviços de nuvem devem ser o controlador de domínio personalizado tooyour unidas. Se você gostaria que toolearn mais sobre Olá diferentes opções disponíveis para como tooconfigure extensão de domínio do AD, use Olá PowerShell ajudar. Aqui estão alguns exemplos:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
