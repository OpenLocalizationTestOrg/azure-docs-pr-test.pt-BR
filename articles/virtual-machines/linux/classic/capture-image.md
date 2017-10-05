---
title: Capturar uma imagem de uma VM do Linux | Microsoft Docs
description: "Saiba como capturar uma imagem de uma VM (máquina virtual) do Azure baseada em Linux criada com o modelo de implantação clássico."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="8ffea-103">Como capturar uma máquina virtual clássica do Linux como uma imagem</span><span class="sxs-lookup"><span data-stu-id="8ffea-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ffea-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8ffea-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ffea-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="8ffea-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8ffea-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffea-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8ffea-107">Saiba como [executar estas etapas usando o modelo do Resource Manager](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ffea-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8ffea-108">Este artigo mostra como capturar uma VM (máquina virtual) do Azure clássica executando o Linux como uma imagem para criar outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8ffea-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="8ffea-109">Esta imagem inclui o disco do sistema operacional e discos de dados anexados à VM.</span><span class="sxs-lookup"><span data-stu-id="8ffea-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="8ffea-110">Ele não inclui a configuração de rede, então você precisará configurá-la quando criar as outras VMs por meio da imagem.</span><span class="sxs-lookup"><span data-stu-id="8ffea-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="8ffea-111">O Azure armazena a imagem em **Imagens**, juntamente com quaisquer imagens carregadas.</span><span class="sxs-lookup"><span data-stu-id="8ffea-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="8ffea-112">Para saber mais sobre imagens, confira [Sobre imagens da Máquina Virtual no Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="8ffea-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ffea-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8ffea-113">Before you begin</span></span>
<span data-ttu-id="8ffea-114">Essas etapas pressupõem que você já criou uma VM do Azure usando o modelo de implantação clássico e configurou o sistema operacional, incluindo a anexação dos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffea-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="8ffea-115">Se você precisar criar uma VM, leia [Como criar uma máquina virtual do Linux][How to Create a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="8ffea-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="8ffea-116">Capturar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8ffea-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="8ffea-117">[Conecte-se à VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) usando um cliente SSH de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="8ffea-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="8ffea-118">Na janela SSH, digite o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ffea-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="8ffea-119">A saída de `waagent` pode variar um pouco dependendo da versão do utilitário:</span><span class="sxs-lookup"><span data-stu-id="8ffea-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="8ffea-120">O comando anterior tenta limpar o sistema e torná-lo adequado para o reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="8ffea-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="8ffea-121">Essa operação realiza as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="8ffea-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="8ffea-122">Remove as chaves de host SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração)</span><span class="sxs-lookup"><span data-stu-id="8ffea-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="8ffea-123">Limpa a configuração de servidor de nomes em /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="8ffea-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="8ffea-124">Remove a senha do usuário `root` de /etc/shadow (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração)</span><span class="sxs-lookup"><span data-stu-id="8ffea-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="8ffea-125">Remove concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="8ffea-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="8ffea-126">Reinicia o nome de host para localdomain.localdomain</span><span class="sxs-lookup"><span data-stu-id="8ffea-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="8ffea-127">Exclui a última conta de usuário provisionado (obtida em /var/lib/waagent) **e dados associados**.</span><span class="sxs-lookup"><span data-stu-id="8ffea-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8ffea-128">O desprovisionamento exclui arquivos e dados para “generalizar” a imagem.</span><span class="sxs-lookup"><span data-stu-id="8ffea-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="8ffea-129">Execute este comando apenas em uma VM que você deseja capturar como um novo modelo de imagem.</span><span class="sxs-lookup"><span data-stu-id="8ffea-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="8ffea-130">Ele não garante que a imagem esteja sem nenhuma informação confidencial ou seja adequada para redistribuição a terceiros.</span><span class="sxs-lookup"><span data-stu-id="8ffea-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="8ffea-131">Digite **y** para continuar.</span><span class="sxs-lookup"><span data-stu-id="8ffea-131">Type **y** to continue.</span></span> <span data-ttu-id="8ffea-132">Você pode adicionar o parâmetro `-force` para evitar esta etapa de confirmação.</span><span class="sxs-lookup"><span data-stu-id="8ffea-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="8ffea-133">Digite **Exit** para fechar o cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="8ffea-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ffea-134">As etapas restantes presumem que você já [instalou a CLI do Azure](../../../cli-install-nodejs.md) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="8ffea-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="8ffea-135">Todas as etapas a seguir também podem ser executadas no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ffea-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="8ffea-136">No computador cliente, abra a CLI do Azure e faça logon com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffea-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="8ffea-137">Para obter detalhes, leia [Conectar-se a uma assinatura do Azure da CLI do Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8ffea-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ffea-138">Faça logon no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffea-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="8ffea-139">Verifique se você está no modo de Gerenciamento de Serviços:</span><span class="sxs-lookup"><span data-stu-id="8ffea-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="8ffea-140">Desligar a VM já desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="8ffea-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="8ffea-141">O exemplo a seguir desliga a VM chamada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8ffea-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="8ffea-142">Se necessário, é possível exibir uma lista de todas as VMs criadas na sua assinatura usando `azure vm list`</span><span class="sxs-lookup"><span data-stu-id="8ffea-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ffea-143">Se você estiver usando o portal do Azure, selecione a VM e clique em **Parar** para desligar a VM.</span><span class="sxs-lookup"><span data-stu-id="8ffea-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="8ffea-144">Quando a VM é interrompida, capture a imagem.</span><span class="sxs-lookup"><span data-stu-id="8ffea-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="8ffea-145">O exemplo a seguir captura a VM denominada `myVM` e cria uma imagem generalizada chamada `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="8ffea-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="8ffea-146">O subcomando `-t` exclui a máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="8ffea-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8ffea-147">No portal do Azure, você pode capturar uma imagem selecionando **Imagem** no menu de hub.</span><span class="sxs-lookup"><span data-stu-id="8ffea-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="8ffea-148">Você precisará fornecer as seguintes informações para a imagem: nome, grupo de recursos, local, tipo do sistema operacional e caminho de blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8ffea-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="8ffea-149">A nova imagem agora está disponível na lista de imagens que podem ser usadas para configurar qualquer nova VM.</span><span class="sxs-lookup"><span data-stu-id="8ffea-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="8ffea-150">Você pode exibi-la com o comando:</span><span class="sxs-lookup"><span data-stu-id="8ffea-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="8ffea-151">No [portal do Azure](http://portal.azure.com), a nova imagem é exibida nas **Imagens de VM (clássico)** que pertencem aos serviços de **Computação**.</span><span class="sxs-lookup"><span data-stu-id="8ffea-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="8ffea-152">É possível acessar as **Imagens de VM (clássico)** clicando em _Mais serviços_ na parte inferior da lista de serviços do Azure e, em seguida, verificando os serviços de **Computação**.</span><span class="sxs-lookup"><span data-stu-id="8ffea-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="8ffea-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ffea-154">Next steps</span></span>
<span data-ttu-id="8ffea-155">A imagem está pronta para ser usada para criar VMs.</span><span class="sxs-lookup"><span data-stu-id="8ffea-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="8ffea-156">É possível usar o comando `azure vm create` da CLI do Azure e fornecer o nome da imagem que você criou.</span><span class="sxs-lookup"><span data-stu-id="8ffea-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="8ffea-157">Para obter mais informações, consulte [Usando a CLI do Azure com o modelo de implantação Clássico](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8ffea-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="8ffea-158">Como alternativa, use o [Portal do Azure](http://portal.azure.com) para criar uma VM personalizada usando o método **Imagem** e selecionando a imagem que você criou.</span><span class="sxs-lookup"><span data-stu-id="8ffea-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="8ffea-159">Para obter mais informações, consulte [Como criar uma VM personalizada][How to Create a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="8ffea-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="8ffea-160">**Consulte também:** [Guia do usuário do agente Linux para o Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8ffea-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
