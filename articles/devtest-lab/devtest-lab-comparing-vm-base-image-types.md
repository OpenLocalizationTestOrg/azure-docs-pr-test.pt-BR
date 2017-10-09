---
title: "aaaComparing imagens personalizadas e as fórmulas em DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre as diferenças de saudação entre imagens personalizadas e as fórmulas como bases de VM para que você possa decidir qual mais adequada para seu ambiente."
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
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="741c8-103">Comparando imagens personalizadas e fórmulas em Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="741c8-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="741c8-104">É possível usar tanto as [imagens personalizadas](devtest-lab-create-template.md) quanto as [fórmulas](devtest-lab-manage-formulas.md) como bases para as [novas VMs criadas](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="741c8-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="741c8-105">No entanto, a principal diferença Olá entre imagens personalizadas e as fórmulas é uma imagem personalizada é simplesmente uma imagem com base em um VHD, enquanto uma fórmula é uma imagem com base em um VHD *além* pré-configurado configurações - como tamanho da VM, uma rede virtual, subrede e artefatos.</span><span class="sxs-lookup"><span data-stu-id="741c8-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="741c8-106">Essas configurações predefinidas são configuradas com valores padrão que podem ser substituídos no tempo de saudação da criação de VM.</span><span class="sxs-lookup"><span data-stu-id="741c8-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="741c8-107">Este artigo explica algumas das vantagens de saudação (profissionais) e desvantagens imagens personalizadas do toousing (contras) versus usando fórmulas.</span><span class="sxs-lookup"><span data-stu-id="741c8-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="741c8-108">Prós e contras das imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="741c8-108">Custom image pros and cons</span></span>
<span data-ttu-id="741c8-109">Imagens personalizadas fornecem um modo estático, imutável toocreate VMs de um ambiente desejado.</span><span class="sxs-lookup"><span data-stu-id="741c8-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="741c8-110">**Prós**</span><span class="sxs-lookup"><span data-stu-id="741c8-110">**Pros**</span></span>

* <span data-ttu-id="741c8-111">Provisionamento de uma imagem personalizada da VM é rápida como nada muda após Olá que passe VM da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="741c8-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="741c8-112">Em outras palavras, não há nenhum tooapply configurações como imagem personalizada Olá é apenas uma imagem sem configurações.</span><span class="sxs-lookup"><span data-stu-id="741c8-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="741c8-113">VMs criadas por meio de uma única imagem personalizada são idênticas.</span><span class="sxs-lookup"><span data-stu-id="741c8-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="741c8-114">**Contras**</span><span class="sxs-lookup"><span data-stu-id="741c8-114">**Cons**</span></span>

* <span data-ttu-id="741c8-115">Se você precisar tooupdate algum aspecto da imagem personalizada do hello, imagem Olá deve ser recriada.</span><span class="sxs-lookup"><span data-stu-id="741c8-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="741c8-116">Prós e contras da fórmula</span><span class="sxs-lookup"><span data-stu-id="741c8-116">Formula pros and cons</span></span>
<span data-ttu-id="741c8-117">Fórmulas fornecem uma maneira dinâmica toocreate VMs do hello desejado configurações.</span><span class="sxs-lookup"><span data-stu-id="741c8-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="741c8-118">**Prós**</span><span class="sxs-lookup"><span data-stu-id="741c8-118">**Pros**</span></span>

* <span data-ttu-id="741c8-119">Alterações no ambiente de saudação podem ser capturadas em Olá instantaneamente por meio de artefatos.</span><span class="sxs-lookup"><span data-stu-id="741c8-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="741c8-120">Por exemplo, se você desejar uma VM instalada com o bits mais recentes de saudação do seu pipeline de versão ou inscrever-se código mais recente de saudação do seu repositório, você simplesmente especificar um artefato que implanta os bits mais recentes hello ou inscreve código mais recente de saudação na fórmula Olá junto com um imagem de base de destino.</span><span class="sxs-lookup"><span data-stu-id="741c8-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="741c8-121">Sempre que essa fórmula é usada toocreate VMs, Olá bits/código mais recente são implantados/inscrito toohello VM.</span><span class="sxs-lookup"><span data-stu-id="741c8-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="741c8-122">As fórmulas podem definir as configurações padrão que as imagens personalizadas não podem fornecer, como configurações de rede virtual e tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="741c8-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="741c8-123">configurações de saudação salvos em uma fórmula são mostradas como valores padrão, mas podem ser modificadas quando Olá VM é criada.</span><span class="sxs-lookup"><span data-stu-id="741c8-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="741c8-124">**Contras**</span><span class="sxs-lookup"><span data-stu-id="741c8-124">**Cons**</span></span>

* <span data-ttu-id="741c8-125">Criar uma VM por meio de uma fórmula pode levar mais tempo do que criar uma VM por meio de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="741c8-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="741c8-126">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="741c8-126">Related blog posts</span></span>
* [<span data-ttu-id="741c8-127">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="741c8-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="741c8-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="741c8-128">Next steps</span></span>
- [<span data-ttu-id="741c8-129">Perguntas frequentes do DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="741c8-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)