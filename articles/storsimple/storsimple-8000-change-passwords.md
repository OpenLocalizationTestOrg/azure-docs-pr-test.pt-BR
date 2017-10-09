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
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Usar toochange de serviço do Gerenciador de dispositivos de StorSimple Olá suas senhas de StorSimple

## <a name="overview"></a>Visão geral
Olá portal do Azure **configurações do dispositivo** opção contém todos os parâmetros de dispositivo de saudação que você pode reconfigurar em um dispositivo StorSimple que é gerenciado por um serviço de Gerenciador de dispositivos do StorSimple. Este tutorial explica como você pode usar o hello **segurança** opção em **configurações do dispositivo** toochange o administrador do dispositivo ou a senha do StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Senha de administrador de dispositivo de Olá de alteração
Quando você usar o dispositivo StorSimple do Windows PowerShell interface tooaccess hello, você está tooenter necessária uma senha de administrador do dispositivo. Quando o primeiro dispositivo de StorSimple Olá é registrado com um serviço, a senha de padrão de saudação para essa interface é *Password1*. Para segurança de saudação dos seus dados, você está toochange necessária essa senha no final de saudação do processo de registro de saudação. Você não pode sair do processo de registro de saudação sem alterar essa senha. Para obter mais informações, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

senha Olá primeiro definida por meio da interface do Windows PowerShell Olá durante o registro pode ser alterada posteriormente por meio de saudação portal do Azure. Execute Olá senha de administrador etapas toochange Olá dispositivo a seguir.

#### <a name="toochange-hello-device-administrator-password"></a>senha de administrador de dispositivo toochange Olá
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**.

2. Na listagem tabular de saudação de dispositivos, selecione e clique em dispositivo Olá cuja senha você pretende toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Em Olá **configurações** folha, ir muito**configurações do dispositivo > segurança**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Em Olá **as configurações de segurança** folha, clique em **senha** toochange senha de administrador de dispositivo de saudação.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. Em Olá **senha** folha, forneça uma senha de administrador que contenha de 8 caracteres too15. senha Olá deve ser uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.

6. Confirme senha hello.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

senha de administrador do dispositivo Olá agora deve ser atualizada. Você pode usar essa senha modificada tooaccess saudação do Windows PowerShell interface.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Definir senha do StorSimple Snapshot Manager Olá
Gerenciador de instantâneos StorSimple software reside no host do Windows e permite que os administradores toomanage backups do seu dispositivo StorSimple na forma de saudação de locais e instantâneos em nuvem.

Ao configurar um dispositivo no Gerenciador de instantâneos do StorSimple, você será solicitado tooprovide Olá tooauthenticate de endereço e a senha IP de dispositivo de seu dispositivo de armazenamento.

Você pode definir ou alterar a senha Olá para o Gerenciador de instantâneos do StorSimple via Olá portal do Azure. Execute Olá tooset as etapas a seguir ou alterar a senha do StorSimple Snapshot Manager hello.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>senha do tooset Olá Gerenciador de instantâneos StorSimple
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**.

2. Na listagem tabular de saudação de dispositivos, selecione e clique em dispositivo Olá cuja senha do StorSimple Snapshot Manager pretende tooset ou alterar.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. Em Olá **configurações** folha, ir muito**configurações do dispositivo > segurança**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. Em Olá **as configurações de segurança** folha, clique em **senha** tooset ou alteração de senha do StorSimple Snapshot Manager hello.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. Em Olá **senha** folha, digite uma senha que é 14 ou 15 caracteres. Verifique se que essa senha Olá contém uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.

6. Confirme senha hello.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

senha do StorSimple Snapshot Manager Olá agora deve ser atualizada.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).
* Saiba mais sobre [como modificar a configuração do dispositivo](storsimple-8000-modify-device-config.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

