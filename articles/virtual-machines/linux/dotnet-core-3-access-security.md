---
title: "aaaAccess e segurança em modelos do Azure para VMs do Linux | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="ab532-103">Acesso e segurança em modelos do Azure Resource Manager para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="ab532-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="ab532-104">Aplicativos hospedados no Azure necessidade provavelmente toobe acesso pela hello, internet ou uma VPN / conexão de rota expressa com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ab532-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="ab532-105">Com o exemplo de aplicativo de repositório de música hello, Olá web site é disponibilizado em Olá internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ab532-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="ab532-106">Com acesso estabelecido, conexões toohello aplicativos e acesso toohello recursos da máquina virtual se devem ser protegidos.</span><span class="sxs-lookup"><span data-stu-id="ab532-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="ab532-107">Essa segurança de acesso é fornecida com um Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="ab532-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="ab532-108">Este documento detalha como Olá aplicativo de repositório de música é protegido no modelo de Gerenciador de recursos do Azure do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ab532-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="ab532-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="ab532-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="ab532-110">Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="ab532-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="ab532-111">modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="ab532-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="ab532-112">Endereço IP público</span><span class="sxs-lookup"><span data-stu-id="ab532-112">Public IP Address</span></span>
<span data-ttu-id="ab532-113">tooprovide acesso público tooan recursos do Azure, um recurso de endereço IP público pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="ab532-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="ab532-114">O endereço IP público pode ser configurado com um endereço IP estático ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="ab532-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="ab532-115">Se um endereço dinâmico é usado e máquina virtual de saudação for interrompida e desalocada, endereços de saudação é removido.</span><span class="sxs-lookup"><span data-stu-id="ab532-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="ab532-116">Quando a máquina de saudação for iniciada novamente, ele pode ser atribuído um endereço IP público diferente.</span><span class="sxs-lookup"><span data-stu-id="ab532-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="ab532-117">tooprevent um IP endereço alterem, um endereço IP reservado pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="ab532-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="ab532-118">Um endereço IP público pode ser adicionado o modelo do Azure Resource Manager tooan usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo um JSON válido em um modelo.</span><span class="sxs-lookup"><span data-stu-id="ab532-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="ab532-119">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span><span class="sxs-lookup"><span data-stu-id="ab532-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="ab532-120">Um endereço IP público pode ser associado a um adaptador de rede virtual ou a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="ab532-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="ab532-121">Neste exemplo, porque Olá site do repositório de música carga balanceada entre várias máquinas virtuais, Olá endereço IP público é anexado toohello balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="ab532-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="ab532-122">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de endereços IP públicos com o balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="ab532-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="ab532-123">Olá endereço IP público como visto no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab532-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="ab532-124">Observe que o endereço IP público de saudação é associado tooa balanceador de carga e não uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab532-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="ab532-125">Balanceadores de carga de rede são detalhadas no próximo documento hello desta série.</span><span class="sxs-lookup"><span data-stu-id="ab532-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Endereço IP público](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="ab532-127">Para obter mais informações sobre os endereços IP públicos do Azure, consulte [Endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ab532-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="ab532-128">Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="ab532-128">Network Security Group</span></span>
<span data-ttu-id="ab532-129">Depois que o acesso foi estabelecida tooAzure recursos, esse acesso deve ser limitado.</span><span class="sxs-lookup"><span data-stu-id="ab532-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="ab532-130">Para máquinas virtuais do Azure, proteger o acesso é feito usando um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="ab532-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="ab532-131">Com exemplo de aplicativo de repositório de música hello, todas as máquinas de virtuais toohello de acesso é restrito exceto pela porta 80 para acesso http e a porta 22 para acesso SSH.</span><span class="sxs-lookup"><span data-stu-id="ab532-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="ab532-132">Um grupo de segurança de rede podem ser adicionado como modelo do Azure Resource Manager tooan usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo um JSON válido em um modelo.</span><span class="sxs-lookup"><span data-stu-id="ab532-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="ab532-133">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [grupo de segurança de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span><span class="sxs-lookup"><span data-stu-id="ab532-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
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
}
```

<span data-ttu-id="ab532-134">Neste exemplo, o grupo de segurança de rede de Olá é associado ao objeto da sub-rede Olá declarado no recurso de rede Virtual hello.</span><span class="sxs-lookup"><span data-stu-id="ab532-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="ab532-135">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de grupo de segurança de rede com a rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span><span class="sxs-lookup"><span data-stu-id="ab532-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

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
```

<span data-ttu-id="ab532-136">É o grupo de segurança de rede Olá semelhante ao seguinte da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab532-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="ab532-137">Observe que um NSG pode associar-se a um adaptador de sub-rede e/ou rede.</span><span class="sxs-lookup"><span data-stu-id="ab532-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="ab532-138">Nesse caso, Olá NSG é associado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ab532-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="ab532-139">Nessa configuração, hello entradas regras se aplicam tooall máquinas virtuais conectadas toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ab532-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Grupo de Segurança de Rede](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="ab532-141">Para obter informações detalhadas sobre grupos de segurança de rede, leia [O que é um Grupo de Segurança de Rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="ab532-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="ab532-142">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="ab532-142">Next step</span></span>
<hr>

[<span data-ttu-id="ab532-143">Etapa 3 – Disponibilidade e escala em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab532-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

