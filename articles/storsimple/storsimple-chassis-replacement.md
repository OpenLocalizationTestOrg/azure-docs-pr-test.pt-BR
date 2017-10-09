---
title: "chassi aaaReplace no dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como tooremove e substituir Olá chassi do compartimento principal do StorSimple ou compartimento EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="e2d75-103">Substitua o chassi Olá em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="e2d75-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="e2d75-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2d75-104">Overview</span></span>
<span data-ttu-id="e2d75-105">Este tutorial explica como tooremove e substituir um chassi em um dispositivo da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="e2d75-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="e2d75-106">modelo de saudação StorSimple 8100 é um dispositivo de compartimento simples (um chassi), enquanto Olá 8600 é um dispositivo de compartimento duplo (dois chassis).</span><span class="sxs-lookup"><span data-stu-id="e2d75-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="e2d75-107">Para um modelo 8600, há potencialmente dois chassis que podem falhar em dispositivo Olá: Olá chassi do compartimento principal hello ou chassi Olá Olá compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="e2d75-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="e2d75-108">Em ambos os casos, o chassi de substituição de saudação que é fornecido pela Microsoft está vazio.</span><span class="sxs-lookup"><span data-stu-id="e2d75-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="e2d75-109">Não será incluído nenhum módulos de energia e resfriamento (PCM), módulo de controlador, unidade de disco de estado sólido (SSD), unidade de disco rígido (HD) ou módulos EBOD.</span><span class="sxs-lookup"><span data-stu-id="e2d75-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2d75-110">Antes de remover e substituir o chassi hello, revise as informações de segurança de Olá em [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="e2d75-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="e2d75-111">Remover o chassi Olá</span><span class="sxs-lookup"><span data-stu-id="e2d75-111">Remove hello chassis</span></span>
<span data-ttu-id="e2d75-112">Execute Olá chassi de saudação do tooremove as etapas a seguir em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2d75-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="e2d75-113">tooremove um chassi</span><span class="sxs-lookup"><span data-stu-id="e2d75-113">tooremove a chassis</span></span>
1. <span data-ttu-id="e2d75-114">Verifique se o dispositivo StorSimple Olá é desligado e desconectado de todas as fontes de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="e2d75-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="e2d75-115">Remova todos os cabos SAS e rede hello, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="e2d75-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="e2d75-116">Remova a unidade de saudação do rack hello.</span><span class="sxs-lookup"><span data-stu-id="e2d75-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="e2d75-117">Remova cada uma das unidades hello e observe os slots de saudação do qual eles serão removidos.</span><span class="sxs-lookup"><span data-stu-id="e2d75-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="e2d75-118">Para obter mais informações, consulte [remover a unidade de disco Olá](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="e2d75-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="e2d75-119">No hello compartimento EBOD (se esse for o chassi Olá que falhou), remova módulos do controlador EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="e2d75-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="e2d75-120">Para obter mais informações, consulte [Remover um controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="e2d75-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="e2d75-121">No hello compartimento principal (se esse for o chassi Olá que falhou), remova Olá controladores e observe os slots de saudação do qual eles serão removidos.</span><span class="sxs-lookup"><span data-stu-id="e2d75-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="e2d75-122">Para obter mais informações, consulte [Remover um controlador](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="e2d75-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="e2d75-123">Instalar o chassi Olá</span><span class="sxs-lookup"><span data-stu-id="e2d75-123">Install hello chassis</span></span>
<span data-ttu-id="e2d75-124">Execute Olá chassi de saudação do tooinstall as etapas a seguir em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2d75-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="e2d75-125">tooinstall um chassi</span><span class="sxs-lookup"><span data-stu-id="e2d75-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="e2d75-126">Monte o chassi Olá em rack hello.</span><span class="sxs-lookup"><span data-stu-id="e2d75-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="e2d75-127">Para saber mais, confira [Montar em rack o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montar em rack o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="e2d75-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="e2d75-128">Depois de saudação chassi estiver montado no rack hello, instale módulos do controlador Olá no hello que mesmas posições que estavam instaladas anteriormente no.</span><span class="sxs-lookup"><span data-stu-id="e2d75-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="e2d75-129">Olá instalar unidades em Olá mesmo posiciona e slots que elas estavam instaladas anteriormente no.</span><span class="sxs-lookup"><span data-stu-id="e2d75-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e2d75-130">É recomendável que você instala Olá SSDs nos slots de saudação primeiro e, em seguida, instala Olá HDDs.</span><span class="sxs-lookup"><span data-stu-id="e2d75-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="e2d75-131">Com hello dispositivo montado no rack hello e componentes Olá instalados, se conectar a fontes de alimentação apropriadas de toohello seu dispositivo e Ativar dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="e2d75-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="e2d75-132">Para obter detalhes, confira [Cabear o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Cabear o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="e2d75-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2d75-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2d75-133">Next steps</span></span>
<span data-ttu-id="e2d75-134">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="e2d75-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

