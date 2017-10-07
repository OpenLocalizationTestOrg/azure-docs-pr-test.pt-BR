---
title: "aaaCreate uma VM com várias NICs - modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: Criar uma VM com diversas NICs usando um modelo do Azure Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="a0d72-103">Criar uma VM com diversas NICs usando um modelo</span><span class="sxs-lookup"><span data-stu-id="a0d72-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a0d72-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a0d72-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a0d72-105">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a0d72-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="a0d72-106">Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0d72-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0d72-107">Prerequisites</span></span>
<span data-ttu-id="a0d72-108">Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="a0d72-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="a0d72-109">concluir a esses recursos, toocreate Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a0d72-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="a0d72-110">Navegue muito[página de modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="a0d72-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="a0d72-111">Na página de modelo hello, toohello à direita do **o grupo de recursos pai**, clique em **implantar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="a0d72-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="a0d72-112">Se necessário, altere os valores de parâmetro hello, siga as etapas de Olá no grupo de recursos de saudação do hello visualização do Azure toodeploy portal.</span><span class="sxs-lookup"><span data-stu-id="a0d72-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0d72-113">Verifique se os nomes da conta de armazenamento são exclusivos.</span><span class="sxs-lookup"><span data-stu-id="a0d72-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="a0d72-114">Você não pode ter nomes de conta de armazenamento duplicados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d72-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="a0d72-115">Entender o modelo de implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="a0d72-115">Understand hello deployment template</span></span>
<span data-ttu-id="a0d72-116">Antes de implantar o modelo de saudação fornecido com esta documentação, certifique-se de que entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="a0d72-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="a0d72-117">Olá, as etapas a seguir fornece uma boa visão geral do modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="a0d72-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="a0d72-118">Navegue muito[página de modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="a0d72-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="a0d72-119">Clique em **azuredeploy.json** tooopen arquivo de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0d72-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="a0d72-120">Saudação de aviso *osType* parâmetro listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="a0d72-121">Esse parâmetro é usado tooselect configurações relacionadas a quais toouse da imagem VM para o servidor de banco de dados hello, juntamente com vários sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="a0d72-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="a0d72-122">Role para baixo na lista de toohello de variáveis e verifique a definição Olá Olá **dbVMSetting** variáveis, listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="a0d72-123">Ele recebe um dos elementos da matriz Olá contidos em Olá **dbVMSettings** variável.</span><span class="sxs-lookup"><span data-stu-id="a0d72-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="a0d72-124">Se você estiver familiarizado com a terminologia de desenvolvimento de software, você pode exibir hello **dbVMSettings** variável como um dicionário ou uma tabela de hash.</span><span class="sxs-lookup"><span data-stu-id="a0d72-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="a0d72-125">Suponha que você decidir toodeploy VMs do Windows que executa o SQL Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="a0d72-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="a0d72-126">Olá, em seguida, o valor para **osType** seria *Windows*e hello **dbVMSetting** variável contém o elemento Olá listado abaixo, que representa o primeiro valor Olá Olá **dbVMSettings** variável.</span><span class="sxs-lookup"><span data-stu-id="a0d72-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="a0d72-127">Saudação de aviso **vmSize** contém valor Olá *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="a0d72-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="a0d72-128">Apenas determinados tamanhos VM permitem uso de saudação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="a0d72-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="a0d72-129">Você pode verificar quais tamanhos de VM oferecem suporte a várias NICs lendo Olá [tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigos.</span><span class="sxs-lookup"><span data-stu-id="a0d72-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="a0d72-130">Role para baixo demais**recursos** e observe Olá primeiro elemento.</span><span class="sxs-lookup"><span data-stu-id="a0d72-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="a0d72-131">Ele descreve uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0d72-131">It describes a storage account.</span></span> <span data-ttu-id="a0d72-132">Esta conta de armazenamento será usado toomaintain discos de dados de Olá usados por cada VM do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="a0d72-133">Nesse cenário, cada VM do banco de dados tem um disco do sistema operacional em armazenamento regular e dois discos de dados em armazenamento SSD (premium).</span><span class="sxs-lookup"><span data-stu-id="a0d72-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="a0d72-134">Role para baixo de toohello próximo recurso, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0d72-135">Esse recurso representa Olá que NIC usada para acesso de banco de dados em cada VM do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="a0d72-136">Aviso uso Olá Olá **cópia** função nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="a0d72-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="a0d72-137">Olá modelo permite que você toodeploy como muitas máquinas virtuais que você desejar, com base em hello **dbCount** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a0d72-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="a0d72-138">Portanto, você precisa toocreate Olá a mesma quantidade de NICs para acesso de banco de dados, uma para cada VM.</span><span class="sxs-lookup"><span data-stu-id="a0d72-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="a0d72-139">Role para baixo de toohello próximo recurso, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0d72-140">Esse recurso representa Olá que NIC usada para o gerenciamento em cada VM do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="a0d72-141">Mais uma vez, você precisará de uma dessas NICs para cada VM do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="a0d72-142">Saudação de aviso **networkSecurityGroup** elemento, vinculando um NSG que permite acesso tooRDP/SSH toothis NIC somente.</span><span class="sxs-lookup"><span data-stu-id="a0d72-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="a0d72-143">Role para baixo de toohello próximo recurso, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="a0d72-144">Esse recurso representará um toobe de conjunto de disponibilidade compartilhado por todas as VMs de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="a0d72-145">Dessa forma, você garante que sempre haja uma VM em Olá definido em execução durante a manutenção.</span><span class="sxs-lookup"><span data-stu-id="a0d72-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="a0d72-146">Role para baixo toohello próximo recurso.</span><span class="sxs-lookup"><span data-stu-id="a0d72-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="a0d72-147">Esse recurso representa o banco de dados de saudação VMs, como visto no hello primeiro algumas linhas listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="a0d72-148">Aviso uso Olá Olá **cópia** funcionar novamente, garantir que várias VMs são criadas com base em Olá **dbCount** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a0d72-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="a0d72-149">Também observe Olá **dependsOn** coleção.</span><span class="sxs-lookup"><span data-stu-id="a0d72-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="a0d72-150">Ela lista duas NICs, sendo necessário toobe criado antes de saudação que VM é implantada, juntamente com o conjunto de disponibilidade hello e conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="a0d72-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="a0d72-151">Role para baixo na Olá VM recurso toohello **networkProfile** elemento, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="a0d72-152">Observe que há duas NICs como referência para cada VM.</span><span class="sxs-lookup"><span data-stu-id="a0d72-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="a0d72-153">Quando você criar várias NICs de uma VM, você deve definir Olá **primário** propriedade de uma saudação NICs muito*true*, e Olá rest muito*false*.</span><span class="sxs-lookup"><span data-stu-id="a0d72-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="a0d72-154">Implantar o modelo do ARM hello usando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="a0d72-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0d72-155">Certifique-se de seguir Olá [pré-requisitos](#Pre-requisites) etapas antes de seguir as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="a0d72-156">Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="a0d72-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="a0d72-157">toodeploy usando esse modelo clique toodeploy, execute [este link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello à direita do **(consulte a documentação) de grupo de recursos de back-end** clique **implantar tooAzure**, substitua Olá valores de parâmetro padrão se necessário e siga as instruções de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0d72-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="a0d72-158">Olá figura a seguir mostra o conteúdo de saudação do novo grupo de recursos Olá, após a implantação.</span><span class="sxs-lookup"><span data-stu-id="a0d72-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Grupo de recursos Back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="a0d72-160">Implante o modelo de saudação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0d72-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="a0d72-161">modelo de saudação toodeploy baixados usando o PowerShell, instalar e configurar o PowerShell executando etapas Olá Olá [instalar e configurar o PowerShell](/powershell/azure/overview) artigo e, em seguida, concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0d72-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="a0d72-162">Executar Olá  **`New-AzureRmResourceGroup`**  toocreate cmdlet um grupo de recursos usando Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="a0d72-163">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="a0d72-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="a0d72-164">Implantar o modelo hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a0d72-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="a0d72-165">modelo de saudação toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="a0d72-166">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="a0d72-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a0d72-167">Executar Olá  **`azure config mode`**  modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a0d72-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a0d72-168">Olá esperado saída segue:</span><span class="sxs-lookup"><span data-stu-id="a0d72-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="a0d72-169">Olá abrir [arquivo de parâmetro](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selecione o seu conteúdo e salve-o arquivo tooa no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a0d72-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="a0d72-170">Neste exemplo, nós salvamos o arquivo de parâmetros Olá muito*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="a0d72-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="a0d72-171">Executar Olá  **`azure group deployment create`**  cmdlet toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima.</span><span class="sxs-lookup"><span data-stu-id="a0d72-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="a0d72-172">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="a0d72-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="a0d72-173">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="a0d72-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

