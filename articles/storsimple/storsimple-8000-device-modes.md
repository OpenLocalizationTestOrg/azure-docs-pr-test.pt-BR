---
title: Alterar o modo do dispositivo StorSimple | Microsoft Docs
description: Descreve os modos de dispositivo StorSimple e explica como usar o Windows PowerShell para StorSimple para alterar o modo de dispositivo.
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
ms.openlocfilehash: dd160ede1189b0de544c8cf5db3b13228d212419
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="751be-103">Alterar o modo do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="751be-103">Change the device mode on your StorSimple device</span></span>

<span data-ttu-id="751be-104">Este artigo fornece uma breve descrição dos diversos modos em que o dispositivo StorSimple pode operar.</span><span class="sxs-lookup"><span data-stu-id="751be-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="751be-105">O dispositivo StorSimple pode funcionar em três modos: normal, manutenção e recuperação.</span><span class="sxs-lookup"><span data-stu-id="751be-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="751be-106">Após ler este artigo, você conhecerá:</span><span class="sxs-lookup"><span data-stu-id="751be-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="751be-107">O que são os modos de dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="751be-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="751be-108">Como descobrir em qual modo o dispositivo StorSimple está</span><span class="sxs-lookup"><span data-stu-id="751be-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="751be-109">Como alterar do modo normal para o modo de manutenção e *vice-versa*</span><span class="sxs-lookup"><span data-stu-id="751be-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="751be-110">As tarefas de gerenciamento acima só podem ser executadas por meio da interface do Windows PowerShell do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="751be-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="751be-111">Sobre os modos do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="751be-111">About StorSimple device modes</span></span>

<span data-ttu-id="751be-112">O dispositivo StorSimple pode operar nos modos normal, de manutenção ou de recuperação.</span><span class="sxs-lookup"><span data-stu-id="751be-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="751be-113">Cada um desses modos é descrito resumidamente abaixo.</span><span class="sxs-lookup"><span data-stu-id="751be-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="751be-114">Modo Normal</span><span class="sxs-lookup"><span data-stu-id="751be-114">Normal mode</span></span>

<span data-ttu-id="751be-115">É definido como o modo operacional normal para um dispositivo StorSimple totalmente configurado.</span><span class="sxs-lookup"><span data-stu-id="751be-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="751be-116">Por padrão, o dispositivo deve estar no modo normal.</span><span class="sxs-lookup"><span data-stu-id="751be-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="751be-117">Modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="751be-117">Maintenance mode</span></span>

<span data-ttu-id="751be-118">Às vezes, o dispositivo StorSimple pode precisar ser colocado no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="751be-119">Esse modo permite realizar a manutenção no dispositivo e instalar atualizações sem interrupção, como aquelas relacionadas ao firmware do disco.</span><span class="sxs-lookup"><span data-stu-id="751be-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="751be-120">Você pode colocar o sistema no modo de manutenção somente por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="751be-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="751be-121">Todas as solicitações de E/S são pausadas neste modo.</span><span class="sxs-lookup"><span data-stu-id="751be-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="751be-122">Serviços como NVRAM (memória de acesso aleatório não volátil) ou o serviço de cluster também são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="751be-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="751be-123">Ambos os controladores são reiniciados quando você entra ou sai desse modo.</span><span class="sxs-lookup"><span data-stu-id="751be-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="751be-124">Quando você sair do modo de manutenção, todos os serviços continuarão e deverão estar íntegros.</span><span class="sxs-lookup"><span data-stu-id="751be-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="751be-125">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="751be-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="751be-126">**Só há suporte ao modo de Manutenção em um dispositivo que esteja funcionando corretamente. Não há suporte para esse modo em um dispositivo no qual um ou ambos os controladores não estejam funcionando.**</span><span class="sxs-lookup"><span data-stu-id="751be-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="751be-127">Modo de recuperação</span><span class="sxs-lookup"><span data-stu-id="751be-127">Recovery mode</span></span>

<span data-ttu-id="751be-128">O modo de recuperação pode ser descrito como "Modo Seguro do Windows com suporte de rede".</span><span class="sxs-lookup"><span data-stu-id="751be-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="751be-129">O modo de recuperação envolve a equipe de Suporte da Microsoft e permite que ela execute o diagnóstico do sistema.</span><span class="sxs-lookup"><span data-stu-id="751be-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="751be-130">O objetivo principal do modo de recuperação é recuperar os logs do sistema.</span><span class="sxs-lookup"><span data-stu-id="751be-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="751be-131">Se o sistema entrar no modo de recuperação, você deverá contatar o Suporte da Microsoft para obter as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="751be-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="751be-132">Para obter mais informações, vá para [Contatar o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="751be-132">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="751be-133">**Você não pode colocar o dispositivo no modo de recuperação. Se o dispositivo estiver em um estado inválido, o modo de recuperação tentará colocá-lo em um estado em que a equipe de Suporte da Microsoft possa examiná-lo.**</span><span class="sxs-lookup"><span data-stu-id="751be-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="751be-134">Determinar o modo do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="751be-134">Determine StorSimple device mode</span></span>

#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="751be-135">Para determinar o modo atual do dispositivo</span><span class="sxs-lookup"><span data-stu-id="751be-135">To determine the current device mode</span></span>

1. <span data-ttu-id="751be-136">Faça logon no console serial do dispositivo seguindo as etapas em [Usar o PuTTY para conectar-se ao console serial do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="751be-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="751be-137">Examine a mensagem do cabeçalho no menu do console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="751be-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="751be-138">A mensagem indica explicitamente se o dispositivo está no modo de manutenção ou de recuperação.</span><span class="sxs-lookup"><span data-stu-id="751be-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="751be-139">Se a mensagem não contiver informações específicas sobre o modo do sistema, o dispositivo está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="751be-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="751be-140">Alterar o modo de dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="751be-140">Change the StorSimple device mode</span></span>

<span data-ttu-id="751be-141">Você pode colocar o dispositivo StorSimple no modo de manutenção (do modo normal) para realizar a manutenção ou instalar atualizações do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="751be-142">Execute os seguintes procedimentos para entrar ou sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="751be-143">Antes de entrar no modo de manutenção, verifique se ambos os controladores de dispositivo estão íntegros acessando **Configurações do dispositivo > Integridade do hardware** do dispositivo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="751be-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Device settings > Hardware health** for your device in the Azure portal.</span></span> <span data-ttu-id="751be-144">Se um ou ambos os controladores não estiverem íntegros, contate o Suporte da Microsoft para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="751be-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="751be-145">Para obter mais informações, vá para [Contatar o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="751be-145">For more information, go to [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="751be-146">Para entrar no modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="751be-146">To enter maintenance mode</span></span>

1. <span data-ttu-id="751be-147">Faça logon no console serial do dispositivo seguindo as etapas em [Usar o PuTTY para conectar-se ao console serial do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="751be-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="751be-148">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="751be-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="751be-149">Quando solicitado, forneça a **senha de administrador do dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="751be-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="751be-150">A senha padrão é: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="751be-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="751be-151">No prompt de comando, digite</span><span class="sxs-lookup"><span data-stu-id="751be-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="751be-152">Você verá uma mensagem de aviso informando que o modo de manutenção interromperá todas as solicitações de E/S e a conexão com o Portal do Azure e sua confirmação será solicitada.</span><span class="sxs-lookup"><span data-stu-id="751be-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="751be-153">Digite **Y** para entrar no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="751be-154">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="751be-154">Both controllers will restart.</span></span> <span data-ttu-id="751be-155">Quando a reinicialização for concluída, outra faixa do console serial será exibida indicando que o dispositivo está em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-155">When the restart is complete, the serial console banner will indicate that the device is in maintenance mode.</span></span> <span data-ttu-id="751be-156">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="751be-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="751be-157">Para sair do modo de manutenção</span><span class="sxs-lookup"><span data-stu-id="751be-157">To exit maintenance mode</span></span>

1. <span data-ttu-id="751be-158">Faça logon no console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="751be-158">Log on to the device serial console.</span></span> <span data-ttu-id="751be-159">Verifique na mensagem do cabeçalho se o dispositivo está no modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-159">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="751be-160">No prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="751be-160">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="751be-161">Uma mensagem de aviso e uma mensagem de confirmação serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="751be-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="751be-162">Digite **Y** para sair do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="751be-162">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="751be-163">Ambos os controladores serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="751be-163">Both controllers will restart.</span></span> <span data-ttu-id="751be-164">Quando a reinicialização for concluída, a faixa do console serial indicará que o dispositivo está no modo normal.</span><span class="sxs-lookup"><span data-stu-id="751be-164">When the restart is complete, the serial console banner indicates that the device is in normal mode.</span></span> <span data-ttu-id="751be-165">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="751be-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure to install on each controller could result in data corruption. Exiting maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to exit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected to Controller0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="751be-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="751be-166">Next steps</span></span>

<span data-ttu-id="751be-167">Saiba como [aplicar atualizações do modo normal e de manutenção](storsimple-update-device.md) no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="751be-167">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

