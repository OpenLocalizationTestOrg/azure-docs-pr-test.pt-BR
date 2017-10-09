---
title: aaaChange senhas por meio do Gerenciador de dispositivos do StorSimple | Microsoft Docs
description: "Descreve como toouse Olá toochange do serviço StorSimple Manager suas senhas de administrador do StorSimple Snapshot Manager e o dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Usar toochange de serviço do StorSimple Manager Olá suas senhas de StorSimple
## <a name="overview"></a>Visão geral
Olá portal clássico do Azure **configurar** página contém todos os parâmetros de dispositivo de saudação que você pode reconfigurar em um dispositivo StorSimple que é gerenciado por um serviço StorSimple Manager. Este tutorial explica como você pode usar o hello **configurar** página toochange o administrador do dispositivo ou a senha do StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Senha de administrador de dispositivo de Olá de alteração
Quando você usar o dispositivo StorSimple do Windows PowerShell interface tooaccess hello, você está tooenter necessária uma senha de administrador do dispositivo. Quando o primeiro dispositivo de StorSimple Olá é registrado com um serviço, a senha de padrão de saudação para essa interface é *Password1*. Para segurança de saudação dos seus dados, você está toochange necessária essa senha no final de saudação do processo de registro de saudação. Você não pode sair do processo de registro de saudação sem alterar essa senha. Para obter mais informações, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

senha Olá primeiro definida por meio da interface do Windows PowerShell Olá durante o registro pode ser alterada por meio de saudação portal clássico do Azure. Execute Olá senha de administrador etapas toochange Olá dispositivo a seguir.

#### <a name="toochange-hello-device-administrator-password"></a>senha de administrador de dispositivo toochange Olá
1. No portal clássico do hello, clique em **dispositivos** > **configurar** para seu dispositivo.
2. Role para baixo toohello **senha de administrador do dispositivo** seção. Forneça uma senha de administrador que contenha de 8 caracteres too15. senha Olá deve ser uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.
3. Confirme senha hello.
4. Clique em **salvar** final Olá Olá página.

senha de administrador do dispositivo Olá agora deve ser atualizada. Você pode usar essa senha modificada tooaccess saudação do Windows PowerShell interface.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Alterar a senha do StorSimple Snapshot Manager Olá
Gerenciador de instantâneos StorSimple software reside no host do Windows e permite que os administradores toomanage backups do seu dispositivo StorSimple na forma de saudação de locais e instantâneos em nuvem.

Ao configurar um dispositivo no Gerenciador de instantâneos do StorSimple, você será solicitado tooprovide Olá tooauthenticate de endereço e a senha IP de dispositivo de seu dispositivo de armazenamento. Essa senha será configurada primeiro por meio da interface do Windows PowerShell hello. Para obter mais informações, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

senha Olá primeiro definida por meio da interface do Windows PowerShell Olá durante o registro pode ser alterada por meio do portal clássico do hello. Execute Olá senha de Gerenciador de instantâneos StorSimple etapas toochange Olá a seguir.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>senha do toochange Olá Gerenciador de instantâneos StorSimple
1. No portal clássico do hello, clique em **dispositivos** > **configurar** para seu dispositivo.
2. Role para baixo toohello **StorSimple Snapshot Manager** seção. Insira uma senha que tenha 14 ou 15 caracteres. Verifique se que essa senha Olá contém uma combinação de 3 ou mais caracteres maiusculo, minúsculo, numérico e especial.
3. Confirme senha hello.
4. Clique em **salvar** final Olá Olá página.

senha do StorSimple Snapshot Manager Olá agora deve ser atualizada.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a [segurança do StorSimple](storsimple-security.md).
* Saiba mais sobre [como modificar a configuração do dispositivo](storsimple-modify-device-config.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

