---
title: "Início Rápido do Azure – Criar CLI da VM | Microsoft Docs"
description: "Aprenda rapidamente criar máquinas virtuais com a CLI do Azure."
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
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="7076c-103">Criar uma máquina virtual Linux com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7076c-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="7076c-104">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="7076c-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="7076c-105">Este guia detalha o uso da CLI do Azure para implantar uma máquina virtual executando um servidor do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7076c-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="7076c-106">Depois que o servidor for implantado, uma conexão SSH é criada e um servidor Web NGINX é instalado.</span><span class="sxs-lookup"><span data-stu-id="7076c-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="7076c-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="7076c-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7076c-108">Se você optar por instalar e usar a CLI localmente, este guia de início rápido exigirá a execução da CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7076c-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7076c-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="7076c-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="7076c-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7076c-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="7076c-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7076c-111">Create a resource group</span></span>

<span data-ttu-id="7076c-112">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7076c-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7076c-113">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7076c-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7076c-114">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*.</span><span class="sxs-lookup"><span data-stu-id="7076c-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7076c-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7076c-115">Create virtual machine</span></span>

<span data-ttu-id="7076c-116">Crie uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7076c-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="7076c-117">O exemplo a seguir cria uma VM denominada *myVM* e cria chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="7076c-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="7076c-118">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="7076c-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="7076c-119">Quando a VM tiver sido criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7076c-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="7076c-120">Anote `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="7076c-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="7076c-121">Esse endereço é usado para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="7076c-121">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="7076c-122">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="7076c-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="7076c-123">Por padrão, somente as conexões de SSH são permitidas em máquinas virtuais Linux implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="7076c-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="7076c-124">Se essa VM for se transformar em um servidor Web, você precisará abrir a porta 80 na Internet.</span><span class="sxs-lookup"><span data-stu-id="7076c-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="7076c-125">Use o comando [az vm open-port](/cli/azure/vm#open-port) para abrir a porta desejada.</span><span class="sxs-lookup"><span data-stu-id="7076c-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="7076c-126">SSH em sua VM</span><span class="sxs-lookup"><span data-stu-id="7076c-126">SSH into your VM</span></span>

<span data-ttu-id="7076c-127">Use o seguinte comando para criar uma sessão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7076c-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="7076c-128">Substitua *<publicIpAddress>* pelo endereço IP público correto de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7076c-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="7076c-129">Em nosso exemplo acima, nosso endereço IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="7076c-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="7076c-130">Instalar o NGINX</span><span class="sxs-lookup"><span data-stu-id="7076c-130">Install NGINX</span></span>

<span data-ttu-id="7076c-131">Use o seguinte script bash para atualizar fontes de pacote e instalar o pacote mais recente do NGINX.</span><span class="sxs-lookup"><span data-stu-id="7076c-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="7076c-132">Exibir a página de boas-vindas do NGINX</span><span class="sxs-lookup"><span data-stu-id="7076c-132">View the NGINX welcome page</span></span>

<span data-ttu-id="7076c-133">Com o NGINX instalado e a porta 80 que agora está aberta na sua VM da Internet, você pode usar um navegador da Web de sua escolha para exibir a página de boas-vindas do NGINX padrão.</span><span class="sxs-lookup"><span data-stu-id="7076c-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="7076c-134">Certifique-se de usar o *publicIPAdress* que você documentou acima para visitar a página padrão.</span><span class="sxs-lookup"><span data-stu-id="7076c-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="7076c-136">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="7076c-136">Clean up resources</span></span>

<span data-ttu-id="7076c-137">Quando não for mais necessário, você pode usar o comando [az group delete](/cli/azure/group#delete) para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="7076c-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7076c-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7076c-138">Next steps</span></span>

<span data-ttu-id="7076c-139">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="7076c-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="7076c-140">Para saber mais sobre máquinas virtuais do Azure, continue o tutorial para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="7076c-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="7076c-141">Tutoriais de máquina virtual do Linux Azure</span><span class="sxs-lookup"><span data-stu-id="7076c-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
