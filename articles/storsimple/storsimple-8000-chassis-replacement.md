---
title: "Substituir o chassi no dispositivo StorSimple série 8000 | Microsoft Docs"
description: "Descreve como remover e substituir o chassi em seu compartimento StorSimple primário ou compartimento EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 073fcf0064f1d1482f4683d733f00cf918ff2f38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="b51c5-103">Substituir o chassi em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b51c5-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="b51c5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b51c5-104">Overview</span></span>
<span data-ttu-id="b51c5-105">Esse tutorial explica como remover e substituir um chassi em um dispositivo StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="b51c5-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="b51c5-106">O modelo StorSimple 8100 é um dispositivo de compartimento único (um chassi), enquanto o 8600 é um dispositivo de compartimento duplo (dois chassis).</span><span class="sxs-lookup"><span data-stu-id="b51c5-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="b51c5-107">No modelo 8600, há potencialmente dois chassis que podem falhar no dispositivo: o chassi do compartimento primário ou o chassi do compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="b51c5-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="b51c5-108">Em ambos os casos, o chassi de substituição enviado pela Microsoft estará vazio.</span><span class="sxs-lookup"><span data-stu-id="b51c5-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="b51c5-109">Não será incluído nenhum módulos de energia e resfriamento (PCM), módulo de controlador, unidade de disco de estado sólido (SSD), unidade de disco rígido (HD) ou módulos EBOD.</span><span class="sxs-lookup"><span data-stu-id="b51c5-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b51c5-110">Antes de remover e substituir p chassi, examine as informações de segurança em [Substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b51c5-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-chassis"></a><span data-ttu-id="b51c5-111">Remover o chassi</span><span class="sxs-lookup"><span data-stu-id="b51c5-111">Remove the chassis</span></span>
<span data-ttu-id="b51c5-112">Execute as seguintes etapas para remover o chassi em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b51c5-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="b51c5-113">Para remover um chassi</span><span class="sxs-lookup"><span data-stu-id="b51c5-113">To remove a chassis</span></span>
1. <span data-ttu-id="b51c5-114">Certifique-se de que o dispositivo StorSimple esteja desligado e desconectado de todas as fontes de alimentação.</span><span class="sxs-lookup"><span data-stu-id="b51c5-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="b51c5-115">Remova todos os cabos SAS e de rede, se houver.</span><span class="sxs-lookup"><span data-stu-id="b51c5-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="b51c5-116">Remova a unidade do rack.</span><span class="sxs-lookup"><span data-stu-id="b51c5-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="b51c5-117">Remova cada uma das unidades e observe os slots do quais são removidas.</span><span class="sxs-lookup"><span data-stu-id="b51c5-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="b51c5-118">Para obter mais informações, consulte [Remover a unidade de disco](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="b51c5-118">For more information, see [Remove the disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="b51c5-119">No compartimento EBOD (se for o chassi com falha), remova os módulos do controlador EBOD.</span><span class="sxs-lookup"><span data-stu-id="b51c5-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="b51c5-120">Para obter mais informações, consulte [Remover um controlador EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="b51c5-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="b51c5-121">No compartimento primário (se for o chassi com falha), remova os controladores e observe os slots dos quais são removidos.</span><span class="sxs-lookup"><span data-stu-id="b51c5-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="b51c5-122">Para obter mais informações, consulte [Remover um controlador](storsimple-8000-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="b51c5-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="b51c5-123">Instalar o chassi</span><span class="sxs-lookup"><span data-stu-id="b51c5-123">Install the chassis</span></span>
<span data-ttu-id="b51c5-124">Execute as seguintes etapas para instalar o chassi em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b51c5-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="b51c5-125">Para instalar um chassi</span><span class="sxs-lookup"><span data-stu-id="b51c5-125">To install a chassis</span></span>
1. <span data-ttu-id="b51c5-126">Monte o chassi no rack.</span><span class="sxs-lookup"><span data-stu-id="b51c5-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="b51c5-127">Para saber mais, confira [Montar em rack o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montar em rack o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="b51c5-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="b51c5-128">Depois que o chassis estiver montado no rack, instale os módulos do controlador nas mesmas posições que eles estavam instalados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b51c5-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="b51c5-129">Instale as unidades nas mesmas posições e slots de que elas estavam instaladas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b51c5-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b51c5-130">É recomendável instalar primeiro os SSDs nos slots e, em seguida, instalar os HDDs.</span><span class="sxs-lookup"><span data-stu-id="b51c5-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
  
4. <span data-ttu-id="b51c5-131">Com o dispositivo montado no rack e os componentes instalados, conecte o dispositivo nas fontes de alimentação apropriadas e ligue o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b51c5-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="b51c5-132">Para obter detalhes, confira [Cabear o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Cabear o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="b51c5-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b51c5-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b51c5-133">Next steps</span></span>
<span data-ttu-id="b51c5-134">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b51c5-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

