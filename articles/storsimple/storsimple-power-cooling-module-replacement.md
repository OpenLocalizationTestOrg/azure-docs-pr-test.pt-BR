---
title: aaaReplace um PCM do dispositivo StorSimple | Microsoft Docs
description: "Explica como tooremove e substituir Olá energia e o módulo de resfriamento (PCM) no seu dispositivo StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Substituir um módulo de energia e resfriamento em seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Olá Power e módulo de resfriamento (PCM) no seu dispositivo StorSimple do Microsoft Azure consiste em uma fonte de alimentação e ventiladores de resfriamento que são controladas pela hello primário e compartimentos EBOD. Há apenas um modelo de PCM que é certificado para cada compartimento. compartimento principal Olá é certificado para um PCM de 764 W e compartimento do EBOD Olá é certificado para um PCM de 580 W. Embora hello PCMs para o compartimento principal hello e compartimento do EBOD Olá forem diferentes, o procedimento de substituição de saudação é idêntico.

Este tutorial explica como:

* Remover um PCM
* Instalar um PCM de reposição

> [!IMPORTANT]
> Antes de remover e substituir um PCM, revise as informações de segurança de saudação em [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="before-you-replace-a-pcm"></a>Antes de substituir um PCM
Esteja ciente das questões importantes a seguir antes de substituir o PCM de saudação:

* Se a fonte de alimentação de saudação do hello PCM falhar, mantenha Olá módulo com falha instalado, mas remova o cabo de alimentação Olá. ventilador Olá continuará tooreceive energia do compartimento hello e continuar tooprovide o resfriamento apropriado. Se Olá ventilador falhar, Olá PCM deve toobe substituído imediatamente.
* Antes de remover Olá PCM, desconecte Olá Olá PCM desligando o interruptor principal hello (se houver) ou removendo fisicamente o cabo de alimentação hello. Isso fornece um sistema de tooyour de aviso que a energia será desligada iminente.
* Certifique-se que Olá para que outro PCM está funcionando continua operação do sistema antes de substituir Olá PCM com falha. Um PCM defeituoso deve ser substituído por um PCM totalmente operacional assim que possível.
* Substituição do módulo PCM leva apenas alguns toocomplete de minutos, mas ela deve ser concluída em 10 minutos da remoção Olá falhado PCM tooprevent superaquecimento.
* Note que Olá substituição 764 W PCM módulos enviados da fábrica de saudação não contém o módulo de bateria de backup hello. Será necessário tooremove bateria de saudação do seu PCM com falha e, em seguida, inseri-lo em substituição do módulo anterior tooperforming saudação do hello substituição. Para obter mais informações, consulte como muito[remover e inserir um módulo de bateria de backup](storsimple-battery-replacement.md).

## <a name="remove-a-pcm"></a>Remover um PCM
Siga estas instruções quando estiver pronto tooremove uma potência e o módulo de resfriamento (PCM) do seu dispositivo StorSimple do Microsoft Azure.

> [!NOTE]
> Antes de remover o PCM, verifique se você tem uma substituição correta (764 W para o compartimento principal Olá) ou 580 W para Olá compartimento EBOD.
> 
> 

#### <a name="tooremove-a-pcm"></a>tooremove um PCM
1. No portal clássico do Azure do hello, clique em **dispositivos** > **manutenção** > **Status do Hardware**. Verificar o status de saudação de componentes PCM Olá em **componentes compartilhados** tooidentify qual PCM falhou:
   
   * Se uma fonte de alimentação no PCM 0 falhou, Olá status de **fonte de alimentação no PCM 0** será vermelho.
   * Se uma fonte de alimentação no PCM 1 tiver falhado, Olá status de **fonte de alimentação no PCM 1** será vermelho.
   * Se o ventilador Olá no PCM 1 tiver falhado, Olá status de **resfriamento 0 para o PCM 0** ou **resfriamento 1 para o PCM 0** será vermelho.
2. Localize Olá PCM com falha em Olá fazer do compartimento primário hello. Se você estiver executando um modelo 8600, identificar compartimento principal Olá examinando Olá número de identificação da unidade de sistema mostradas na exibição de LED do painel frontal Olá. Olá padrão é a ID de unidade exibida no compartimento primário Olá **00**, enquanto o saudação padrão ID de unidade exibida no compartimento EBOD de saudação é **01**. Olá seguinte diagrama e tabela explicam painel frontal de saudação da exibição Olá LED.
   
    ![ID do sistema na no painel de operações frontal](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Figura 1** painel frontal do dispositivo Olá  
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |Botão silenciar |
   | 2 |Energia do sistema |
   | 3 |Falha do módulo |
   | 4 |Falha lógica |
   | 5 |Exibição da ID da unidade |
3. Olá LEDs indicadores no hello parte traseira do compartimento principal Olá de monitoramento também pode ser usado tooidentify Olá PCM com falha. Consulte Olá seguinte diagrama e tabela toounderstand como toouse Olá LEDs toolocate Olá PCM com falha. Por exemplo, se hello LED correspondente toohello **falha do ventilador** estiver aceso, Olá ventilador falhou. Da mesma forma, se hello LED correspondente muito**falha de CA** estiver aceso, Olá alimentação falhou. 
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Figura 2** Parte posterior do PCM com LEDs indicadores
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |Falha de energia CA |
   | 2 |Falha do ventilador |
   | 3 |Falha de bateria |
   | 4 |PCM OK |
   | 5 |Falha de energia CC |
   | 6 |Bateria íntegra |
4. Consulte toohello diagrama de saudação parte posterior do módulo do PCM Olá StorSimple dispositivo toolocate Olá falhado a seguir. PCM 0 está Olá esquerda e PCM 1 está saudação à direita. tabela Olá a seguir explica módulos hello.
   
     ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Figura 3** Parte traseira do dispositivo com módulos de plug-in 
   
   | Rótulo | Descrição |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
5. Ativar logoff Olá PCM com falha e desconecte o cabo da fonte de alimentação hello. Agora você pode remover Olá PCM.
6. Segure a trava hello e Olá da saudação PCM tratar entre o polegar e o dedo indicador e pressione-as alça de saudação tooopen juntos.
   
    ![Abrindo a alça do PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Figura 4** tratar Olá abertura PCM
7. Segure a alça de saudação e remova Olá PCM.
   
    ![Removendo o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Figura 5** Olá removendo PCM

## <a name="install-a-replacement-pcm"></a>Instalar um PCM de reposição
Siga essas instruções tooinstall um PCM no seu dispositivo StorSimple. Certifique-se de que você inseriu Olá bateria de backup anteriores tooinstalling Olá substituição do módulo de PCM (aplica-se too764 PCMs W). Para obter mais informações, consulte como muito[remover e inserir um módulo de bateria de backup](storsimple-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall um PCM
1. Verifique se você tem Olá PCM de substituição correto para esse compartimento. compartimento principal Olá precisa de um PCM de 764 W e Olá compartimento EBOD precisa de um PCM de 580 W. Não tente toouse Olá PCM de 580 W no compartimento primário hello, ou Olá PCM de 764 W em Olá compartimento EBOD. Olá a imagem a seguir mostra onde tooidentify essas informações em Olá rótulo que é afixada toohello PCM.
   
    ![Etiqueta do PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Figura 6** Etiqueta do PCM
2. Verifique se há compartimento de toohello dano, prestando atenção especial toohello conectores. 
   
   > [!NOTE]
   > **Não instale o módulo de saudação se os pinos do conector estiver torto.**
   > 
   > 
3. Com hello PCM manipular Olá abra posição, módulo de saudação do slide para compartimento de saudação.
   
    ![Instalando o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Figura 7** Olá instalando PCM
4. Feche manualmente a alça do PCM hello. Você ouvirá um clique quando Olá trava da alça encaixar. 
   
   > [!NOTE]
   > tooensure que Olá pinos do conector estão encaixados, puxe levemente no identificador de saudação sem soltar a trava hello. Se Olá PCM Deslizar para fora, significa que Olá trava fechou antes do conectores Olá envolvido.
   > 
   > 
5. Conecte a fonte de alimentação Olá power cabos toohello e toohello PCM.
6. Proteja a tensão Olá alívio de tensão. 
7. Ative Olá PCM.
8. Verificar se a substituição de saudação foi bem-sucedida: Olá portal clássico do Azure do seu serviço StorSimple Manager, navegue muito**dispositivos** > **manutenção**  >  **Status do hardware**. Em **componentes compartilhados**, status de saudação do hello PCM deve estar verde. 
   
   > [!NOTE]
   > Ele pode levar alguns minutos para inicializar de toocompletely PCM de substituição de saudação.
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

