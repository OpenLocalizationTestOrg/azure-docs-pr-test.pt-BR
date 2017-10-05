---
title: "Dimensionar automaticamente os conjuntos de dimensionamento de máquinas virtuais do Linux | Microsoft Docs"
description: "Configurar o dimensionamento automático para um conjunto de escala de máquina virtual do Linux usando a CLI do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="29fee-103">Dimensionar automaticamente computadores Linux em um conjunto de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="29fee-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="29fee-104">Os conjuntos de escala de máquina virtual facilitam a implantação e o gerenciamento de máquinas virtuais idênticas como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="29fee-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="29fee-105">Os conjuntos de dimensionamento fornecem uma camada de computação altamente escalonável e personalizável para aplicativos de hiperescala e suporte a imagens da plataforma Windows, imagens da plataforma Linux, imagens personalizadas e extensões.</span><span class="sxs-lookup"><span data-stu-id="29fee-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="29fee-106">Para saber mais, consulte [Visão geral de conjuntos de escala de máquina virtual](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="29fee-107">Este tutorial mostra como criar um conjunto de escala de máquinas virtuais Linux usando a versão mais recente do Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="29fee-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="29fee-108">O tutorial também mostra como dimensionar automaticamente as máquinas no conjunto.</span><span class="sxs-lookup"><span data-stu-id="29fee-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="29fee-109">Crie o conjunto de escala e defina o dimensionamento criando um modelo do Azure Resource Manager e implantando-o com o uso da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="29fee-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="29fee-110">Para obter mais informações sobre modelos, confira [Criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="29fee-111">Para saber mais sobre o dimensionamento automático de conjuntos de escala, consulte [Dimensionamento automático e conjuntos de escala de máquina virtual](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="29fee-112">Neste tutorial, você pode implantar os seguintes recursos e extensões:</span><span class="sxs-lookup"><span data-stu-id="29fee-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="29fee-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="29fee-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="29fee-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="29fee-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="29fee-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="29fee-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="29fee-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="29fee-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="29fee-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="29fee-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="29fee-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="29fee-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="29fee-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="29fee-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="29fee-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="29fee-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="29fee-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="29fee-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="29fee-122">Para obter mais informações sobre os recursos do Resource Manager, consulte [Azure Resource Manager versus implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="29fee-123">Antes de começar as etapas neste tutorial, [instale a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="29fee-124">Etapa 1: Criar um grupo de recursos e uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="29fee-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="29fee-125">**Entrar no Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="29fee-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="29fee-126">Em sua interface de linha de comando (Bash, Terminal, prompt de comando), mude para o modo do Resource Manager e [entre com sua ID corporativa ou de estudante](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Siga os prompts para ter uma experiência de logon interativo em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="29fee-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="29fee-127">Se tiver uma ID de trabalho ou de estudante e não tiver a autenticação de dois fatores habilitada, você poderá usar `azure login -u` com a ID de trabalho ou de estudante para fazer logon sem uma sessão interativa.</span><span class="sxs-lookup"><span data-stu-id="29fee-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="29fee-128">Caso não tenha uma ID de trabalho ou de estudante, você poderá [criar uma ID de trabalho ou de estudante em sua conta pessoal da Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="29fee-129">**Criar um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="29fee-129">**Create a resource group**</span></span>  
<span data-ttu-id="29fee-130">Todos os recursos devem estar implantados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="29fee-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="29fee-131">Para este tutorial, nomeie o grupo de recursos **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="29fee-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="29fee-132">**Implantar uma conta de armazenamento para o novo grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="29fee-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="29fee-133">É nessa conta de armazenamento que o modelo é armazenado.</span><span class="sxs-lookup"><span data-stu-id="29fee-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="29fee-134">Crie uma conta de armazenamento denominada **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="29fee-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="29fee-135">Etapa 2: Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="29fee-135">Step 2: Create the template</span></span>
<span data-ttu-id="29fee-136">Um modelo do Gerenciador de Recursos do Azure permite implantar e gerenciar recursos do Azure juntos usando uma descrição JSON dos recursos e parâmetros de implantação associados.</span><span class="sxs-lookup"><span data-stu-id="29fee-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="29fee-137">Em seu editor favorito, crie o arquivo VMSSTemplate.json e adicione a estrutura inicial do JSON para dar suporte ao modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="29fee-138">Parâmetros nem sempre são necessários, mas eles fornecem uma maneira de entrar valores quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="29fee-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="29fee-139">Adicione esses parâmetros sob o elemento pai de parâmetros que você adicionou ao modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="29fee-140">Um nome para a máquina virtual separada que é usado para acessar as máquinas no conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="29fee-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="29fee-141">Um nome para a conta de armazenamento onde o modelo é armazenado.</span><span class="sxs-lookup"><span data-stu-id="29fee-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="29fee-142">O número de instâncias de máquinas virtuais para criar inicialmente no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29fee-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="29fee-143">Um nome e senha da conta de administrador nas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="29fee-144">Um prefixo de nome para os recursos criados para dar suporte ao conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="29fee-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="29fee-145">As variáveis podem ser usadas em um modelo para especificar valores que podem ser alterados com frequência ou que precisam ser criados com base em uma combinação de valores de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="29fee-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="29fee-146">Adicione essas variáveis sob o elemento pai de variáveis que você adicionou ao modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-146">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="29fee-147">Nomes DNS que são usados pelas interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="29fee-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="29fee-148">Os nomes de endereços IP e prefixos para a rede virtual e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="29fee-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="29fee-149">Os nomes e os identificadores da rede virtual, balanceador de carga e interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="29fee-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="29fee-150">Nomes de conta de armazenamento para as contas associadas com as máquinas no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29fee-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="29fee-151">Configurações para a Extensão de diagnóstico que é instalada nas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="29fee-152">Para obter mais informações sobre a Extensão de diagnóstico, confira [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando o Modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29fee-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="29fee-153">Adicione o recurso de conta de armazenamento sob o elemento pai de recursos que você adicionou ao modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="29fee-154">Este modelo usa um loop para criar as cinco contas de armazenamento recomendadas nas quais os discos do sistema operacional e os dados de diagnóstico estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="29fee-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="29fee-155">Este conjunto de contas pode oferecer suporte a até 100 máquinas virtuais em um conjunto de dimensionamento, que é o máximo atual.</span><span class="sxs-lookup"><span data-stu-id="29fee-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="29fee-156">Cada conta de armazenamento é nomeada com um designador que foi definido nas variáveis combinadas com o sufixo que você fornecer nos parâmetros do modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. <span data-ttu-id="29fee-157">Adicione o recurso de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="29fee-157">Add the virtual network resource.</span></span> <span data-ttu-id="29fee-158">Confira [Provedor de Recurso de Rede](../virtual-network/resource-groups-networking.md)para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="29fee-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="29fee-159">Adicione os recursos de endereço IP público que são usados pelo balanceador de carga e interface de rede.</span><span class="sxs-lookup"><span data-stu-id="29fee-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="29fee-160">Adicione o recurso de balanceador de carga que é usado pelo conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29fee-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="29fee-161">Para obter mais informações, confira [Suporte do Gerenciador de Recursos do Azure para Balanceador de Carga](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="29fee-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="29fee-162">Adicione o recurso de interface de rede que é usado pela máquina virtual separada.</span><span class="sxs-lookup"><span data-stu-id="29fee-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="29fee-163">Como máquinas em um conjunto de escala não são diretamente acessíveis usando um endereço IP público, uma máquina virtual separada é criada na mesma rede virtual para acessar remotamente as máquinas.</span><span class="sxs-lookup"><span data-stu-id="29fee-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="29fee-164">Adicione a máquina virtual separada à mesma rede do conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="29fee-164">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="29fee-165">Adicione o recurso do conjunto de escala de máquina virtual e especifique a extensão de diagnóstico que é instalada em todas as máquinas virtuais no conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="29fee-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="29fee-166">Muitas das configurações desse recurso são semelhantes ao recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29fee-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="29fee-167">As principais diferenças são o elemento de capacidade que especifica o número de máquinas virtuais no conjunto de escala e upgradePolicy, que especifica como as atualizações são feitas em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="29fee-168">O conjunto de escala não será criado até que todas as contas de armazenamento sejam criadas conforme especificado no elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="29fee-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="29fee-169">Adicione o recurso autoscaleSettings, que define como o conjunto de escalas se ajusta com base no uso do processador nas máquinas no conjunto.</span><span class="sxs-lookup"><span data-stu-id="29fee-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    <span data-ttu-id="29fee-170">Para este tutorial, estes valores são importantes:</span><span class="sxs-lookup"><span data-stu-id="29fee-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="29fee-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="29fee-171">**metricName**</span></span>  
    <span data-ttu-id="29fee-172">Este valor é o mesmo que o contador de desempenho que definimos na variável wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="29fee-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="29fee-173">Usando essa variável, a Extensão de diagnóstico coleta o contador **Processor\PercentProcessorTime**.</span><span class="sxs-lookup"><span data-stu-id="29fee-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="29fee-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="29fee-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="29fee-175">Este valor é o identificador de recurso do conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="29fee-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="29fee-176">**timeGrain**</span></span>  
    <span data-ttu-id="29fee-177">Este valor é a granularidade das métricas que são coletadas.</span><span class="sxs-lookup"><span data-stu-id="29fee-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="29fee-178">Neste modelo, ele é definido como um minuto.</span><span class="sxs-lookup"><span data-stu-id="29fee-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="29fee-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="29fee-179">**statistic**</span></span>  
    <span data-ttu-id="29fee-180">Este valor determina como as métricas são combinadas para acomodar a ação de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29fee-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="29fee-181">Os valores possíveis são: Média, Mín, Máx.</span><span class="sxs-lookup"><span data-stu-id="29fee-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="29fee-182">Neste modelo, o uso médio de CPU total das máquinas virtuais é coletado.</span><span class="sxs-lookup"><span data-stu-id="29fee-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="29fee-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="29fee-183">**timeWindow**</span></span>  
    <span data-ttu-id="29fee-184">Este valor é o intervalo em que os dados da instância são coletados.</span><span class="sxs-lookup"><span data-stu-id="29fee-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="29fee-185">Deve estar entre 5 minutos e 12 horas.</span><span class="sxs-lookup"><span data-stu-id="29fee-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="29fee-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="29fee-186">**timeAggregation**</span></span>  
    <span data-ttu-id="29fee-187">Este valor determina como os dados coletados devem ser combinados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="29fee-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="29fee-188">O valor padrão é Average.</span><span class="sxs-lookup"><span data-stu-id="29fee-188">The default value is Average.</span></span> <span data-ttu-id="29fee-189">Os valores possíveis são: Média, Mínimo, Máximo, Último, Total, Contagem.</span><span class="sxs-lookup"><span data-stu-id="29fee-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="29fee-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="29fee-190">**operator**</span></span>  
    <span data-ttu-id="29fee-191">Este valor é o operador usado para comparar os dados de métrica e o limite.</span><span class="sxs-lookup"><span data-stu-id="29fee-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="29fee-192">Os valores possíveis são: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="29fee-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="29fee-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="29fee-193">**threshold**</span></span>  
    <span data-ttu-id="29fee-194">Este é o valor que dispara a ação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29fee-194">This value triggers the scale action.</span></span> <span data-ttu-id="29fee-195">Neste modelo, máquinas são adicionadas ao conjunto de dimensionamento quando o uso médio de CPU entre máquinas no conjunto é mais de 50%.</span><span class="sxs-lookup"><span data-stu-id="29fee-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="29fee-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="29fee-196">**direction**</span></span>  
    <span data-ttu-id="29fee-197">Este valor determina a ação que é executada quando o valor de limite for atingido.</span><span class="sxs-lookup"><span data-stu-id="29fee-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="29fee-198">Os valores possíveis são Aumentar ou Diminuir.</span><span class="sxs-lookup"><span data-stu-id="29fee-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="29fee-199">Neste modelo, o número de máquinas virtuais no conjunto de dimensionamento é aumentado se o limite for acima de 50% na janela de tempo definido.</span><span class="sxs-lookup"><span data-stu-id="29fee-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="29fee-200">**tipo**</span><span class="sxs-lookup"><span data-stu-id="29fee-200">**type**</span></span>  
    <span data-ttu-id="29fee-201">Este valor é o tipo de ação que deve ocorrer e deve ser definido como ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="29fee-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="29fee-202">**valor**</span><span class="sxs-lookup"><span data-stu-id="29fee-202">**value**</span></span>  
    <span data-ttu-id="29fee-203">Este valor é o número de máquinas virtuais que são adicionadas ou removidas do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29fee-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="29fee-204">Este valor deve ser 1 ou maior.</span><span class="sxs-lookup"><span data-stu-id="29fee-204">This value must be 1 or greater.</span></span> <span data-ttu-id="29fee-205">O valor padrão é 1.</span><span class="sxs-lookup"><span data-stu-id="29fee-205">The default value is 1.</span></span> <span data-ttu-id="29fee-206">Neste modelo, o número de máquinas no conjunto de dimensionamento aumenta em 1 quando o limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="29fee-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="29fee-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="29fee-207">**cooldown**</span></span>  
    <span data-ttu-id="29fee-208">Este valor é a quantidade de tempo de espera desde a última ação de dimensionamento antes que ocorra a próxima ação.</span><span class="sxs-lookup"><span data-stu-id="29fee-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="29fee-209">Esse valor deve estar entre um minuto e uma semana.</span><span class="sxs-lookup"><span data-stu-id="29fee-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="29fee-210">Salvar o arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="29fee-211">Etapa 3: Carregar o modelo para armazenamento</span><span class="sxs-lookup"><span data-stu-id="29fee-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="29fee-212">O modelo pode ser carregado, desde que você saiba o nome e a chave primária da conta de armazenamento que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="29fee-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="29fee-213">Em sua interface de linha de comando (Bash, Terminal, Prompt de comando), execute esses comandos para definir as variáveis de ambiente necessárias para acessar a conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="29fee-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="29fee-214">Você pode obter a chave clicando no ícone de chave ao exibir o recurso de conta de armazenamento no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29fee-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="29fee-215">Ao usar um prompt de comando do Windows, digite **set** em vez de export.</span><span class="sxs-lookup"><span data-stu-id="29fee-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="29fee-216">Crie o contêiner para armazenar o modelo.</span><span class="sxs-lookup"><span data-stu-id="29fee-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="29fee-217">Carregue o arquivo de modelo para o novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="29fee-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="29fee-218">Etapa 4: Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="29fee-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="29fee-219">Agora que você criou o modelo, pode começar a implantar os recursos.</span><span class="sxs-lookup"><span data-stu-id="29fee-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="29fee-220">Use este comando para iniciar o processo:</span><span class="sxs-lookup"><span data-stu-id="29fee-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="29fee-221">Quando você pressiona a tecla enter, é solicitado a fornecer valores para as variáveis que você atribuiu.</span><span class="sxs-lookup"><span data-stu-id="29fee-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="29fee-222">Forneça esses valores:</span><span class="sxs-lookup"><span data-stu-id="29fee-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="29fee-223">Deve levar cerca de 15 minutos para todos os recursos serem implantados com êxito.</span><span class="sxs-lookup"><span data-stu-id="29fee-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="29fee-224">Você também pode usar a capacidade do portal para implantar os recursos.</span><span class="sxs-lookup"><span data-stu-id="29fee-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="29fee-225">Use este link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="29fee-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="29fee-226">Etapa 5: monitorar recursos</span><span class="sxs-lookup"><span data-stu-id="29fee-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="29fee-227">Você pode obter informações sobre os conjuntos de dimensionamento de máquina virtual usando estes métodos:</span><span class="sxs-lookup"><span data-stu-id="29fee-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="29fee-228">O portal do Azure - Atualmente você pode obter uma quantidade limitada de informações usando o portal.</span><span class="sxs-lookup"><span data-stu-id="29fee-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="29fee-229">O [Gerenciador de Recursos do Azure](https://resources.azure.com/) – Esta é a melhor ferramenta para explorar o estado atual do conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="29fee-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="29fee-230">Siga este caminho e você deverá ver a exibição da instância do conjunto de dimensionamento que você criou:</span><span class="sxs-lookup"><span data-stu-id="29fee-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="29fee-231">CLI do Azure - use esse comando para obter algumas informações:</span><span class="sxs-lookup"><span data-stu-id="29fee-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="29fee-232">Conecte-se à máquina virtual de jumpbox exatamente como faria com qualquer outra máquina e, em seguida, você pode acessar remotamente as máquinas virtuais no conjunto de dimensionamento para monitorar os processos individuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="29fee-233">Uma API REST completa para obter informações sobre conjuntos de escalas podem ser encontradas nos [Conjuntos de Escalas de Máquina Virtual](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="29fee-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="29fee-234">Etapa 6: remover os recursos</span><span class="sxs-lookup"><span data-stu-id="29fee-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="29fee-235">Como você é cobrado pelos recursos usados no Azure, sempre é uma boa prática excluir os recursos que não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="29fee-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="29fee-236">Você não precisa excluir cada recurso separadamente de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="29fee-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="29fee-237">Você pode excluir o grupo de recursos e todos os seus recursos serão excluídos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="29fee-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="29fee-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29fee-238">Next steps</span></span>
* <span data-ttu-id="29fee-239">Encontre exemplos de recursos de monitoramento do Azure Monitor nos [Exemplos de início rápido da CLI de plataforma cruzada do Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="29fee-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="29fee-240">Saiba sobre os recursos de notificação em [Usar ações de dimensionamento automático para enviar notificações de alerta por email e webhook no Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="29fee-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="29fee-241">Saiba como [Usar logs de auditoria para enviar notificações de alerta por email e webhook no Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="29fee-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="29fee-242">Confira o modelo de [aplicativo de demonstração de dimensionamento automático no Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) que configura um aplicativo Python/Bottle para praticar a funcionalidade de dimensionamento automático de Conjuntos de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="29fee-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

