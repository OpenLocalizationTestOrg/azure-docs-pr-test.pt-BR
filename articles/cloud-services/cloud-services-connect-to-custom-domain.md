---
title: "Conectar um Serviço de Nuvem em um Controlador de Domínio personalizado | Microsoft Docs"
description: "Saiba como conectar suas funções web/de trabalho a um domínio do AD personalizado usando o PowerShell e a extensão de domínio do AD"
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="29af6-103">Conectando funções dos Serviços de Nuvem do Azure a um controlador de domínio do AD personalizado hospedado no Azure</span><span class="sxs-lookup"><span data-stu-id="29af6-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="29af6-104">Primeiro iremos definir a uma Rede Virtual (VNet) no Azure.</span><span class="sxs-lookup"><span data-stu-id="29af6-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="29af6-105">Em seguida, adicionaremos um Controlador de Domínio do Active Directory (hospedado em uma Máquina Virtual do Azure) à VNet.</span><span class="sxs-lookup"><span data-stu-id="29af6-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="29af6-106">Em seguida, adicionaremos funções de serviço de nuvem existentes à VNet pré-criada e as conectaremos ao controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="29af6-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="29af6-107">Antes de começar, algumas das coisas que você precisa ter em mente:</span><span class="sxs-lookup"><span data-stu-id="29af6-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="29af6-108">Este tutorial usa o PowerShell; portanto, certifique-se de que o Azure PowerShell esteja instalado e pronto.</span><span class="sxs-lookup"><span data-stu-id="29af6-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="29af6-109">Para obter ajuda na configuração do Azure PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29af6-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="29af6-110">As instâncias do controlador de domínio do AD e a função web/de trabalho precisam estar na VNet.</span><span class="sxs-lookup"><span data-stu-id="29af6-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="29af6-111">Siga este guia passo a passo e, se tiver algum problema, deixe um comentário ao final do artigo.</span><span class="sxs-lookup"><span data-stu-id="29af6-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="29af6-112">Alguém entrará em contato com você (sim, lemos comentários).</span><span class="sxs-lookup"><span data-stu-id="29af6-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="29af6-113">A rede que é referenciada pelo serviço de nuvem deve ser uma **rede virtual clássica**.</span><span class="sxs-lookup"><span data-stu-id="29af6-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="29af6-114">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="29af6-114">Create a Virtual Network</span></span>
<span data-ttu-id="29af6-115">Você pode criar uma Rede Virtual no Azure usando o Portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29af6-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="29af6-116">Para este tutorial, usaremos o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29af6-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="29af6-117">Para criar uma Rede Virtual usando o Portal do Azure, confira [Criar uma Rede Virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="29af6-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="29af6-118">Criar uma Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="29af6-118">Create a Virtual Machine</span></span>
<span data-ttu-id="29af6-119">Depois de ter concluído a configuração da rede virtual, você precisará criar um controlador de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="29af6-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="29af6-120">Para este tutorial, vamos configurar um controlador de domínio do AD em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="29af6-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="29af6-121">Para fazer isso, crie uma máquina virtual por meio do PowerShell usando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29af6-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="29af6-122">Promova a máquina virtual a um controlador de domínio</span><span class="sxs-lookup"><span data-stu-id="29af6-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="29af6-123">Para configurar a máquina virtual como um controlador de domínio do AD, você precisará fazer logon na VM e configurá-la.</span><span class="sxs-lookup"><span data-stu-id="29af6-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="29af6-124">Para fazer logon na VM, você pode obter o arquivo RDP por meio do PowerShell. Use os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29af6-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="29af6-125">Depois de fazer logon na VM, configure sua Máquina virtual como um Controlador de domínio do AD, seguindo o guia passo a passo [Como configurar o Controlador de domínio do AD do cliente](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="29af6-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="29af6-126">Adicionar seu Serviço de Nuvem à Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="29af6-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="29af6-127">Em seguida, você precisa adicionar a implantação do serviço de nuvem à nova VNet.</span><span class="sxs-lookup"><span data-stu-id="29af6-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="29af6-128">Para fazer isso, modifique seu cscfg do serviço de nuvem adicionando as seções relevantes ao seu cscfg usando o Visual Studio ou o editor de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="29af6-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="29af6-129">Em seguida, compile o projeto de serviços de nuvem e implante-o no Azure.</span><span class="sxs-lookup"><span data-stu-id="29af6-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="29af6-130">Para obter ajuda com a implantação do pacote de serviços de nuvem no Azure, consulte [Como criar e implantar um Serviço de Nuvem](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="29af6-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="29af6-131">Conectar suas funções Web/de trabalho ao domínio</span><span class="sxs-lookup"><span data-stu-id="29af6-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="29af6-132">Quando seu projeto de serviço de nuvem for implantado no Azure, conecte suas instâncias de função ao domínio do AD personalizado usando a extensão de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="29af6-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="29af6-133">Para adicionar a Extensão de Domínio do AD à sua implantação de serviços de nuvem existente e ingressar no domínio personalizado, execute os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="29af6-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="29af6-134">E isso é tudo.</span><span class="sxs-lookup"><span data-stu-id="29af6-134">And that's it.</span></span>

<span data-ttu-id="29af6-135">Os serviços de nuvem devem ser ingressados no seu controlador de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="29af6-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="29af6-136">Se você gostaria de saber mais sobre as diferentes opções disponíveis para configurar a extensão do domínio do AD, use a Ajuda do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29af6-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="29af6-137">Aqui estão alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="29af6-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
