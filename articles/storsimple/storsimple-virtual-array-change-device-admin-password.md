---
title: senha de administrador de dispositivo de matriz Virtual StorSimple aaaChange | Microsoft Docs
description: "Descreve como toouse hello ou portal do Azure ou da interface do usuário de web de matriz Virtual StorSimple toochange senha de administrador do dispositivo de saudação."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="3316c-103">Alterar senha do administrador de dispositivo Olá matriz Virtual StorSimple por meio do Gerenciador de dispositivos do StorSimple</span><span class="sxs-lookup"><span data-stu-id="3316c-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="3316c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3316c-104">Overview</span></span>

<span data-ttu-id="3316c-105">Quando você usar tooaccess de interface do Windows PowerShell Olá Olá matriz Virtual StorSimple, você estará tooenter necessária uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3316c-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="3316c-106">Quando o dispositivo StorSimple Olá primeiro é provisionado e iniciado, a senha de padrão de saudação é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="3316c-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="3316c-107">Para segurança de saudação dos seus dados, Olá padrão expirar Olá primeira vez que você entrar e é necessária toochange essa senha.</span><span class="sxs-lookup"><span data-stu-id="3316c-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="3316c-108">Você também pode usar qualquer Olá web local da interface do usuário ou hello toochange portal do Azure Olá dispositivo senha de administrador a qualquer momento depois que o dispositivo de saudação for implantado em seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3316c-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="3316c-109">Cada um desses procedimentos é descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3316c-109">Each of these procedures is described in this article.</span></span>

 ![folha de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="3316c-111">Use senha de saudação do hello toochange portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3316c-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="3316c-112">Execute Olá seguindo a senha de administrador de dispositivo etapas toochange Olá por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3316c-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="3316c-113">senha de administrador de dispositivo toochange Olá via Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3316c-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="3316c-114">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **gerenciamento** seção, clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="3316c-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="3316c-115">Isso abre o hello **dispositivos** folha que lista todos os dispositivos de matriz Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3316c-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="3316c-116">Em Olá **dispositivos** folha, clique duas vezes no dispositivo de saudação que requer uma alteração de senha.</span><span class="sxs-lookup"><span data-stu-id="3316c-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="3316c-117">Em Olá **configurações** folha do seu dispositivo, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="3316c-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="3316c-118">Em Olá **as configurações de segurança** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3316c-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="3316c-119">Role para baixo toohello **senha de administrador do dispositivo** seção.</span><span class="sxs-lookup"><span data-stu-id="3316c-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="3316c-120">Forneça uma senha de administrador que contenha de 8 caracteres too15.</span><span class="sxs-lookup"><span data-stu-id="3316c-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="3316c-121">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="3316c-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="3316c-122">Clique em **salvar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="3316c-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="3316c-123">senha de administrador do dispositivo Hello está atualizada.</span><span class="sxs-lookup"><span data-stu-id="3316c-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="3316c-124">Você pode usar este dispositivo de saudação tooaccess senha modificada localmente.</span><span class="sxs-lookup"><span data-stu-id="3316c-124">You can use this modified password tooaccess hello device locally.</span></span>

![Folha Configurações de segurança](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="3316c-126">Use senha de Olá Olá web local da interface do usuário toochange</span><span class="sxs-lookup"><span data-stu-id="3316c-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="3316c-127">Execute Olá senha de administrador de dispositivo etapas toochange Olá por meio da interface do usuário da web local Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3316c-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="3316c-128">senha de administrador de dispositivo toochange Olá por meio da interface do usuário da web local Olá</span><span class="sxs-lookup"><span data-stu-id="3316c-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="3316c-129">No hello interface da web local, clique em **manutenção** > **alteração de senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3316c-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![alterar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="3316c-131">Digite hello **senha atual**.</span><span class="sxs-lookup"><span data-stu-id="3316c-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="3316c-132">Forneça uma **Nova senha**.</span><span class="sxs-lookup"><span data-stu-id="3316c-132">Provide a **New Password**.</span></span> <span data-ttu-id="3316c-133">senha Olá deve ter pelo menos 8 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3316c-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="3316c-134">Ele deve conter 3 de 4 dos seguintes Olá: caracteres maiusculo, minúsculo, numérico e especial.</span><span class="sxs-lookup"><span data-stu-id="3316c-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="3316c-135">Observe que a senha não pode ser Olá mesmo Olá últimas 24 senhas.</span><span class="sxs-lookup"><span data-stu-id="3316c-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="3316c-136">Reinsira Olá senha tooconfirm-lo.</span><span class="sxs-lookup"><span data-stu-id="3316c-136">Reenter hello password tooconfirm it.</span></span>
   
    ![alterar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="3316c-138">Final Olá Olá página, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="3316c-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="3316c-139">nova senha de saudação agora é aplicada.</span><span class="sxs-lookup"><span data-stu-id="3316c-139">hello new password is now applied.</span></span> <span data-ttu-id="3316c-140">Se a alteração da senha Olá não for bem-sucedida, você verá Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="3316c-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![erro de senha](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="3316c-142">Depois de senha Olá foi atualizada com êxito, você será notificado.</span><span class="sxs-lookup"><span data-stu-id="3316c-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="3316c-143">Você pode usar este dispositivo de saudação tooaccess senha modificada localmente.</span><span class="sxs-lookup"><span data-stu-id="3316c-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3316c-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3316c-144">Next steps</span></span>
<span data-ttu-id="3316c-145">Saiba como muito[administrar sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="3316c-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

