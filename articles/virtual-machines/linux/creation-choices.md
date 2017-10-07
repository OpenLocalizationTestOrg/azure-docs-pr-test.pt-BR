---
title: maneiras de aaaDifferent toocreate uma VM do Linux no Azure | Microsoft Azure
description: "Saiba mais maneiras diferentes de saudação toocreate uma máquina virtual do Linux no Azure, incluindo links tootools e tutoriais para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="fd6a2-103">Diferentes maneiras toocreate uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="fd6a2-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="fd6a2-104">Você tem Olá flexibilidade no Azure toocreate uma máquina virtual Linux (VM) usando ferramentas e fluxos de trabalho tooyou confortável.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="fd6a2-105">Este artigo resume essas diferenças e exemplos para criar suas VMs do Linux, incluindo Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="fd6a2-106">Você também pode exibir as opções de criação, incluindo Olá [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="fd6a2-107">Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) está disponível em plataformas por meio de um pacote de npm, pacotes de distribuição fornecido ou contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="fd6a2-108">Instalar o build de hello mais apropriado para seu ambiente e de log em tooan conta do Azure usando [logon az](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="fd6a2-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="fd6a2-109">Criar uma VM do Linux com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="fd6a2-110">Crie um grupo de recursos com [az group create](/cli/azure/group#create) chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="fd6a2-111">Criar uma VM com [criar vm az](/cli/azure/vm#create) chamado *myVM* usando hello mais recente *UbuntuLTS* imagem e gerar as chaves de SSH se eles ainda não existir no *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="fd6a2-112">Criar uma VM do Linux com um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="fd6a2-113">Olá exemplo a seguir usa [criar implantação de grupo az](/cli/azure/group/deployment#create) toocreate uma máquina virtual de um modelo armazenado no GitHub:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="fd6a2-114">Criar uma VM do Linux e personalizá-la com cloud-init</span><span class="sxs-lookup"><span data-stu-id="fd6a2-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="fd6a2-115">Criar um aplicativo de alta disponibilidade e com balanceamento de carga em várias VMs Linux</span><span class="sxs-lookup"><span data-stu-id="fd6a2-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="fd6a2-116">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-116">Azure portal</span></span>
<span data-ttu-id="fd6a2-117">Olá [portal do Azure](https://portal.azure.com) permite que você tooquickly criar uma máquina virtual porque não há nada tooinstall em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="fd6a2-118">Use Olá toocreate portal do Azure Olá VM:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="fd6a2-119">Criar uma VM do Linux usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="fd6a2-120">Sistema operacional e opções de imagem</span><span class="sxs-lookup"><span data-stu-id="fd6a2-120">Operating system and image choices</span></span>
<span data-ttu-id="fd6a2-121">Ao criar uma máquina virtual, você pode escolher uma imagem com base em Olá deseja toorun do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="fd6a2-122">A Azure e seus parceiros oferecem muitas imagens, algumas delas incluem aplicativos e ferramentas pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="fd6a2-123">Ou, carregar uma de suas próprias imagens (consulte [Olá seguinte seção](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="fd6a2-124">Imagens do Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-124">Azure images</span></span>
<span data-ttu-id="fd6a2-125">Saudação de uso [a imagem da vm az](/cli/azure/vm/image) comandos toosee que está disponível, publisher, versão de distribuição e compilações.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="fd6a2-126">Liste os editores disponíveis:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="fd6a2-127">Listar produtos (ofertas) disponíveis para determinado editor:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="fd6a2-128">Listar SKUs disponíveis (versões de distribuição) de determinada oferta:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="fd6a2-129">Liste todas as imagens disponíveis para determinada versão:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="fd6a2-130">Para obter mais exemplos de navegação e usar imagens disponíveis, consulte [navegue e selecione as imagens de máquina virtual do Azure com hello CLI do Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="fd6a2-131">Olá [criar vm az](/cli/azure/vm#create) comando tem aliases que você pode usar o acesso de tooquickly Olá distribuições mais comuns e suas versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="fd6a2-132">Usando aliases geralmente é mais rápido do que especificar publicador hello, oferta, SKU e versão cada vez que você cria uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="fd6a2-133">Alias</span><span class="sxs-lookup"><span data-stu-id="fd6a2-133">Alias</span></span> | <span data-ttu-id="fd6a2-134">Editor</span><span class="sxs-lookup"><span data-stu-id="fd6a2-134">Publisher</span></span> | <span data-ttu-id="fd6a2-135">Oferta</span><span class="sxs-lookup"><span data-stu-id="fd6a2-135">Offer</span></span> | <span data-ttu-id="fd6a2-136">SKU</span><span class="sxs-lookup"><span data-stu-id="fd6a2-136">SKU</span></span> | <span data-ttu-id="fd6a2-137">Versão</span><span class="sxs-lookup"><span data-stu-id="fd6a2-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd6a2-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-138">CentOS</span></span> |<span data-ttu-id="fd6a2-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="fd6a2-139">OpenLogic</span></span> |<span data-ttu-id="fd6a2-140">Centos</span><span class="sxs-lookup"><span data-stu-id="fd6a2-140">Centos</span></span> |<span data-ttu-id="fd6a2-141">7,2</span><span class="sxs-lookup"><span data-stu-id="fd6a2-141">7.2</span></span> |<span data-ttu-id="fd6a2-142">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-142">latest</span></span> |
| <span data-ttu-id="fd6a2-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-143">CoreOS</span></span> |<span data-ttu-id="fd6a2-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-144">CoreOS</span></span> |<span data-ttu-id="fd6a2-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-145">CoreOS</span></span> |<span data-ttu-id="fd6a2-146">Estável</span><span class="sxs-lookup"><span data-stu-id="fd6a2-146">Stable</span></span> |<span data-ttu-id="fd6a2-147">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-147">latest</span></span> |
| <span data-ttu-id="fd6a2-148">Debian</span><span class="sxs-lookup"><span data-stu-id="fd6a2-148">Debian</span></span> |<span data-ttu-id="fd6a2-149">credativ</span><span class="sxs-lookup"><span data-stu-id="fd6a2-149">credativ</span></span> |<span data-ttu-id="fd6a2-150">Debian</span><span class="sxs-lookup"><span data-stu-id="fd6a2-150">Debian</span></span> |<span data-ttu-id="fd6a2-151">8</span><span class="sxs-lookup"><span data-stu-id="fd6a2-151">8</span></span> |<span data-ttu-id="fd6a2-152">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-152">latest</span></span> |
| <span data-ttu-id="fd6a2-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="fd6a2-153">openSUSE</span></span> |<span data-ttu-id="fd6a2-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="fd6a2-154">SUSE</span></span> |<span data-ttu-id="fd6a2-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="fd6a2-155">openSUSE</span></span> |<span data-ttu-id="fd6a2-156">13.2</span><span class="sxs-lookup"><span data-stu-id="fd6a2-156">13.2</span></span> |<span data-ttu-id="fd6a2-157">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-157">latest</span></span> |
| <span data-ttu-id="fd6a2-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="fd6a2-158">RHEL</span></span> |<span data-ttu-id="fd6a2-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="fd6a2-159">Redhat</span></span> |<span data-ttu-id="fd6a2-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="fd6a2-160">RHEL</span></span> |<span data-ttu-id="fd6a2-161">7,2</span><span class="sxs-lookup"><span data-stu-id="fd6a2-161">7.2</span></span> |<span data-ttu-id="fd6a2-162">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-162">latest</span></span> |
| <span data-ttu-id="fd6a2-163">SLES</span><span class="sxs-lookup"><span data-stu-id="fd6a2-163">SLES</span></span> |<span data-ttu-id="fd6a2-164">SLES</span><span class="sxs-lookup"><span data-stu-id="fd6a2-164">SLES</span></span> |<span data-ttu-id="fd6a2-165">SLES</span><span class="sxs-lookup"><span data-stu-id="fd6a2-165">SLES</span></span> |<span data-ttu-id="fd6a2-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="fd6a2-166">12-SP1</span></span> |<span data-ttu-id="fd6a2-167">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-167">latest</span></span> |
| <span data-ttu-id="fd6a2-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-168">UbuntuLTS</span></span> |<span data-ttu-id="fd6a2-169">Canônico</span><span class="sxs-lookup"><span data-stu-id="fd6a2-169">Canonical</span></span> |<span data-ttu-id="fd6a2-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="fd6a2-170">UbuntuServer</span></span> |<span data-ttu-id="fd6a2-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="fd6a2-171">14.04.4-LTS</span></span> |<span data-ttu-id="fd6a2-172">mais recente</span><span class="sxs-lookup"><span data-stu-id="fd6a2-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="fd6a2-173">Usar sua própria imagem</span><span class="sxs-lookup"><span data-stu-id="fd6a2-173">Use your own image</span></span>
<span data-ttu-id="fd6a2-174">Se você precisar de personalizações específicas, poderá usar uma imagem com base em uma VM existente do Azure capturando essa VM.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="fd6a2-175">Você também pode carregar uma imagem criada no local.</span><span class="sxs-lookup"><span data-stu-id="fd6a2-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="fd6a2-176">Para obter mais informações sobre as distribuições com suporte e como toouse suas próprias imagens, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="fd6a2-177">Distribuições endossadas pelo Azure</span><span class="sxs-lookup"><span data-stu-id="fd6a2-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="fd6a2-178">Informações para distribuições não endossadas</span><span class="sxs-lookup"><span data-stu-id="fd6a2-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="fd6a2-179">[Como uma imagem de uma VM do Azure existente de toocreate](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="fd6a2-180">Exemplo de início rápido comandos toocreate uma imagem de uma VM do Azure existente:</span><span class="sxs-lookup"><span data-stu-id="fd6a2-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="fd6a2-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd6a2-181">Next steps</span></span>
* <span data-ttu-id="fd6a2-182">Criar uma VM do Linux com hello [CLI](quick-create-cli.md), da saudação [portal](quick-create-portal.md), ou usando um [modelo do Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="fd6a2-183">Depois de criar uma VM do Linux, [saiba mais sobre discos e armazenamento do Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="fd6a2-184">Rápida etapas muito[redefinir uma senha ou as chaves de SSH e gerenciar usuários](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="fd6a2-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
