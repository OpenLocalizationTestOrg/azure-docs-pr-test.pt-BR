---
title: "aaaTurn seu dispositivo da série StorSimple 8000 ou desativar | Microsoft Docs"
description: "Explica como ativar um dispositivo que foi desligado ou perdido de energia tooturn em um novo dispositivo StorSimple, e desativar um dispositivo em execução."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Ativar ou desativar seu dispositivo StorSimple série 8000
## <a name="overview"></a>Visão geral
Desligar um dispositivo Microsoft Azure StorSimple não é necessário como parte da operação normal do sistema. No entanto, talvez seja necessário tooturn em um novo dispositivo ou um dispositivo que teve toobe desligar. Em geral, um desligamento é necessário em casos em que você deve substituir o hardware com falha, mover uma unidade fisicamente ou retirar um dispositivo de serviço. Este tutorial descreve o procedimento Olá necessário para ligar e desligar seu dispositivo StorSimple em cenários diferentes.

## <a name="turn-on-a-new-device"></a>Ativar um novo dispositivo
Olá etapas para ativar um dispositivo StorSimple para Olá primeira vez diferem dependendo se o dispositivo de saudação é um 8100 ou um modelo 8600. Olá 8100 tem um único compartimento primário, enquanto Olá 8600 é um dispositivo de duplo compartimento com um compartimento principal e um compartimento EBOD. Olá etapas detalhadas para ambos os modelos são abordadas em Olá seções a seguir.

* [Novo dispositivo com apenas o compartimento primário](#new-device-with-primary-enclosure-only)
* [Novo dispositivo com o compartimento EBOD](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Novo dispositivo com apenas o compartimento primário
modelo de saudação StorSimple 8100 é um dispositivo de compartimento único. Seu dispositivo inclui PCMs (Módulos de Energia e Refrigeração) redundantes. Ambos os PCMs devem ser instalados e conectados toodifferent power fontes tooensure alta disponibilidade.

Execute Olá toocable as etapas a seguir seu dispositivo de alimentação.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Para obter instruções de cabeamento e concluir configuração do dispositivo, vá muito[instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md). Certifique-se de que você siga as instruções de saudação exatamente.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Novo dispositivo com o compartimento EBOD
modelo Olá 8600 StorSimple possui um compartimento principal e um compartimento EBOD. Isso requer Olá unidades toobe cabeada de alimentação e conectividade de SCSI Serial anexado (SAS).

Ao configurar este dispositivo para Olá primeira vez, execute as etapas de saudação para cabeamento SAS primeiro hello, em seguida, concluir etapas para cabeamento de alimentação.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Para obter instruções de cabeamento e concluir configuração do dispositivo, vá muito[instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md). Certifique-se de que você siga as instruções de saudação exatamente.

## <a name="turn-on-a-device-after-shutdown"></a>Ativar um dispositivo após o desligamento
etapas de saudação para ativar um dispositivo StorSimple depois que ele foi desligado são diferentes dependendo se o dispositivo de saudação é um 8100 ou um modelo 8600. Olá 8100 tem um único compartimento primário, enquanto Olá 8600 é um dispositivo de duplo compartimento com um compartimento principal e um compartimento EBOD.

* [Dispositivo com apenas o compartimento primário](#device-with-primary-enclosure-only)
* [Dispositivo com o compartimento EBOD](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Dispositivo com apenas o compartimento primário
Após um desligamento, use Olá tooturn do procedimento a seguir em um dispositivo StorSimple com um compartimento principal e nenhum agrupamento EBOD.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn em um dispositivo com apenas um compartimento principal
1. Certificar-se de que Olá interruptores sobre ambas as fontes de alimentação e módulos de refrigeração (PCMs) estão na posição OFF de saudação. Se Olá opções não estão na posição de OFF hello, em seguida, inverta-los toohello desliga e aguarde Olá luzes toogo off.
2. Ative o dispositivo Olá colocando os interruptores Olá em ambos os PCMs toohello na posição. Olá dispositivo deve estar ligado.
3. Olá seleção após tooverify que Olá dispositivo esteja completamente ligado:
   
   1. Olá Okey LEDs em ambos os módulos PCM estão verdes.
   2. Olá LEDs de ambos os controladores estão verdes sólidos.
   3. Olá piscando, o LED azul em um dos controladores de saudação que indica que Olá controlador está ativo.
      
      Se alguma dessas condições não for atendida, o dispositivo não está íntegro. [Entre em contato com o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Dispositivo com o compartimento EBOD
Após um desligamento, use Olá tooturn do procedimento a seguir em um dispositivo StorSimple com um compartimento principal e um compartimento EBOD. Execute cada etapa na sequência exatamente conforme descrito. Portanto, toodo falha pode resultar em perda de dados.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn em um dispositivo com um principal e um compartimento EBOD
1. Certifique-se de que Olá compartimento EBOD é o compartimento principal toohello conectado. Para obter mais informações, consulte [Instalar o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Certifique-se de que Olá Power e módulos de refrigeração (PCMs) no hello EBOD e compartimentos primários estão na posição OFF de saudação. Se Olá opções não estão na posição de OFF hello, em seguida, inverta-los toohello desliga e aguarde Olá luzes toogo off.
3. Ative Olá compartimento EBOD primeiro colocando os interruptores Olá em ambos os PCMs toohello na posição. Olá LEDs de PCM deve estar verde. Um controlador do EBOD LED verde nesta unidade indica que o compartimento EBOD de saudação é no.
4. Ative o compartimento principal Olá colocando os interruptores Olá em ambos os PCMs toohello na posição. todo o sistema Olá agora deverá estar ligado.
5. Verifique se Olá LEDs de SAS estão verdes, o que garante que essa conexão Olá entre hello compartimento EBOD e compartimento principal Olá é bom.

## <a name="turn-on-a-device-after-a-power-loss"></a>Ativar um dispositivo após uma queda de energia
Uma interrupção de energia pode desligar um dispositivo StorSimple. falta de energia Olá pode ocorrer em uma das fontes de alimentação hello ou ambas as fontes de alimentação. etapas de recuperação de saudação são diferentes dependendo se o dispositivo de saudação é um 8100 ou um modelo 8600. Olá 8100 tem um único compartimento primário, enquanto Olá 8600 é um dispositivo de duplo compartimento com um compartimento principal e um compartimento EBOD. Esta seção descreve o procedimento de recuperação Olá para cada cenário.

* [Dispositivo com apenas o compartimento primário](#8100)
* [Dispositivo com o compartimento EBOD](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Dispositivo com apenas o compartimento primário <a name="8100">
sistema de saudação pode continuar sua operação normal, se houver tooone de perda de energia de suas fontes de alimentação. No entanto, tooensure alta disponibilidade do dispositivo hello, restauração power toohello fonte de alimentação assim que possível.

Se houver uma queda de energia ou queda de energia em ambas as fontes de alimentação, sistema de saudação será desligado de forma controlada e ordenada. Quando Olá energia for restaurada, o sistema Olá será automaticamente ligado.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Dispositivo com o compartimento EBOD <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Perda de energia em uma fonte de alimentação
sistema de Olá pode continuar sua operação normal, se houver tooone de perda de energia de suas fontes de alimentação no compartimento principal hello ou compartimento do EBOD hello. No entanto, tooensure alta disponibilidade do dispositivo hello, restaure alimentação de energia toohello assim que possível.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Perda de energia em ambas as fontes de alimentação nos compartimentos primário e EBOD
Se houver uma queda de energia interrupção ou energia em ambas as fontes de alimentação, Olá compartimento EBOD será desligado imediatamente e o compartimento principal Olá será desligado de forma controlada e ordenada. Quando a energia for restaurada, o dispositivo Olá será iniciado automaticamente.

Se power Olá for desligado manualmente, depois, pegue Olá etapas toorestore alimentação toohello de sistema a seguir.

1. Ative Olá compartimento EBOD.
2. Depois de Olá compartimento EBOD está ativado, ative o compartimento principal hello.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Perda de energia em ambas as fontes de alimentação no compartimento EBOD
Quando você configura os cabos, você deve garantir que Olá EBOD nunca é conectado sozinho tooa separar PDU. Se hello EBOD e o compartimento principal falharem em Olá mesmo tempo, o sistema Olá recuperará.

Se apenas Olá compartimento EBOD falha em ambas as fontes de alimentação, o sistema de saudação não se recuperará automaticamente. Obtém Olá tooturn as etapas a seguir no sistema hello e restaurá-lo tooa o estado íntegro:

1. Se o compartimento principal Olá é ativado, desative os módulos de energia e resfriamento (PCMs).
2. Aguarde alguns minutos para Olá sistema tooshut para baixo.
3. Ative Olá compartimento EBOD.
4. Depois de Olá compartimento EBOD está ativado, ative o compartimento principal hello.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Ativar um dispositivo após Olá primária e a conexão do compartimento EBOD for perdida
Se a conexão de saudação for perdida entre o controlador em espera hello e controlador EBOD correspondente de Olá, dispositivo Olá continua toowork. Se a conexão Olá entre o controlador ativo do sistema hello e o controlador EBOD correspondente de saudação for perdida, failover deve ocorrer e dispositivo Olá deve continuar toowork como normal.

Quando ambos os cabos de SCSI Serial anexado (SAS) forem removidos ou conexão Olá entre hello compartimento EBOD e o compartimento principal Olá for desfeita, o dispositivo Olá irá parar de funcionar. Neste ponto, execute Olá etapas a seguir.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn no dispositivo de saudação após a conexão for perdida
1. Saudação de acesso parte posterior do dispositivo hello.
2. Se Olá conexão de cabo SAS entre o compartimento do EBOD hello e o compartimento principal Olá for interrompida, todos os SAS LEDs da rota em Olá compartimento EBOD ficarão desligados.
3. Desligue os módulos de energia e resfriamento (PCMs) no compartimento do EBOD hello e o compartimento principal hello.
4. Aguarde até que todas as luzes Olá Olá parte posterior de ambos os compartimentos Olá desativar.
5. Insira novamente os cabos SAS hello e certifique-se de que haja uma boa conexão entre o compartimento do EBOD hello e o compartimento principal hello.
6. Ative Olá compartimento EBOD primeiro colocando ambos os comutadores PCM toohello na posição.
7. Certifique-se de que o compartimento EBOD de saudação é ativado por verificando se o LED verde do hello está ON.
8. Ative o compartimento principal hello.
9. Certifique-se de que o compartimento principal Olá é ativado por verificando se o LED verde do controlador de saudação está no.
10. Verifique se que essa conexão do compartimento EBOD com o compartimento principal Olá Olá é boa verificando rota de SAS que Olá LEDs (quatro por controlador EBOD) estão todos em.

> [!IMPORTANT]
> Se os cabos SAS de saudação estiverem com defeito ou conexão Olá entre hello compartimento EBOD e o compartimento principal Olá não for boa, quando você ativar o sistema hello, ele entrará no modo de recuperação. [Entre em contato com o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) se isso ocorrer.


## <a name="turn-off-a-running-device"></a>Desativar um dispositivo em execução
Um dispositivo StorSimple em execução pode ser necessário toobe desligado se ele estiver sendo movido, retirado de serviço, ou tem um componente de mau funcionamento que precisa toobe substituído. etapas de saudação são diferentes dependendo se o dispositivo StorSimple Olá é um 8100 ou em um modelo 8600. Olá 8100 tem um único compartimento primário, enquanto Olá 8600 é um dispositivo de duplo compartimento com um compartimento principal e um compartimento EBOD. Esta seção detalha Olá etapas tooshut um dispositivo em execução.

* [Dispositivo com o compartimento primário](#8100a)
* [Dispositivo com o compartimento EBOD](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Dispositivo com o compartimento primário <a name="8100a">
tooshut dispositivo saudação de forma controlada e ordenada, você pode fazer isso por meio da saudação portal clássico do Azure ou saudação do Windows PowerShell para StorSimple. 

> [!IMPORTANT]
> Não desligue um dispositivo em execução usando o botão liga / desliga Olá em Olá parte posterior do dispositivo hello.
> 
> Antes de desligar o dispositivo hello, certifique-se de que todos os componentes do dispositivo Olá estão íntegros. Olá portal clássico do Azure no, navegue muito**dispositivos** > **manutenção** > **Status do Hardware**e verifique se o status de todos os Olá componentes está verde. Isso se aplica apenas a um sistema íntegro. Se o sistema hello está sendo desligado tooreplace um componente de mau funcionamento, você verá um falha (vermelho) ou degradado (amarelo) status de componente respectivos Olá Olá **Status do Hardware**.
> 
> 

Depois de acessar saudação do Windows PowerShell para StorSimple ou hello portal clássico do Azure, siga as etapas de saudação em [desligar um dispositivo StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Dispositivo com o compartimento EBOD <a name="8600a">
> [!IMPORTANT]
> Antes de desligar o compartimento principal hello e compartimento do EBOD hello, certifique-se de que todos os componentes do dispositivo Olá estão íntegros. Olá portal do Azure no, navegue muito**dispositivos** > **Monitor** > **a integridade do Hardware**e verifique se todos os componentes de saudação estão íntegros.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut um dispositivo em execução com o compartimento EBOD
1. Siga todas as etapas de Olá listadas na [desligar um dispositivo StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) para o compartimento principal hello.
2. Após Olá compartimento principal for desligado, desligue Olá EBOD colocando desativar as opções de energia e o módulo de resfriamento (PCM).
3. tooverify que Olá EBOD desligou, verifique se todas as luzes na Olá parte traseira do compartimento do EBOD Olá são desativados.

> [!NOTE]
> cabos SAS de Hello são usadas tooconnect Olá EBOD compartimento toohello compartimento principal não devem ser removidos até depois Olá sistema é desligado.

## <a name="next-steps"></a>Próximas etapas
[Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) se você encontrar problemas ao ativar ou desligar um dispositivo StorSimple.

