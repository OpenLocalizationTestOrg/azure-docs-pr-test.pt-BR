---
title: aaaCapture uma imagem de uma VM do Linux no Azure usando a CLI 2.0 | Microsoft Docs
description: "Capture uma imagem de toouse uma VM do Azure para implantações em massa usando Olá 2.0 do CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="0e6d3-103">Como toocreate uma imagem de uma máquina virtual ou um VHD</span><span class="sxs-lookup"><span data-stu-id="0e6d3-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="0e6d3-104">toocreate várias cópias de um toouse de máquina virtual (VM) no Azure, capturar uma imagem de VM de saudação ou Olá VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="0e6d3-105">toocreate uma imagem, você precisa remover informações pessoais da conta que torna mais segura toodeploy várias vezes.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="0e6d3-106">Em Olá etapas cancelar o provisionamento de uma VM existente, desalocar e criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="0e6d3-107">Você pode usar essa imagem toocreate VMs em qualquer grupo de recursos dentro de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="0e6d3-108">Se você deseja toocreate uma cópia da VM Linux existente para backup ou de depuração ou carrega um VHD Linux especializadas de uma VM local, consulte [carregar e criar uma VM do Linux de imagem de disco personalizado](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="0e6d3-109">Você também pode usar **Packer** toocreate sua configuração personalizada.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="0e6d3-110">Para obter mais informações sobre como usar Packer, consulte [como as imagens de máquina virtual do toouse Packer toocreate Linux no Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="0e6d3-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0e6d3-111">Before you begin</span></span>
<span data-ttu-id="0e6d3-112">Certifique-se de atender Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="0e6d3-113">Você precisa de uma VM do Azure criada no modelo de implantação do Gerenciador de recursos do hello usando discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="0e6d3-114">Se você ainda não criou uma VM do Linux, você pode usar o hello [portal](quick-create-portal.md), Olá [CLI do Azure](quick-create-cli.md), ou [modelos do Gerenciador de recursos](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="0e6d3-115">Configure Olá VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-115">Configure hello VM as needed.</span></span> <span data-ttu-id="0e6d3-116">Por exemplo, [adicionar discos de dados](add-disk.md), aplicar atualizações e instalar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="0e6d3-117">Você também precisa toohave hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0e6d3-118">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="0e6d3-118">Quick commands</span></span>

<span data-ttu-id="0e6d3-119">Para uma versão simplificada deste tópico, para testar, avaliando ou aprender sobre máquinas virtuais no Azure, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="0e6d3-120">Etapa 1: Desprovisionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="0e6d3-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="0e6d3-121">Desprovisionar o hello VM, usando o agente de VM do Azure hello, toodelete arquivos específicos da máquina e dados.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="0e6d3-122">Saudação de uso `waagent` com hello *-desprovisionamento + user* parâmetro em sua fonte de VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="0e6d3-123">Para obter mais informações, consulte Olá [guia do usuário do agente Linux do Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="0e6d3-124">Conecte-se tooyour VM do Linux usando um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="0e6d3-125">Na janela SSH hello, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="0e6d3-126">Somente execute esse comando em uma máquina virtual que você pretende toocapture como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="0e6d3-127">Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para redistribuição.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="0e6d3-128">Olá *+ user* parâmetro também remove a última conta de usuário provisionado hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="0e6d3-129">Se você quiser tookeep credenciais da conta no hello VM, basta usar *-desprovisionamento* tooleave conta de usuário de saudação em vigor.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="0e6d3-130">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-130">Type **y** toocontinue.</span></span> <span data-ttu-id="0e6d3-131">Você pode adicionar Olá **-force** parâmetro tooavoid essa etapa de confirmação.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="0e6d3-132">Após a conclusão do comando hello, digite **sair**.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="0e6d3-133">Esta etapa fecha cliente SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="0e6d3-134">Etapa 2: Criar a imagem de VM</span><span class="sxs-lookup"><span data-stu-id="0e6d3-134">Step 2: Create VM image</span></span>
<span data-ttu-id="0e6d3-135">Usar Olá 2.0 do CLI do Azure toomark Olá VM generalizado e capturar a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="0e6d3-136">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0e6d3-137">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="0e6d3-138">Desalocar Olá VM desprovisionada com [az vm desalocar](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="0e6d3-139">exemplo a seguir Hello desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="0e6d3-140">Saudação de marca VM como generalizado com [az vm generalizar](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="0e6d3-141">Olá seguinte exemplo marcas Olá Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup* como generalizado:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="0e6d3-142">Agora crie uma imagem do recurso VM Olá com [criar imagem az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="0e6d3-143">Olá, exemplo a seguir cria uma imagem chamada *myImage* no grupo de recursos de saudação denominado *myResourceGroup* usando o recurso VM Olá denominado *myVM*:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="0e6d3-144">Olá imagem é criada no hello mesmo grupo de recursos como a fonte de VM.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="0e6d3-145">Você pode criar VMs em qualquer grupo de recursos em sua assinatura desde esta imagem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="0e6d3-146">De uma perspectiva de gerenciamento, talvez você queira toocreate um grupo de recursos específicos para seus recursos VM e imagens.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="0e6d3-147">Etapa 3: Criar uma VM da imagem capturada de saudação</span><span class="sxs-lookup"><span data-stu-id="0e6d3-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="0e6d3-148">Criar uma VM usando a imagem de saudação criado com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0e6d3-149">Olá, exemplo a seguir cria uma VM denominada *myVMDeployed* de imagem Olá chamada *myImage*:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="0e6d3-150">Criando Olá VM em outro grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0e6d3-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="0e6d3-151">Com os discos gerenciados, você pode criar VMs de uma imagem em qualquer grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="0e6d3-152">toocreate uma VM em um grupo de recursos diferente que a imagem Olá, especifique a imagem de tooyour de ID de recurso completo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="0e6d3-153">Use [lista de imagens az](/cli/azure/image#list) tooview uma lista de imagens.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="0e6d3-154">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="0e6d3-155">Olá exemplo a seguir usa [criar vm az](/cli/azure/vm#create) toocreate uma VM em um grupo de recursos diferente que a imagem de origem Olá especificando a ID de recurso de imagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="0e6d3-156">Etapa 4: Verificar a implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="0e6d3-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="0e6d3-157">Agora SSH toohello máquina virtual é criada a implantação de saudação tooverify e começar a usar Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="0e6d3-158">tooconnect via SSH, localizar o endereço IP de saudação ou FQDN da VM com [Mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="0e6d3-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="0e6d3-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e6d3-159">Next steps</span></span>
<span data-ttu-id="0e6d3-160">Você pode criar várias máquinas virtuais da sua imagem de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="0e6d3-161">Se você precisa de imagem de tooyour toomake alterações:</span><span class="sxs-lookup"><span data-stu-id="0e6d3-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="0e6d3-162">Crie uma VM usando sua imagem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-162">Create a VM from your image.</span></span>
- <span data-ttu-id="0e6d3-163">Faça quaisquer atualizações ou alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="0e6d3-164">Siga Olá etapas novamente toodeprovision, desalocar, generalizar e criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="0e6d3-165">Use essa nova imagem para implantações futuras.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-165">Use this new image for future deployments.</span></span> <span data-ttu-id="0e6d3-166">Se desejar, exclua imagem original hello.</span><span class="sxs-lookup"><span data-stu-id="0e6d3-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="0e6d3-167">Para obter mais informações sobre como gerenciar suas VMs com hello CLI, consulte [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e6d3-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
