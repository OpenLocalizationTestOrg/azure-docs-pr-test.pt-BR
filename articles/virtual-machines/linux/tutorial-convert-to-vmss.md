---
title: conjunto de escala de tooa uma VM do Azure aaaConvert | Microsoft Docs
description: "Crie e implante uma escala de máquina virtual do Linux Azure com hello CLI do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="a7dd1-103">Converter um conjunto de escala de tooa de máquina virtual do Azure existente</span><span class="sxs-lookup"><span data-stu-id="a7dd1-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="a7dd1-104">Este tutorial mostra como tooconvert toouse 2.0 do CLI do Azure uma escala de máquina virtual de tooa de máquina virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="a7dd1-105">Você também aprenderá como definir a configuração de saudação tooautomate de máquinas virtuais de saudação na escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="a7dd1-106">Para obter mais informações sobre como tooinstall CLI do Azure 2.0, consulte [guia de Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="a7dd1-107">Para obter mais informações sobre conjuntos de dimensionamento, confira [Conjuntos de Dimensionamento de Máquina Virtual](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="a7dd1-108">Etapa 1 - Olá desprovisionamento VM</span><span class="sxs-lookup"><span data-stu-id="a7dd1-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="a7dd1-109">Use SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="a7dd1-110">Saudação de desprovisionamento VM usando hello Azure VM agent toodelete arquivos e dados.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="a7dd1-111">Para obter uma visão geral detalhada do cancelamento do provisionamento, consulte [Capturar uma máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="a7dd1-112">Etapa 2 - capturar uma imagem de VM de saudação</span><span class="sxs-lookup"><span data-stu-id="a7dd1-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="a7dd1-113">Para obter uma visão geral detalhada da captura, consulte [Capturar uma máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="a7dd1-114">Desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="a7dd1-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a7dd1-115">Generalize Olá VM com [az vm generalizar](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="a7dd1-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a7dd1-116">Criar uma imagem do recurso VM Olá com [criar imagem az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="a7dd1-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="a7dd1-117">Etapa 3 - criar conjunto de escala Olá</span><span class="sxs-lookup"><span data-stu-id="a7dd1-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="a7dd1-118">Obter Olá **id** da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="a7dd1-119">Crie uma VM com base no recurso de imagem com [az vmss create](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="a7dd1-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="a7dd1-120">Esse comando também anexou um disco de dados de 10 GB.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="a7dd1-121">Tenha em mente que, dependendo da saudação VM tamanho escolhido (usamos **Standard_DS1_v2**), Olá número de discos de dados permitido é diferente.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="a7dd1-122">Para obter mais informações, examine Olá [tamanhos de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="a7dd1-123">Depois que o conjunto de escala de saudação for concluída, conecte-se tooit.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="a7dd1-124">Obter uma lista de endereços IP para instâncias de saudação para SSH com [az vmss lista-instância-conexão-info](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="a7dd1-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="a7dd1-125">Agora você pode conectar um disco de dados saudação do tooinitialize de instância de máquina virtual toohello</span><span class="sxs-lookup"><span data-stu-id="a7dd1-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="a7dd1-126">Etapa 4 - disco de dados Olá inicializar</span><span class="sxs-lookup"><span data-stu-id="a7dd1-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="a7dd1-127">Enquanto a máquina virtual de toohello conectado, particionar o disco de saudação com `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="a7dd1-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="a7dd1-128">Gravar uma partição de toohello do sistema de arquivos com hello `mkfs` comando:</span><span class="sxs-lookup"><span data-stu-id="a7dd1-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="a7dd1-129">Monte o disco novo Olá para que seja acessível no sistema operacional de saudação:</span><span class="sxs-lookup"><span data-stu-id="a7dd1-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="a7dd1-130">disco Olá agora pode ser acessa por meio de montagem de datadrive hello, que pode ser verificado com `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="a7dd1-131">Olá encerrar a sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="a7dd1-132">Etapa 5 – Configurar o firewall</span><span class="sxs-lookup"><span data-stu-id="a7dd1-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="a7dd1-133">Fazem uma tachinha Olá firewall toohello servidor da Web hospedado pelo conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="a7dd1-134">Quando o conjunto de escala Olá foi criado, um balanceador de carga também foi criado e você o usou **SSH** toohello máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="a7dd1-135">tooopen uma porta, você precisa de duas informações, que pode ser obtido usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="a7dd1-136">**Pool de endereços IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="a7dd1-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="a7dd1-137">**Pool de endereços IP de back-end**</span><span class="sxs-lookup"><span data-stu-id="a7dd1-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="a7dd1-138">Com esses dois nomes, você pode abrir a porta **80**.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="a7dd1-139">Etapa 6 – Automatizar a configuração</span><span class="sxs-lookup"><span data-stu-id="a7dd1-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="a7dd1-140">disco de dados Olá precisa toobe configurado em cada instância de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="a7dd1-141">É possível automatizar a configuração de Olá da máquina virtual Olá Olá **CustomScript** extensão.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="a7dd1-142">Primeiro, crie um *. sh* script que inclui comandos de formatação de disco hello.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="a7dd1-143">Em seguida, carregar esse Olá de toowhere do arquivo de script **CustomScript** extensão pode acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="a7dd1-144">Uma cópia está disponível [aqui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="a7dd1-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="a7dd1-145">Crie um arquivo local chamado **settings.json** e coloque hello seguinte bloco JSON nele.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="a7dd1-146">Olá `flieUris` propriedade deve ser definida como toowhere carregado o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="a7dd1-147">Implantar essa escala de tooyour de comando com hello **CustomScript** extensão, referenciando Olá **settings.json** arquivo que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="a7dd1-148">Essa extensão é executada automaticamente em todas as instâncias e em todas as instâncias criadas posteriormente pelo dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="a7dd1-149">Etapa 7 – Configurar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="a7dd1-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="a7dd1-150">Atualmente, as regras de dimensionamento automático não podem ser definidas na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="a7dd1-151">Saudação de uso [portal do Azure](https://portal.azure.com) tooconfigure AutoEscala.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="a7dd1-152">Etapa 8 – Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a7dd1-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="a7dd1-153">Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="a7dd1-154">Além disso, convém toocreate scripts que automatizam várias tarefas de ciclo de vida e Olá CLI do Azure fornece uma maneira rápida toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="a7dd1-155">Estas são algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="a7dd1-156">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="a7dd1-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="a7dd1-157">Definir a contagem de instâncias (escala manual)</span><span class="sxs-lookup"><span data-stu-id="a7dd1-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="a7dd1-158">Excluir grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a7dd1-158">Delete resource group</span></span>

<span data-ttu-id="a7dd1-159">Excluir um grupo de recursos exclui todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="a7dd1-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a7dd1-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a7dd1-160">Next steps</span></span>
<span data-ttu-id="a7dd1-161">toolearn mais sobre escala de máquinas virtuais Olá definir recursos apresentados neste tutorial, consulte Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7dd1-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="a7dd1-162">Visão geral dos conjuntos de dimensionamento de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="a7dd1-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="a7dd1-163">Visão geral do Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a7dd1-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="a7dd1-164">Controlar o fluxo de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="a7dd1-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)