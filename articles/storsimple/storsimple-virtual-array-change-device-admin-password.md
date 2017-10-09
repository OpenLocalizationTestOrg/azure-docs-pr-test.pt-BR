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
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Alterar senha do administrador de dispositivo Olá matriz Virtual StorSimple por meio do Gerenciador de dispositivos do StorSimple

## <a name="overview"></a>Visão geral

Quando você usar tooaccess de interface do Windows PowerShell Olá Olá matriz Virtual StorSimple, você estará tooenter necessária uma senha de administrador do dispositivo. Quando o dispositivo StorSimple Olá primeiro é provisionado e iniciado, a senha de padrão de saudação é *Password1*. Para segurança de saudação dos seus dados, Olá padrão expirar Olá primeira vez que você entrar e é necessária toochange essa senha.

Você também pode usar qualquer Olá web local da interface do usuário ou hello toochange portal do Azure Olá dispositivo senha de administrador a qualquer momento depois que o dispositivo de saudação for implantado em seu ambiente de produção. Cada um desses procedimentos é descrito neste artigo.

 ![folha de dispositivos](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Use senha de saudação do hello toochange portal do Azure

Execute Olá seguindo a senha de administrador de dispositivo etapas toochange Olá por meio de saudação portal do Azure.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>senha de administrador de dispositivo toochange Olá via Olá portal do Azure

1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **gerenciamento** seção, clique em **dispositivos**. Isso abre o hello **dispositivos** folha que lista todos os dispositivos de matriz Virtual StorSimple.

2. Em Olá **dispositivos** folha, clique duas vezes no dispositivo de saudação que requer uma alteração de senha.

3. Em Olá **configurações** folha do seu dispositivo, clique em **segurança**.

4. Em Olá **as configurações de segurança** folha, Olá a seguir:
   
   1. Role para baixo toohello **senha de administrador do dispositivo** seção. Forneça uma senha de administrador que contenha de 8 caracteres too15.
   2. Confirme senha hello.
   3. Clique em **salvar** na parte superior de saudação da folha de saudação.

senha de administrador do dispositivo Hello está atualizada. Você pode usar este dispositivo de saudação tooaccess senha modificada localmente.

![Folha Configurações de segurança](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Use senha de Olá Olá web local da interface do usuário toochange

Execute Olá senha de administrador de dispositivo etapas toochange Olá por meio da interface do usuário da web local Olá a seguir.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>senha de administrador de dispositivo toochange Olá por meio da interface do usuário da web local Olá

1. No hello interface da web local, clique em **manutenção** > **alteração de senha** para seu dispositivo.
   
    ![alterar password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Digite hello **senha atual**.
3. Forneça uma **Nova senha**. senha Olá deve ter pelo menos 8 caracteres. Ele deve conter 3 de 4 dos seguintes Olá: caracteres maiusculo, minúsculo, numérico e especial.
   
    Observe que a senha não pode ser Olá mesmo Olá últimas 24 senhas.
4. Reinsira Olá senha tooconfirm-lo.
   
    ![alterar password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Final Olá Olá página, clique em **aplicar**. nova senha de saudação agora é aplicada. Se a alteração da senha Olá não for bem-sucedida, você verá Olá erro a seguir:
   
    ![erro de senha](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Depois de senha Olá foi atualizada com êxito, você será notificado. Você pode usar este dispositivo de saudação tooaccess senha modificada localmente.


## <a name="next-steps"></a>Próximas etapas
Saiba como muito[administrar sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

