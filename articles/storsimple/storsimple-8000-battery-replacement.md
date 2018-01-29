---
title: "Substituir a bateria em um dispositivo Microsoft Azure StorSimple da série 8000 | Microsoft Docs"
description: "Descreve como remover, substituir e realizar manutenção no módulo de bateria de backup do dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: jeconnoc
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 01/09/2018
ms.author: alkohli
ms.openlocfilehash: f8071cde67017ff031418f0d97da15a618c4969b
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a>Substitua o módulo de bateria de backup no dispositivo StorSimple

## <a name="overview"></a>Visão geral
O módulo de energia e refrigeração (PCM) do compartimento primário no dispositivo Microsoft Azure StorSimple tem um pacote de bateria adicional. Esse pacote fornece energia para que o dispositivo StorSimple possa salvar dados caso haja perda de energia CA no compartimento primário. Esse pacote de bateria é conhecido como *módulo de bateria de backup*. O módulo de bateria de backup existe somente para o compartimento primário em seu dispositivo StorSimple (o compartimento EBOD não contém um módulo de bateria de backup).

Este tutorial explica como:

* Remover o módulo de bateria de backup
* Instalar um novo módulo de bateria de backup
* Realizar manutenção no módulo de bateria de backup

> [!IMPORTANT]
> Antes de remover e de substituir um módulo de bateria de backup, examine as informações de segurança em [Introdução à substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-the-backup-battery-module"></a>Remover o módulo de bateria de backup
O módulo de bateria de backup de seu dispositivo StorSimple é uma unidade substituível no local. Antes de ser instalado no PCM, o módulo de bateria deve ser armazenado em seu pacote original. Execute as etapas a seguir para remover a bateria de backup.

#### <a name="to-remove-the-backup-battery-module"></a>Para remover o módulo de bateria de backup
1. No Portal do Azure, acesse sua folha do serviço do Gerenciador de Dispositivos do StorSimple. Acesse **Dispositivos** e selecione seu dispositivo na lista de dispositivos. Navegue até **Monitorar** > **Integridade de hardware**. Em **Componentes compartilhados**, observe o status da bateria.
2. Identifique o PCM no qual a bateria falhou. A Figura 1 mostra a parte traseira do dispositivo StorSimple.
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    **Figura 1** Parte traseira do dispositivo primário mostrando os módulos de controlador e PCM
   
   | Rótulo | DESCRIÇÃO |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
   
    Conforme mostrado pelo número 3 na Figura 2, o LED indicador de monitoramento no PCM 0 que corresponde à **Falha de bateria** deve estar aceso.
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    **Figura 2** Parte traseira do PCM mostrando os LEDs indicadores de monitoramento
   
   | Rótulo | DESCRIÇÃO |
   |:--- |:--- |
   | 1 |Falha de energia CA |
   | 2 |Falha do ventilador |
   | 3 |Falha de bateria |
   | 4 |PCM OK |
   | 5 |Falha de energia CC |
   | 6 |Bateria íntegra |
3. Para remover o PCM com uma bateria com falha, siga as etapas em [Remover um PCM](storsimple-8000-power-cooling-module-replacement.md#remove-a-pcm).
4. Com o PCM removido, levante e gire a alça do módulo da bateria para cima, conforme indicado na figura a seguir, e puxe-a para remover a bateria.
   
    ![Removendo bateria do PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Figura 3** Remoção da bateria do PCM
5. Coloque o módulo na embalagem da unidade substituível no local.
6. Devolva a unidade com defeito à Microsoft para que a manutenção e o manuseio adequados sejam realizados.

## <a name="install-a-new-backup-battery-module"></a>Instalar um novo módulo de bateria de backup
Execute as etapas a seguir para instalar o módulo de bateria de reposição no PCM no compartimento primário do seu dispositivo StorSimple.

#### <a name="to-install-the-battery-module"></a>Para instalar o módulo de bateria
1. Coloque o módulo de bateria de backup na direção correta no PCM.
2. Pressione para baixo a alça do módulo da bateria até o conector no banco
3. Substitua o PCM no compartimento primário, seguindo as orientações em [Substituir um módulo de energia e refrigeração no seu dispositivo StorSimple](storsimple-8000-power-cooling-module-replacement.md).
4. Após a conclusão da substituição, acesse seu dispositivo e vá para **Monitorar** > **Integridade de hardware** no Portal do Azure. Verifique o status da bateria para se certificar de que a instalação foi bem-sucedida. Um status verde indica que a bateria está íntegra.

## <a name="maintain-the-backup-battery-module"></a>Realizar manutenção no módulo de bateria de backup
No seu dispositivo StorSimple, o módulo de bateria de backup fornece energia ao controlador durante um evento de perda de energia. Ele permite que o dispositivo StorSimple salve dados críticos antes de encerrar de maneira controlada. Com duas baterias completamente carregadas nos PCMs, o sistema pode manipular dois eventos consecutivos de perda.

No Portal do Azure, a **Integridade de hardware** abaixo da folha **Monitorar** indica se a bateria está com defeito ou se ela está próxima do fim do tempo de vida. O status da bateria é indicado por **Bateria no PCM 0** ou **Bateria no PCM 1** em **Componentes compartilhados**. Essa folha mostrará um estado **DEGRADADO** quando ela estiver próxima do fim do tempo de vida e **FALHA** quando atingir o fim do tempo de vida.

> [!NOTE]
> A bateria pode relatar **FALHA** quando precisar apenas ser carregada.


Se o estado **DEGRADADO** for exibido, recomendamos o seguinte curso de ação:

* O sistema pode ter tido uma perda de energia recente ou as baterias podem estar passando por manutenção periódica. Observe o sistema por 12 horas antes de continuar.
  
  * Se o estado ainda estiver **DEGRADADO** após 12 horas de conexão contínua à energia CA com os controladores e os PCMs em execução, então a bateria precisará ser substituída. Por favor [Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) para obter um módulo de bateria de backup de reposição.
  * Se o estado estiver OK após 12 horas, a bateria está operacional e precisava apenas de uma carga de manutenção.
* Se não houve uma perda associada à energia AC e o PCM está ligado e conectado à corrente alternada, a bateria precisa ser substituído. [Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) para solicitar um módulo de bateria de reposição.

> [!IMPORTANT]
> Descarte a bateria com falha de acordo com as regulamentações nacionais e regionais.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).

