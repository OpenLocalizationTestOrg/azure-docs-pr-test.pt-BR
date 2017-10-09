---
title: aaaCapture uma imagem de uma VM do Linux | Microsoft Docs
description: "Saiba como toocapture uma imagem de uma baseados em Linux do Azure máquina virtual (VM) criados com o modelo de implantação clássico hello."
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
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="7c2be-103">Como uma máquina de virtual do Linux clássica como uma imagem de toocapture</span><span class="sxs-lookup"><span data-stu-id="7c2be-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7c2be-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7c2be-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7c2be-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="7c2be-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7c2be-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c2be-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7c2be-107">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c2be-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7c2be-108">Este artigo mostra como toocapture uma máquina de virtual do Azure (VM) clássica executando o Linux como uma imagem toocreate outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7c2be-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="7c2be-109">Esta imagem inclui o disco do sistema operacional hello e discos de dados anexados toohello VM.</span><span class="sxs-lookup"><span data-stu-id="7c2be-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="7c2be-110">Não inclui a configuração de rede, portanto, você precisa tooconfigure que quando você cria Olá outra VM da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c2be-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="7c2be-111">Repositórios do Azure Olá imagem em **imagens**, junto com as imagens que você carregou.</span><span class="sxs-lookup"><span data-stu-id="7c2be-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="7c2be-112">Para saber mais sobre imagens, confira [Sobre imagens da Máquina Virtual no Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="7c2be-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c2be-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7c2be-113">Before you begin</span></span>
<span data-ttu-id="7c2be-114">Essas etapas pressupõem que você já criou uma VM do Azure usando o modelo de implantação clássico hello e sistema de operacional de saudação configurado, incluindo anexar discos de dados.</span><span class="sxs-lookup"><span data-stu-id="7c2be-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="7c2be-115">Se você precisar toocreate uma VM, leia [como tooCreate uma máquina Virtual Linux][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="7c2be-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="7c2be-116">Capturar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="7c2be-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="7c2be-117">[Conecte-se a VM do toohello](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) usando um cliente SSH de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="7c2be-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="7c2be-118">Na janela SSH hello, digite Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c2be-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="7c2be-119">saudação de saída de `waagent` podem variar um pouco dependendo da versão de saudação do utilitário:</span><span class="sxs-lookup"><span data-stu-id="7c2be-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="7c2be-120">Olá comando anterior tentativas tooclean sistema de saudação e torná-lo adequado para reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="7c2be-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="7c2be-121">Essa operação fará Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c2be-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="7c2be-122">Remove as chaves de host do SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração de saudação)</span><span class="sxs-lookup"><span data-stu-id="7c2be-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="7c2be-123">Limpa a configuração de servidor de nomes em /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="7c2be-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="7c2be-124">Olá remove `root` senha de usuário de/etc/sombra (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração de saudação)</span><span class="sxs-lookup"><span data-stu-id="7c2be-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="7c2be-125">Remove concessões de cliente DHCP em cache</span><span class="sxs-lookup"><span data-stu-id="7c2be-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="7c2be-126">Redefine toolocalhost.localdomain de nome de host</span><span class="sxs-lookup"><span data-stu-id="7c2be-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="7c2be-127">Exclui a conta de usuário provisionado última hello (obtida /var/lib/waagent) **e dados associados**.</span><span class="sxs-lookup"><span data-stu-id="7c2be-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7c2be-128">Desprovisionamento exclui arquivos e dados muito "generalizar" hello imagem.</span><span class="sxs-lookup"><span data-stu-id="7c2be-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="7c2be-129">Somente execute esse comando em uma máquina virtual que você pretende toocapture como um novo modelo de imagem.</span><span class="sxs-lookup"><span data-stu-id="7c2be-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="7c2be-130">Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para partes de toothird de redistribuição.</span><span class="sxs-lookup"><span data-stu-id="7c2be-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="7c2be-131">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7c2be-131">Type **y** toocontinue.</span></span> <span data-ttu-id="7c2be-132">Você pode adicionar Olá `-force` parâmetro tooavoid essa etapa de confirmação.</span><span class="sxs-lookup"><span data-stu-id="7c2be-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="7c2be-133">Tipo **Exit** cliente SSH tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="7c2be-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7c2be-134">Olá etapas restantes supõem que você já tiver [instalado Olá CLI do Azure](../../../cli-install-nodejs.md) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="7c2be-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="7c2be-135">Olá todas as etapas a seguir também pode ser feito no hello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c2be-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="7c2be-136">No computador cliente, abra CLI do Azure e logon tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c2be-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="7c2be-137">Para obter detalhes, leia [conectar tooan assinatura do Azure do hello CLI do Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7c2be-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="7c2be-138">No portal do Azure de Olá, faça logon no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="7c2be-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="7c2be-139">Verifique se você está no modo de Gerenciamento de Serviços:</span><span class="sxs-lookup"><span data-stu-id="7c2be-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="7c2be-140">Desligar Olá VM já desprovisionada.</span><span class="sxs-lookup"><span data-stu-id="7c2be-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="7c2be-141">Olá exemplo a seguir é desligado Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="7c2be-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="7c2be-142">Se necessário, você pode exibir uma lista Olá todas as máquinas virtuais criadas na sua assinatura usando`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="7c2be-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="7c2be-143">Se você estiver usando Olá portal do Azure, selecione Olá VM e clique em **parar** desligar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="7c2be-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="7c2be-144">Quando Olá VM é interrompido, capture a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c2be-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="7c2be-145">Olá capturas de exemplo a seguir Olá VM denominada `myVM` e cria uma imagem generalizada chamada `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="7c2be-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="7c2be-146">Olá `-t` subcomando exclusões Olá máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="7c2be-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c2be-147">Em Olá portal do Azure, você pode capturar uma imagem selecionando **imagem** no menu de hub hello.</span><span class="sxs-lookup"><span data-stu-id="7c2be-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="7c2be-148">Você precisa Olá toosupply informações Olá imagem a seguir: nome do grupo de recursos, local, tipo de sistema operacional e caminho de blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7c2be-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="7c2be-149">Olá nova imagem está agora disponível na lista de saudação de imagens que podem ser tooconfigure de usados qualquer nova VM.</span><span class="sxs-lookup"><span data-stu-id="7c2be-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="7c2be-150">Você pode exibi-lo com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="7c2be-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="7c2be-151">Em Olá [portal do Azure](http://portal.azure.com), Olá nova imagem aparecerá em Olá **imagens da VM (clássico)** que pertence a toohello **de computação** serviços.</span><span class="sxs-lookup"><span data-stu-id="7c2be-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="7c2be-152">Você pode acessar **imagens da VM (clássico)** clicando _mais serviços_ na parte inferior de saudação do hello Azure lista de serviço e, em seguida, verificando Olá **de computação** serviços.</span><span class="sxs-lookup"><span data-stu-id="7c2be-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="7c2be-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c2be-154">Next steps</span></span>
<span data-ttu-id="7c2be-155">imagem de saudação está pronto toobe usado toocreate VMs.</span><span class="sxs-lookup"><span data-stu-id="7c2be-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="7c2be-156">Você pode usar o comando CLI do Azure de saudação `azure vm create` e o nome de imagem Olá fonte criado por você.</span><span class="sxs-lookup"><span data-stu-id="7c2be-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="7c2be-157">Para obter mais informações, consulte [usando Olá CLI do Azure com o modelo de implantação clássico](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7c2be-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="7c2be-158">Como alternativa, use Olá [portal do Azure](http://portal.azure.com) toocreate uma VM personalizada usando Olá **imagem** método hello a seleção de imagem e você criou.</span><span class="sxs-lookup"><span data-stu-id="7c2be-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="7c2be-159">Para obter mais informações, consulte [como tooCreate uma VM personalizada][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="7c2be-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="7c2be-160">**Consulte também:** [Guia do usuário do agente Linux para o Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7c2be-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
