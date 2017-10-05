---
title: "Acesso e segurança em modelos do Azure para VMs do Windows | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ad1b5c4763cf56f681a50bb1bccc825311bbfdf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="8039c-103">Acesso e segurança em modelos do Azure Resource Manager para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="8039c-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="8039c-104">Aplicativos hospedados no Azure provavelmente precisam ser acessados pela Internet ou por uma VPN/conexão de rota expressa com o Azure.</span><span class="sxs-lookup"><span data-stu-id="8039c-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="8039c-105">Com o exemplo de aplicativo de Loja de Música, o site da Web é disponibilizado na Internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8039c-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="8039c-106">Com acesso estabelecido, as conexões com o aplicativo e o acessa aos recursos de máquina virtual devem ser protegidos.</span><span class="sxs-lookup"><span data-stu-id="8039c-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="8039c-107">Essa segurança de acesso é fornecida com um Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="8039c-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="8039c-108">Este documento fornece detalhes sobre como o aplicativo de Loja de Música é protegido no modelo do Azure Resource Manager de exemplo.</span><span class="sxs-lookup"><span data-stu-id="8039c-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="8039c-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="8039c-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8039c-110">Para obter a melhor experiência, pré-implante uma instância da solução em sua assinatura do Azure e trabalhe com o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8039c-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="8039c-111">O modelo completo pode ser encontrado aqui – [Implantação de Loja de Música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="8039c-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="8039c-112">Endereço IP público</span><span class="sxs-lookup"><span data-stu-id="8039c-112">Public IP Address</span></span>
<span data-ttu-id="8039c-113">Para fornecer acesso público a um recurso do Azure, um recurso de endereço IP público pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="8039c-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="8039c-114">O endereço IP público pode ser configurado com um endereço IP estático ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8039c-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="8039c-115">Se um endereço dinâmico for usado e a máquina virtual for interrompida e desalocada, os endereços serão removidos.</span><span class="sxs-lookup"><span data-stu-id="8039c-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="8039c-116">Quando o computador for iniciado novamente, ele poderá ser atribuído um endereço IP público diferente.</span><span class="sxs-lookup"><span data-stu-id="8039c-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="8039c-117">Para impedir a alteração de um endereço IP, um endereço IP reservado pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="8039c-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="8039c-118">Um endereço IP público pode ser adicionado a um modelo do Azure Resource Manager usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo.</span><span class="sxs-lookup"><span data-stu-id="8039c-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="8039c-119">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="8039c-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="8039c-120">Um endereço IP público pode ser associado a um adaptador de rede virtual ou a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8039c-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="8039c-121">Neste exemplo, como o site de Loja de Música tem carga balanceada entre várias máquinas virtuais, o endereço IP público está conectado ao balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8039c-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="8039c-122">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de endereço IP público com balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="8039c-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="8039c-123">O endereço IP público como visto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8039c-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="8039c-124">Observe que o endereço IP público está associado a um balanceador de carga, e não a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8039c-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="8039c-125">Balanceadores de carga de rede são detalhados no seguinte documento desta série.</span><span class="sxs-lookup"><span data-stu-id="8039c-125">Network load balancers are detailed in the next document of this series.</span></span>

![Endereço IP público](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="8039c-127">Para obter mais informações sobre os endereços IP públicos do Azure, consulte [Endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8039c-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="8039c-128">Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="8039c-128">Network Security Group</span></span>
<span data-ttu-id="8039c-129">Depois de estabelecer acesso aos recursos do Azure, esse acesso deve ser limitado.</span><span class="sxs-lookup"><span data-stu-id="8039c-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="8039c-130">Para máquinas virtuais do Azure, proteger o acesso é feito usando um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="8039c-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="8039c-131">Com o exemplo do aplicativo de Loja de Música, todo o acesso à máquina virtual é restrito exceto pela porta 80 para o acesso http e a porta 3389 para acesso do RDP.</span><span class="sxs-lookup"><span data-stu-id="8039c-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="8039c-132">Um grupo de segurança de rede pode ser adicionado a um modelo do Azure Resource Manager usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo.</span><span class="sxs-lookup"><span data-stu-id="8039c-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="8039c-133">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Grupo de segurança de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="8039c-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="8039c-134">Neste exemplo, o grupo de segurança de rede é associado com o objeto de sub-rede declarado no recurso de Rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="8039c-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="8039c-135">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de grupo de segurança de rede com Rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="8039c-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

<span data-ttu-id="8039c-136">Aqui está a aparência do grupo de segurança de rede no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8039c-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="8039c-137">Observe que um NSG pode associar-se a um adaptador de sub-rede e/ou rede.</span><span class="sxs-lookup"><span data-stu-id="8039c-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="8039c-138">Nesse caso, o NSG é associado a uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8039c-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="8039c-139">Nessa configuração, as regras de entrada se aplicam a todas as máquinas virtuais conectadas à sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8039c-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![Grupo de Segurança de Rede](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="8039c-141">Para obter informações detalhadas sobre grupos de segurança de rede, leia [O que é um Grupo de Segurança de Rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="8039c-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="8039c-142">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="8039c-142">Next step</span></span>
<hr>

[<span data-ttu-id="8039c-143">Etapa 3 – Disponibilidade e escala em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8039c-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

