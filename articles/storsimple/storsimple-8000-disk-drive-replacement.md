---
title: "aaaReplace uma unidade de disco em um dispositivo da série StorSimple 8000 | Microsoft Docs"
description: Explica como tooreplace um disco da unidade em um compartimento principal do StorSimple ou um compartimento EBOD.
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="be20e-103">Substituir uma unidade de disco em um dispositivo StorSimple da série 8000</span><span class="sxs-lookup"><span data-stu-id="be20e-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="be20e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="be20e-104">Overview</span></span>
<span data-ttu-id="be20e-105">Este tutorial explica como remover e substituir uma unidade de disco rígido com defeito ou com falha em um dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="be20e-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="be20e-106">tooreplace uma unidade de disco, você precisa:</span><span class="sxs-lookup"><span data-stu-id="be20e-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="be20e-107">Solte o bloqueio inviolável Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="be20e-108">Remova a unidade de disco de saudação</span><span class="sxs-lookup"><span data-stu-id="be20e-108">Remove hello disk drive</span></span>
* <span data-ttu-id="be20e-109">Instalar a unidade de disco de substituição Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be20e-110">Antes de remover e substituir uma unidade de disco, revise as informações de segurança de saudação em [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="be20e-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="be20e-111">Solte o bloqueio inviolável Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="be20e-112">Este procedimento explica como os bloqueios invioláveis de saudação em seu dispositivo StorSimple podem ser encaixados ou desencaixados ao substituir Olá unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="be20e-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="be20e-113">bloqueios invioláveis Olá são encaixados nas alças da portadora unidade hello e eles são acessados por meio de uma pequena abertura na seção de trava de saudação do identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="be20e-114">As unidades são fornecidas com hello bloqueios conjunto toohello bloqueado posição.</span><span class="sxs-lookup"><span data-stu-id="be20e-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="be20e-115">bloqueio inviolável do toounlock Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="be20e-116">Insira cuidadosamente a chave de bloqueio de saudação (uma fenda T10 "inviolável" que a Microsoft forneceu) na abertura de saudação na alça de saudação e no soquete.</span><span class="sxs-lookup"><span data-stu-id="be20e-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="be20e-117">Se ativar o bloqueio inviolável hello, indicador Olá vermelho estará visível na abertura de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Unidade de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="be20e-119">**Figura 1** Bloqueio antiviolação ativado</span><span class="sxs-lookup"><span data-stu-id="be20e-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="be20e-120">Rótulo</span><span class="sxs-lookup"><span data-stu-id="be20e-120">Label</span></span> | <span data-ttu-id="be20e-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="be20e-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="be20e-122">1</span><span class="sxs-lookup"><span data-stu-id="be20e-122">1</span></span> |<span data-ttu-id="be20e-123">Abertura do indicador</span><span class="sxs-lookup"><span data-stu-id="be20e-123">Indicator aperture</span></span> |
   | <span data-ttu-id="be20e-124">2</span><span class="sxs-lookup"><span data-stu-id="be20e-124">2</span></span> |<span data-ttu-id="be20e-125">Bloqueio antiviolação</span><span class="sxs-lookup"><span data-stu-id="be20e-125">Antitamper lock</span></span> |
2. <span data-ttu-id="be20e-126">Rotação da chave de saudação no sentido anti-horário até que o indicador vermelho de saudação não estiver visível na abertura de saudação acima chave hello.</span><span class="sxs-lookup"><span data-stu-id="be20e-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="be20e-127">Remova a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-127">Remove hello key.</span></span>
   
    ![Unidade de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="be20e-129">**Figura 2** Unidade de disco desbloqueada</span><span class="sxs-lookup"><span data-stu-id="be20e-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="be20e-130">unidade de disco Olá agora podem ser removida.</span><span class="sxs-lookup"><span data-stu-id="be20e-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="be20e-131">Siga as etapas de saudação no bloqueio de saudação tooengage inversa.</span><span class="sxs-lookup"><span data-stu-id="be20e-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="be20e-132">Remova a unidade de disco de saudação</span><span class="sxs-lookup"><span data-stu-id="be20e-132">Remove hello disk drive</span></span>
<span data-ttu-id="be20e-133">O dispositivo StorSimple dá suporte a uma configuração de espaços de armazenamento similar a RAID 10.</span><span class="sxs-lookup"><span data-stu-id="be20e-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="be20e-134">Isso significa que ele pode operar normalmente com um disco com falha, unidade de estado sólido (SSD) ou unidade de disco rígido (HD).</span><span class="sxs-lookup"><span data-stu-id="be20e-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="be20e-135">Se o sistema tiver mais de um disco com falha, não remova mais de um SSD ou HDD do sistema hello em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="be20e-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="be20e-136">Isso pode resultar em perda de dados.</span><span class="sxs-lookup"><span data-stu-id="be20e-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="be20e-137">Lembre-se de colocar um SSD de reposição em um slot que continha anteriormente um SSD.</span><span class="sxs-lookup"><span data-stu-id="be20e-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="be20e-138">Da mesma forma, coloque um HDD de reposição em um slot que continha anteriormente um HDD.</span><span class="sxs-lookup"><span data-stu-id="be20e-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="be20e-139">Em Olá portal do Azure, as entradas são numeradas de 0 a 11.</span><span class="sxs-lookup"><span data-stu-id="be20e-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="be20e-140">Portanto, se o portal de saudação mostra que um disco no slot 2 falhou, no dispositivo Olá, procure Olá o disco com falha no terceiro slot de saudação do hello superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="be20e-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="be20e-141">Unidades podem ser removidas e substituídas enquanto o sistema hello está funcionando.</span><span class="sxs-lookup"><span data-stu-id="be20e-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="be20e-142">tooremove uma unidade</span><span class="sxs-lookup"><span data-stu-id="be20e-142">tooremove a drive</span></span>
1. <span data-ttu-id="be20e-143">Olá tooidentify falha de disco, em Olá portal do Azure, vá tooyour dispositivo **Configurações > integridade do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="be20e-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="be20e-144">Como um disco pode falhar no compartimento primário hello e/ou em um compartimento EBOD (se você estiver usando um modelo 8600), examinar status Olá de discos de saudação em **componentes compartilhados** e, em **componentes compartilhados do EBOD** .</span><span class="sxs-lookup"><span data-stu-id="be20e-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="be20e-145">Um disco com falha em um compartimento será mostrado com  status vermelho.</span><span class="sxs-lookup"><span data-stu-id="be20e-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="be20e-146">Localize Olá unidades na frente de saudação do compartimento principal hello ou compartimento do EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="be20e-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="be20e-147">Se o disco Olá estiver desbloqueado, continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="be20e-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="be20e-148">Se Olá disco estiver bloqueado, desbloqueá-lo seguindo o procedimento Olá [desencaixar o bloqueio inviolável Olá](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="be20e-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="be20e-149">Pressione Olá preto trava no módulo Olá de portador de unidade e puxe a alça do portador da unidade Olá para fora da frente de saudação do chassi de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Liberando a alça da unidade de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="be20e-151">**Figura 3** liberando identificador de unidade de saudação</span><span class="sxs-lookup"><span data-stu-id="be20e-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="be20e-152">Quando a alça do portador da unidade Olá estiver totalmente expandida, deslize o portador da unidade de saudação fora do chassi de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Deslizando o disco para fora da unidade de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="be20e-154">**Figura 4** deslizante Olá a unidade de disco fora da portadora Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="be20e-155">Instalar a unidade de disco de substituição Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="be20e-156">Depois de uma unidade falhou no seu dispositivo StorSimple e removê-lo, siga este procedimento tooreplace com uma nova unidade.</span><span class="sxs-lookup"><span data-stu-id="be20e-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="be20e-157">tooinsert uma unidade</span><span class="sxs-lookup"><span data-stu-id="be20e-157">tooinsert a drive</span></span>
1. <span data-ttu-id="be20e-158">Verifique a alça do portador da unidade hello está totalmente estendida, conforme mostrado no Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="be20e-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Unidade de disco com alça estendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="be20e-160">**Figura 5** Unidade com alça estendida</span><span class="sxs-lookup"><span data-stu-id="be20e-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="be20e-161">Deslize o portador da unidade de saudação todo caminho de saudação no chassi hello.</span><span class="sxs-lookup"><span data-stu-id="be20e-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Deslizando o disco para dentro do suporte da unidade de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="be20e-163">**Figura 6** portador da unidade de saudação deslizante no chassi Olá</span><span class="sxs-lookup"><span data-stu-id="be20e-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="be20e-164">Com hello unidade operadora Olá inserido, feche unidade operadora identificador ao continuando toopush Olá portador da unidade no chassi hello, até que a alça do portador da unidade Olá chegue à posição bloqueada.</span><span class="sxs-lookup"><span data-stu-id="be20e-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="be20e-165">Use Olá chave de bloqueio fornecida pela alça do portador da Microsoft (de fenda Torx inviolável) toosecure Olá no lugar ativando o parafuso de bloqueio Olá um quarto de volta no sentido horário.</span><span class="sxs-lookup"><span data-stu-id="be20e-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="be20e-166">Verifique se Olá substituição foi bem-sucedida e unidade hello está funcionando.</span><span class="sxs-lookup"><span data-stu-id="be20e-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="be20e-167">Acessar Olá portal do Azure e navegar muito**configurações** > **a integridade do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="be20e-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="be20e-168">Em **componentes compartilhados** ou **componentes compartilhados do EBOD**, status da unidade Olá deve estar verde, indicando que ele esteja íntegro.</span><span class="sxs-lookup"><span data-stu-id="be20e-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="be20e-169">Ele pode levar algumas horas para Olá disco status tooturn verde após a substituição de saudação.</span><span class="sxs-lookup"><span data-stu-id="be20e-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="be20e-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be20e-170">Next steps</span></span>
<span data-ttu-id="be20e-171">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="be20e-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

