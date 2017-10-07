---
title: modo de dispositivo do StorSimple aaaChange | Microsoft Docs
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="79ace-103">Alterar o modo de dispositivo Olá em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="79ace-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="79ace-104">Este artigo fornece uma breve descrição da saudação vários modos em que o seu dispositivo StorSimple pode operar.</span><span class="sxs-lookup"><span data-stu-id="79ace-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="79ace-105">O dispositivo StorSimple pode funcionar em três modos: normal, manutenção e recuperação.</span><span class="sxs-lookup"><span data-stu-id="79ace-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="79ace-106">Após ler este artigo, você conhecerá:</span><span class="sxs-lookup"><span data-stu-id="79ace-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="79ace-107">Quais são os modos do dispositivo StorSimple Olá</span><span class="sxs-lookup"><span data-stu-id="79ace-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="79ace-108">Como toofigure o modo de Olá dispositivo StorSimple está em</span><span class="sxs-lookup"><span data-stu-id="79ace-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="79ace-109">Como toochange de modo toomaintenance normal e *vice-versa*</span><span class="sxs-lookup"><span data-stu-id="79ace-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="79ace-110">Olá acima tarefas de gerenciamento só pode ser executada por meio da interface do Windows PowerShell de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="79ace-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="79ace-111">Sobre os modos do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="79ace-111">About StorSimple device modes</span></span>

<span data-ttu-id="79ace-112">O dispositivo StorSimple pode operar nos modos normal, de manutenção ou de recuperação.</span><span class="sxs-lookup"><span data-stu-id="79ace-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="79ace-113">Cada um desses modos é descrito resumidamente abaixo.</span><span class="sxs-lookup"><span data-stu-id="79ace-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="79ace-114">Modo Normal</span><span class="sxs-lookup"><span data-stu-id="79ace-114">Normal mode</span></span>

<span data-ttu-id="79ace-115">Isso é definido como modo operacional normal de saudação para um dispositivo StorSimple totalmente configurado.</span><span class="sxs-lookup"><span data-stu-id="79ace-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="79ace-116">Por padrão, o dispositivo deve estar no modo normal.</span><span class="sxs-lookup"><span data-stu-id="79ace-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="79ace-117">Modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="79ace-117">Maintenance mode</span></span>

<span data-ttu-id="79ace-118">Às vezes, hello dispositivo StorSimple pode ser necessário toobe colocado em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="79ace-119">Esse modo permite que você tooperform manutenção no dispositivo de saudação e instalar atualizações sem interrupção, como aquelas relacionadas toodisk firmware.</span><span class="sxs-lookup"><span data-stu-id="79ace-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="79ace-120">Você pode colocar o sistema de saudação em modo de manutenção por meio de saudação do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="79ace-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="79ace-121">Todas as solicitações de E/S são pausadas neste modo.</span><span class="sxs-lookup"><span data-stu-id="79ace-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="79ace-122">Serviços, como a memória de acesso aleatório não volátil (NVRAM) ou Olá serviço também são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="79ace-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="79ace-123">Ambos os controladores de saudação são reiniciados quando você entra ou sai deste modo.</span><span class="sxs-lookup"><span data-stu-id="79ace-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="79ace-124">Quando você sair do modo de manutenção hello, todos os serviços de saudação serão retomada e devem ser íntegros.</span><span class="sxs-lookup"><span data-stu-id="79ace-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="79ace-125">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="79ace-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="79ace-126">**Só há suporte ao modo de Manutenção em um dispositivo que esteja funcionando corretamente. Não há suporte em um dispositivo no qual um ou ambos os controladores de saudação não estão funcionando.**</span><span class="sxs-lookup"><span data-stu-id="79ace-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="79ace-127">Modo de recuperação</span><span class="sxs-lookup"><span data-stu-id="79ace-127">Recovery mode</span></span>

<span data-ttu-id="79ace-128">O modo de recuperação pode ser descrito como "Modo Seguro do Windows com suporte de rede".</span><span class="sxs-lookup"><span data-stu-id="79ace-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="79ace-129">Modo de recuperação aciona a equipe do Microsoft Support hello e permite tooperform diagnósticos no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="79ace-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="79ace-130">Olá principal objetivo do modo de recuperação é tooretrieve Olá sistema logs.</span><span class="sxs-lookup"><span data-stu-id="79ace-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="79ace-131">Se o sistema entrar no modo de recuperação, você deverá contatar o Suporte da Microsoft para obter as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="79ace-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="79ace-132">Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="79ace-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="79ace-133">**Você não pode colocar o dispositivo Olá no modo de recuperação. Se o dispositivo de saudação está em um estado inválido, o modo de recuperação tenta tooget dispositivo de saudação em um estado em que a equipe do Microsoft Support possa examiná-lo.**</span><span class="sxs-lookup"><span data-stu-id="79ace-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="79ace-134">Determinar o modo do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="79ace-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="79ace-135">modo de dispositivo toodetermine Olá atual</span><span class="sxs-lookup"><span data-stu-id="79ace-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="79ace-136">Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="79ace-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="79ace-137">Examine a mensagem de saudação do banner no menu do console serial saudação do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="79ace-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="79ace-138">Esta mensagem indica explicitamente se o dispositivo hello está no modo de manutenção ou recuperação.</span><span class="sxs-lookup"><span data-stu-id="79ace-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="79ace-139">Se a mensagem de saudação não contém informações específicas relativas toohello modo de sistema, o dispositivo de saudação está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="79ace-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="79ace-140">Alterar o modo de saudação do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="79ace-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="79ace-141">Você pode colocar o dispositivo StorSimple Olá em manutenção de tooperform modo (no modo normal) de manutenção ou instalar atualizações do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="79ace-142">Execute Olá modo de manutenção de tooenter ou sair de procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="79ace-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79ace-143">Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros acessando Olá **configurações do dispositivo > integridade do Hardware** para seu dispositivo no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79ace-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="79ace-144">Se um ou ambos os controladores de saudação não estão íntegros, entre em contato com o Microsoft Support para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="79ace-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="79ace-145">Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="79ace-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="79ace-146">modo de manutenção de tooenter</span><span class="sxs-lookup"><span data-stu-id="79ace-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="79ace-147">Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="79ace-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="79ace-148">No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="79ace-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="79ace-149">Quando solicitado, forneça Olá **senha de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="79ace-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="79ace-150">Olá a senha padrão é: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="79ace-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="79ace-151">No prompt de comando hello, digite</span><span class="sxs-lookup"><span data-stu-id="79ace-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="79ace-152">Você verá uma mensagem de aviso informando que o modo de manutenção irá interromper todas as solicitações de e/s e servidor Olá conexão toohello portal do Azure, e você será solicitado a confirmar.</span><span class="sxs-lookup"><span data-stu-id="79ace-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="79ace-153">Tipo **Y** tooenter modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="79ace-154">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="79ace-154">Both controllers will restart.</span></span> <span data-ttu-id="79ace-155">Quando Olá reinicialização é concluída, faixa de console serial Olá indicará que dispositivo hello está no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="79ace-156">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="79ace-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="79ace-157">modo de manutenção de tooexit</span><span class="sxs-lookup"><span data-stu-id="79ace-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="79ace-158">Faça logon no console serial do dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="79ace-158">Log on toohello device serial console.</span></span> <span data-ttu-id="79ace-159">Verificar da mensagem de saudação do banner que seu dispositivo está no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="79ace-160">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="79ace-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="79ace-161">Uma mensagem de aviso e uma mensagem de confirmação serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="79ace-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="79ace-162">Tipo **Y** tooexit modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="79ace-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="79ace-163">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="79ace-163">Both controllers will restart.</span></span> <span data-ttu-id="79ace-164">Quando Olá reinicialização é concluída, faixa de console serial Olá indica que dispositivo hello está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="79ace-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="79ace-165">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="79ace-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="79ace-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79ace-166">Next steps</span></span>

<span data-ttu-id="79ace-167">Saiba como muito[aplicar as atualizações do modo normal e manutenção](storsimple-update-device.md) em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="79ace-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

