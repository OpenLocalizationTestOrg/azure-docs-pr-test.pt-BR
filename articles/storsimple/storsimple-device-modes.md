---
title: "o modo do dispositivo StorSimple aaaChange Olá | Microsoft Docs"
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="433b8-103">Alterar o modo de dispositivo Olá em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="433b8-103">Change hello device mode on your StorSimple device</span></span>
<span data-ttu-id="433b8-104">Este artigo fornece uma breve descrição da saudação vários modos em que o seu dispositivo StorSimple pode operar.</span><span class="sxs-lookup"><span data-stu-id="433b8-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="433b8-105">O dispositivo StorSimple pode funcionar em três modos: normal, manutenção e recuperação.</span><span class="sxs-lookup"><span data-stu-id="433b8-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="433b8-106">Após ler este artigo, você conhecerá:</span><span class="sxs-lookup"><span data-stu-id="433b8-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="433b8-107">Quais são os modos do dispositivo StorSimple Olá</span><span class="sxs-lookup"><span data-stu-id="433b8-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="433b8-108">Como toofigure o modo de Olá dispositivo StorSimple está em</span><span class="sxs-lookup"><span data-stu-id="433b8-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="433b8-109">Como toochange de modo toomaintenance normal e *vice-versa*</span><span class="sxs-lookup"><span data-stu-id="433b8-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="433b8-110">Olá acima tarefas de gerenciamento só pode ser executada por meio da interface do Windows PowerShell de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="433b8-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="433b8-111">Sobre os modos do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="433b8-111">About StorSimple device modes</span></span>
<span data-ttu-id="433b8-112">O dispositivo StorSimple pode operar nos modos normal, de manutenção ou de recuperação.</span><span class="sxs-lookup"><span data-stu-id="433b8-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="433b8-113">Cada um desses modos é descrito resumidamente abaixo.</span><span class="sxs-lookup"><span data-stu-id="433b8-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="433b8-114">Modo Normal</span><span class="sxs-lookup"><span data-stu-id="433b8-114">Normal mode</span></span>
<span data-ttu-id="433b8-115">Isso é definido como modo operacional normal de saudação para um dispositivo StorSimple totalmente configurado.</span><span class="sxs-lookup"><span data-stu-id="433b8-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="433b8-116">Por padrão, o dispositivo deve estar no modo normal.</span><span class="sxs-lookup"><span data-stu-id="433b8-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="433b8-117">Modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="433b8-117">Maintenance mode</span></span>
<span data-ttu-id="433b8-118">Às vezes, hello dispositivo StorSimple pode ser necessário toobe colocado em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="433b8-119">Esse modo permite que você tooperform manutenção no dispositivo de saudação e instalar atualizações sem interrupção, como aquelas relacionadas toodisk firmware.</span><span class="sxs-lookup"><span data-stu-id="433b8-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="433b8-120">Você pode colocar o sistema de saudação em modo de manutenção por meio de saudação do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="433b8-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="433b8-121">Todas as solicitações de E/S são pausadas neste modo.</span><span class="sxs-lookup"><span data-stu-id="433b8-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="433b8-122">Serviços, como a memória de acesso aleatório não volátil (NVRAM) ou Olá serviço também são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="433b8-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="433b8-123">Ambos os controladores de saudação são reiniciados quando você entra ou sai deste modo.</span><span class="sxs-lookup"><span data-stu-id="433b8-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="433b8-124">Quando você sair do modo de manutenção hello, todos os serviços de saudação serão retomada e devem ser íntegros.</span><span class="sxs-lookup"><span data-stu-id="433b8-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="433b8-125">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="433b8-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="433b8-126">**Só há suporte ao modo de Manutenção em um dispositivo que esteja funcionando corretamente. Não há suporte em um dispositivo no qual um ou ambos os controladores de saudação não estão funcionando.**
> </span><span class="sxs-lookup"><span data-stu-id="433b8-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="433b8-127">Modo de recuperação</span><span class="sxs-lookup"><span data-stu-id="433b8-127">Recovery mode</span></span>
<span data-ttu-id="433b8-128">O modo de recuperação pode ser descrito como "Modo Seguro do Windows com suporte de rede".</span><span class="sxs-lookup"><span data-stu-id="433b8-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="433b8-129">Modo de recuperação aciona a equipe do Microsoft Support hello e permite tooperform diagnósticos no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="433b8-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="433b8-130">Olá principal objetivo do modo de recuperação é tooretrieve Olá sistema logs.</span><span class="sxs-lookup"><span data-stu-id="433b8-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="433b8-131">Se o sistema entrar no modo de recuperação, você deverá contatar o Suporte da Microsoft para obter as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="433b8-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="433b8-132">Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="433b8-132">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="433b8-133">**Você não pode colocar o dispositivo Olá no modo de recuperação. Se o dispositivo de saudação está em um estado inválido, o modo de recuperação tenta tooget dispositivo de saudação em um estado em que a equipe do Microsoft Support possa examiná-lo.**</span><span class="sxs-lookup"><span data-stu-id="433b8-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="433b8-134">Determinar o modo do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="433b8-134">Determine StorSimple device mode</span></span>
#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="433b8-135">modo de dispositivo toodetermine Olá atual</span><span class="sxs-lookup"><span data-stu-id="433b8-135">toodetermine hello current device mode</span></span>
1. <span data-ttu-id="433b8-136">Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="433b8-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="433b8-137">Examine a mensagem de saudação do banner no menu do console serial saudação do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="433b8-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="433b8-138">Esta mensagem indica explicitamente se o dispositivo hello está no modo de manutenção ou recuperação.</span><span class="sxs-lookup"><span data-stu-id="433b8-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="433b8-139">Se a mensagem de saudação não contém informações específicas relativas toohello modo de sistema, o dispositivo de saudação está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="433b8-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="433b8-140">Alterar o modo de saudação do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="433b8-140">Change hello StorSimple device mode</span></span>
<span data-ttu-id="433b8-141">Você pode colocar o dispositivo StorSimple Olá em manutenção de tooperform modo (no modo normal) de manutenção ou instalar atualizações do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="433b8-142">Execute Olá modo de manutenção de tooenter ou sair de procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="433b8-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="433b8-143">Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros acessando Olá **Status do Hardware** em Olá **manutenção** página Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="433b8-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="433b8-144">Se um ou ambos os controladores de saudação não estão íntegros, entre em contato com o Microsoft Support para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="433b8-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="433b8-145">Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="433b8-145">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="433b8-146">modo de manutenção de tooenter</span><span class="sxs-lookup"><span data-stu-id="433b8-146">tooenter maintenance mode</span></span>
1. <span data-ttu-id="433b8-147">Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="433b8-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="433b8-148">No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="433b8-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="433b8-149">Quando solicitado, forneça Olá **senha de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="433b8-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="433b8-150">Olá a senha padrão é: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="433b8-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="433b8-151">No prompt de comando hello, digite</span><span class="sxs-lookup"><span data-stu-id="433b8-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="433b8-152">Você verá uma mensagem de aviso informando que o modo de manutenção irá interromper todas as solicitações de e/s e servidor Olá conexão toohello portal clássico do Azure, e você será solicitado a confirmar.</span><span class="sxs-lookup"><span data-stu-id="433b8-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="433b8-153">Tipo **Y** tooenter modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="433b8-154">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="433b8-154">Both controllers will restart.</span></span> <span data-ttu-id="433b8-155">Quando a saudação reinicialização é concluída, outra mensagem será exibida indicando que o dispositivo hello está no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-155">When hello restart is complete, another message will appear indicating that hello device is in maintenance mode.</span></span>

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="433b8-156">modo de manutenção de tooexit</span><span class="sxs-lookup"><span data-stu-id="433b8-156">tooexit maintenance mode</span></span>
1. <span data-ttu-id="433b8-157">Faça logon no console serial do dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="433b8-157">Log on toohello device serial console.</span></span> <span data-ttu-id="433b8-158">Verificar da mensagem de saudação do banner que seu dispositivo está no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-158">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="433b8-159">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="433b8-159">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="433b8-160">Uma mensagem de aviso e uma mensagem de confirmação serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="433b8-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="433b8-161">Tipo **Y** tooexit modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="433b8-161">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="433b8-162">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="433b8-162">Both controllers will restart.</span></span> <span data-ttu-id="433b8-163">Quando a saudação reinicialização é concluída, outra mensagem será exibida indicando que o dispositivo Olá está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="433b8-163">When hello restart is complete, another message will appear indicating that hello device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="433b8-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="433b8-164">Next steps</span></span>
<span data-ttu-id="433b8-165">Saiba como muito[aplicar as atualizações do modo normal e manutenção](storsimple-update-device.md) em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="433b8-165">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

