---
title: Alterar a senha de administrador do dispositivo da StorSimple Virtual Array | Microsoft Docs
description: "Descreve como usar o portal do Azure ou a interface do usuário da Web da Matriz Virtual StorSimple para alterar a senha do administrador do dispositivo."
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
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="d1d21-103">Alterar a senha de administrador do dispositivo StorSimple Virtual Array por meio do Gerenciador de Dispositivos do StorSimple</span><span class="sxs-lookup"><span data-stu-id="d1d21-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="d1d21-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d1d21-104">Overview</span></span>

<span data-ttu-id="d1d21-105">Quando você usar a interface do Windows PowerShell para acessar o dispositivo da Matriz Virtual StorSimple, será solicitada a inserção de uma senha do administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d1d21-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="d1d21-106">Quando o dispositivo StorSimple é configurado e iniciado pela primeira vez, a senha padrão é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d1d21-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="d1d21-107">Para a segurança dos seus dados, a senha padrão expira na primeira vez que você entra e é necessário alterá-la.</span><span class="sxs-lookup"><span data-stu-id="d1d21-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="d1d21-108">Você também pode usar a interface do usuário da Web local ou o portal do Azure para alterar a senha do administrador do dispositivo a qualquer momento depois que o dispositivo for implantado no seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d1d21-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="d1d21-109">Cada um desses procedimentos é descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d1d21-109">Each of these procedures is described in this article.</span></span>

 ![folha de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="d1d21-111">Usar o portal do Azure para alterar a senha</span><span class="sxs-lookup"><span data-stu-id="d1d21-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="d1d21-112">Execute as etapas a seguir para alterar a senha do administrador do dispositivo por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1d21-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="d1d21-113">Para alterar a senha do administrador do dispositivo por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d1d21-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="d1d21-114">Na página de aterrissagem do serviço, selecione o seu serviço, clique duas vezes no nome do serviço e na seção **Gerenciamento**, clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="d1d21-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="d1d21-115">Isso abre a folha **Dispositivos** que lista todos os dispositivos de Matriz Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d1d21-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="d1d21-116">Na folha **Dispositivos**, clique duas vezes no dispositivo que requer uma alteração de senha.</span><span class="sxs-lookup"><span data-stu-id="d1d21-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="d1d21-117">Na folha **Configurações** do seu dispositivo, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="d1d21-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="d1d21-118">Na folha **Configurações de segurança**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d1d21-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="d1d21-119">Role para baixo até a seção **Senha de Administrador do Dispositivo** .</span><span class="sxs-lookup"><span data-stu-id="d1d21-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="d1d21-120">Forneça uma senha do administrador que contenha de 8 a 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1d21-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="d1d21-121">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="d1d21-121">Confirm the password.</span></span>
   3. <span data-ttu-id="d1d21-122">Clique em **Salvar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="d1d21-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="d1d21-123">A senha de administrador do dispositivo agora está atualizada.</span><span class="sxs-lookup"><span data-stu-id="d1d21-123">The device administrator password is now updated.</span></span> <span data-ttu-id="d1d21-124">Você pode usar essa senha modificada para acessar o dispositivo localmente.</span><span class="sxs-lookup"><span data-stu-id="d1d21-124">You can use this modified password to access the device locally.</span></span>

![Folha Configurações de segurança](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="d1d21-126">Usar a interface do usuário da Web local para alterar a senha</span><span class="sxs-lookup"><span data-stu-id="d1d21-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="d1d21-127">Execute as etapas a seguir para alterar a senha do administrador do dispositivo por meio da interface do usuário da Web local.</span><span class="sxs-lookup"><span data-stu-id="d1d21-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="d1d21-128">Para alterar a senha do administrador do dispositivo por meio da interface do usuário da web local</span><span class="sxs-lookup"><span data-stu-id="d1d21-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="d1d21-129">Na interface do usuário da Web local, clique em **Manutenção** > **Alteração de senha** para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d1d21-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![alterar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="d1d21-131">Insira a **Senha atual**.</span><span class="sxs-lookup"><span data-stu-id="d1d21-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="d1d21-132">Forneça uma **Nova senha**.</span><span class="sxs-lookup"><span data-stu-id="d1d21-132">Provide a **New Password**.</span></span> <span data-ttu-id="d1d21-133">A senha deve ter pelo menos oito caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1d21-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="d1d21-134">Deve conter três dentre estas quatro opções: caracteres maiúsculos, minúsculos, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="d1d21-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="d1d21-135">Observe que sua senha não pode ser igual às 24 últimas senhas.</span><span class="sxs-lookup"><span data-stu-id="d1d21-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="d1d21-136">Insira a senha novamente para confirmá-la.</span><span class="sxs-lookup"><span data-stu-id="d1d21-136">Reenter the password to confirm it.</span></span>
   
    ![alterar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="d1d21-138">Na parte inferior da página, clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d1d21-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="d1d21-139">A nova senha foi aplicada.</span><span class="sxs-lookup"><span data-stu-id="d1d21-139">The new password is now applied.</span></span> <span data-ttu-id="d1d21-140">Se a alteração da senha não for concluída com êxito, você verá o erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1d21-140">If the password change is not successful, you see the following error:</span></span>
   
    ![erro de senha](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="d1d21-142">Depois que a senha for atualizada com êxito, você será notificado.</span><span class="sxs-lookup"><span data-stu-id="d1d21-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="d1d21-143">Pode-se usar essa senha modificada para acessar o dispositivo localmente.</span><span class="sxs-lookup"><span data-stu-id="d1d21-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d1d21-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1d21-144">Next steps</span></span>
<span data-ttu-id="d1d21-145">Aprenda como [administrar sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="d1d21-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

