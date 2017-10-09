---
title: "aaaAzure início rápido - criar VM CLI | Microsoft Docs"
description: "Aprenda rapidamente máquinas virtuais de toocreate com hello CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="ce781-103">Criar uma máquina virtual Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ce781-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="ce781-104">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="ce781-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="ce781-105">Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual com o servidor do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ce781-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="ce781-106">Depois que o servidor de saudação for implantado, é criada uma conexão SSH e um servidor de Web NGINX está instalado.</span><span class="sxs-lookup"><span data-stu-id="ce781-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="ce781-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ce781-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ce781-108">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ce781-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ce781-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce781-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ce781-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ce781-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="ce781-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ce781-111">Create a resource group</span></span>

<span data-ttu-id="ce781-112">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ce781-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ce781-113">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ce781-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ce781-114">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="ce781-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="ce781-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ce781-115">Create virtual machine</span></span>

<span data-ttu-id="ce781-116">Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ce781-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="ce781-117">Olá, exemplo a seguir cria uma VM denominada *myVM* e cria as chaves de SSH se eles ainda não existir em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="ce781-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="ce781-118">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="ce781-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="ce781-119">Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce781-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="ce781-120">Anote Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="ce781-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="ce781-121">Esse endereço é usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ce781-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="ce781-122">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="ce781-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="ce781-123">Por padrão, somente as conexões de SSH são permitidas em máquinas virtuais Linux implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="ce781-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="ce781-124">Se essa VM for toobe um servidor Web, você precisa tooopen porta 80 de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="ce781-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="ce781-125">Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.</span><span class="sxs-lookup"><span data-stu-id="ce781-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="ce781-126">SSH em sua VM</span><span class="sxs-lookup"><span data-stu-id="ce781-126">SSH into your VM</span></span>

<span data-ttu-id="ce781-127">A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce781-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="ce781-128">Certifique-se de que tooreplace  *<publicIpAddress>*  com hello corrija o endereço IP público de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ce781-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="ce781-129">Em nosso exemplo acima, nosso endereço IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="ce781-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="ce781-130">Instalar o NGINX</span><span class="sxs-lookup"><span data-stu-id="ce781-130">Install NGINX</span></span>

<span data-ttu-id="ce781-131">Use a seguir de saudação bash origens do pacote do script tooupdate e instala pacote NGINX mais recente de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce781-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="ce781-132">Página de boas-vindas do modo de exibição Olá NGINX</span><span class="sxs-lookup"><span data-stu-id="ce781-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="ce781-133">Com NGINX instalado e a porta 80 agora aberta na sua VM do hello Internet - você pode usar um navegador da web da sua página Bem-vindo escolha tooview saudação padrão NGINX.</span><span class="sxs-lookup"><span data-stu-id="ce781-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="ce781-134">Ser Olá-se de toouse *publicIpAddress* documentado acima da página do toovisit saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="ce781-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="ce781-136">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="ce781-136">Clean up resources</span></span>

<span data-ttu-id="ce781-137">Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.</span><span class="sxs-lookup"><span data-stu-id="ce781-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ce781-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce781-138">Next steps</span></span>

<span data-ttu-id="ce781-139">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="ce781-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="ce781-140">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="ce781-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="ce781-141">Tutoriais de máquina virtual do Linux Azure</span><span class="sxs-lookup"><span data-stu-id="ce781-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
