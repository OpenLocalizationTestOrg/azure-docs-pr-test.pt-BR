---
title: aaaChange suas senhas StorSimple | Microsoft Docs
description: "Descreve como toouse Olá toochange de serviço do Gerenciador de dispositivos de StorSimple suas senhas de administrador do StorSimple Snapshot Manager e o dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="980c1-103">Usar toochange de serviço do Gerenciador de dispositivos de StorSimple Olá suas senhas de StorSimple</span><span class="sxs-lookup"><span data-stu-id="980c1-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="980c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="980c1-104">Overview</span></span>
<span data-ttu-id="980c1-105">Olá portal do Azure **configurações do dispositivo** opção contém todos os parâmetros de dispositivo de saudação que você pode reconfigurar em um dispositivo StorSimple que é gerenciado por um serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="980c1-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="980c1-106">Este tutorial explica como você pode usar o hello **segurança** opção em **configurações do dispositivo** toochange o administrador do dispositivo ou a senha do StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="980c1-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="980c1-107">Senha de administrador de dispositivo de Olá de alteração</span><span class="sxs-lookup"><span data-stu-id="980c1-107">Change hello device administrator password</span></span>
<span data-ttu-id="980c1-108">Quando você usar o dispositivo StorSimple do Windows PowerShell interface tooaccess hello, você está tooenter necessária uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="980c1-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="980c1-109">Quando o primeiro dispositivo de StorSimple Olá é registrado com um serviço, a senha de padrão de saudação para essa interface é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="980c1-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="980c1-110">Para segurança de saudação dos seus dados, você está toochange necessária essa senha no final de saudação do processo de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="980c1-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="980c1-111">Você não pode sair do processo de registro de saudação sem alterar essa senha.</span><span class="sxs-lookup"><span data-stu-id="980c1-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="980c1-112">Para obter mais informações, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="980c1-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="980c1-113">senha Olá primeiro definida por meio da interface do Windows PowerShell Olá durante o registro pode ser alterada posteriormente por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="980c1-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="980c1-114">Execute Olá senha de administrador etapas toochange Olá dispositivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="980c1-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="980c1-115">senha de administrador de dispositivo toochange Olá</span><span class="sxs-lookup"><span data-stu-id="980c1-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="980c1-116">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="980c1-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="980c1-117">Na listagem tabular de saudação de dispositivos, selecione e clique em dispositivo Olá cuja senha você pretende toochange.</span><span class="sxs-lookup"><span data-stu-id="980c1-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="980c1-118">Em Olá **configurações** folha, ir muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="980c1-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="980c1-119">Em Olá **as configurações de segurança** folha, clique em **senha** toochange senha de administrador de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="980c1-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="980c1-120">Em Olá **senha** folha, forneça uma senha de administrador que contenha de 8 caracteres too15.</span><span class="sxs-lookup"><span data-stu-id="980c1-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="980c1-121">senha Olá deve ser uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.</span><span class="sxs-lookup"><span data-stu-id="980c1-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="980c1-122">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="980c1-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="980c1-123">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="980c1-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="980c1-124">senha de administrador do dispositivo Olá agora deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="980c1-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="980c1-125">Você pode usar essa senha modificada tooaccess saudação do Windows PowerShell interface.</span><span class="sxs-lookup"><span data-stu-id="980c1-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="980c1-126">Definir senha do StorSimple Snapshot Manager Olá</span><span class="sxs-lookup"><span data-stu-id="980c1-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="980c1-127">Gerenciador de instantâneos StorSimple software reside no host do Windows e permite que os administradores toomanage backups do seu dispositivo StorSimple na forma de saudação de locais e instantâneos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="980c1-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="980c1-128">Ao configurar um dispositivo no Gerenciador de instantâneos do StorSimple, você será solicitado tooprovide Olá tooauthenticate de endereço e a senha IP de dispositivo de seu dispositivo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="980c1-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="980c1-129">Você pode definir ou alterar a senha Olá para o Gerenciador de instantâneos do StorSimple via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="980c1-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="980c1-130">Execute Olá tooset as etapas a seguir ou alterar a senha do StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="980c1-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="980c1-131">senha do tooset Olá Gerenciador de instantâneos StorSimple</span><span class="sxs-lookup"><span data-stu-id="980c1-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="980c1-132">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="980c1-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="980c1-133">Na listagem tabular de saudação de dispositivos, selecione e clique em dispositivo Olá cuja senha do StorSimple Snapshot Manager pretende tooset ou alterar.</span><span class="sxs-lookup"><span data-stu-id="980c1-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="980c1-134">Em Olá **configurações** folha, ir muito**configurações do dispositivo > segurança**.</span><span class="sxs-lookup"><span data-stu-id="980c1-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="980c1-135">Em Olá **as configurações de segurança** folha, clique em **senha** tooset ou alteração de senha do StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="980c1-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="980c1-136">Em Olá **senha** folha, digite uma senha que é 14 ou 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="980c1-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="980c1-137">Verifique se que essa senha Olá contém uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.</span><span class="sxs-lookup"><span data-stu-id="980c1-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="980c1-138">Confirme senha hello.</span><span class="sxs-lookup"><span data-stu-id="980c1-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="980c1-139">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="980c1-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="980c1-140">senha do StorSimple Snapshot Manager Olá agora deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="980c1-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="980c1-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="980c1-141">Next steps</span></span>
* <span data-ttu-id="980c1-142">Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="980c1-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="980c1-143">Saiba mais sobre [como modificar a configuração do dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="980c1-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="980c1-144">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="980c1-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

