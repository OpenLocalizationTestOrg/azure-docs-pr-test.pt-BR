---
title: "aaaDeploying recursos de computação do Windows com modelos do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="2893f-103">Arquitetura de aplicativos com modelos do Azure Resource Manager para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="2893f-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="2893f-104">Ao desenvolver uma implantação do Azure Resource Manager, requisitos de computação necessário toobe mapeado tooAzure recursos e serviços.</span><span class="sxs-lookup"><span data-stu-id="2893f-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="2893f-105">Se um aplicativo consiste em vários pontos de extremidade http, um banco de dados e um serviço de cache de dados, hello recursos do Azure que hospedam cada um desses componentes precisa toobe planejada.</span><span class="sxs-lookup"><span data-stu-id="2893f-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="2893f-106">Por exemplo, o aplicativo de repositório de música de exemplo hello inclui um aplicativo web que é hospedado em uma máquina virtual e um banco de dados SQL, que é hospedado no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2893f-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="2893f-107">Este documento fornece detalhes sobre como os recursos de computação do repositório de música Olá são configurados no modelo de Gerenciador de recursos do Azure do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="2893f-108">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="2893f-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="2893f-109">Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="2893f-110">modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="2893f-110">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="2893f-111">Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="2893f-111">Virtual Machine</span></span>
<span data-ttu-id="2893f-112">saudação de aplicativo de repositório de música inclui um aplicativo da web onde os clientes podem procurar e comprar músicas.</span><span class="sxs-lookup"><span data-stu-id="2893f-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="2893f-113">Embora haja vários serviços do Azure que podem hospedar aplicativos Web, para este exemplo, uma máquina virtual é usada.</span><span class="sxs-lookup"><span data-stu-id="2893f-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="2893f-114">Usando o modelo de repositório de música de exemplo hello, uma máquina virtual é implantada, instalar um servidor web e site do repositório de música Olá instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="2893f-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="2893f-115">Para a mesma Olá deste artigo, somente a implantação de máquina virtual Olá é detalhada.</span><span class="sxs-lookup"><span data-stu-id="2893f-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="2893f-116">configuração de saudação do servidor de web hello e aplicativo hello é detalhada em um artigo posterior.</span><span class="sxs-lookup"><span data-stu-id="2893f-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="2893f-117">Modelo tooa usando o Visual Studio adicionar novos recursos do assistente, ou inserindo um JSON válido no modelo de implantação de saudação do hello pode ser adicionada a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2893f-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="2893f-118">Ao implantar uma máquina virtual, também são necessários vários recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2893f-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="2893f-119">Se usar o modelo do Visual Studio toocreate hello, esses recursos são criados para você.</span><span class="sxs-lookup"><span data-stu-id="2893f-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="2893f-120">Se construir manualmente modelo hello, esses recursos devem toobe inserido e configurado.</span><span class="sxs-lookup"><span data-stu-id="2893f-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="2893f-121">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [JSON de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="2893f-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

<span data-ttu-id="2893f-122">Uma vez implantado, propriedades de máquina virtual Olá podem ser vistas no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2893f-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Máquina Virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="2893f-124">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2893f-124">Storage Account</span></span>
<span data-ttu-id="2893f-125">Contas de armazenamento têm muitos recursos e opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2893f-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="2893f-126">Contexto Olá máquinas virtuais do Azure, uma conta de armazenamento contém discos rígidos virtuais de saudação da máquina virtual de saudação e discos de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="2893f-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="2893f-127">exemplo de repositório de música Hello inclui um armazenamento conta toohold Olá disco rígido virtual de cada máquina virtual na implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2893f-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="2893f-128">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="2893f-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="2893f-129">Uma conta de armazenamento é associado uma máquina virtual dentro da declaração de modelo Olá Gerenciador de recursos de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2893f-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="2893f-130">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de máquina Virtual e a conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="2893f-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="2893f-131">Após a implantação, a conta de armazenamento Olá pode ser exibida no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2893f-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Conta de armazenamento](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="2893f-133">Clicar em um contêiner de blob de conta de armazenamento hello, arquivo de disco rígido virtual Olá para cada máquina virtual implantada com o modelo de saudação pode ser visto.</span><span class="sxs-lookup"><span data-stu-id="2893f-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Discos rígidos virtuais](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="2893f-135">Para obter mais informações sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="2893f-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="2893f-136">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="2893f-136">Virtual Network</span></span>
<span data-ttu-id="2893f-137">Se uma máquina virtual requer uma rede interna, como Olá capacidade toocommunicate com outras máquinas virtuais e os recursos do Azure, uma rede Virtual do Azure é necessária.</span><span class="sxs-lookup"><span data-stu-id="2893f-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="2893f-138">Uma rede virtual não faz a máquina virtual de saudação acessível pela internet de hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="2893f-139">A conectividade pública exige um endereço IP público, que é detalhado posteriormente nesta série.</span><span class="sxs-lookup"><span data-stu-id="2893f-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="2893f-140">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [rede Virtual e sub-redes](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="2893f-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

<span data-ttu-id="2893f-141">De Olá portal do Azure, rede virtual Olá parece Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="2893f-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="2893f-142">Observe que todas as máquinas virtuais implantadas com o modelo de saudação rede virtual toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="2893f-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Rede Virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="2893f-144">Interface de rede</span><span class="sxs-lookup"><span data-stu-id="2893f-144">Network Interface</span></span>
 <span data-ttu-id="2893f-145">Uma interface de rede se conecta a uma rede virtual da máquina virtual tooa, mais especificamente sub-rede tooa que foi definido na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="2893f-146">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [Interface de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="2893f-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="2893f-147">Cada recurso de máquina virtual inclui um perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="2893f-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="2893f-148">interface de rede Hello está associado a máquina virtual de saudação neste perfil.</span><span class="sxs-lookup"><span data-stu-id="2893f-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="2893f-149">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [perfil de rede da máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="2893f-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="2893f-150">De Olá portal do Azure, interface de rede Olá parece Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="2893f-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="2893f-151">endereço IP interno de saudação e associação de máquina virtual Olá podem ser vistos no recurso de interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="2893f-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interface de rede](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="2893f-153">Para obter mais informações sobre Redes Virtuais do Azure, consulte [Documentação da Rede Virtual do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="2893f-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="2893f-154">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="2893f-154">Azure SQL Database</span></span>
<span data-ttu-id="2893f-155">Além disso, tooa máquina de virtual que hospeda o site do repositório de música hello, um banco de dados do SQL Azure é o banco de dados de repositório de música de Olá toohost implantado.</span><span class="sxs-lookup"><span data-stu-id="2893f-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="2893f-156">vantagem de saudação do uso de banco de dados do SQL Azure aqui é que um segundo conjunto de máquinas virtuais não é necessário e escala e disponibilidade baseia-se no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="2893f-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="2893f-157">Um banco de dados do SQL Azure pode ser adicionado usando Olá Visual Studio adicionar novos recursos do assistente, ou inserindo um JSON válido em um modelo.</span><span class="sxs-lookup"><span data-stu-id="2893f-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="2893f-158">saudação de recurso do SQL Server inclui um nome de usuário e senha que recebeu direitos administrativos na instância do SQL hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="2893f-159">Além disso, um recurso de firewall do SQL é adicionado.</span><span class="sxs-lookup"><span data-stu-id="2893f-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="2893f-160">Por padrão, os aplicativos hospedados no Azure são capaz de tooconnect com a instância do SQL hello.</span><span class="sxs-lookup"><span data-stu-id="2893f-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="2893f-161">aplicativo externo tooallow tal um SQL Server Management studio tooconnect toohello instância do SQL, firewall Olá precisa toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="2893f-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="2893f-162">Para bem Olá de demonstração do repositório de música Olá, a configuração padrão de saudação é suficiente.</span><span class="sxs-lookup"><span data-stu-id="2893f-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="2893f-163">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="2893f-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="2893f-164">Uma exibição de saudação SQL server e banco de dados MusicStore como visto no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2893f-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="2893f-166">Para obter mais informações sobre como implantar o Banco de Dados SQL do Azure, consulte [Documentação do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="2893f-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="2893f-167">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="2893f-167">Next step</span></span>
<hr>

[<span data-ttu-id="2893f-168">Etapa 2 – Acesso e segurança em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2893f-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

