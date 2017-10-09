---
title: "aaaModify DATA 0 configurações de dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooreconfigure Olá interface de rede 0 de dados no seu dispositivo StorSimple."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a>Modificar configurações de interface de rede 0 Olá dados em seu dispositivo da série StorSimple 8000

## <a name="overview"></a>Visão geral

Seu dispositivo do Microsoft Azure StorSimple possui seis interfaces de rede, de DATA 0 tooDATA 5. Olá DATA 0 interface é sempre configurada através da interface do Windows PowerShell hello ou console serial hello e será automaticamente habilitado para a nuvem. Observe que você não pode configurar a interface de rede 0 de dados por meio de saudação portal do Azure.

Olá interface DATA 0 é primeiro configurada por meio do Assistente de instalação Olá durante a implantação inicial do dispositivo do StorSimple hello. Quando o dispositivo de saudação estiver em um modo operacional, talvez seja necessário tooreconfigure DATA 0 configurações. Este tutorial fornece dois métodos toomodify dados 0 as configurações de rede, tanto por meio do Windows PowerShell para StorSimple.

Depois de ler este tutorial, você poderá:

* Modificar dados 0 configuração por meio do Assistente de instalação de saudação de rede
* Modificar as configurações de rede 0 de dados por meio de saudação `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modificar as configurações de rede de DADOS 0 por meio do assistente de instalação
Você pode reconfigurar as configurações de rede 0 de dados conectando-se a interface do Windows PowerShell toohello do seu dispositivo StorSimple e iniciar uma sessão do Assistente de instalação. Executar Olá seguindo as etapas toomodify DATA 0 configurações:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>configurações de rede 0 toomodify dados por meio do Assistente de instalação
1. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado forneça Olá **senha de administrador do dispositivo**. Olá a senha padrão é `Password1`.
2. No prompt de comando hello, digite:
   
    `Invoke-HcsSetupWizard`
3. Um Assistente de instalação aparece toohelp configurar Olá DATA 0 interface do dispositivo. Fornece novos valores de máscara de rede, o gateway e o endereço IP de saudação.

> [!NOTE]
> Olá fixa controladores IPs precisará toobe reconfigurada por meio de saudação **as configurações de rede** folha do dispositivo StorSimple Olá Olá portal do Azure. Para obter mais informações, vá muito[modificar interfaces de rede](storsimple-8000-modify-device-config.md#modify-network-interfaces).

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modificar as configurações de rede de DADOS 0 por meio do cmdlet Set-HcsNetInterface
Tooreconfigure uma maneira alternativa DATA 0 é de interface de rede através do uso de saudação do hello `Set-HcsNetInterface` cmdlet. Olá cmdlet é executado na interface do Windows PowerShell de saudação do seu dispositivo StorSimple. Ao usar esse procedimento, IPs fixos do controlador Olá também pode ser configurado aqui. Executar Olá seguindo as etapas toomodify Olá DATA 0 configurações: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>configurações de rede 0 toomodify dados por meio do cmdlet Set-HcsNetInterface de saudação
1. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado forneça a senha de administrador de dispositivo de saudação. Olá a senha padrão é `Password1`.
2. No prompt de comando hello, digite:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Olá angular parênteses, digite Olá valores a seguir para DATA 0:
   
   * Endereço IPv4
   * Gateway IPv4
   * Máscara da sub-rede IPv4
   * Endereço IPv4 fixo para o controlador 0
   * Endereço IPv4 fixo para o controlador 1
     
     Para obter mais informações sobre o uso de saudação desse cmdlet, vá muito[do Windows PowerShell para referência de cmdlet do StorSimple](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Próximas etapas
* interfaces de rede tooconfigure diferente de DATA 0, você pode usar o hello [definir configurações de rede no portal do Azure de saudação](storsimple-8000-modify-device-config.md). 
* Se você tiver problemas ao configurar as interfaces de rede, consulte muito[solucionar problemas de implantação](storsimple-troubleshoot-deployment.md).

