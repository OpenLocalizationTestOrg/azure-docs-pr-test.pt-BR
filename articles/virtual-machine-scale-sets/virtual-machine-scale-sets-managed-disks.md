---
title: "aaaUsing gerenciados discos com o Azure escala conjuntos de máquinas virtuais | Microsoft Docs"
description: "Saiba por que e como toouse gerenciados discos com conjuntos de escala de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="94fd2-103">Conjuntos de dimensionamento de VMs do Azure e discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="94fd2-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="94fd2-104">Os [conjuntos de dimensionamento de máquinas virtuais](/azure/virtual-machine-scale-sets/) do Azure oferecem suporte a máquinas virtuais com discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="94fd2-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="94fd2-105">O uso de discos gerenciados com conjuntos de dimensionamento tem vários benefícios, incluindo:</span><span class="sxs-lookup"><span data-stu-id="94fd2-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="94fd2-106">Você não precisa mais toopre-criar e gerenciar os discos de armazenamento de contas toostore Olá SO para VMs do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="94fd2-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="94fd2-107">Você pode anexar um conjunto de escala de toohello de discos de dados gerenciados.</span><span class="sxs-lookup"><span data-stu-id="94fd2-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="94fd2-108">Com o disco gerenciado, um conjunto de dimensionamento poderá ter a capacidade de até 1.000 VMs se for baseado em uma imagem de plataforma, ou 100 VMs se for baseado em uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="94fd2-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="94fd2-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="94fd2-109">Get started</span></span>

<span data-ttu-id="94fd2-110">Uma maneira simples tooget iniciado com conjuntos de escala de disco gerenciado é toodeploy de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94fd2-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="94fd2-111">Para obter mais informações, consulte [este artigo](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="94fd2-112">Outra maneira simple tooget iniciado é toouse [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy uma escala definida.</span><span class="sxs-lookup"><span data-stu-id="94fd2-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="94fd2-113">Olá exemplo a seguir mostra como toocreate um Ubuntu com base em escala com 10 VMs, cada um com um disco de 50 GB e 100 GB de dados:</span><span class="sxs-lookup"><span data-stu-id="94fd2-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="94fd2-114">Como alternativa, você pode examinar Olá [repositório GitHub de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) para pastas que contêm `vmss` toosee pré-criadas exemplos de modelos que implantar conjuntos de escala.</span><span class="sxs-lookup"><span data-stu-id="94fd2-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="94fd2-115">tootell quais modelos já estiver usando discos gerenciados, você pode consultar muito[essa lista](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94fd2-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94fd2-116">Next steps</span></span>

<span data-ttu-id="94fd2-117">Para obter mais informações sobre discos gerenciados em geral, confira [este artigo](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="94fd2-118">toosee como tooconvert conjuntos de uma escala de tooprovision de modelo do Gerenciador de recursos com gerenciado discos, consulte [neste artigo](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="94fd2-119">Olá, modelos de Gerenciador de recursos do mesmo modificações toohello aplicam toohello API REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="94fd2-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="94fd2-120">toolearn mais sobre como usar discos de dados gerenciado com conjuntos de escala, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="94fd2-121">toobegin trabalhando com conjuntos de grande escala, consulte muito[neste artigo](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="94fd2-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


