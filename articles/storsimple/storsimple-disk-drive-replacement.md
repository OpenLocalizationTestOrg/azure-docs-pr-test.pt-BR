---
title: Substituir uma unidade de disco em um dispositivo StorSimple | Microsoft Docs
description: "Explica como substituir uma unidade de disco em um compartimento primário StorSimple ou em um compartimento EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="758ce-103">Substituir uma unidade de disco em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="758ce-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="758ce-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="758ce-104">Overview</span></span>
<span data-ttu-id="758ce-105">Este tutorial explica como remover e substituir uma unidade de disco rígido com defeito ou com falha em um dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="758ce-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="758ce-106">Para trocar uma unidade de disco, é necessário:</span><span class="sxs-lookup"><span data-stu-id="758ce-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="758ce-107">Soltar o bloqueio antiviolação</span><span class="sxs-lookup"><span data-stu-id="758ce-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="758ce-108">Remover a unidade de disco</span><span class="sxs-lookup"><span data-stu-id="758ce-108">Remove the disk drive</span></span>
* <span data-ttu-id="758ce-109">Instalar a unidade de disco de reposição</span><span class="sxs-lookup"><span data-stu-id="758ce-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="758ce-110">Antes de remover e substituir uma unidade de disco, examine as informações de segurança em [Substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="758ce-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="758ce-111">Soltar o bloqueio antiviolação</span><span class="sxs-lookup"><span data-stu-id="758ce-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="758ce-112">Este procedimento explica como os bloqueios antiviolação em seu dispositivo StorSimple podem ser ativados ou desativados ao substituir as unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="758ce-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="758ce-113">Os bloqueios antiviolação são ajustados nas alças do suporte da unidade e são acessados por meio de uma abertura pequena na parte da trava da alça.</span><span class="sxs-lookup"><span data-stu-id="758ce-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="758ce-114">As unidades são fornecidas com os bloqueios na posição travada.</span><span class="sxs-lookup"><span data-stu-id="758ce-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="758ce-115">Para destravar o bloqueio antiviolação</span><span class="sxs-lookup"><span data-stu-id="758ce-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="758ce-116">Cuidadosamente, insira a chave de bloqueio (uma chave de fenda T10 "à prova de violações" fornecidos pela Microsoft) no encaixe da abertura da alça.</span><span class="sxs-lookup"><span data-stu-id="758ce-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="758ce-117">Se o bloqueio antiviolação estiver ativado, o indicador vermelho ficará visível na abertura.</span><span class="sxs-lookup"><span data-stu-id="758ce-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Unidade de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="758ce-119">**Figura 1** Bloqueio antiviolação ativado</span><span class="sxs-lookup"><span data-stu-id="758ce-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="758ce-120">Rótulo</span><span class="sxs-lookup"><span data-stu-id="758ce-120">Label</span></span> | <span data-ttu-id="758ce-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="758ce-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="758ce-122">1</span><span class="sxs-lookup"><span data-stu-id="758ce-122">1</span></span> |<span data-ttu-id="758ce-123">Abertura do indicador</span><span class="sxs-lookup"><span data-stu-id="758ce-123">Indicator aperture</span></span> |
   | <span data-ttu-id="758ce-124">2</span><span class="sxs-lookup"><span data-stu-id="758ce-124">2</span></span> |<span data-ttu-id="758ce-125">Bloqueio antiviolação</span><span class="sxs-lookup"><span data-stu-id="758ce-125">Antitamper lock</span></span> |
2. <span data-ttu-id="758ce-126">Gire a chave no sentido anti-horário até que o indicador vermelho não esteja visível na abertura acima da chave.</span><span class="sxs-lookup"><span data-stu-id="758ce-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="758ce-127">Remova a chave.</span><span class="sxs-lookup"><span data-stu-id="758ce-127">Remove the key.</span></span>
   
    ![Unidade de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="758ce-129">**Figura 2** Unidade de disco desbloqueada</span><span class="sxs-lookup"><span data-stu-id="758ce-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="758ce-130">A unidade de disco agora pode ser removida.</span><span class="sxs-lookup"><span data-stu-id="758ce-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="758ce-131">Siga as etapas na ordem inversa para ativar o bloqueio.</span><span class="sxs-lookup"><span data-stu-id="758ce-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="758ce-132">Remover a unidade de disco</span><span class="sxs-lookup"><span data-stu-id="758ce-132">Remove the disk drive</span></span>
<span data-ttu-id="758ce-133">O dispositivo StorSimple dá suporte a uma configuração de espaços de armazenamento similar a RAID 10.</span><span class="sxs-lookup"><span data-stu-id="758ce-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="758ce-134">Isso significa que ele pode operar normalmente com um disco com falha, unidade de estado sólido (SSD) ou unidade de disco rígido (HD).</span><span class="sxs-lookup"><span data-stu-id="758ce-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="758ce-135">Se o seu sistema tiver mais de um disco com falha, nunca remova mais de um SSD ou HDD do sistema.</span><span class="sxs-lookup"><span data-stu-id="758ce-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="758ce-136">Isso pode resultar em perda de dados.</span><span class="sxs-lookup"><span data-stu-id="758ce-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="758ce-137">Lembre-se de colocar um SSD de reposição em um slot que continha anteriormente um SSD.</span><span class="sxs-lookup"><span data-stu-id="758ce-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="758ce-138">Da mesma forma, coloque um HDD de reposição em um slot que continha anteriormente um HDD.</span><span class="sxs-lookup"><span data-stu-id="758ce-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="758ce-139">No Portal clássico do Azure, os slots são numerados de 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="758ce-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="758ce-140">Portanto, se o portal mostra que um disco no slot 2 falhou, no dispositivo, localize o disco com falha no terceiro slot da parte superior esquerda.</span><span class="sxs-lookup"><span data-stu-id="758ce-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="758ce-141">As unidades podem ser removidas e substituídas enquanto o sistema estiver funcionando.</span><span class="sxs-lookup"><span data-stu-id="758ce-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="758ce-142">Para remover uma unidade</span><span class="sxs-lookup"><span data-stu-id="758ce-142">To remove a drive</span></span>
1. <span data-ttu-id="758ce-143">Para identificar o disco com falha, no portal clássico do Azure, acesse **Dispositivos** > **Manutenção** > **Status de Hardware**.</span><span class="sxs-lookup"><span data-stu-id="758ce-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="758ce-144">Como um disco pode falhar no compartimento primário e/ou em um compartimento EBOD (se você estiver usando um modelo 8600), observe o status dos discos em **Componentes Compartilhados** e em **Componentes Compartilhados do compartimento EBOD**.</span><span class="sxs-lookup"><span data-stu-id="758ce-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="758ce-145">Um disco com falha em um compartimento será mostrado com  status vermelho.</span><span class="sxs-lookup"><span data-stu-id="758ce-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="758ce-146">Localize as unidades na frente do compartimento primário ou do compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="758ce-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="758ce-147">Se o disco estiver desbloqueado, prossiga para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="758ce-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="758ce-148">Se o disco estiver bloqueado, desbloqueie-o seguindo o procedimento [Desativar o bloqueio antiviolação](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="758ce-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="758ce-149">Pressione a trava preta no módulo do suporte da unidade e puxe a alça do suporte da unidade para fora da parte frontal do chassi.</span><span class="sxs-lookup"><span data-stu-id="758ce-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Liberando a alça da unidade de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="758ce-151">**Figura 3** Liberação da alça da unidade</span><span class="sxs-lookup"><span data-stu-id="758ce-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="758ce-152">Quando a alça do suporte da unidade estiver totalmente estendida, deslize o suporte da unidade para fora do chassi.</span><span class="sxs-lookup"><span data-stu-id="758ce-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Deslizando o disco para fora da unidade de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="758ce-154">**Figura 4** Deslizando a unidade de disco para fora do suporte</span><span class="sxs-lookup"><span data-stu-id="758ce-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="758ce-155">Instalar a unidade de disco de reposição</span><span class="sxs-lookup"><span data-stu-id="758ce-155">Install the replacement disk drive</span></span>
<span data-ttu-id="758ce-156">Após uma falha de unidade em seu dispositivo StorSimple e depois que você removê-la, siga este procedimento para substituí-la por uma nova unidade.</span><span class="sxs-lookup"><span data-stu-id="758ce-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="758ce-157">Para inserir uma unidade</span><span class="sxs-lookup"><span data-stu-id="758ce-157">To insert a drive</span></span>
1. <span data-ttu-id="758ce-158">Verifique se que a alça do suporte da unidade está totalmente estendida, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="758ce-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Unidade de disco com alça estendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="758ce-160">**Figura 5** Unidade com alça estendida</span><span class="sxs-lookup"><span data-stu-id="758ce-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="758ce-161">Deslize o suporte da unidade completamente para dentro do chassi.</span><span class="sxs-lookup"><span data-stu-id="758ce-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Deslizando o disco para dentro do suporte da unidade de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="758ce-163">**Figura 6** Deslizando o suporte da unidade para dentro do chassi</span><span class="sxs-lookup"><span data-stu-id="758ce-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="758ce-164">Com o suporte da unidade inserido, feche a alça do suporte enquanto continua a empurrar o suporte da unidade para dentro do chassi, até que a alça se encaixe na posição travada.</span><span class="sxs-lookup"><span data-stu-id="758ce-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="758ce-165">Use a chave de bloqueio que foi fornecida pela Microsoft (chave de fenda Torx à prova de violações) para prender a alça do suporte no lugar girando os parafusos um quarto de volta no sentido horário.</span><span class="sxs-lookup"><span data-stu-id="758ce-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="758ce-166">Verifique se a substituição foi bem-sucedida e se a unidade está funcionando acessando o portal clássico do Azure e navegando até **Manutenção** > **Status de Hardware**.</span><span class="sxs-lookup"><span data-stu-id="758ce-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="758ce-167">Em **Componentes Compartilhados** ou **Componentes Compartilhados do compartimento EBOD**, o status da unidade deverá ficar verde, indicando que está íntegra.</span><span class="sxs-lookup"><span data-stu-id="758ce-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="758ce-168">Pode levar várias horas até que o status do disco fique verde após a troca.</span><span class="sxs-lookup"><span data-stu-id="758ce-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="758ce-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="758ce-169">Next steps</span></span>
<span data-ttu-id="758ce-170">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="758ce-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

