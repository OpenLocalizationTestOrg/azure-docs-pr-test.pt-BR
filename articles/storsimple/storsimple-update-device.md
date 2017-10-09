---
title: aaaUpdate seu dispositivo StorSimple | Microsoft Docs
description: "Explica como atualizar o hello toouse StorSimple recurso tooinstall regular e atualizações do modo de manutenção e hotfixes."
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
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="6ba3e-103">Atualizar seu dispositivo do StorSimple série 8000</span><span class="sxs-lookup"><span data-stu-id="6ba3e-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="6ba3e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6ba3e-104">Overview</span></span>
<span data-ttu-id="6ba3e-105">Olá StorSimple atualizações recursos permitem que você tooeasily manter atualizado o seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="6ba3e-106">Dependendo do tipo de atualização Olá, você pode aplicar o dispositivo toohello de atualizações por meio de saudação portal clássico do Azure ou por meio da interface do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="6ba3e-107">Este tutorial descreve os tipos de atualização de saudação e como tooinstall cada um deles.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="6ba3e-108">Você pode aplicar dois tipos de atualização de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="6ba3e-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="6ba3e-109">Atualizações regulares (ou modo Normal)</span><span class="sxs-lookup"><span data-stu-id="6ba3e-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="6ba3e-110">Atualizações no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="6ba3e-110">Maintenance mode updates</span></span>

<span data-ttu-id="6ba3e-111">Você pode instalar atualizações regulares via Olá portal clássico do Azure ou o Windows PowerShell; No entanto, você deve usar o Windows PowerShell tooinstall atualizações do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="6ba3e-112">Cada tipo de atualização será descrito separadamente a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="6ba3e-113">Atualizações regulares</span><span class="sxs-lookup"><span data-stu-id="6ba3e-113">Regular updates</span></span>
<span data-ttu-id="6ba3e-114">As atualizações regulares são atualizações sem interrupção que podem ser instaladas quando o dispositivo hello está no modo Normal.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="6ba3e-115">Essas atualizações são aplicadas por meio do controlador do dispositivo Olá Microsoft Update site tooeach.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6ba3e-116">Um failover de controlador pode ocorrer durante o processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="6ba3e-117">No entanto, isso não afetará a disponibilidade do sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="6ba3e-118">Para obter detalhes sobre como tooinstall regular atualiza via Olá portal clássico do Azure, consulte [instalar atualizações regulares via Olá portal clássico do Azure](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="6ba3e-119">Você também pode instalar atualizações regulares por meio do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="6ba3e-120">Para obter detalhes, consulte [Instalar atualizações regulares por meio do Windows PowerShell para StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="6ba3e-121">Atualizações no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="6ba3e-121">Maintenance mode updates</span></span>
<span data-ttu-id="6ba3e-122">As atualizações do Modo de Manutenção são atualizações com interrupção, como atualizações de firmware de disco.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="6ba3e-123">Essas atualizações exigem Olá dispositivo toobe colocar em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="6ba3e-124">Para obter detalhes, consulte [Etapa 2: Entrar no modo de Manutenção](#step2).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="6ba3e-125">Você não pode usar as atualizações do modo de manutenção do hello tooinstall de portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="6ba3e-126">Em vez disso, você deverá usar o Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="6ba3e-127">Para obter detalhes sobre como o modo de manutenção tooinstall atualizações, consulte [atualizações do modo de manutenção instalar por meio do Windows PowerShell para StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ba3e-128">Modo de manutenção, as atualizações devem ser aplicadas separadamente tooeach controlador.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="6ba3e-129">Instalar as atualizações regulares via Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6ba3e-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="6ba3e-130">Você pode usar o dispositivo StorSimple de tooyour de atualizações do hello tooapply de portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="6ba3e-131">Instalar atualizações regulares por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="6ba3e-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="6ba3e-132">Como alternativa, você pode usar o Windows PowerShell para atualizações do StorSimple tooapply regular (modo Normal).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ba3e-133">Embora você possa instalar atualizações regulares usando o Windows PowerShell para StorSimple, é altamente recomendável que você instale atualizações regulares por meio de saudação portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="6ba3e-134">Começando com atualização 1, pré-verificações de será executada tooinstalling anterior atualizações do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="6ba3e-135">Essas verificações evitarão falhas e garantirão uma experiência mais uniforme.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="6ba3e-136">Instalar atualizações do modo de Manutenção instalar por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="6ba3e-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="6ba3e-137">Usar o Windows PowerShell para StorSimple tooapply manutenção modo atualizações tooyour o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="6ba3e-138">Todas as solicitações de E/S são pausadas neste modo.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="6ba3e-139">Serviços, como a memória de acesso aleatório não volátil (NVRAM) ou Olá serviço também são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="6ba3e-140">Ambos os controladores são reiniciados quando você entra ou sai desse modo.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="6ba3e-141">Quando você sair deste modo, todos os serviços de saudação serão retomada e devem ser íntegros.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="6ba3e-142">(Isso pode levar alguns minutos).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="6ba3e-143">Se você precisar tooapply atualizações do modo de manutenção, você receberá um alerta por meio de saudação portal clássico do Azure que você possui atualizações que devem ser instaladas.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="6ba3e-144">Esse alerta inclui instruções sobre como usar o Windows PowerShell para atualizações do StorSimple tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="6ba3e-145">Depois de atualizar seu dispositivo, use Olá mesmo modo tooRegular do procedimento toochange Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="6ba3e-146">Para obter instruções passo a passo, consulte [Etapa 4: Sair do modo de Manutenção](#step4).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="6ba3e-147">Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros verificando Olá **Status do Hardware** em Olá **manutenção** página Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="6ba3e-148">Se o controlador de saudação não está íntegro, entre em contato com o Microsoft Support para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="6ba3e-149">Para obter mais informações, acesse tooContact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="6ba3e-150">Quando você estiver no modo de manutenção, é necessário tooapply Olá atualização pela primeira vez em um controlador e, em seguida, em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="6ba3e-151">Etapa 1: Conectar o console serial toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="6ba3e-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="6ba3e-152">Primeiro, use um aplicativo, como o PuTTY tooaccess Olá console serial.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="6ba3e-153">Olá procedimento a seguir explica como console serial do toohello toouse tooconnect PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="6ba3e-154">Etapa 2: Entrar no modo de Manutenção <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="6ba3e-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="6ba3e-155">Depois de conectar o console toohello, determinar se há atualizações tooinstall e insira tooinstall do modo de manutenção-los.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="6ba3e-156">Etapa 3: Instalar as atualizações <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="6ba3e-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="6ba3e-157">Em seguida, instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="6ba3e-158">Etapa 4: Sair do modo de Manutenção <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="6ba3e-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="6ba3e-159">Por fim, saia do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="6ba3e-160">Instale correções por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="6ba3e-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="6ba3e-161">Ao contrário de atualizações para o Microsoft Azure StorSimple, os hotfixes são instalados de uma pasta compartilhada.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="6ba3e-162">Assim como acontece com as atualizações, há dois tipos de hotfixes:</span><span class="sxs-lookup"><span data-stu-id="6ba3e-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="6ba3e-163">Hotfixes regulares</span><span class="sxs-lookup"><span data-stu-id="6ba3e-163">Regular hotfixes</span></span> 
* <span data-ttu-id="6ba3e-164">Hotfixes no modo de Manutenção</span><span class="sxs-lookup"><span data-stu-id="6ba3e-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="6ba3e-165">Olá procedimentos a seguir explicam como toouse do Windows PowerShell para StorSimple tooinstall regular e hotfixes do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="6ba3e-166">O que acontece tooupdates se você executar uma fábrica de redefinição do dispositivo Olá?</span><span class="sxs-lookup"><span data-stu-id="6ba3e-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="6ba3e-167">Se um dispositivo for toofactory de redefinir as configurações, todas as atualizações de saudação serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="6ba3e-168">Depois que o dispositivo de redefinição de fábrica Olá é registrado e configurado, você precisará toomanually instalar as atualizações por meio de saudação portal clássico do Azure e/ou do Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ba3e-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="6ba3e-169">Para obter mais informações sobre a redefinição de fábrica, consulte [redefinir as configurações padrão do hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ba3e-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ba3e-170">Next steps</span></span>
* <span data-ttu-id="6ba3e-171">Saiba mais sobre [usando o Windows PowerShell para StorSimple tooadminister seu dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="6ba3e-172">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6ba3e-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

