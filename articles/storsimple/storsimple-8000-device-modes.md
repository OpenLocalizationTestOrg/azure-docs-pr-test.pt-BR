---
title: modo de dispositivo do StorSimple aaaChange | Microsoft Docs
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
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


### <a name="recovery-mode"></a>Modo de recuperação

O modo de recuperação pode ser descrito como "Modo Seguro do Windows com suporte de rede". Modo de recuperação aciona a equipe do Microsoft Support hello e permite tooperform diagnósticos no sistema de saudação. Olá principal objetivo do modo de recuperação é tooretrieve Olá sistema logs.

Se o sistema entrar no modo de recuperação, você deverá contatar o Suporte da Microsoft para obter as próximas etapas. Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).

> [!NOTE]
> **Você não pode colocar o dispositivo Olá no modo de recuperação. Se o dispositivo de saudação está em um estado inválido, o modo de recuperação tenta tooget dispositivo de saudação em um estado em que a equipe do Microsoft Support possa examiná-lo.**

## <a name="determine-storsimple-device-mode"></a>Determinar o modo do dispositivo StorSimple

#### <a name="toodetermine-hello-current-device-mode"></a>modo de dispositivo toodetermine Olá atual

1. Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Examine a mensagem de saudação do banner no menu do console serial saudação do dispositivo hello. Esta mensagem indica explicitamente se o dispositivo hello está no modo de manutenção ou recuperação. Se a mensagem de saudação não contém informações específicas relativas toohello modo de sistema, o dispositivo de saudação está no modo normal.

## <a name="change-hello-storsimple-device-mode"></a>Alterar o modo de saudação do dispositivo StorSimple

Você pode colocar o dispositivo StorSimple Olá em manutenção de tooperform modo (no modo normal) de manutenção ou instalar atualizações do modo de manutenção. Execute Olá modo de manutenção de tooenter ou sair de procedimentos a seguir.

> [!IMPORTANT]
> Antes de entrar no modo de manutenção, verifique se ambos os controladores estão íntegros acessando Olá **configurações do dispositivo > integridade do Hardware** para seu dispositivo no hello portal do Azure. Se um ou ambos os controladores de saudação não estão íntegros, entre em contato com o Microsoft Support para as próximas etapas hello. Para obter mais informações, vá muito[entre em contato com o suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).
 

#### <a name="tooenter-maintenance-mode"></a>modo de manutenção de tooenter

1. Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado, forneça Olá **senha de administrador do dispositivo**. Olá a senha padrão é: `Password1`.
3. No prompt de comando hello, digite 
   
    `Enter-HcsMaintenanceMode`
4. Você verá uma mensagem de aviso informando que o modo de manutenção irá interromper todas as solicitações de e/s e servidor Olá conexão toohello portal do Azure, e você será solicitado a confirmar. Tipo **Y** tooenter modo de manutenção.
5. Ambos os controladores serão reiniciados. Quando Olá reinicialização é concluída, faixa de console serial Olá indicará que dispositivo hello está no modo de manutenção. Um exemplo de saída é mostrado abaixo.

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>modo de manutenção de tooexit

1. Faça logon no console serial do dispositivo toohello. Verificar da mensagem de saudação do banner que seu dispositivo está no modo de manutenção.
2. No prompt de comando hello, digite:
   
    `Exit-HcsMaintenanceMode`
3. Uma mensagem de aviso e uma mensagem de confirmação serão exibidas. Tipo **Y** tooexit modo de manutenção.
4. Ambos os controladores serão reiniciados. Quando Olá reinicialização é concluída, faixa de console serial Olá indica que dispositivo hello está no modo normal. Um exemplo de saída é mostrado abaixo.

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[aplicar as atualizações do modo normal e manutenção](storsimple-update-device.md) em seu dispositivo StorSimple.

