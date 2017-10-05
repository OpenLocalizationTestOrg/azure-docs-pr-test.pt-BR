---
title: Alterar suas senhas do StorSimple | Microsoft Docs
description: "Descreve como usar o serviço Gerenciador de Dispositivos do StorSimple para alterar suas senhas de administrador do dispositivo e do StorSimple Snapshot Manager."
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
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="4d1fc-103">Usar o serviço do Gerenciador de Dispositivos do StorSimple para alterar suas senhas do StorSimple</span><span class="sxs-lookup"><span data-stu-id="4d1fc-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="4d1fc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4d1fc-104">Overview</span></span>
<span data-ttu-id="4d1fc-105">A opção **Configurações de dispositivo** do Portal do Azure contém todos os parâmetros de dispositivo que podem ser reconfigurados em um dispositivo StorSimple gerenciado por um serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="4d1fc-106">Este tutorial explica como você pode usar a opção **Segurança** nas **Configurações do dispositivo** para alterar sua senha de administrador do dispositivo ou do StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="4d1fc-107">Alterar a senha de administrador do dispositivo</span><span class="sxs-lookup"><span data-stu-id="4d1fc-107">Change the device administrator password</span></span>
<span data-ttu-id="4d1fc-108">Quando você usar a interface do Windows PowerShell para acessar o dispositivo StorSimple, será solicitada a inserção de uma senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="4d1fc-109">Quando o primeiro dispositivo StorSimple é registrado em um serviço, a senha padrão para essa interface é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="4d1fc-110">Para a segurança de seus dados, você deve alterar essa senha no fim do processo de registro.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="4d1fc-111">Não é possível sair do processo de registro sem alterar essa senha.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="4d1fc-112">Para obter mais informações, consulte a [Etapa 3: configurar e registrar o dispositivo por meio do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="4d1fc-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="4d1fc-113">A senha que foi definida pela primeira vez por meio da interface do Windows PowerShell durante o registro pode ser alterada mais tarde no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="4d1fc-114">Execute as etapas a seguir para alterar a senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="4d1fc-115">Para alterar a senha de administrador do dispositivo</span><span class="sxs-lookup"><span data-stu-id="4d1fc-115">To change the device administrator password</span></span>
1. <span data-ttu-id="4d1fc-116">Acesse o serviço Gerenciador de Dispositivo StorSimple e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="4d1fc-117">Na listagem tabular dos dispositivos, selecione e clique no dispositivo cuja senha você deseja alterar.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="4d1fc-118">Na folha **Configurações**, acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="4d1fc-119">Na folha **Configurações de segurança**, clique em **Senha** para alterar a senha de administrador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="4d1fc-120">Na folha **Senha**, forneça uma senha do administrador contendo de 8 a 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="4d1fc-121">A senha deve ser uma combinação de três ou mais caracteres maiúsculos, minúsculos, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="4d1fc-122">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="4d1fc-123">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="4d1fc-124">A senha do administrador do dispositivo agora deve estar atualizada.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="4d1fc-125">Você pode usar essa senha modificada para acessar a interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="4d1fc-126">Definir a senha do StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="4d1fc-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="4d1fc-127">O software Gerenciador de Instantâneos StorSimple software reside no host Windows e permite que os administradores gerenciem backups do seu dispositivo StorSimple na forma de instantâneos locais e de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="4d1fc-128">Ao configurar um dispositivo no StorSimple Snapshot Manager, será solicitado que você forneça o endereço IP e a senha do dispositivo para autenticar o dispositivo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="4d1fc-129">Você pode definir ou alterar a senha do StorSimple Snapshot Manager pelo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="4d1fc-130">Realize as etapas a seguir para definir ou alterar a senha do StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="4d1fc-131">Para definir a senha do StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="4d1fc-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="4d1fc-132">Acesse o serviço Gerenciador de Dispositivo StorSimple e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="4d1fc-133">Na listagem tabular dos dispositivos, selecione e clique no dispositivo cuja senha do StorSimple Snapshot Manager você deseja definir ou alterar.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="4d1fc-134">Na folha **Configurações**, acesse **Configurações do dispositivo > Segurança**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="4d1fc-135">Na folha **Configurações de segurança**, clique em **Senha** para definir ou alterar a senha do StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="4d1fc-136">Na folha **Senha**, insira uma senha que tenha 14 ou 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="4d1fc-137">Verifique se a senha contém uma combinação de três ou mais caracteres maiúsculos, minúsculos, numéricos e especiais.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="4d1fc-138">Confirme a senha.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="4d1fc-139">Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="4d1fc-140">A senha do StorSimple Snapshot Manager agora deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="4d1fc-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d1fc-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d1fc-141">Next steps</span></span>
* <span data-ttu-id="4d1fc-142">Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="4d1fc-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="4d1fc-143">Saiba mais sobre [como modificar a configuração do dispositivo](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="4d1fc-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="4d1fc-144">Saiba mais sobre como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4d1fc-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

