---
title: "Implantar recursos de computação do Windows com os modelos do Azure Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="ee041-103">Arquitetura de aplicativos com modelos do Azure Resource Manager para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="ee041-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="ee041-104">Ao desenvolver uma implantação do Azure Resource Manager, os requisitos de computação precisam ser mapeados para os serviços e recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee041-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="ee041-105">Se um aplicativo consistir em vários pontos de extremidade http, um banco de dados e um serviço de cache de dados, os recursos do Azure que hospedam cada desses componentes precisarão ser racionalizados.</span><span class="sxs-lookup"><span data-stu-id="ee041-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="ee041-106">Por exemplo, o aplicativo de Loja de Música de exemplo inclui um aplicativo Web hospedado em uma máquina virtual e um banco de dados SQL, hospedado no banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee041-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="ee041-107">Este documento fornece detalhes sobre como os recursos de computação da Loja de Música são configurados no modelo do Azure Resource Manager de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee041-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="ee041-108">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="ee041-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="ee041-109">Para obter a melhor experiência, pré-implante uma instância da solução em sua assinatura do Azure e trabalhe com o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee041-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="ee041-110">O modelo completo pode ser encontrado aqui – [Implantação de Loja de Música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="ee041-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="ee041-111">Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="ee041-111">Virtual Machine</span></span>
<span data-ttu-id="ee041-112">O aplicativo de Loja de Música inclui um aplicativo Web em que os clientes podem procurar e comprar músicas.</span><span class="sxs-lookup"><span data-stu-id="ee041-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="ee041-113">Embora haja vários serviços do Azure que podem hospedar aplicativos Web, para este exemplo, uma máquina virtual é usada.</span><span class="sxs-lookup"><span data-stu-id="ee041-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="ee041-114">Usando o modelo de Loja de Música de exemplo, uma máquina virtual é implantada, um servidor Web é instalado e o site da Loja de Música é instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="ee041-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="ee041-115">Neste artigo, apenas a implantação de máquina virtual é detalhada.</span><span class="sxs-lookup"><span data-stu-id="ee041-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="ee041-116">A configuração do servidor Web e do aplicativo é detalhada em um artigo posterior.</span><span class="sxs-lookup"><span data-stu-id="ee041-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="ee041-117">Uma máquina virtual pode ser adicionada a um modelo usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="ee041-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="ee041-118">Ao implantar uma máquina virtual, também são necessários vários recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ee041-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="ee041-119">Se usar o Visual Studio para criar o modelo, esses recursos serão criados para você.</span><span class="sxs-lookup"><span data-stu-id="ee041-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="ee041-120">Se construir manualmente o modelo, esses recursos precisarão ser inseridos e configurados.</span><span class="sxs-lookup"><span data-stu-id="ee041-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="ee041-121">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [JSON de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="ee041-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

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

<span data-ttu-id="ee041-122">Uma vez implantado, as propriedades da máquina virtual podem ser vistas no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee041-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Máquina Virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="ee041-124">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ee041-124">Storage Account</span></span>
<span data-ttu-id="ee041-125">Contas de armazenamento têm muitos recursos e opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ee041-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="ee041-126">Para o contexto de máquinas virtuais do Azure, uma conta de armazenamento mantém os discos rígidos virtuais da máquina virtual e discos de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="ee041-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="ee041-127">O exemplo de Loja de Música inclui uma conta de armazenamento para manter o disco rígido virtual de cada máquina virtual na implantação.</span><span class="sxs-lookup"><span data-stu-id="ee041-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="ee041-128">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="ee041-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

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

<span data-ttu-id="ee041-129">Uma conta de armazenamento é associada uma máquina virtual dentro da declaração de modelo do Resource Manager da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ee041-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="ee041-130">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de máquina virtual e conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="ee041-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

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

<span data-ttu-id="ee041-131">Após a implantação, a conta de armazenamento pode ser exibida no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee041-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Conta de armazenamento](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="ee041-133">Clique no contêiner de blob da conta de armazenamento; o arquivo de driver de disco rígido virtual para cada máquina virtual implantada com o modelo pode ser visto.</span><span class="sxs-lookup"><span data-stu-id="ee041-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Discos rígidos virtuais](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="ee041-135">Para obter mais informações sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="ee041-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="ee041-136">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="ee041-136">Virtual Network</span></span>
<span data-ttu-id="ee041-137">Se uma máquina virtual requer uma rede interna, como a capacidade de se comunicar com outras máquinas virtuais e recursos do Azure, uma Rede Virtual do Azure é necessária.</span><span class="sxs-lookup"><span data-stu-id="ee041-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="ee041-138">Uma rede virtual não torna a máquina virtual acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="ee041-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="ee041-139">A conectividade pública exige um endereço IP público, que é detalhado posteriormente nesta série.</span><span class="sxs-lookup"><span data-stu-id="ee041-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="ee041-140">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Rede virtual e sub-redes](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="ee041-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

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

<span data-ttu-id="ee041-141">No portal do Azure, a rede virtual é semelhante à imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee041-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="ee041-142">Observe que todas as máquinas virtuais implantadas com o modelo estão conectadas à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ee041-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Rede Virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="ee041-144">Interface de rede</span><span class="sxs-lookup"><span data-stu-id="ee041-144">Network Interface</span></span>
 <span data-ttu-id="ee041-145">Um adaptador de rede conecta uma máquina virtual a uma rede virtual, mais especificamente a uma sub-rede que foi definida na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ee041-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="ee041-146">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Adaptador de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="ee041-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

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

<span data-ttu-id="ee041-147">Cada recurso de máquina virtual inclui um perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="ee041-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="ee041-148">O adaptador de rede está associado a uma máquina virtual neste perfil.</span><span class="sxs-lookup"><span data-stu-id="ee041-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="ee041-149">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Perfil de rede da máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="ee041-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="ee041-150">No portal do Azure, o adaptador de rede é semelhante à imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee041-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="ee041-151">O endereço IP interno e a associação da máquina virtual podem ser vistos no recurso de adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="ee041-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Interface de rede](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="ee041-153">Para obter mais informações sobre Redes Virtuais do Azure, consulte [Documentação da Rede Virtual do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="ee041-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="ee041-154">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee041-154">Azure SQL Database</span></span>
<span data-ttu-id="ee041-155">Além de uma máquina virtual que hospeda o site de Loja de Música, um banco de dados SQL do Azure é implantado para hospedar o banco de dados da Loja de Música.</span><span class="sxs-lookup"><span data-stu-id="ee041-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="ee041-156">A vantagem de usar o banco de dados SQL do Azure aqui é que um segundo conjunto de máquinas virtuais não é necessário, e a escala e a disponibilidade baseiam-se no serviço.</span><span class="sxs-lookup"><span data-stu-id="ee041-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="ee041-157">Um banco de dados SQL do Azure pode ser adicionado usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo.</span><span class="sxs-lookup"><span data-stu-id="ee041-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="ee041-158">O recurso SQL Server inclui um nome de usuário e uma senha que tenha direitos administrativos na instância do SQL.</span><span class="sxs-lookup"><span data-stu-id="ee041-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="ee041-159">Além disso, um recurso de firewall do SQL é adicionado.</span><span class="sxs-lookup"><span data-stu-id="ee041-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="ee041-160">Por padrão, os aplicativos hospedados no Azure são capazes de se conectar com a instância do SQL.</span><span class="sxs-lookup"><span data-stu-id="ee041-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="ee041-161">Para permitir que o aplicativo externo como um SQL Server Management Studio se conecte à instância do SQL, o firewall precisa ser configurado.</span><span class="sxs-lookup"><span data-stu-id="ee041-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="ee041-162">Para fins de demonstração da Loja de Música, a configuração padrão é suficiente.</span><span class="sxs-lookup"><span data-stu-id="ee041-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="ee041-163">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Banco de dados SQL do Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="ee041-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

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

<span data-ttu-id="ee041-164">Um modo de exibição do SQL Server e do banco de dados MusicStore como visto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee041-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="ee041-166">Para obter mais informações sobre como implantar o Banco de Dados SQL do Azure, consulte [Documentação do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ee041-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="ee041-167">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="ee041-167">Next step</span></span>
<hr>

[<span data-ttu-id="ee041-168">Etapa 2 – Acesso e segurança em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee041-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

