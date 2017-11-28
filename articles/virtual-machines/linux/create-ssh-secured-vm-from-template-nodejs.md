---
title: aaaCreate uma VM do Linux usando um modelo do Azure com o Azure CLI 1.0 | Microsoft Docs
description: Crie uma VM do Linux no Azure usando hello 1.0 da CLI do Azure e um modelo do Gerenciador de recursos do Azure.
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
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="e6d1b-103">Como toocreate uma VM do Linux usando Olá CLI do Azure 1.0 um modelo do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d1b-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="e6d1b-104">Este artigo mostra como tooquickly implantar uma máquina Virtual do Linux usando hello 1.0 da CLI do Azure e um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="e6d1b-105">artigo Olá requer:</span><span class="sxs-lookup"><span data-stu-id="e6d1b-105">hello article requires:</span></span>

* <span data-ttu-id="e6d1b-106">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="e6d1b-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="e6d1b-107">Olá [Azure CLI 1.0](../../cli-install-nodejs.md) conectado `azure login`.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="e6d1b-108">Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="e6d1b-109">Você pode implantar rapidamente um modelo de VM do Linux usando Olá [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e6d1b-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e6d1b-110">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="e6d1b-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e6d1b-111">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6d1b-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e6d1b-112">[1.0 de CLI do Azure](#quick-command-summary) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="e6d1b-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e6d1b-113">[2.0 do CLI do Azure](create-ssh-secured-vm-from-template.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="e6d1b-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="e6d1b-114">Resumo rápido do comando</span><span class="sxs-lookup"><span data-stu-id="e6d1b-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e6d1b-115">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="e6d1b-115">Detailed Walkthrough</span></span>
<span data-ttu-id="e6d1b-116">Modelos permitem toocreate VMs no Azure com as configurações que você deseja toocustomize durante a inicialização de hello, configurações, como nomes de usuário e nomes de host.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="e6d1b-117">Neste artigo, estamos iniciando um modelo do Azure utilizando uma VM do Ubuntu junto com um grupo de segurança de rede (NSG) com a porta 22 aberta para o SSH.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="e6d1b-118">Os modelos do Azure Resource Manager são arquivos JSON que podem ser usados para tarefas únicas simples, como iniciar uma VM Ubuntu, como feito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="e6d1b-119">Modelos do Azure também podem ser usado tooconstruct as configurações do Azure complexas de ambientes inteiros como uma pilha de implantação de produção, desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="e6d1b-120">Criar hello VM do Linux</span><span class="sxs-lookup"><span data-stu-id="e6d1b-120">Create hello Linux VM</span></span>
<span data-ttu-id="e6d1b-121">Olá mostra exemplo de código a seguir como toocall `azure group create` toocreate um recurso de grupo e implantar uma VM do Linux protegidos SSH no hello mesmo tempo usando [este modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e6d1b-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="e6d1b-122">Lembre-se de que o exemplo é necessário toouse nomes de ambiente tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="e6d1b-123">Este exemplo usa *myResourceGroup* como nome do grupo de recursos hello e *myVM* como nome da VM hello.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="e6d1b-124">saída de Hello deve ter aparência Olá bloco de saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6d1b-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="e6d1b-125">Esse exemplo implantado uma VM usando Olá `--template-uri` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="e6d1b-126">Você também pode baixar ou criar um modelo localmente e passar o modelo de saudação usando Olá `--template-file` parâmetro com um arquivo de modelo do caminho toohello como um argumento.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="e6d1b-127">Olá CLI do Azure solicita parâmetros Olá exigidos pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6d1b-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6d1b-128">Next steps</span></span>
<span data-ttu-id="e6d1b-129">Saudação de pesquisa [Galeria de modelos](https://azure.microsoft.com/documentation/templates/) toodiscover que toodeploy de estruturas de aplicativo Avançar.</span><span class="sxs-lookup"><span data-stu-id="e6d1b-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

