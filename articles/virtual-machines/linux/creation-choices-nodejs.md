---
title: Diferentes maneiras de criar uma VM Linux com a CLI do Azure 1.0 | Microsoft Docs
description: "Aprenda as diferentes maneiras de criar uma máquina virtual do Linux no Azure, incluindo links para ferramentas e tutoriais para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="305a1-103">Diferentes maneiras de criar uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="305a1-104">Você tem a flexibilidade no Azure de criar uma máquina virtual Linux (VM) usando ferramentas e fluxos de trabalho confortáveis para você.</span><span class="sxs-lookup"><span data-stu-id="305a1-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="305a1-105">Este artigo resume essas diferenças e exemplos para criar suas VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="305a1-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="305a1-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-106">Azure CLI</span></span>
<span data-ttu-id="305a1-107">Você pode criar VMs no Azure usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="305a1-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="305a1-108">CLI 1.0 do Azure – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="305a1-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="305a1-109">[CLI do Azure 2.0](../windows/creation-choices.md) – nossa próxima geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="305a1-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="305a1-110">A CLI 1.0 do Azure está disponível entre plataformas por meio de um pacote npm, pacotes de distribuição fornecida ou contêineres de Docker.</span><span class="sxs-lookup"><span data-stu-id="305a1-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="305a1-111">Você pode ler mais sobre [como instalar e configurar a CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="305a1-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="305a1-112">Os tutoriais a seguir fornecem exemplos sobre como usar a CLI 1.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="305a1-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="305a1-113">Leia cada artigo para obter mais detalhes sobre os comandos de início rápido da CLI mostrados:</span><span class="sxs-lookup"><span data-stu-id="305a1-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="305a1-114">Criar uma VM do Linux na CLI do Azure para desenvolvimento e teste</span><span class="sxs-lookup"><span data-stu-id="305a1-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="305a1-115">O exemplo a seguir cria uma VM CoreOS usando uma chave pública chamada *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="305a1-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="305a1-116">Criar uma VM do Linux protegida usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="305a1-117">O exemplo a seguir cria uma VM usando um modelo armazenado no GitHub:</span><span class="sxs-lookup"><span data-stu-id="305a1-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="305a1-118">Criar um ambiente Linux completo usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="305a1-119">Inclui a criação de um balanceador de carga e várias VMs em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="305a1-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="305a1-120">Adicionar um disco a uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="305a1-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="305a1-121">O exemplo a seguir adiciona um disco de *5* GB a uma VM existente chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="305a1-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="305a1-122">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-122">Azure portal</span></span>
<span data-ttu-id="305a1-123">O [portal do Azure](https://portal.azure.com) permite que você crie rapidamente uma VM porque não há nada para instalar em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="305a1-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="305a1-124">Use o portal do Azure para criar a VM:</span><span class="sxs-lookup"><span data-stu-id="305a1-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="305a1-125">Criar uma VM do Linux usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="305a1-126">Sistema operacional e opções de imagem</span><span class="sxs-lookup"><span data-stu-id="305a1-126">Operating system and image choices</span></span>
<span data-ttu-id="305a1-127">Ao criar uma VM, você escolherá uma imagem com base no sistema operacional que deseja executar.</span><span class="sxs-lookup"><span data-stu-id="305a1-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="305a1-128">A Azure e seus parceiros oferecem muitas imagens, algumas delas incluem aplicativos e ferramentas pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="305a1-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="305a1-129">Ou carregue uma de suas próprias imagens (consulte [a seção a seguir](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="305a1-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="305a1-130">Imagens do Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-130">Azure images</span></span>
<span data-ttu-id="305a1-131">Use os `azure vm image` comandos da CLI para ver o que está disponível no editor, versão de distribuição e compilações.</span><span class="sxs-lookup"><span data-stu-id="305a1-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="305a1-132">Liste os editores disponíveis como a seguir:</span><span class="sxs-lookup"><span data-stu-id="305a1-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="305a1-133">Liste os produtos (ofertas) disponíveis para um determinado editor como a seguir:</span><span class="sxs-lookup"><span data-stu-id="305a1-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="305a1-134">Liste os SKUs disponíveis (versões de distribuição) de uma determinada oferta como a seguir:</span><span class="sxs-lookup"><span data-stu-id="305a1-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="305a1-135">Liste todas as imagens disponíveis para uma determinada versão como a seguir:</span><span class="sxs-lookup"><span data-stu-id="305a1-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="305a1-136">Os comandos `azure vm quick-create` e `azure vm create` têm aliases que você pode usar para acessar rapidamente as distribuições mais comuns e suas versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="305a1-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="305a1-137">Usar aliases geralmente é mais rápido do que especificar o editor, oferta, SKU e versão sempre que você cria uma VM:</span><span class="sxs-lookup"><span data-stu-id="305a1-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="305a1-138">Alias</span><span class="sxs-lookup"><span data-stu-id="305a1-138">Alias</span></span> | <span data-ttu-id="305a1-139">Editor</span><span class="sxs-lookup"><span data-stu-id="305a1-139">Publisher</span></span> | <span data-ttu-id="305a1-140">Oferta</span><span class="sxs-lookup"><span data-stu-id="305a1-140">Offer</span></span> | <span data-ttu-id="305a1-141">SKU</span><span class="sxs-lookup"><span data-stu-id="305a1-141">SKU</span></span> | <span data-ttu-id="305a1-142">Versão</span><span class="sxs-lookup"><span data-stu-id="305a1-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="305a1-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="305a1-143">CentOS</span></span> |<span data-ttu-id="305a1-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="305a1-144">OpenLogic</span></span> |<span data-ttu-id="305a1-145">Centos</span><span class="sxs-lookup"><span data-stu-id="305a1-145">Centos</span></span> |<span data-ttu-id="305a1-146">7,2</span><span class="sxs-lookup"><span data-stu-id="305a1-146">7.2</span></span> |<span data-ttu-id="305a1-147">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-147">latest</span></span> |
| <span data-ttu-id="305a1-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="305a1-148">CoreOS</span></span> |<span data-ttu-id="305a1-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="305a1-149">CoreOS</span></span> |<span data-ttu-id="305a1-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="305a1-150">CoreOS</span></span> |<span data-ttu-id="305a1-151">Estável</span><span class="sxs-lookup"><span data-stu-id="305a1-151">Stable</span></span> |<span data-ttu-id="305a1-152">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-152">latest</span></span> |
| <span data-ttu-id="305a1-153">Debian</span><span class="sxs-lookup"><span data-stu-id="305a1-153">Debian</span></span> |<span data-ttu-id="305a1-154">credativ</span><span class="sxs-lookup"><span data-stu-id="305a1-154">credativ</span></span> |<span data-ttu-id="305a1-155">Debian</span><span class="sxs-lookup"><span data-stu-id="305a1-155">Debian</span></span> |<span data-ttu-id="305a1-156">8</span><span class="sxs-lookup"><span data-stu-id="305a1-156">8</span></span> |<span data-ttu-id="305a1-157">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-157">latest</span></span> |
| <span data-ttu-id="305a1-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="305a1-158">openSUSE</span></span> |<span data-ttu-id="305a1-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="305a1-159">SUSE</span></span> |<span data-ttu-id="305a1-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="305a1-160">openSUSE</span></span> |<span data-ttu-id="305a1-161">13.2</span><span class="sxs-lookup"><span data-stu-id="305a1-161">13.2</span></span> |<span data-ttu-id="305a1-162">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-162">latest</span></span> |
| <span data-ttu-id="305a1-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="305a1-163">RHEL</span></span> |<span data-ttu-id="305a1-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="305a1-164">Redhat</span></span> |<span data-ttu-id="305a1-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="305a1-165">RHEL</span></span> |<span data-ttu-id="305a1-166">7,2</span><span class="sxs-lookup"><span data-stu-id="305a1-166">7.2</span></span> |<span data-ttu-id="305a1-167">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-167">latest</span></span> |
| <span data-ttu-id="305a1-168">SLES</span><span class="sxs-lookup"><span data-stu-id="305a1-168">SLES</span></span> |<span data-ttu-id="305a1-169">SLES</span><span class="sxs-lookup"><span data-stu-id="305a1-169">SLES</span></span> |<span data-ttu-id="305a1-170">SLES</span><span class="sxs-lookup"><span data-stu-id="305a1-170">SLES</span></span> |<span data-ttu-id="305a1-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="305a1-171">12-SP1</span></span> |<span data-ttu-id="305a1-172">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-172">latest</span></span> |
| <span data-ttu-id="305a1-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="305a1-173">UbuntuLTS</span></span> |<span data-ttu-id="305a1-174">Canônico</span><span class="sxs-lookup"><span data-stu-id="305a1-174">Canonical</span></span> |<span data-ttu-id="305a1-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="305a1-175">UbuntuServer</span></span> |<span data-ttu-id="305a1-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="305a1-176">14.04.4-LTS</span></span> |<span data-ttu-id="305a1-177">mais recente</span><span class="sxs-lookup"><span data-stu-id="305a1-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="305a1-178">Usar sua própria imagem</span><span class="sxs-lookup"><span data-stu-id="305a1-178">Use your own image</span></span>
<span data-ttu-id="305a1-179">Se você precisar de personalizações específicas, poderá usar uma imagem com base em uma VM existente do Azure *capturando* essa VM.</span><span class="sxs-lookup"><span data-stu-id="305a1-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="305a1-180">Você também pode carregar uma imagem criada no local.</span><span class="sxs-lookup"><span data-stu-id="305a1-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="305a1-181">Para obter mais informações sobre as distribuições com suporte e como usar suas próprias imagens, confira os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="305a1-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="305a1-182">Distribuições endossadas pelo Azure</span><span class="sxs-lookup"><span data-stu-id="305a1-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="305a1-183">Informações para distribuições não endossadas</span><span class="sxs-lookup"><span data-stu-id="305a1-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="305a1-184">Carregar e criar uma VM Linux com base em uma imagem de disco personalizada</span><span class="sxs-lookup"><span data-stu-id="305a1-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="305a1-185">[Como capturar uma máquina virtual do Linux como um modelo do Resource Manager](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="305a1-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="305a1-186">Comandos de exemplo de início rápido para capturar uma VM existente:</span><span class="sxs-lookup"><span data-stu-id="305a1-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="305a1-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="305a1-187">Next steps</span></span>
* <span data-ttu-id="305a1-188">Crie uma VM do Linux o [portal](quick-create-portal.md), com a [CLI](quick-create-cli.md) ou usando um [modelo do Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="305a1-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="305a1-189">Depois de criar uma VM do Linux, [adicione um disco de dados](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="305a1-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="305a1-190">Etapas rápidas para [redefinir uma senha ou chaves SSH e gerenciar os usuários](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="305a1-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

