---
title: bateria aaaReplace no dispositivo StorSimple do Microsoft Azure | Microsoft Docs
description: "Descreve como tooremove, substituir e manter o módulo de bateria de backup Olá em seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Substituir o módulo de bateria de backup Olá em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
compartimento principal de saudação Power e módulo de resfriamento (PCM) no seu dispositivo StorSimple do Microsoft Azure tem um pacote adicional de bateria. Esse pacote fornece energia para que hello dispositivo StorSimple pode salvar dados caso haja perda de compartimento principal de toohello de alimentação de CA. Esse pacote de bateria é chamado tooas Olá *módulo de bateria de backup*. módulo de bateria de backup Olá existe somente para o compartimento principal de saudação em seu dispositivo StorSimple (Olá compartimento EBOD não contém um módulo de bateria de backup). 

Este tutorial explica como:

* Remover o módulo de bateria de backup Olá 
* Instalar um novo módulo de bateria de backup
* Manter o módulo de bateria de backup Olá

> [!IMPORTANT]
> Antes de remover e substituir um módulo de bateria de backup, analisar informações de segurança Olá Olá [substituição de componentes de hardware Introdução tooStorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-backup-battery-module"></a>Remover o módulo de bateria de backup Olá
módulo de bateria de backup Olá para seu dispositivo StorSimple é uma unidade substituível de campo. Antes de ser instalada em Olá PCM, o módulo da bateria Olá deve ser armazenado em sua embalagem original. Execute Olá bateria de backup tooremove Olá etapas a seguir.

#### <a name="tooremove-hello-backup-battery-module"></a>módulo de bateria de backup Olá tooremove
1. No hello portal clássico do Azure, vá muito**dispositivos** > **manutenção** > **Status do Hardware**. Em **componentes compartilhados**, observar Olá status da bateria hello.
2. Identifica Olá PCM no qual Olá bateria falhou. A Figura 1 mostra Olá parte posterior do dispositivo do StorSimple hello.
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    **Figura 1** Parte traseira do dispositivo primário mostrando os módulos de controlador e PCM
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
   
    Conforme mostrado pelo número 3 na Figura 2 de hello, Olá monitoramento indicador LED no PCM 0 que corresponde muito**falha de bateria** deve estar aceso.
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    **Figura 2** saudação do parte posterior do PCM mostrando LEDs indicadores de monitoramento
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |Falha de energia CA |
   | 2 |Falha do ventilador |
   | 3 |Falha de bateria |
   | 4 |PCM OK |
   | 5 |Falha de energia CC |
   | 6 |Bateria íntegra |
3. Olá tooremove PCM com uma bateria com falha, execute as etapas de saudação em [remover um PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Olá PCM removido, comparação de precisão e bateria Olá girar módulo tratar para cima, conforme indicado na figura a seguir de saudação e levante-o backup de bateria de saudação tooremove.
   
    ![Removendo bateria do PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Figura 3** removendo bateria de saudação do hello PCM
5. Coloque o módulo de saudação no pacote da unidade substituível em campo hello.
6. Retorne Olá tooMicrosoft de unidade defeituosa para serviços e reparos adequados.

## <a name="install-a-new-backup-battery-module"></a>Instalar um novo módulo de bateria de backup
Execute Olá seguindo o módulo de bateria de substituição etapas tooinstall Olá no hello PCM no compartimento primário de saudação do seu dispositivo StorSimple.

#### <a name="tooinstall-hello-battery-module"></a>módulo de bateria Olá tooinstall
1. Coloque o módulo de bateria de backup de saudação na orientação correta de saudação no hello PCM.
2. Pressione para baixo o módulo da bateria Olá lidar com todas as conector de Olá Olá maneira tooseat.
3. Substituir Olá PCM no compartimento primário Olá seguindo as diretrizes Olá [substituir de energia e resfriamento módulo em seu dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).
4. Após a conclusão da substituição hello, vá muito**dispositivos** > **manutenção** > **Status de Hardware** no hello portal clássico do Azure. Verificar o status da saudação do hello bateria toomake-se de que a instalação de saudação foi bem-sucedida. Um status verde indica que a bateria hello está íntegra.

## <a name="maintain-hello-backup-battery-module"></a>Manter o módulo de bateria de backup Olá
Em seu dispositivo StorSimple, o módulo de bateria de backup Olá fornece controlador toohello de energia durante um evento de perda de energia. Ele permite Olá StorSimple dispositivo toosave dados críticos anterior tooshutting para baixo de forma controlada. Com duas baterias completamente no hello PCMs, sistema Olá pode lidar com dois eventos consecutivos de perda.

No portal clássico do Azure do hello, Olá **Status do Hardware** em Olá **manutenção** página indica se a bateria hello está funcionando corretamente ou Olá fim da vida está se aproximando. status da bateria Olá é indicado por **bateria no PCM 0** ou **bateria no PCM 1** em **componentes compartilhados**. Essa página mostrará um estado **DEGRADADO** quando próximo do fim da vida útil e **FALHA** quando atingir o fim da vida útil. 

> [!NOTE]
> Olá bateria pode relatar **falha** quando ele precisa apenas toobe cobrado.
> 
> 

Se hello **DEGRADADO** estado é exibido, é recomendável Olá curso de ação a seguir:

* sistema Olá pode encontraram uma perda de energia recentes ou baterias Olá podem ser passando por manutenção periódica. Observe o sistema Olá para 12 horas antes de continuar.
  
  * Se o estado de saudação ainda **DEGRADADO** após 12 horas de energia de tooAC de conexão contínua com hello controladores e execução, de PCMs, em seguida, Olá bateria precisa toobe substituído. Por favor [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para obter um módulo de bateria de backup de reposição.
  * Se o estado da saudação se tornará Okey após 12 horas, Olá bateria está operacional e somente é necessário um custo de manutenção.
* Se não houve uma perda associada alternada e hello PCM está ligada e conectado tooAC power, bateria Olá precisa toobe substituído. [Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) tooorder uma substituição de módulo de bateria de backup.

> [!IMPORTANT]
> Descarte Olá Falha na bateria de acordo com as normas regionais e toonational. 
> 
> 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

