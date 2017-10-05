---
title: Criar uma VM do Linux no Azure usando um modelo | Microsoft Docs
description: Como usar a CLI 2.0 do Azure para criar uma VM do Linux de um modelo do Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="a5453-103">Como criar uma máquina virtual do Linux com os modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a5453-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="a5453-104">Este artigo mostra como implantar rapidamente uma VM (máquina virtual) do Linux com a CLI 2.0 do Azure e modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a5453-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="a5453-105">Você também pode executar essas etapas com a [CLI do Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a5453-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="a5453-106">Visão geral de modelos</span><span class="sxs-lookup"><span data-stu-id="a5453-106">Templates overview</span></span>
<span data-ttu-id="a5453-107">Os modelos do Azure Resource Manager são arquivos JSON que definem a infraestrutura e a configuração de sua solução do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5453-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="a5453-108">Usando um modelo, você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="a5453-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="a5453-109">Para saber mais sobre o formato do modelo e como construí-o, veja [Criar seu primeiro modelo do Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a5453-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="a5453-110">Para exibir a sintaxe JSON para os tipos de recursos, consulte [Definir recursos nos modelos do Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="a5453-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="a5453-111">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a5453-111">Create resource group</span></span>
<span data-ttu-id="a5453-112">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a5453-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="a5453-113">Você deve criar um grupo de recursos antes de criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a5453-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="a5453-114">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroupVM* na região *eastus*:</span><span class="sxs-lookup"><span data-stu-id="a5453-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="a5453-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a5453-115">Create virtual machine</span></span>
<span data-ttu-id="a5453-116">O exemplo a seguir cria uma VM [neste modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) com [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="a5453-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="a5453-117">Forneça o valor de sua própria chave pública SSH, como o conteúdo de *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="a5453-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="a5453-118">Se você precisar criar um par de chaves SSH, confira [Como criar um par de chaves SSH para VMs Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="a5453-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="a5453-119">Neste exemplo, você especificou um modelo armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5453-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="a5453-120">Também é possível baixar ou criar um modelo e especificar o caminho local com o mesmo parâmetro `--template-file`.</span><span class="sxs-lookup"><span data-stu-id="a5453-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="a5453-121">Para enviar por SSH à sua VM, obtenha o endereço IP público com [az network public-ip show](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="a5453-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="a5453-122">Depois, você pode enviar por SSH para sua VM, como de costume:</span><span class="sxs-lookup"><span data-stu-id="a5453-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="a5453-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5453-123">Next steps</span></span>
<span data-ttu-id="a5453-124">Neste exemplo, você criou uma VM básica do Linux.</span><span class="sxs-lookup"><span data-stu-id="a5453-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="a5453-125">Para obter mais modelos do Resource Manager que incluem estruturas de aplicativo ou criam ambientes mais complexos, procure a [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="a5453-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>