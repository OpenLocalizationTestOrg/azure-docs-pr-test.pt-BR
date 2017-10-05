---
title: Atualizar o dispositivo StorSimple | Microsoft Docs
description: "Explica como usar o recurso de atualização do StorSimple para instalar hotfixes e atualizações regulares e no modo de manutenção."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="d8ff8-103">Atualizar seu dispositivo do StorSimple série 8000</span><span class="sxs-lookup"><span data-stu-id="d8ff8-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="d8ff8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d8ff8-104">Overview</span></span>
<span data-ttu-id="d8ff8-105">Os recursos de atualização do StorSimple permitem que você mantenha seu dispositivo StorSimple atualizado com facilidade.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="d8ff8-106">Dependendo do tipo de atualização, você poderá aplicar as atualizações ao dispositivo por meio do Portal Clássico do Azure ou por meio da interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="d8ff8-107">Este tutorial descreve os tipos de atualização e como instalar cada um deles.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="d8ff8-108">Você pode aplicar dois tipos de atualização de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d8ff8-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="d8ff8-109">Atualizações regulares (ou modo Normal)</span><span class="sxs-lookup"><span data-stu-id="d8ff8-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="d8ff8-110">Atualizações no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="d8ff8-110">Maintenance mode updates</span></span>

<span data-ttu-id="d8ff8-111">Você pode instalar atualizações regulares por meio do Portal Clássico do Azure ou do Windows PowerShell; no entanto, você deve usar o Windows PowerShell para instalar atualizações do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="d8ff8-112">Cada tipo de atualização será descrito separadamente a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="d8ff8-113">Atualizações regulares</span><span class="sxs-lookup"><span data-stu-id="d8ff8-113">Regular updates</span></span>
<span data-ttu-id="d8ff8-114">As atualizações regulares são atualizações sem interrupções que podem ser instaladas quando o dispositivo estiver em modo Normal.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="d8ff8-115">Essas atualizações são aplicadas por meio do site Microsoft Update para cada controlador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d8ff8-116">Um failover de controlador pode ocorrer durante o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="d8ff8-117">No entanto, isso não afetará a disponibilidade do sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="d8ff8-118">Para obter detalhes sobre como instalar atualizações regulares por meio do portal clássico o Azure, consulte [Instalar atualizações regulares por meio do portal clássico do Azure](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="d8ff8-119">Você também pode instalar atualizações regulares por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d8ff8-120">Para obter detalhes, consulte [Instalar atualizações regulares por meio do Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="d8ff8-121">Atualizações no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="d8ff8-121">Maintenance mode updates</span></span>
<span data-ttu-id="d8ff8-122">As atualizações do Modo de Manutenção são atualizações com interrupção, como atualizações de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="d8ff8-123">Essas atualizações exigem que o dispositivo seja colocado em modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="d8ff8-124">Para obter detalhes, consulte [Etapa 2: Entrar no modo de Manutenção](#step2).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="d8ff8-125">Você não pode usar o Portal clássico do Azure para instalar atualizações do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="d8ff8-126">Em vez disso, você deverá usar o Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="d8ff8-127">Para obter detalhes sobre como instalar atualizações do modo de Manutenção, consulte [Instalar atualizações do modo de Manutenção instalar por meio do Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8ff8-128">As atualizações do modo de Manutenção devem ser aplicadas separadamente para cada controlador.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="d8ff8-129">Instalar atualizações regulares por meio do Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="d8ff8-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="d8ff8-130">Você pode usar o Portal clássico do Azure para aplicar atualizações ao dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d8ff8-131">Instalar atualizações regulares por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="d8ff8-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d8ff8-132">Como alternativa, você pode usar o Windows PowerShell para StorSimple para aplicar atualizações regulares (modo Normal).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8ff8-133">Embora seja possível instalar atualizações regulares usando o Windows PowerShell para StorSimple, é altamente recomendável que você instale atualizações regulares pelo Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="d8ff8-134">Começando da Atualização 1, serão executadas verificações prévias antes da instalação de atualizações pelo portal.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="d8ff8-135">Essas verificações evitarão falhas e garantirão uma experiência mais uniforme.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d8ff8-136">Instalar atualizações do modo de Manutenção instalar por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="d8ff8-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d8ff8-137">Você pode usar o Windows PowerShell para StorSimple para aplicar atualizações do modo de Manutenção ao dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="d8ff8-138">Todas as solicitações de E/S são pausadas neste modo.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="d8ff8-139">Serviços como NVRAM (memória de acesso aleatório não volátil) ou o serviço de cluster também são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="d8ff8-140">Ambos os controladores são reiniciados quando você entra ou sai desse modo.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="d8ff8-141">Quando você sair desse modo, todos os serviços serão retomados e deverão estar íntegros.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="d8ff8-142">(Isso pode levar alguns minutos).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="d8ff8-143">Se você precisar aplicar atualizações do modo de Manutenção, receberá um alerta por meio do Portal clássico do Azure indicando que há atualizações que devem ser instaladas.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="d8ff8-144">Esse alerta incluirá instruções para o uso do Windows PowerShell para StorSimple para instalar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="d8ff8-145">Depois de atualizar o dispositivo, use o mesmo procedimento para alterar o dispositivo para o modo Normal.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="d8ff8-146">Para obter instruções passo a passo, consulte [Etapa 4: Sair do modo de Manutenção](#step4).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d8ff8-147">Antes de entrar no modo de Manutenção, verifique se ambos os controladores de dispositivo estão íntegros, verificando o **Status de Hardware** na página **Manutenção** no Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="d8ff8-148">Se o controlador não estiver íntegro, contate o Suporte da Microsoft para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="d8ff8-149">Para saber mais, acesse Contatar Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="d8ff8-150">Quando você estiver no modo de Manutenção, precisará aplicar a atualização primeiro em um controlador e então no outro controlador.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="d8ff8-151">Etapa 1: Conectar-se ao console serial <a name="step1"></span><span class="sxs-lookup"><span data-stu-id="d8ff8-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="d8ff8-152">Primeiro, use um aplicativo como o PuTTY para acessar o console serial.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="d8ff8-153">O procedimento a seguir explica como usar o PuTTY para se conectar ao console serial.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="d8ff8-154">Etapa 2: Entrar no modo de Manutenção <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="d8ff8-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="d8ff8-155">Depois de se conectar ao console, determine se há atualizações a serem instaladas e entre no modo de manutenção para instalá-las.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="d8ff8-156">Etapa 3: Instalar as atualizações <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="d8ff8-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="d8ff8-157">Em seguida, instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="d8ff8-158">Etapa 4: Sair do modo de Manutenção <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="d8ff8-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="d8ff8-159">Por fim, saia do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d8ff8-160">Instale correções por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="d8ff8-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d8ff8-161">Ao contrário de atualizações para o Microsoft Azure StorSimple, os hotfixes são instalados de uma pasta compartilhada.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="d8ff8-162">Assim como acontece com as atualizações, há dois tipos de hotfixes:</span><span class="sxs-lookup"><span data-stu-id="d8ff8-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="d8ff8-163">Hotfixes regulares</span><span class="sxs-lookup"><span data-stu-id="d8ff8-163">Regular hotfixes</span></span> 
* <span data-ttu-id="d8ff8-164">Hotfixes no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="d8ff8-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="d8ff8-165">Os procedimentos a seguir explicam como usar o Windows PowerShell para StorSimple para instalar hotfixes regulares e no modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="d8ff8-166">O que acontece com as atualizações se você executar uma redefinição de fábrica do dispositivo?</span><span class="sxs-lookup"><span data-stu-id="d8ff8-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="d8ff8-167">Se um dispositivo for redefinido para as configurações de fábrica, então todas as atualizações serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="d8ff8-168">Depois que o dispositivo com a redefinição de fábrica for registrado e configurado, você precisará instalar manualmente as atualizações por meio do Portal clássico do Azure e/ou do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d8ff8-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d8ff8-169">Para saber mais sobre as redefinições de fábrica, consulte [Redefinir o dispositivo para as configurações padrão de fábrica](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8ff8-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8ff8-170">Next steps</span></span>
* <span data-ttu-id="d8ff8-171">Saiba mais sobre [como usar o Windows PowerShell para StorSimple a fim de administrar seu dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d8ff8-172">Saiba mais sobre o [uso do serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d8ff8-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

