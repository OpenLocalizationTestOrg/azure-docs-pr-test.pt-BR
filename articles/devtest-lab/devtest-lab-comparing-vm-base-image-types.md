---
title: "Comparando as imagens personalizadas e as fórmulas nos DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre as diferenças entre imagens personalizadas e fórmulas como bases de VM para que você possa decidir qual é mais adequada para seu ambiente."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="5dbe8-103">Comparando imagens personalizadas e fórmulas em Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="5dbe8-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="5dbe8-104">É possível usar tanto as [imagens personalizadas](devtest-lab-create-template.md) quanto as [fórmulas](devtest-lab-manage-formulas.md) como bases para as [novas VMs criadas](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="5dbe8-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="5dbe8-105">No entanto, a principal diferença entre fórmulas e imagens personalizadas é que uma imagem personalizada é simplesmente uma imagem baseada em um VHD, enquanto uma fórmula é uma imagem baseada em um VHD, *além de* definições pré-configuradas, como tamanho da VM, rede virtual, sub-rede e artefatos.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="5dbe8-106">Essas configurações pré-configuradas são definidas com valores padrão que podem ser substituídos no momento da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="5dbe8-107">Este artigo explica algumas das vantagens (prós) e desvantagens (contras) de usar imagens personalizadas versus usar fórmulas.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="5dbe8-108">Prós e contras das imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="5dbe8-108">Custom image pros and cons</span></span>
<span data-ttu-id="5dbe8-109">As imagens personalizadas fornecem uma maneira estática e imutável para criar VMs em um ambiente desejado.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="5dbe8-110">**Prós**</span><span class="sxs-lookup"><span data-stu-id="5dbe8-110">**Pros**</span></span>

* <span data-ttu-id="5dbe8-111">O provisionamento da VM de uma imagem personalizada é rápido, uma vez que nada muda depois que a VM é criada por meio da imagem.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="5dbe8-112">Em outras palavras, não há nenhuma configuração a ser aplicada, uma vez que a imagem personalizada é apenas uma imagem sem configurações.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="5dbe8-113">VMs criadas por meio de uma única imagem personalizada são idênticas.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="5dbe8-114">**Contras**</span><span class="sxs-lookup"><span data-stu-id="5dbe8-114">**Cons**</span></span>

* <span data-ttu-id="5dbe8-115">Se você precisar atualizar algum aspecto da imagem personalizada, a imagem precisará ser recriada.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="5dbe8-116">Prós e contras da fórmula</span><span class="sxs-lookup"><span data-stu-id="5dbe8-116">Formula pros and cons</span></span>
<span data-ttu-id="5dbe8-117">As fórmulas fornecem uma maneira dinâmica de criar VMs por meio das configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="5dbe8-118">**Prós**</span><span class="sxs-lookup"><span data-stu-id="5dbe8-118">**Pros**</span></span>

* <span data-ttu-id="5dbe8-119">As alterações no ambiente podem ser capturadas em tempo real por meio de artefatos.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="5dbe8-120">Por exemplo, se você deseja uma VM instalada com os bits mais recentes do seu pipeline de lançamento ou inscrever o código mais recente do seu repositório, pode especificar simplesmente um artefato que implanta os bits mais recentes ou inscreve o código mais recente na fórmula juntamente com uma imagem base de destino.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="5dbe8-121">Sempre que essa fórmula é usada para criar VMs, os bits/códigos mais recentes são implantados/inscritos na VM.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="5dbe8-122">As fórmulas podem definir as configurações padrão que as imagens personalizadas não podem fornecer, como configurações de rede virtual e tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="5dbe8-123">As configurações salvas em uma fórmula são exibidas como valores padrão, mas podem ser modificadas quando a VM é criada.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="5dbe8-124">**Contras**</span><span class="sxs-lookup"><span data-stu-id="5dbe8-124">**Cons**</span></span>

* <span data-ttu-id="5dbe8-125">Criar uma VM por meio de uma fórmula pode levar mais tempo do que criar uma VM por meio de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="5dbe8-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="5dbe8-126">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="5dbe8-126">Related blog posts</span></span>
* [<span data-ttu-id="5dbe8-127">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="5dbe8-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="5dbe8-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dbe8-128">Next steps</span></span>
- [<span data-ttu-id="5dbe8-129">Perguntas frequentes do DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5dbe8-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)