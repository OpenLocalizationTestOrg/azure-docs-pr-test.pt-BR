---
title: Capturar uma VM do Linux do Azure para usar como modelo | Microsoft Docs
description: "Saiba como capturar e generalizar uma imagem de uma VM (máquina virtual) do Azure baseada no Linux criada com o modelo de implantação do Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="ef0bf-103">Capturar uma máquina virtual do Linux em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="ef0bf-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="ef0bf-104">Siga as etapas neste artigo para generalizar e capturar sua VM (máquina virtual) do Linux do Azure no modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="ef0bf-105">Ao generalizar a VM, você remove informações de conta pessoal e prepara a VM a ser usada como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="ef0bf-106">Em seguida, você captura a imagem de um VHD (disco rígido virtual) generalizado para o sistema operacional, VHDs para discos de dados anexados e um [modelo do Resource Manager](../../azure-resource-manager/resource-group-overview.md) para novas implantações de VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="ef0bf-107">Este artigo fornece detalhes sobre como capturar uma imagem de VM com a CLI do Azure 1.0 para uma VM usando discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="ef0bf-108">Você também pode [capturar uma VM usando o Azure Managed Disks com a CLI 2.0 do Azure](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ef0bf-109">Os Managed Disks são tratados pela plataforma do Azure e não exigem nenhuma preparação ou local para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="ef0bf-110">Para saber mais, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="ef0bf-111">Para criar VMs usando a imagem, configure recursos de rede para cada nova VM e use o modelo (um arquivo JavaScript Object Notation ou JSON) para implantá-lo por meio de imagens VHD capturadas.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="ef0bf-112">Dessa forma, você pode replicar uma VM com sua configuração atual de software, da mesma forma como usa imagens no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="ef0bf-113">Se quiser criar uma cópia de sua VM Linux existente com seu estado especializado para depuração ou backup, confira [Criar uma cópia de uma máquina virtual do Linux em execução no Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ef0bf-114">Se você quiser carregar um VHD do Linux na VM local, confira [Carregar e criar uma VM do Linux por meio da imagem de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ef0bf-115">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="ef0bf-115">CLI versions to complete the task</span></span>
<span data-ttu-id="ef0bf-116">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ef0bf-117">[CLI 1.0 do Azure](#before-you-begin) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="ef0bf-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ef0bf-118">[CLI 2.0 do Azure](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="ef0bf-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef0bf-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ef0bf-119">Before you begin</span></span>
<span data-ttu-id="ef0bf-120">Verifique se os seguintes pré-requisitos foram atendidos:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="ef0bf-121">**VM do Azure criada no modelo de implantação do Gerenciador de Recursos** - se você ainda não criou uma VM do Linux, pode usar o [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), a [CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [modelos do Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="ef0bf-122">Configure a VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-122">Configure the VM as needed.</span></span> <span data-ttu-id="ef0bf-123">Por exemplo, [adicionar discos de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aplicar atualizações e instalar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="ef0bf-124">**CLI do Azure** - instalar a [CLI do Azure](../../cli-install-nodejs.md) em um computador local.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="ef0bf-125">Etapa 1: remover o agente Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="ef0bf-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="ef0bf-126">Primeiro, execute o comando **waagent** com o parâmetro **deprovision** na VM Linux.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="ef0bf-127">Esse comando exclui arquivos e dados para preparar a VM para generalização.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="ef0bf-128">Para obter detalhes, confira o [Guia do usuário do Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="ef0bf-129">Conecte-se à VM do Linux usando um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="ef0bf-130">Na janela SSH, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="ef0bf-131">Execute o comando apenas em uma VM que você pretende capturar como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="ef0bf-132">Ele não garante que a imagem esteja sem nenhuma informação confidencial ou seja adequada para redistribuição.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="ef0bf-133">Digite **y** para continuar.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-133">Type **y** to continue.</span></span> <span data-ttu-id="ef0bf-134">Você pode adicionar o parâmetro **-force** para evitar essa etapa de confirmação.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="ef0bf-135">Após a conclusão do comando, digite **sair**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="ef0bf-136">Esta etapa fecha o cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="ef0bf-137">Etapa 2: Capturar a VM</span><span class="sxs-lookup"><span data-stu-id="ef0bf-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="ef0bf-138">Use a CLI do Azure para generalizar e capturar a VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="ef0bf-139">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ef0bf-140">Os nomes de parâmetro de exemplo incluem **myResourceGroup**, **myVnet** e **myVM**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="ef0bf-141">No computador local, abra a CLI do Azure e [faça logon com sua assinatura do Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="ef0bf-142">Certifique-se de estar no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="ef0bf-143">Desligue a VM que você já desprovisionou usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="ef0bf-144">Generalize a VM com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="ef0bf-145">Agora, execute o comando **azure vm capture**, que captura a VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="ef0bf-146">No exemplo a seguir, os VHDs de imagem são capturados com nomes que começam com **MyVHDNamePrefix**, e a opção **-t** especifica um caminho para o modelo **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="ef0bf-147">Os arquivos de imagem VHD são criados por padrão na mesma conta de armazenamento da VM original usada.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="ef0bf-148">Use a *mesma conta de armazenamento* para armazenar os VHDs de novas VMs que você criar com base na imagem.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="ef0bf-149">Para encontrar o local de uma imagem capturada, abra o modelo JSON em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="ef0bf-150">Em **storageProfile**, encontre o **uri** da **imagem** localizado no contêiner do **sistema**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="ef0bf-151">Por exemplo, o URI da imagem de disco do sistema operacional é semelhante a `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="ef0bf-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="ef0bf-152">Etapa 3: criar uma VM com base na imagem capturada</span><span class="sxs-lookup"><span data-stu-id="ef0bf-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="ef0bf-153">Agora, use a imagem com um modelo para criar uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="ef0bf-154">Essas etapas mostram como usar a CLI do Azure e o modelo de arquivo JSON capturado para criar a VM em uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="ef0bf-155">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="ef0bf-155">Create network resources</span></span>
<span data-ttu-id="ef0bf-156">Para usar o modelo, primeiro é necessário configurar uma rede virtual e uma NIC para sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="ef0bf-157">Recomendamos criar um grupo de recursos para esses recursos na localização em que a imagem de VM está armazenada.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="ef0bf-158">Execute comandos semelhantes aos seguintes, substituindo os nomes dos seus recursos e um local apropriado do Azure ("centralus" nesses comandos):</span><span class="sxs-lookup"><span data-stu-id="ef0bf-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="ef0bf-159">Obter a Id da NIC</span><span class="sxs-lookup"><span data-stu-id="ef0bf-159">Get the Id of the NIC</span></span>
<span data-ttu-id="ef0bf-160">Para implantar uma VM a partir da imagem usando o JSON salvo durante a captura, é necessária a ID do NIC.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="ef0bf-161">Obtenha-a executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="ef0bf-162">A **Id** na saída é semelhante a `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="ef0bf-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="ef0bf-163">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ef0bf-163">Create a VM</span></span>
<span data-ttu-id="ef0bf-164">Agora, execute o comando a seguir para criar a VM com base na imagem de VM capturada.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="ef0bf-165">Use o parâmetro **-f** para especificar o caminho para o arquivo JSON de modelo salvo.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="ef0bf-166">Na saída do comando, você precisará fornecer um novo nome da VM, nome de usuário administrador, senha e a ID da NIC criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="ef0bf-167">O seguinte exemplo mostra o que você vê para uma implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-the-deployment"></a><span data-ttu-id="ef0bf-168">Verificar a implantação</span><span class="sxs-lookup"><span data-stu-id="ef0bf-168">Verify the deployment</span></span>
<span data-ttu-id="ef0bf-169">Agora, use o SSH na máquina virtual que você criou para verificar a implantação e começar a usar a nova VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="ef0bf-170">Para se conectar via SSH, localize o endereço IP da VM criada executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="ef0bf-171">O endereço IP público é listado na saída do comando.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="ef0bf-172">Por padrão, você conecta a VM Linux por SSH na porta 22.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="ef0bf-173">Criar VMs adicionais</span><span class="sxs-lookup"><span data-stu-id="ef0bf-173">Create additional VMs</span></span>
<span data-ttu-id="ef0bf-174">Use a imagem capturada e o modelo para implantar VMs adicionais usando as etapas da seção anterior.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="ef0bf-175">Outras opções para criar VMs com base na imagem incluem usar um modelo de início rápido ou executar o comando **azure vm create**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="ef0bf-176">Usar o modelo capturado</span><span class="sxs-lookup"><span data-stu-id="ef0bf-176">Use the captured template</span></span>
<span data-ttu-id="ef0bf-177">Para usar a imagem capturada e o modelo, siga estas etapas (detalhadas na seção anterior):</span><span class="sxs-lookup"><span data-stu-id="ef0bf-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="ef0bf-178">Verifique se a imagem da VM está na mesma conta de armazenamento que hospeda o VHD da VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="ef0bf-179">Copie o arquivo de modelo JSON e especifique um nome exclusivo para o disco do sistema operacional do VHD (ou VHDs) da nova VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="ef0bf-180">Por exemplo, em **storageProfile**, em **vhd**, em **uri**, especifique um nome exclusivo para o VHD **osDisk**, semelhante a `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="ef0bf-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="ef0bf-181">Crie uma NIC na mesma rede virtual ou em uma diferente.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="ef0bf-182">Usando o arquivo JSON de modelo modificado, crie uma implantação no grupo de recursos em que você configura a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="ef0bf-183">Usar um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="ef0bf-183">Use a quickstart template</span></span>
<span data-ttu-id="ef0bf-184">Se desejar que a rede seja configurada automaticamente quando você criar uma VM por meio da imagem, você poderá especificar esses recursos em um modelo.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="ef0bf-185">Por exemplo, confira [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="ef0bf-186">Esse modelo cria uma VM de sua imagem personalizada e da rede virtual necessária, endereço IP público e recursos da NIC.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="ef0bf-187">Para obter uma explicação sobre como usar o modelo no Portal do Azure, confira [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)(Como criar uma máquina virtual de uma imagem personalizada usando um modelo do Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="ef0bf-188">Usar o comando azure vm create</span><span class="sxs-lookup"><span data-stu-id="ef0bf-188">Use the azure vm create command</span></span>
<span data-ttu-id="ef0bf-189">Geralmente, é mais fácil de usar um modelo do Resource Manager para criar uma VM com base na imagem.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="ef0bf-190">No entanto, você pode criar a VM *de modo forçado* usando o comando **azure vm create** com o parâmetro **-Q** (**--image-urn**).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="ef0bf-191">Se usar este método, você também passará o parâmetro **-d** (**--os-disk-vhd**) para especificar a localização do arquivo.vhd do sistema operacional para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="ef0bf-192">O arquivo deve estar no contêiner de vhds da conta de armazenamento na qual o arquivo VHD da imagem está armazenado.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="ef0bf-193">O comando copia o VHD para a nova VM automaticamente para o contêiner de **vhds**.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="ef0bf-194">Antes de executar **azure vm create** com a imagem, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ef0bf-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="ef0bf-195">Crie um grupo de recursos ou identifique um grupo de recursos existente para a implantação.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="ef0bf-196">Crie um recurso do endereço IP público e um recurso NIC para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="ef0bf-197">Para obter as etapas para criar uma rede virtual, endereço IP público e NIC usando a CLI, confira o que foi escrito anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="ef0bf-198">(o**azure vm create** também pode criar uma NIC, mas você precisa passar parâmetros adicionais para uma rede virtual e uma sub-rede.)</span><span class="sxs-lookup"><span data-stu-id="ef0bf-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="ef0bf-199">Em seguida, execute um comando que passa URIs para o novo arquivo de VHD do sistema operacional e a imagem existente.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="ef0bf-200">Neste exemplo, um tamanho de VM Standard_A1 é criado na região Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="ef0bf-201">Para obter opções adicionais de comando, execute `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="ef0bf-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef0bf-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef0bf-202">Next steps</span></span>
<span data-ttu-id="ef0bf-203">Para gerenciar suas VMs com a CLI, consulte as tarefas em [Implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de Recursos do Azure e a CLI do Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="ef0bf-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

