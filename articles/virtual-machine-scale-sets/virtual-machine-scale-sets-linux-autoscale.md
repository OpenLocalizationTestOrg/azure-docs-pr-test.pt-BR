---
title: "aaaAutoscale conjuntos de escala de máquinas virtuais do Linux | Microsoft Docs"
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
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="c172a-103">Dimensionar automaticamente computadores Linux em um conjunto de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c172a-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="c172a-104">Conjuntos de escala de máquinas virtuais tornam mais fácil para você toodeploy e gerenciam máquinas virtuais idênticas como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="c172a-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="c172a-105">Os conjuntos de dimensionamento fornecem uma camada de computação altamente escalonável e personalizável para aplicativos de hiperescala e suporte a imagens da plataforma Windows, imagens da plataforma Linux, imagens personalizadas e extensões.</span><span class="sxs-lookup"><span data-stu-id="c172a-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="c172a-106">mais, consulte toolearn [visão geral de conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="c172a-107">Este tutorial mostra como conjunto de toocreate uma escala de máquinas virtuais do Linux usando a versão mais recente de saudação do Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="c172a-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="c172a-108">tutorial Olá também mostra como definir tooautomatically máquinas de saudação de escala em hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="c172a-109">Você cria escala Olá definir e configurar o dimensionamento criando um modelo do Gerenciador de recursos do Azure e implantá-la usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c172a-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="c172a-110">Para obter mais informações sobre modelos, confira [Criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="c172a-111">toolearn mais sobre o dimensionamento automático de conjuntos de escala, consulte [o dimensionamento automático e conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="c172a-112">Neste tutorial, você implanta a seguir Olá recursos e extensões:</span><span class="sxs-lookup"><span data-stu-id="c172a-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="c172a-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="c172a-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="c172a-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="c172a-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="c172a-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="c172a-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="c172a-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="c172a-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="c172a-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="c172a-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="c172a-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="c172a-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="c172a-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="c172a-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="c172a-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="c172a-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="c172a-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="c172a-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="c172a-122">Para obter mais informações sobre os recursos do Resource Manager, consulte [Azure Resource Manager versus implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="c172a-123">Antes de começar as etapas de saudação neste tutorial, [instalar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="c172a-124">Etapa 1: Criar um grupo de recursos e uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c172a-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="c172a-125">**Entrar tooMicrosoft do Azure**</span><span class="sxs-lookup"><span data-stu-id="c172a-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="c172a-126">Na sua interface de linha de comando (Bash, prompt comando Terminal,) alternar modo do Gerenciador de tooResource e, em seguida, [fazer logon com sua id de trabalho ou da escola](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Siga os prompts de saudação para uma experiência de logon interativo tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c172a-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="c172a-127">Se você tem um trabalho ou de estudante ID e você não tiver habilitada de autenticação de dois fatores, use `azure login -u` com toolog de ID de saudação em sem uma sessão interativa.</span><span class="sxs-lookup"><span data-stu-id="c172a-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="c172a-128">Caso não tenha uma ID de trabalho ou de estudante, você poderá [criar uma ID de trabalho ou de estudante em sua conta pessoal da Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="c172a-129">**Criar um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="c172a-129">**Create a resource group**</span></span>  
<span data-ttu-id="c172a-130">Todos os recursos devem ser implantados tooa grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c172a-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="c172a-131">Para este tutorial, nomeie o grupo de recursos de saudação **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="c172a-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="c172a-132">**Implantar uma conta de armazenamento no novo grupo de recursos Olá**</span><span class="sxs-lookup"><span data-stu-id="c172a-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="c172a-133">Esta conta de armazenamento é onde o modelo de saudação é armazenado.</span><span class="sxs-lookup"><span data-stu-id="c172a-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="c172a-134">Crie uma conta de armazenamento denominada **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="c172a-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="c172a-135">Etapa 2: Criar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="c172a-135">Step 2: Create hello template</span></span>
<span data-ttu-id="c172a-136">Um modelo do Gerenciador de recursos do Azure possibilita que você toodeploy e gerenciar recursos do Azure juntos usando uma descrição de JSON dos recursos de saudação e parâmetros de implantação associados.</span><span class="sxs-lookup"><span data-stu-id="c172a-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="c172a-137">Em seu editor favorito, crie o arquivo de Olá VMSSTemplate.json e adicione a saudação inicial JSON toosupport Olá modelo de estrutura.</span><span class="sxs-lookup"><span data-stu-id="c172a-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="c172a-138">Parâmetros não são sempre obrigatórias, mas eles fornecem uma maneira tooinput valores quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="c172a-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="c172a-139">Adicione esses parâmetros no elemento de pai do hello parâmetros que você adicionou toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="c172a-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="c172a-140">Um nome para Olá outra máquina virtual que é usado tooaccess Olá máquinas no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="c172a-141">Um nome para a conta de armazenamento Olá onde o modelo de saudação é armazenado.</span><span class="sxs-lookup"><span data-stu-id="c172a-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="c172a-142">número de saudação de instâncias de máquinas virtuais tooinitially cria no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="c172a-143">Um nome e a senha da conta de administrador de saudação em máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="c172a-144">Um prefixo de nome para recursos de saudação que são criados a escala de saudação toosupport definido.</span><span class="sxs-lookup"><span data-stu-id="c172a-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="c172a-145">Variáveis podem ser usadas em valores de toospecify um modelo que podem ser alterados com frequência ou valores que precisam de toobe criadas de uma combinação de valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c172a-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="c172a-146">Adicione essas variáveis no elemento de pai do hello variáveis que você adicionou toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="c172a-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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

   * <span data-ttu-id="c172a-147">Nomes DNS que são usados por Olá interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="c172a-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="c172a-148">nomes de endereços IP Hello e prefixos de rede virtual hello e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="c172a-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="c172a-149">Olá nomes e identificadores de rede virtual do hello, balanceador de carga e interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="c172a-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="c172a-150">Nomes de conta de armazenamento para contas de saudação associadas máquinas Olá no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="c172a-151">Configurações de extensão de diagnóstico está instalado em máquinas virtuais de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="c172a-152">Para obter mais informações sobre Olá extensão de diagnóstico, consulte [criar uma máquina Virtual do Windows com o monitoramento e diagnóstico usando o modelo do Gerenciador de recursos do Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c172a-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="c172a-153">Adicione o recurso de conta de armazenamento Olá sob o elemento de pai do hello recursos que você adicionou toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="c172a-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="c172a-154">Este modelo usa uma saudação de toocreate loop recomendada cinco contas de armazenamento onde os discos do sistema operacional hello e dados de diagnóstico são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c172a-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="c172a-155">Esse conjunto de contas pode dar suporte a backup de máquinas virtuais de too100 em um conjunto de escala, que é o máximo de saudação atual.</span><span class="sxs-lookup"><span data-stu-id="c172a-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="c172a-156">Cada conta de armazenamento é nomeada com um designador que foi definido em variáveis de saudação combinados com sufixo Olá que você fornecer parâmetros Olá para modelo hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="c172a-157">Adicione recursos de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-157">Add hello virtual network resource.</span></span> <span data-ttu-id="c172a-158">Confira [Provedor de Recurso de Rede](../virtual-network/resource-groups-networking.md)para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c172a-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="c172a-159">Adicione Olá públicos recursos de endereço IP que são usados por Olá balanceador de carga e interface de rede.</span><span class="sxs-lookup"><span data-stu-id="c172a-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="c172a-160">Adicione o recurso de Balanceador de carga de saudação que é usado pelo conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="c172a-161">Para obter mais informações, confira [Suporte do Gerenciador de Recursos do Azure para Balanceador de Carga](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c172a-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="c172a-162">Adicione recurso Olá de interface de rede que é usado pela máquina virtual separada de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="c172a-163">Como máquinas em um conjunto de escala não são acessíveis por meio de um endereço IP público, uma outra máquina virtual é criada no hello mesmo virtual tooremotely máquinas de saudação de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="c172a-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="c172a-164">Adicione máquina virtual separada de saudação em Olá mesma rede como conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="c172a-165">Adicionar recursos do conjunto de escala de máquinas virtuais hello e especifique a extensão de diagnóstico de saudação que é instalado em todas as máquinas virtuais no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="c172a-166">Muitas das configurações de saudação do recurso são semelhantes com o recurso de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="c172a-167">Olá principais diferenças são elementos de capacidade de saudação que especifica o número de saudação de máquinas virtuais no conjunto de escala de saudação e upgradePolicy que especifica como as atualizações são feitas toovirtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="c172a-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="c172a-168">Olá conjunto de escala não é criado até que todas as contas de armazenamento Olá são criadas conforme especificado com o elemento de dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="c172a-169">Adicione Olá autoscaleSettings recurso que define como o conjunto de escala Olá ajusta com base no uso do processador nas máquinas Olá Olá conjunto.</span><span class="sxs-lookup"><span data-stu-id="c172a-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
    
    <span data-ttu-id="c172a-170">Para este tutorial, estes valores são importantes:</span><span class="sxs-lookup"><span data-stu-id="c172a-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="c172a-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="c172a-171">**metricName**</span></span>  
    <span data-ttu-id="c172a-172">Esse valor é Olá mesmo que o contador de desempenho de saudação que definimos na variável de wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="c172a-173">Usando essa variável, Olá extensão de diagnóstico coleta Olá **Processor\PercentProcessorTime** contador.</span><span class="sxs-lookup"><span data-stu-id="c172a-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="c172a-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="c172a-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="c172a-175">Esse valor é o identificador de recurso de saudação do conjunto de escala de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="c172a-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="c172a-176">**timeGrain**</span></span>  
    <span data-ttu-id="c172a-177">Esse valor é a granularidade de saudação de métricas de saudação que são coletadas.</span><span class="sxs-lookup"><span data-stu-id="c172a-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="c172a-178">Neste modelo, ele é definido tooone minuto.</span><span class="sxs-lookup"><span data-stu-id="c172a-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="c172a-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="c172a-179">**statistic**</span></span>  
    <span data-ttu-id="c172a-180">Esse valor determina como as métricas de saudação são combinados tooaccommodate Olá automática de ação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="c172a-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="c172a-181">Olá os valores possíveis são: média, Mín, máx.</span><span class="sxs-lookup"><span data-stu-id="c172a-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="c172a-182">Neste modelo, Olá médio total da CPU de máquinas virtuais de saudação é coletada.</span><span class="sxs-lookup"><span data-stu-id="c172a-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="c172a-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="c172a-183">**timeWindow**</span></span>  
    <span data-ttu-id="c172a-184">Esse valor é Olá intervalo de tempo no qual os dados de instância são coletados.</span><span class="sxs-lookup"><span data-stu-id="c172a-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="c172a-185">Deve estar entre 5 minutos e 12 horas.</span><span class="sxs-lookup"><span data-stu-id="c172a-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="c172a-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="c172a-186">**timeAggregation**</span></span>  
    <span data-ttu-id="c172a-187">o valor determina como os dados de saudação que são coletados devem ser combinados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="c172a-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="c172a-188">valor padrão de saudação é média.</span><span class="sxs-lookup"><span data-stu-id="c172a-188">hello default value is Average.</span></span> <span data-ttu-id="c172a-189">Olá os valores possíveis são: média, mínimo, máximo, último, Total, contagem.</span><span class="sxs-lookup"><span data-stu-id="c172a-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="c172a-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="c172a-190">**operator**</span></span>  
    <span data-ttu-id="c172a-191">Esse valor é o operador Olá toocompare usado Olá métrica dados e hello limite.</span><span class="sxs-lookup"><span data-stu-id="c172a-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="c172a-192">Olá os valores possíveis são: igual a, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="c172a-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="c172a-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="c172a-193">**threshold**</span></span>  
    <span data-ttu-id="c172a-194">Esse valor dispara a ação de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-194">This value triggers hello scale action.</span></span> <span data-ttu-id="c172a-195">Neste modelo, as máquinas são adicionadas toohello escala definida quando o uso médio de CPU Olá entre as máquinas no conjunto de saudação é acima de 50%.</span><span class="sxs-lookup"><span data-stu-id="c172a-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="c172a-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="c172a-196">**direction**</span></span>  
    <span data-ttu-id="c172a-197">Esse valor determina a ação de saudação que é obtida quando o valor de limite de saudação é obtida.</span><span class="sxs-lookup"><span data-stu-id="c172a-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="c172a-198">Olá possíveis valores são aumento ou diminuição.</span><span class="sxs-lookup"><span data-stu-id="c172a-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="c172a-199">Neste modelo, hello número de máquinas virtuais no conjunto de escala de saudação é aumentado se o limite de saudação é acima de 50% na janela de tempo de saudação definida.</span><span class="sxs-lookup"><span data-stu-id="c172a-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="c172a-200">**tipo**</span><span class="sxs-lookup"><span data-stu-id="c172a-200">**type**</span></span>  
    <span data-ttu-id="c172a-201">Esse valor é o tipo de saudação de ação que deve ocorrer e deve ser definido como tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="c172a-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="c172a-202">**valor**</span><span class="sxs-lookup"><span data-stu-id="c172a-202">**value**</span></span>  
    <span data-ttu-id="c172a-203">Esse valor é o número de saudação de máquinas virtuais que são adicionados ou removidos do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="c172a-204">Este valor deve ser 1 ou maior.</span><span class="sxs-lookup"><span data-stu-id="c172a-204">This value must be 1 or greater.</span></span> <span data-ttu-id="c172a-205">valor padrão de saudação é 1.</span><span class="sxs-lookup"><span data-stu-id="c172a-205">hello default value is 1.</span></span> <span data-ttu-id="c172a-206">Neste modelo, número de saudação de máquinas em escala Olá conjunto aumenta por 1 quando Olá limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="c172a-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="c172a-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="c172a-207">**cooldown**</span></span>  
    <span data-ttu-id="c172a-208">Esse valor é Olá toowait tempo desde a última ação de escala Olá antes da próxima ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="c172a-209">Esse valor deve estar entre um minuto e uma semana.</span><span class="sxs-lookup"><span data-stu-id="c172a-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="c172a-210">Salve o arquivo de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="c172a-211">Etapa 3: Carregar Olá modelo toostorage</span><span class="sxs-lookup"><span data-stu-id="c172a-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="c172a-212">modelo de saudação pode ser carregado desde que saiba o nome de saudação e a chave primária Olá da conta de armazenamento que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="c172a-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="c172a-213">Na sua interface de linha de comando (Bash, prompt comando Terminal,) execute estes comandos variáveis de ambiente Olá tooset necessário tooaccess Olá conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c172a-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="c172a-214">Você pode obter a chave de saudação clicando o ícone de chave Olá ao exibir o recurso de conta de armazenamento Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c172a-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="c172a-215">Ao usar um prompt de comando do Windows, digite **set** em vez de export.</span><span class="sxs-lookup"><span data-stu-id="c172a-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="c172a-216">Crie contêiner Olá para armazenar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="c172a-217">Carregar Olá modelo arquivo toohello novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="c172a-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="c172a-218">Etapa 4: Implantar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="c172a-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="c172a-219">Agora que você criou o modelo de hello, você pode iniciar a implantação recursos hello.</span><span class="sxs-lookup"><span data-stu-id="c172a-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="c172a-220">Use esse processo de saudação do comando toostart:</span><span class="sxs-lookup"><span data-stu-id="c172a-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="c172a-221">Quando você pressiona insira, são solicitadas tooprovide valores variáveis de Olá atribuída.</span><span class="sxs-lookup"><span data-stu-id="c172a-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="c172a-222">Forneça esses valores:</span><span class="sxs-lookup"><span data-stu-id="c172a-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="c172a-223">Ele deve levar cerca de 15 minutos para todos os toosuccessfully de recursos de saudação ser implantada.</span><span class="sxs-lookup"><span data-stu-id="c172a-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="c172a-224">Você também pode usar os recursos de saudação do portal Olá capacidade toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c172a-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="c172a-225">Use este link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="c172a-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="c172a-226">Etapa 5: monitorar recursos</span><span class="sxs-lookup"><span data-stu-id="c172a-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="c172a-227">Você pode obter informações sobre os conjuntos de dimensionamento de máquina virtual usando estes métodos:</span><span class="sxs-lookup"><span data-stu-id="c172a-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="c172a-228">Olá portal do Azure - no momento você pode obter uma quantidade limitada de informações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="c172a-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="c172a-229">Olá [Gerenciador de recursos do Azure](https://resources.azure.com/) -essa ferramenta é hello melhor para explorar o estado atual de saudação do seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="c172a-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="c172a-230">Siga este caminho e você deverá ver a exibição de instância de saudação de escala Olá definido que você criou:</span><span class="sxs-lookup"><span data-stu-id="c172a-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="c172a-231">CLI do Azure - Use esse comando tooget algumas informações:</span><span class="sxs-lookup"><span data-stu-id="c172a-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="c172a-232">Conecte máquina de virtual jumpbox toohello exatamente como faria com qualquer outro computador e, em seguida, você pode acessar remotamente máquinas virtuais Olá Olá escala conjunto toomonitor individuais processos.</span><span class="sxs-lookup"><span data-stu-id="c172a-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c172a-233">Uma API REST completa para obter informações sobre conjuntos de escalas podem ser encontradas nos [Conjuntos de Escalas de Máquina Virtual](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="c172a-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="c172a-234">Etapa 6: Remover recursos Olá</span><span class="sxs-lookup"><span data-stu-id="c172a-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="c172a-235">Como você é cobrado pelos recursos usados no Azure, sempre é um recurso de toodelete de práticas recomendadas que não é mais necessários.</span><span class="sxs-lookup"><span data-stu-id="c172a-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="c172a-236">Você não precisa toodelete cada recurso separadamente de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c172a-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="c172a-237">Você pode excluir o grupo de recursos de saudação e todos os seus recursos são excluídos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c172a-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="c172a-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c172a-238">Next steps</span></span>
* <span data-ttu-id="c172a-239">Encontre exemplos de recursos de monitoramento do Azure Monitor nos [Exemplos de início rápido da CLI de plataforma cruzada do Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c172a-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="c172a-240">Saiba mais sobre os recursos de notificação no [usar AutoEscala ações toosend email e webhook notificações de alerta no Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="c172a-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="c172a-241">Saiba como muito[notificações de alerta de e-mail e webhook toosend os logs de auditoria de uso no Monitor do Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="c172a-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="c172a-242">Check-out Olá [aplicativo de demonstração de dimensionamento automático no Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modelo configura uma saudação do Python/garrafa aplicativo tooexercise automático de escala a funcionalidade de máquina Virtual define de escala.</span><span class="sxs-lookup"><span data-stu-id="c172a-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

