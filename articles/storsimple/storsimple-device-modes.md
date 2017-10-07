---
title: "o modo do dispositivo StorSimple aaaChange Olá | Microsoft Docs"
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Alterar o modo de dispositivo Olá em seu dispositivo StorSimple
Este artigo fornece uma breve descrição da saudação vários modos em que o seu dispositivo StorSimple pode operar. O dispositivo StorSimple pode funcionar em três modos: normal, manutenção e recuperação. 

Após ler este artigo, você conhecerá:

* Quais são os modos do dispositivo StorSimple Olá
* Como toofigure o modo de Olá dispositivo StorSimple está em
* Como toochange de modo toomaintenance normal e *vice-versa*

Olá acima tarefas de gerenciamento só pode ser executada por meio da interface do Windows PowerShell de saudação do seu dispositivo StorSimple.

## <a name="about-storsimple-device-modes"></a>Sobre os modos do dispositivo StorSimple
O dispositivo StorSimple pode operar nos modos normal, de manutenção ou de recuperação. Cada um desses modos é descrito resumidamente abaixo.

### <a name="normal-mode"></a>Modo Normal
Isso é definido como modo operacional normal de saudação para um dispositivo StorSimple totalmente configurado. Por padrão, o dispositivo deve estar no modo normal.

### <a name="maintenance-mode"></a>Modo de Manutenção
Às vezes, hello dispositivo StorSimple pode ser necessário toobe colocado em modo de manutenção. Esse modo permite que você tooperform manutenção no dispositivo de saudação e instalar atualizações sem interrupção, como aquelas relacionadas toodisk firmware.

Você pode colocar o sistema de saudação em modo de manutenção por meio de saudação do Windows PowerShell para StorSimple. Todas as solicitações de E/S são pausadas neste modo. Serviços, como a memória de acesso aleatório não volátil (NVRAM) ou Olá serviço também são interrompidos. Ambos os controladores de saudação são reiniciados quando você entra ou sai deste modo. Quando você sair do modo de manutenção hello, todos os serviços de saudação serão retomada e devem ser íntegros. Isso pode levar alguns minutos.

> [!NOTE]
> **Só há suporte ao modo de Manutenção em um dispositivo que esteja funcionando corretamente. Não há suporte em um dispositivo no qual um ou ambos os controladores de saudação não estão funcionando.**
> </br>
> 
> 

### <a name="recovery-mode"></a>Modo de recuperação
O modo de recuperação pode ser descrito como "Modo Seguro do Windows com suporte de rede". Modo de recuperação aciona a equipe do Microsoft Support hello e permite tooperform diagnósticos no sistema de saudação. Olá principal objetivo do modo de recuperação é tooretrieve Olá sistema logs.

Se o sistema entrar no modo de recuperação, você deverá contatar o Suporte da Microsoft para obter as próximas etapas. Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-contact-microsoft-support.md).

> [!NOTE]
> **Você não pode colocar o dispositivo Olá no modo de recuperação. Se o dispositivo de saudação está em um estado inválido, o modo de recuperação tenta tooget dispositivo de saudação em um estado em que a equipe do Microsoft Support possa examiná-lo.**
> 
> 

## <a name="determine-storsimple-device-mode"></a>Determinar o modo do dispositivo StorSimple
#### <a name="toodetermine-hello-current-device-mode"></a>modo de dispositivo toodetermine Olá atual
1. Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Examine a mensagem de saudação do banner no menu do console serial saudação do dispositivo hello. Esta mensagem indica explicitamente se o dispositivo hello está no modo de manutenção ou recuperação. Se a mensagem de saudação não contém informações específicas relativas toohello modo de sistema, o dispositivo de saudação está no modo normal.

## <a name="change-hello-storsimple-device-mode"></a>Alterar o modo de saudação do dispositivo StorSimple
Você pode colocar o dispositivo StorSimple Olá em manutenção de tooperform modo (no modo normal) de manutenção ou instalar atualizações do modo de manutenção. Execute Olá modo de manutenção de tooenter ou sair de procedimentos a seguir.

> [!IMPORTANT]
> Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros acessando Olá **Status do Hardware** em Olá **manutenção** página Olá portal clássico do Azure. Se um ou ambos os controladores de saudação não estão íntegros, entre em contato com o Microsoft Support para as próximas etapas hello. Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-contact-microsoft-support.md).
> 
> 

#### <a name="tooenter-maintenance-mode"></a>modo de manutenção de tooenter
1. Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado, forneça Olá **senha de administrador do dispositivo**. Olá a senha padrão é: `Password1`.
3. No prompt de comando hello, digite 
   
    `Enter-HcsMaintenanceMode`
4. Você verá uma mensagem de aviso informando que o modo de manutenção irá interromper todas as solicitações de e/s e servidor Olá conexão toohello portal clássico do Azure, e você será solicitado a confirmar. Tipo **Y** tooenter modo de manutenção.
5. Ambos os controladores serão reiniciados. Quando a saudação reinicialização é concluída, outra mensagem será exibida indicando que o dispositivo hello está no modo de manutenção.

#### <a name="tooexit-maintenance-mode"></a>modo de manutenção de tooexit
1. Faça logon no console serial do dispositivo toohello. Verificar da mensagem de saudação do banner que seu dispositivo está no modo de manutenção.
2. No prompt de comando hello, digite:
   
    `Exit-HcsMaintenanceMode`
3. Uma mensagem de aviso e uma mensagem de confirmação serão exibidas. Tipo **Y** tooexit modo de manutenção.
4. Ambos os controladores serão reiniciados. Quando a saudação reinicialização é concluída, outra mensagem será exibida indicando que o dispositivo Olá está no modo normal.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[aplicar as atualizações do modo normal e manutenção](storsimple-update-device.md) em seu dispositivo StorSimple.

