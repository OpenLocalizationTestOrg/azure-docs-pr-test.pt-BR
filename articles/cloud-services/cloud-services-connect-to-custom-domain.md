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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="bfbf5-103">Conectando a funções de serviços de nuvem do Azure tooa personalizado controlador de domínio do AD hospedado no Azure</span><span class="sxs-lookup"><span data-stu-id="bfbf5-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="bfbf5-104">Primeiro iremos definir a uma Rede Virtual (VNet) no Azure.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="bfbf5-105">Em seguida, adicionaremos um toohello rede virtual do controlador de domínio do Active Directory (hospedada em uma máquina Virtual do Azure).</span><span class="sxs-lookup"><span data-stu-id="bfbf5-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="bfbf5-106">Em seguida, podemos adicionar toohello de funções de serviço de nuvem existente criado previamente VNet e conectá-los toohello controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="bfbf5-107">Antes de começar, algumas das coisas tookeep em mente:</span><span class="sxs-lookup"><span data-stu-id="bfbf5-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="bfbf5-108">Este tutorial usa o PowerShell, portanto, verifique se você tiver o Azure PowerShell instalado e pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="bfbf5-109">tooget ajuda a configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bfbf5-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="bfbf5-110">Suas instâncias de controlador de domínio do AD e a função Web/trabalho necessário toobe em Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="bfbf5-111">Siga este guia passo a passo e se você tiver problemas, faça um comentário final Olá Olá artigo.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="bfbf5-112">Alguém irá contatá-tooyou (Sim, podemos ler comentários).</span><span class="sxs-lookup"><span data-stu-id="bfbf5-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="bfbf5-113">Olá rede que é referenciado pelo serviço de nuvem Olá deve ser um **rede virtual clássica**.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="bfbf5-114">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="bfbf5-114">Create a Virtual Network</span></span>
<span data-ttu-id="bfbf5-115">Você pode criar uma rede Virtual no Azure usando Olá portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="bfbf5-116">Para este tutorial, usaremos o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="bfbf5-117">toocreate usando uma rede Virtual hello Azure portal, consulte [criar rede Virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bfbf5-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="bfbf5-118">Criar uma Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="bfbf5-118">Create a Virtual Machine</span></span>
<span data-ttu-id="bfbf5-119">Depois de concluir a configuração de rede Virtual de saudação, você precisará toocreate um controlador de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="bfbf5-120">Para este tutorial, vamos configurar um controlador de domínio do AD em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="bfbf5-121">toodo isso, crie uma máquina virtual por meio do PowerShell usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfbf5-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="bfbf5-122">Promover o controlador de domínio de tooa de máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="bfbf5-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="bfbf5-123">Olá tooconfigure Máquina Virtual como um controlador de domínio do AD, será necessário toolog em toohello VM e configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="bfbf5-124">toolog em toohello VM, você pode obter o arquivo RDP de saudação por meio do PowerShell, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfbf5-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="bfbf5-125">Quando você estiver entrado toohello VM, configurar sua máquina Virtual como um controlador de domínio do AD pelo seguinte guia passo a passo de saudação em [como tooset seu controlador de domínio do AD do cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfbf5-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="bfbf5-126">Adicionar sua rede Virtual de toohello do serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="bfbf5-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="bfbf5-127">Em seguida, você precisa tooadd seu toohello de implantação do serviço de nuvem nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="bfbf5-128">toodo isso, modifique o cscfg do serviço de nuvem adicionando Olá seções relevantes tooyour cscfg usando o Visual Studio ou Olá editor de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

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

<span data-ttu-id="bfbf5-129">Em seguida compilar o projeto de serviços de nuvem e implantá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="bfbf5-130">tooget ajuda com a implantação de seu tooAzure de pacote de serviços de nuvem, consulte [como tooCreate e implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="bfbf5-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="bfbf5-131">Conecte-se o seu domínio de toohello funções web/de trabalho</span><span class="sxs-lookup"><span data-stu-id="bfbf5-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="bfbf5-132">Quando seu projeto de serviço de nuvem é implantado no Azure, conecte-se o domínio de toohello AD personalizado de instâncias de função usando Olá extensão de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="bfbf5-133">Olá tooadd implantação dos serviços de nuvem existente extensão de domínio do AD tooyour e ingressar no domínio personalizado hello, execute Olá comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfbf5-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

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

<span data-ttu-id="bfbf5-134">E isso é tudo.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-134">And that's it.</span></span>

<span data-ttu-id="bfbf5-135">Os serviços de nuvem devem ser o controlador de domínio personalizado tooyour unidas.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="bfbf5-136">Se você gostaria que toolearn mais sobre Olá diferentes opções disponíveis para como tooconfigure extensão de domínio do AD, use Olá PowerShell ajudar.</span><span class="sxs-lookup"><span data-stu-id="bfbf5-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="bfbf5-137">Aqui estão alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="bfbf5-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
