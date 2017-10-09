---
title: aaaCapture toouse uma VM do Linux do Azure como um modelo | Microsoft Docs
description: "Saiba como toocapture e generalizar a imagem de uma baseados em Linux do Azure máquina virtual (VM) criada com o modelo de implantação do Azure Resource Manager hello."
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
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="40c8b-103">Capturar uma máquina virtual do Linux em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="40c8b-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="40c8b-104">Siga as etapas de saudação toogeneralize neste artigo e capturar sua máquina virtual do Linux do Azure (VM) no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="40c8b-105">Quando você generaliza Olá VM, você remove informações pessoais da conta e preparar Olá VM toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="40c8b-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="40c8b-106">Em seguida, você captura a imagem de um disco rígido virtual (VHD) generalizado para Olá SO VHDs para discos de dados anexado, e um [modelo do Gerenciador de recursos](../../azure-resource-manager/resource-group-overview.md) para novas implantações de VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="40c8b-107">Este artigo fornece detalhes sobre como toocapture uma VM da imagem com hello 1.0 da CLI do Azure para uma máquina virtual usando discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="40c8b-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="40c8b-108">Você também pode [capturar uma VM com discos gerenciado do Azure hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40c8b-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40c8b-109">Discos gerenciados são tratados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los.</span><span class="sxs-lookup"><span data-stu-id="40c8b-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="40c8b-110">Para saber mais, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40c8b-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="40c8b-111">toocreate VMs usando imagem hello, configurar recursos de rede para cada nova VM e usar toodeploy de modelo (um arquivo JavaScript Object Notation ou JSON,) de saudação do hello capturar imagens de VHD.</span><span class="sxs-lookup"><span data-stu-id="40c8b-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="40c8b-112">Dessa forma, você pode replicar uma VM com sua configuração atual do software, modo toohello semelhante, você use imagens em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="40c8b-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="40c8b-113">Se você quiser toocreate uma cópia da VM Linux existente com seu estado especializado para backup ou a depuração, consulte [criar uma cópia de uma máquina virtual do Linux em execução no Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40c8b-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40c8b-114">E se você quiser tooupload um VHD de uma VM do local do Linux, consulte [carregar e criar uma VM do Linux de imagem de disco personalizado](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40c8b-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="40c8b-115">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="40c8b-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="40c8b-116">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="40c8b-117">[1.0 de CLI do Azure](#before-you-begin) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="40c8b-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="40c8b-118">[2.0 do CLI do Azure](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="40c8b-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="40c8b-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="40c8b-119">Before you begin</span></span>
<span data-ttu-id="40c8b-120">Certifique-se de atender Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="40c8b-121">**VM do Azure criada no modelo de implantação do Gerenciador de recursos de saudação** -se você não criou uma VM do Linux, você pode usar o hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Olá [CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ou [Gerenciador de recursos modelos de](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="40c8b-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="40c8b-122">Configure Olá VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="40c8b-122">Configure hello VM as needed.</span></span> <span data-ttu-id="40c8b-123">Por exemplo, [adicionar discos de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aplicar atualizações e instalar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="40c8b-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="40c8b-124">**CLI do Azure** -Olá Install [CLI do Azure](../../cli-install-nodejs.md) em um computador local.</span><span class="sxs-lookup"><span data-stu-id="40c8b-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="40c8b-125">Etapa 1: Remover agente do Linux Azure Olá</span><span class="sxs-lookup"><span data-stu-id="40c8b-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="40c8b-126">Primeiro execute Olá **waagent** com hello **desprovisionamento** parâmetro hello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="40c8b-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="40c8b-127">Esse comando exclui os arquivos e dados toomake Olá pronto para generalizar da VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="40c8b-128">Para obter detalhes, consulte Olá [guia do usuário do agente Linux do Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40c8b-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="40c8b-129">Conecte-se tooyour VM do Linux usando um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="40c8b-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="40c8b-130">Na janela SSH hello, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="40c8b-131">Somente execute esse comando em uma máquina virtual que você pretende toocapture como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="40c8b-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="40c8b-132">Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para redistribuição.</span><span class="sxs-lookup"><span data-stu-id="40c8b-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="40c8b-133">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="40c8b-133">Type **y** toocontinue.</span></span> <span data-ttu-id="40c8b-134">Você pode adicionar Olá **-force** parâmetro tooavoid essa etapa de confirmação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="40c8b-135">Após a conclusão do comando hello, digite **sair**.</span><span class="sxs-lookup"><span data-stu-id="40c8b-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="40c8b-136">Esta etapa fecha cliente SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="40c8b-137">Etapa 2: Capturar Olá VM</span><span class="sxs-lookup"><span data-stu-id="40c8b-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="40c8b-138">Use Olá CLI do Azure toogeneralize e capturar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="40c8b-139">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="40c8b-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="40c8b-140">Os nomes de parâmetro de exemplo incluem **myResourceGroup**, **myVnet** e **myVM**.</span><span class="sxs-lookup"><span data-stu-id="40c8b-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="40c8b-141">Em seu computador local, abra Olá CLI do Azure e [tooyour logon assinatura do Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="40c8b-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="40c8b-142">Certifique-se de estar no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40c8b-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="40c8b-143">Desligar Olá VM que você já desprovisionada usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="40c8b-144">Generalize Olá VM com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="40c8b-145">Agora execute Olá **captura de vm do azure** comando, que captura Olá VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="40c8b-146">Em Olá exemplo a seguir, imagem Olá VHDs são capturados com nomes que começam com **MyVHDNamePrefix**e hello **-t** opção especifica um modelo de caminho de toohello **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="40c8b-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="40c8b-147">os arquivos de imagem do VHD Olá obtenham criados por padrão no hello usada da mesma conta de armazenamento que Olá VM original.</span><span class="sxs-lookup"><span data-stu-id="40c8b-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="40c8b-148">Saudação de uso *mesma conta de armazenamento* toostore Olá VHDs para novas VMs criar da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="40c8b-149">local de saudação toofind de uma imagem capturada, o modelo JSON Olá aberto em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="40c8b-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="40c8b-150">Em Olá **storageProfile**, localize Olá **uri** de saudação **imagem** localizado em Olá **sistema** contêiner.</span><span class="sxs-lookup"><span data-stu-id="40c8b-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="40c8b-151">Por exemplo, hello URI da imagem de disco Olá SO assemelha-se muito`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="40c8b-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="40c8b-152">Etapa 3: Criar uma VM da imagem capturada de saudação</span><span class="sxs-lookup"><span data-stu-id="40c8b-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="40c8b-153">Agora use imagem Olá com um modelo toocreate uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="40c8b-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="40c8b-154">Estas etapas mostram como toouse Olá CLI do Azure e Olá capturados toocreate Olá VM em uma nova rede virtual de modelo de arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="40c8b-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="40c8b-155">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="40c8b-155">Create network resources</span></span>
<span data-ttu-id="40c8b-156">modelo de saudação toouse, primeiro é necessário tooset um NIC e de rede virtual para sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="40c8b-157">Recomendamos que você crie um grupo de recursos para esses recursos no local de saudação onde a imagem VM é armazenada.</span><span class="sxs-lookup"><span data-stu-id="40c8b-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="40c8b-158">Execute comandos semelhante toohello a seguir, substituindo os nomes de seus recursos e um local apropriado do Azure ("centralus" esses comandos):</span><span class="sxs-lookup"><span data-stu-id="40c8b-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="40c8b-159">Obter Olá Id da saudação NIC</span><span class="sxs-lookup"><span data-stu-id="40c8b-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="40c8b-160">toodeploy uma VM da imagem hello usando Olá salvo durante a captura JSON, você precisa Olá Id da saudação NIC.</span><span class="sxs-lookup"><span data-stu-id="40c8b-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="40c8b-161">Obtê-lo executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="40c8b-162">Olá **Id** no Olá a saída é semelhante muito`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="40c8b-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="40c8b-163">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="40c8b-163">Create a VM</span></span>
<span data-ttu-id="40c8b-164">Agora o comando a seguir de execução Olá toocreate sua VM do hello capturar a imagem VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="40c8b-165">Saudação de uso **-f** modelo de toohello parâmetro toospecify Olá caminho JSON do arquivo salvo.</span><span class="sxs-lookup"><span data-stu-id="40c8b-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="40c8b-166">Na saída do comando hello, são solicitada toosupply um novo nome VM, nome de usuário de administrador hello e senha e Olá Id da saudação NIC que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="40c8b-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="40c8b-167">saudação de exemplo a seguir mostra o que você vê uma implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="40c8b-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
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

### <a name="verify-hello-deployment"></a><span data-ttu-id="40c8b-168">Verificar a implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="40c8b-168">Verify hello deployment</span></span>
<span data-ttu-id="40c8b-169">Agora SSH toohello máquina virtual é criada a implantação de saudação tooverify e começar a usar Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="40c8b-170">tooconnect via SSH, localizar o endereço IP de saudação do Olá VM criada executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="40c8b-171">endereço IP público de saudação é listado na saída do comando hello.</span><span class="sxs-lookup"><span data-stu-id="40c8b-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="40c8b-172">Por padrão, você se conectar toohello VM Linux por SSH na porta 22.</span><span class="sxs-lookup"><span data-stu-id="40c8b-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="40c8b-173">Criar VMs adicionais</span><span class="sxs-lookup"><span data-stu-id="40c8b-173">Create additional VMs</span></span>
<span data-ttu-id="40c8b-174">Olá Use capturados toodeploy de imagem e o modelo usar etapas Olá Olá anterior a seção de VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="40c8b-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="40c8b-175">Outra opções toocreate VMs da imagem de saudação incluem usando um modelo de início rápido ou executando Olá **criar vm do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="40c8b-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="40c8b-176">Usar modelo capturada Olá</span><span class="sxs-lookup"><span data-stu-id="40c8b-176">Use hello captured template</span></span>
<span data-ttu-id="40c8b-177">toouse Olá capturada a imagem e o modelo, siga estas etapas (detalhadas no hello anterior seção):</span><span class="sxs-lookup"><span data-stu-id="40c8b-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="40c8b-178">Certifique-se de que a imagem VM está em Olá mesma conta de armazenamento que hospeda o VHD da VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="40c8b-179">Copie o arquivo JSON do modelo hello e especifique um nome exclusivo para o disco do sistema operacional de saudação do VHD Olá nova VM (ou VHDs).</span><span class="sxs-lookup"><span data-stu-id="40c8b-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="40c8b-180">Por exemplo, em Olá **storageProfile**, em **vhd**, na **uri**, especifique um nome exclusivo para Olá **osDisk** VHD, semelhante muito`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="40c8b-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="40c8b-181">Crie uma NIC em qualquer Olá mesmo ou em uma rede virtual diferente.</span><span class="sxs-lookup"><span data-stu-id="40c8b-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="40c8b-182">Usando o arquivo JSON do modelo de saudação modificado, crie uma implantação no grupo de recursos de saudação em que você configura rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="40c8b-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="40c8b-183">Usar um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="40c8b-183">Use a quickstart template</span></span>
<span data-ttu-id="40c8b-184">Se você quiser rede Olá configurada automaticamente quando você cria uma VM da imagem hello, você pode especificar esses recursos em um modelo.</span><span class="sxs-lookup"><span data-stu-id="40c8b-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="40c8b-185">Por exemplo, consulte Olá [modelo 101 vm de usuário imagem](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="40c8b-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="40c8b-186">Este modelo cria uma VM de sua imagem personalizada e de rede virtual necessária hello, endereço IP público e recursos NIC.</span><span class="sxs-lookup"><span data-stu-id="40c8b-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="40c8b-187">Para obter uma explicação de como usar o modelo Olá em Olá portal do Azure, consulte [como uma máquina virtual de uma imagem personalizada usando um modelo do Gerenciador de recursos de toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="40c8b-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="40c8b-188">Use hello azure vm criar comando</span><span class="sxs-lookup"><span data-stu-id="40c8b-188">Use hello azure vm create command</span></span>
<span data-ttu-id="40c8b-189">Geralmente, é mais fácil toouse um modelo de Gerenciador de recursos toocreate uma VM da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="40c8b-190">No entanto, você pode criar hello VM *imperativa* usando Olá **criar vm do azure** com hello **-Q** (**– imagem urn**) parâmetro .</span><span class="sxs-lookup"><span data-stu-id="40c8b-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="40c8b-191">Se você usar esse método, você também pode passar Olá **-d** (**vhd de disco de SO –**) local de saudação do parâmetro toospecify do arquivo. vhd Olá SO Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="40c8b-192">Esse arquivo deve estar no contêiner de vhds Olá Olá da conta de armazenamento onde o arquivo VHD de imagem de saudação é armazenado.</span><span class="sxs-lookup"><span data-stu-id="40c8b-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="40c8b-193">Olá comando cópias hello VHD para Olá nova VM automaticamente toohello **vhds** contêiner.</span><span class="sxs-lookup"><span data-stu-id="40c8b-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="40c8b-194">Antes de executar **criar vm do azure** com imagem hello, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c8b-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="40c8b-195">Criar um grupo de recursos ou identificar o grupo de recursos para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="40c8b-196">Criar um público recurso de endereço IP e um recurso NIC para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="40c8b-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="40c8b-197">Para etapas toocreate uma rede virtual, endereço IP público e NIC usando Olá CLI, consulte neste artigo.</span><span class="sxs-lookup"><span data-stu-id="40c8b-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="40c8b-198">(**criar vm do azure** também pode criar uma NIC, mas você precisa de parâmetros adicionais de toopass para uma rede virtual e sub-rede.)</span><span class="sxs-lookup"><span data-stu-id="40c8b-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="40c8b-199">Em seguida, execute um comando que passa URIs tooboth Olá novo arquivo. VHD do sistema operacional e Olá existente de imagem.</span><span class="sxs-lookup"><span data-stu-id="40c8b-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="40c8b-200">Neste exemplo, um tamanho de VM Standard_A1 é criado na região Leste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c8b-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="40c8b-201">Para obter opções adicionais de comando, execute `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="40c8b-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c8b-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40c8b-202">Next steps</span></span>
<span data-ttu-id="40c8b-203">toomanage suas VMs com hello CLI, consulte tarefas de saudação [implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e Olá CLI do Azure](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="40c8b-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

