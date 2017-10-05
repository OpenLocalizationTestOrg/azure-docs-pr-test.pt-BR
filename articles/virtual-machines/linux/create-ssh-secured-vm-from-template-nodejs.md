---
title: Criar uma VM do Linux usando um modelo do Azure com a CLI 1.0 do Azure | Microsoft Docs
description: Crie uma VM do Linux no Azure usando a CLI 1.0 do Azure e um modelo do Azure Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="6d29f-103">Como criar uma VM do Linux usando a CLI 1.0 do Azure e um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d29f-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="6d29f-104">Este artigo mostra como implantar rapidamente uma máquina virtual do Linux usando a CLI 1.0 do Azure e um Modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6d29f-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="6d29f-105">O artigo exige:</span><span class="sxs-lookup"><span data-stu-id="6d29f-105">The article requires:</span></span>

* <span data-ttu-id="6d29f-106">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="6d29f-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="6d29f-107">a [CLI 1.0 do Azure](../../cli-install-nodejs.md) conectada com o `azure login`.</span><span class="sxs-lookup"><span data-stu-id="6d29f-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="6d29f-108">A CLI do Azure *deve estar no* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="6d29f-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="6d29f-109">Você também pode implantar rapidamente um modelo de VM do Linux usando o [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d29f-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6d29f-110">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="6d29f-110">CLI versions to complete the task</span></span>
<span data-ttu-id="6d29f-111">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="6d29f-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6d29f-112">[CLI 1.0 do Azure](#quick-command-summary) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="6d29f-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6d29f-113">[CLI 2.0 do Azure](create-ssh-secured-vm-from-template.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="6d29f-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="6d29f-114">Resumo rápido do comando</span><span class="sxs-lookup"><span data-stu-id="6d29f-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="6d29f-115">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="6d29f-115">Detailed Walkthrough</span></span>
<span data-ttu-id="6d29f-116">Os modelos permitem criar VMs no Azure com as configurações que você deseja personalizar durante a inicialização, como nomes de usuário e nomes de host.</span><span class="sxs-lookup"><span data-stu-id="6d29f-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="6d29f-117">Neste artigo, estamos iniciando um modelo do Azure utilizando uma VM do Ubuntu junto com um grupo de segurança de rede (NSG) com a porta 22 aberta para o SSH.</span><span class="sxs-lookup"><span data-stu-id="6d29f-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="6d29f-118">Os modelos do Azure Resource Manager são arquivos JSON que podem ser usados para tarefas únicas simples, como iniciar uma VM Ubuntu, como feito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6d29f-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="6d29f-119">Os Modelos do Azure também podem ser usados para construir configurações complexas do Azure de ambientes inteiros como uma pilha de implantação de teste, desenvolvimento ou produção.</span><span class="sxs-lookup"><span data-stu-id="6d29f-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="6d29f-120">Criar a VM Linux</span><span class="sxs-lookup"><span data-stu-id="6d29f-120">Create the Linux VM</span></span>
<span data-ttu-id="6d29f-121">O exemplo de código a seguir mostra como chamar o `azure group create` para criar um grupo de recursos e implantar uma VM do Linux protegida por SSH ao mesmo tempo usando [este modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6d29f-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="6d29f-122">Lembre-se de que, em seu exemplo, você precisará usar nomes que sejam exclusivos para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="6d29f-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="6d29f-123">Esse exemplo usa *myResourceGroup* como o nome do grupo de recursos e *myVM* como o nome da VM.</span><span class="sxs-lookup"><span data-stu-id="6d29f-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="6d29f-124">A saída deve ser semelhante ao bloco de saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d29f-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="6d29f-125">Este exemplo implantou uma VM usando o parâmetro `--template-uri` .</span><span class="sxs-lookup"><span data-stu-id="6d29f-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="6d29f-126">Você também pode baixar ou criar um modelo localmente e passar o modelo usando o parâmetro `--template-file` com um caminho para o arquivo de modelo como um argumento.</span><span class="sxs-lookup"><span data-stu-id="6d29f-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="6d29f-127">A CLI do Azure solicita os parâmetros necessários ao modelo.</span><span class="sxs-lookup"><span data-stu-id="6d29f-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d29f-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d29f-128">Next steps</span></span>
<span data-ttu-id="6d29f-129">Pesquise a [galeria de modelos](https://azure.microsoft.com/documentation/templates/) para descobrir quais estruturas de aplicativos implantar em seguida.</span><span class="sxs-lookup"><span data-stu-id="6d29f-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

