---
title: aaaCreate e gerenciar VMs do Linux com hello CLI do Azure | Microsoft Docs
description: "Tutorial - criar e gerenciar máquinas virtuais Linux com hello CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="576ef-103">Criar e gerenciar máquinas virtuais Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="576ef-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="576ef-104">Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível.</span><span class="sxs-lookup"><span data-stu-id="576ef-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="576ef-105">Este tutorial aborda itens básicos de implantação de máquina virtual do Azure, como a seleção de um tamanho de VM, seleção de uma imagem de VM e implantação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="576ef-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="576ef-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="576ef-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="576ef-107">Criar e conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="576ef-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="576ef-108">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-108">Select and use VM images</span></span>
> * <span data-ttu-id="576ef-109">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="576ef-110">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="576ef-110">Resize a VM</span></span>
> * <span data-ttu-id="576ef-111">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="576ef-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="576ef-112">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="576ef-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="576ef-113">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="576ef-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="576ef-114">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="576ef-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="576ef-115">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="576ef-115">Create resource group</span></span>

<span data-ttu-id="576ef-116">Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="576ef-117">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="576ef-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="576ef-118">Você deve criar um grupo de recursos antes de criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="576ef-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="576ef-119">Neste exemplo, um grupo de recursos denominado *myResourceGroupVM* é criado no hello *eastus* região.</span><span class="sxs-lookup"><span data-stu-id="576ef-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="576ef-120">grupo de recursos de saudação é especificado ao criar ou modificar uma VM, que pode ser vista em todo este tutorial.</span><span class="sxs-lookup"><span data-stu-id="576ef-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="576ef-121">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="576ef-121">Create virtual machine</span></span>

<span data-ttu-id="576ef-122">Criar uma máquina virtual com hello [criar vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="576ef-123">Há várias opções disponíveis ao criar uma máquina virtual, como a imagem do sistema operacional, as credenciais administrativas e o dimensionamento do disco.</span><span class="sxs-lookup"><span data-stu-id="576ef-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="576ef-124">Neste exemplo, criaremos uma máquina virtual chamada *myVM* no Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="576ef-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="576ef-125">Uma vez Olá que VM foi criada, Olá CLI do Azure gera informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="576ef-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="576ef-126">Anote Olá `publicIpAddress`, esse endereço pode ser usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="576ef-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="576ef-127">Conecte-se tooVM</span><span class="sxs-lookup"><span data-stu-id="576ef-127">Connect tooVM</span></span>

<span data-ttu-id="576ef-128">Agora você pode conectar toohello VM usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="576ef-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="576ef-129">Substitua o endereço IP de exemplo hello com hello `publicIpAddress` anotados na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="576ef-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="576ef-130">Depois de concluir Olá VM, feche a sessão SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="576ef-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="576ef-131">Entender as imagens de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-131">Understand VM images</span></span>

<span data-ttu-id="576ef-132">Olá marketplace do Azure inclui muitas imagens que podem ser usados toocreate VMs.</span><span class="sxs-lookup"><span data-stu-id="576ef-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="576ef-133">Nas etapas anteriores do hello, uma máquina virtual foi criada usando uma imagem do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="576ef-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="576ef-134">Nesta etapa, Olá que CLI do Azure é marketplace de saudação toosearch usado para uma imagem CentOS, que é então usado toodeploy uma segunda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="576ef-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="576ef-135">toosee uma lista de saudação imagens usadas mais comumente, use Olá [lista de imagens de vm az](/cli/azure/vm/image#list) comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="576ef-136">saída do comando Olá retorna imagens da VM mais populares Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="576ef-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="576ef-137">Uma lista completa pode ser vista adicionando Olá `--all` argumento.</span><span class="sxs-lookup"><span data-stu-id="576ef-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="576ef-138">lista de imagens Olá também pode ser filtrada por `--publisher` ou `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="576ef-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="576ef-139">Neste exemplo, lista de saudação é filtrada para todas as imagens com uma oferta que corresponde a *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="576ef-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="576ef-140">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="576ef-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="576ef-141">toodeploy uma VM usando uma imagem específica, anote o valor de Olá Olá *Urn* coluna.</span><span class="sxs-lookup"><span data-stu-id="576ef-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="576ef-142">Ao especificar a imagem de hello, número de versão de imagem Olá pode ser substituído por "mais recente", que seleciona a versão mais recente de saudação da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="576ef-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="576ef-143">Neste exemplo, Olá `--image` argumento é usado toospecify versão mais recente do hello de uma imagem CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="576ef-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="576ef-144">Entender os tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-144">Understand VM sizes</span></span>

<span data-ttu-id="576ef-145">Um tamanho de máquina virtual determina a quantidade de saudação de recursos de computação, como memória, CPU e GPU que são feitas a máquina virtual de toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="576ef-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="576ef-146">Máquinas virtuais precisam toobe dimensionada apropriadamente para carga de trabalho Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="576ef-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="576ef-147">Se a carga de trabalho aumentar, uma máquina virtual existente pode ser redimensionada.</span><span class="sxs-lookup"><span data-stu-id="576ef-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="576ef-148">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-148">VM Sizes</span></span>

<span data-ttu-id="576ef-149">Olá, a tabela a seguir categoriza tamanhos em casos de uso.</span><span class="sxs-lookup"><span data-stu-id="576ef-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="576ef-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="576ef-150">Type</span></span>                     | <span data-ttu-id="576ef-151">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="576ef-151">Sizes</span></span>           |    <span data-ttu-id="576ef-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="576ef-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="576ef-153">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="576ef-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="576ef-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="576ef-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="576ef-155">CPU/memória equilibrados.</span><span class="sxs-lookup"><span data-stu-id="576ef-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="576ef-156">Ideal para desenvolvimento / teste e pequenas toomedium soluções de aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="576ef-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="576ef-157">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="576ef-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="576ef-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="576ef-158">Fs, F</span></span>             | <span data-ttu-id="576ef-159">Relação de CPU/memória alta.</span><span class="sxs-lookup"><span data-stu-id="576ef-159">High CPU-to-memory.</span></span> <span data-ttu-id="576ef-160">Boa para aplicativos de tráfego médio, dispositivos de rede e processos em lote.</span><span class="sxs-lookup"><span data-stu-id="576ef-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="576ef-161">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="576ef-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="576ef-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="576ef-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="576ef-163">Relação de memória/núcleo alta.</span><span class="sxs-lookup"><span data-stu-id="576ef-163">High memory-to-core.</span></span> <span data-ttu-id="576ef-164">Excelente para bancos de dados relacionais, caches toolarge médios e análise de memória.</span><span class="sxs-lookup"><span data-stu-id="576ef-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="576ef-165">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="576ef-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="576ef-166">Ls</span><span class="sxs-lookup"><span data-stu-id="576ef-166">Ls</span></span>                | <span data-ttu-id="576ef-167">Alta taxa de transferência de disco e de E/S.</span><span class="sxs-lookup"><span data-stu-id="576ef-167">High disk throughput and IO.</span></span> <span data-ttu-id="576ef-168">Ideal para Big Data, SQL e bancos de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="576ef-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="576ef-169">GPU</span><span class="sxs-lookup"><span data-stu-id="576ef-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="576ef-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="576ef-170">NV, NC</span></span>            | <span data-ttu-id="576ef-171">VMs especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.</span><span class="sxs-lookup"><span data-stu-id="576ef-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="576ef-172">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="576ef-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="576ef-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="576ef-173">H, A8-11</span></span>          | <span data-ttu-id="576ef-174">Nossas VMs de CPU mais potentes com adaptadores de rede de alto rendimento (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="576ef-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="576ef-175">Encontrar tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="576ef-175">Find available VM sizes</span></span>

<span data-ttu-id="576ef-176">toosee uma lista de VM tamanhos disponíveis em uma determinada região, use Olá [lista-tamanhos de vm az](/cli/azure/vm#list-sizes) comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="576ef-177">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="576ef-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="576ef-178">Criar VM com um tamanho específico</span><span class="sxs-lookup"><span data-stu-id="576ef-178">Create VM with specific size</span></span>

<span data-ttu-id="576ef-179">No exemplo de criação VM anterior hello, um tamanho não foi fornecida, que resulta em um tamanho padrão.</span><span class="sxs-lookup"><span data-stu-id="576ef-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="576ef-180">Um tamanho de VM pode ser selecionado no momento da criação usando [criar vm az](/cli/azure/vm#create) e hello `--size` argumento.</span><span class="sxs-lookup"><span data-stu-id="576ef-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="576ef-181">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="576ef-181">Resize a VM</span></span>

<span data-ttu-id="576ef-182">Depois que uma máquina virtual foi implantada, pode ser redimensionada tooincrease ou diminuir a alocação de recursos.</span><span class="sxs-lookup"><span data-stu-id="576ef-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="576ef-183">Antes de redimensionar uma VM, verifique se hello tamanho desejado está disponível no cluster do Azure atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="576ef-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="576ef-184">Olá [az vm lista-vm--opções de redimensionamento](/cli/azure/vm#list-vm-resize-options) Olá retorna a lista de tamanhos de comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="576ef-185">Se Olá desejado tamanho estiver disponível, hello VM pode ser redimensionada de um estado ligado, mas ele é reinicializado durante a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="576ef-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="576ef-186">Saudação de uso [az vm redimensionar]( /cli/azure/vm#resize) comando tooperform Olá redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="576ef-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="576ef-187">Se o tamanho desejado de saudação não está em cluster atual hello, Olá VM necessidades toobe desalocada antes da operação de redimensionamento Olá pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="576ef-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="576ef-188">Saudação de uso [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comando e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="576ef-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="576ef-189">Observe que quando hello VM está ligada novamente, os dados no disco temporário Olá podem ser removidos.</span><span class="sxs-lookup"><span data-stu-id="576ef-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="576ef-190">endereço IP público de saudação também altera a menos que um endereço IP estático está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="576ef-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="576ef-191">Depois de desalocada, Olá redimensionamento pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="576ef-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="576ef-192">Depois de redimensionar hello, Olá VM pode ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="576ef-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="576ef-193">Estados de energia da VM</span><span class="sxs-lookup"><span data-stu-id="576ef-193">VM power states</span></span>

<span data-ttu-id="576ef-194">Uma VM do Azure pode ter um dentre vários estados de energia.</span><span class="sxs-lookup"><span data-stu-id="576ef-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="576ef-195">Nesse estado representa o estado atual de saudação do hello VM do ponto de vista de saudação do hipervisor Olá.</span><span class="sxs-lookup"><span data-stu-id="576ef-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="576ef-196">Estados de energia</span><span class="sxs-lookup"><span data-stu-id="576ef-196">Power states</span></span>

| <span data-ttu-id="576ef-197">Estado de energia</span><span class="sxs-lookup"><span data-stu-id="576ef-197">Power State</span></span> | <span data-ttu-id="576ef-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="576ef-198">Description</span></span>
|----|----|
| <span data-ttu-id="576ef-199">Iniciando</span><span class="sxs-lookup"><span data-stu-id="576ef-199">Starting</span></span> | <span data-ttu-id="576ef-200">Indica a máquina virtual de hello está sendo iniciada.</span><span class="sxs-lookup"><span data-stu-id="576ef-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="576ef-201">Executando</span><span class="sxs-lookup"><span data-stu-id="576ef-201">Running</span></span> | <span data-ttu-id="576ef-202">Indica que a máquina virtual hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="576ef-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="576ef-203">Parando</span><span class="sxs-lookup"><span data-stu-id="576ef-203">Stopping</span></span> | <span data-ttu-id="576ef-204">Indica que a máquina virtual hello está sendo interrompida.</span><span class="sxs-lookup"><span data-stu-id="576ef-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="576ef-205">Parada</span><span class="sxs-lookup"><span data-stu-id="576ef-205">Stopped</span></span> | <span data-ttu-id="576ef-206">Indica que a máquina virtual hello está parada.</span><span class="sxs-lookup"><span data-stu-id="576ef-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="576ef-207">Máquinas virtuais no estado interrompido de saudação ainda incorrerá em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="576ef-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="576ef-208">Desalocando</span><span class="sxs-lookup"><span data-stu-id="576ef-208">Deallocating</span></span> | <span data-ttu-id="576ef-209">Indica que a máquina virtual hello está sendo desalocada.</span><span class="sxs-lookup"><span data-stu-id="576ef-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="576ef-210">Desalocada</span><span class="sxs-lookup"><span data-stu-id="576ef-210">Deallocated</span></span> | <span data-ttu-id="576ef-211">Indica que a máquina virtual Olá é removido da saudação hipervisor, mas ainda está disponível no plano de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="576ef-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="576ef-212">Máquinas virtuais no estado desalocada da saudação não incorrerá em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="576ef-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="576ef-213">Indica que o estado de energia de saudação da máquina virtual de saudação é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="576ef-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="576ef-214">Localizar o estado de energia</span><span class="sxs-lookup"><span data-stu-id="576ef-214">Find power state</span></span>

<span data-ttu-id="576ef-215">estado de saudação tooretrieve de uma VM específica, use Olá [az vm obter exibição de instância](/cli/azure/vm#get-instance-view) comando.</span><span class="sxs-lookup"><span data-stu-id="576ef-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="576ef-216">Ser toospecify se um nome válido para uma máquina virtual e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="576ef-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="576ef-217">Saída:</span><span class="sxs-lookup"><span data-stu-id="576ef-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="576ef-218">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="576ef-218">Management tasks</span></span>

<span data-ttu-id="576ef-219">Durante a saudação ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="576ef-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="576ef-220">Além disso, talvez você queira toocreate scripts tooautomate repetitivas ou complexas tarefas.</span><span class="sxs-lookup"><span data-stu-id="576ef-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="576ef-221">Usando Olá CLI do Azure, muitas tarefas comuns de gerenciamento podem ser executadas da linha de comando hello, ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="576ef-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="576ef-222">Como obter o endereço IP</span><span class="sxs-lookup"><span data-stu-id="576ef-222">Get IP address</span></span>

<span data-ttu-id="576ef-223">Esse comando retorna os endereços IP públicos e privados de saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="576ef-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="576ef-224">Como interromper uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="576ef-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="576ef-225">Como iniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="576ef-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="576ef-226">Excluir grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="576ef-226">Delete resource group</span></span>

<span data-ttu-id="576ef-227">Excluir um grupo de recursos exclui todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="576ef-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="576ef-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="576ef-228">Next steps</span></span>

<span data-ttu-id="576ef-229">Neste tutorial, você aprendeu sobre a criação e o gerenciamento básico de VM e como:</span><span class="sxs-lookup"><span data-stu-id="576ef-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="576ef-230">Criar e conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="576ef-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="576ef-231">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-231">Select and use VM images</span></span>
> * <span data-ttu-id="576ef-232">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="576ef-233">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="576ef-233">Resize a VM</span></span>
> * <span data-ttu-id="576ef-234">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="576ef-234">View and understand VM state</span></span>

<span data-ttu-id="576ef-235">Avançar toohello toolearn próximo de tutorial sobre discos de VM.</span><span class="sxs-lookup"><span data-stu-id="576ef-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="576ef-236">Criar e gerenciar discos de VM</span><span class="sxs-lookup"><span data-stu-id="576ef-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
