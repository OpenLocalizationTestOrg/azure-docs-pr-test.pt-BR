---
title: aaaCreate uma VM do Linux no Azure de um modelo | Microsoft Docs
description: Como toouse hello Azure CLI 2.0 toocreate uma VM do Linux de um modelo do Gerenciador de recursos
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
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="cb2a9-103">Como toocreate uma máquina virtual de Linux com modelos do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="cb2a9-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="cb2a9-104">Este artigo mostra como tooquickly implantar uma máquina virtual do Linux (VM) com modelos do Gerenciador de recursos do Azure e hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="cb2a9-105">Você também pode executar essas etapas com hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="cb2a9-106">Visão geral de modelos</span><span class="sxs-lookup"><span data-stu-id="cb2a9-106">Templates overview</span></span>
<span data-ttu-id="cb2a9-107">Modelos do Gerenciador de recursos do Azure são arquivos JSON que definem a infraestrutura de saudação e a configuração de sua solução do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="cb2a9-108">Usando um modelo, você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="cb2a9-109">toolearn mais sobre o formato de saudação do modelo de saudação e de como você cria, consulte [criar seu primeiro modelo do Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="cb2a9-110">Olá tooview sintaxe JSON para tipos de recursos, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="cb2a9-111">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cb2a9-111">Create resource group</span></span>
<span data-ttu-id="cb2a9-112">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="cb2a9-113">Você deve criar um grupo de recursos antes de criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="cb2a9-114">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupVM* em Olá *eastus* região:</span><span class="sxs-lookup"><span data-stu-id="cb2a9-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="cb2a9-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cb2a9-115">Create virtual machine</span></span>
<span data-ttu-id="cb2a9-116">Olá, exemplo a seguir cria uma VM do [este modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) com [criar implantação de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="cb2a9-117">Fornecer o valor de saudação do sua própria chave pública SSH, como conteúdo de saudação do *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="cb2a9-118">Se você precisar toocreate um par de chave SSH, consulte [como toocreate e use um SSH par de chaves para VMs do Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="cb2a9-119">Neste exemplo, você especificou um modelo armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="cb2a9-120">Você também pode baixar ou criar um modelo e especificar o caminho de local de saudação com hello mesmo `--template-file` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="cb2a9-121">tooSSH tooyour VM, obter o endereço IP público de saudação com [az rede ip público exibir](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="cb2a9-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="cb2a9-122">Você pode, em seguida, SSH tooyour VM como normal:</span><span class="sxs-lookup"><span data-stu-id="cb2a9-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="cb2a9-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb2a9-123">Next steps</span></span>
<span data-ttu-id="cb2a9-124">Neste exemplo, você criou uma VM básica do Linux.</span><span class="sxs-lookup"><span data-stu-id="cb2a9-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="cb2a9-125">Mais modelos de Gerenciador de recursos que incluem estruturas de aplicativo ou criar um ambiente mais complexo, procurar Olá [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="cb2a9-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
