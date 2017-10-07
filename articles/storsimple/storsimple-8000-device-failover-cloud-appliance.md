---
title: "aaaStorSimple failover, recuperação de desastres tooa StorSimple Appliance de nuvem | Microsoft Docs"
description: "Saiba como toofail sobre seu tooa de dispositivo físico StorSimple 8000 series nuvem de dispositivo."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Failover tooyour StorSimple Appliance de nuvem

## <a name="overview"></a>Visão geral

Este tutorial descreve Olá etapas necessárias toofail em um tooa de dispositivo físico StorSimple 8000 series StorSimple Appliance de nuvem se houver um desastre. StorSimple usa dados saudação dispositivo failover recurso toomigrate de um dispositivo físico de origem no dispositivo de nuvem Olá datacenter tooa em execução no Azure. Guia de saudação neste tutorial se aplica a dispositivos físicos de série tooStorSimple 8000 e soluções de nuvem que executam versões do software Update 3 e posterior.

toolearn mais informações sobre failover de dispositivo e como ele é usado toorecover de um desastre, ir muito[Failover e recuperação de desastres para dispositivos da série StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail em um dispositivo físico tooanother dispositivo físico StorSimple, ir muito[failover do dispositivo físico do StorSimple tooa](storsimple-8000-device-failover-physical-device.md). toofail em tooitself um dispositivo, vá muito[failover toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Pré-requisitos

- Certifique-se de ter revisado as considerações de saudação para failover de dispositivo. Para obter mais informações, vá muito[considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Você deve ter um Dispositivo de Nuvem StorSimple criado e configurado antes de executar este procedimento. Se atualizar 3 versão do software ou posteriormente, considere o uso de um dispositivo de nuvem 8020 para execução Olá DR. modelo 8020 Olá tem 64 TB e usa o armazenamento Premium. Para obter mais informações, vá muito[implantar e gerenciar um dispositivo de nuvem StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Etapas toofail sobre tooa appliance de nuvem

Execute Olá seguindo as etapas toorestore Olá tooa de destino do dispositivo StorSimple Appliance de nuvem.

1.  Verifique se o contêiner de volume Olá que desejar toofail pela associou os instantâneos em nuvem. Para obter mais informações, vá muito[toocreate de serviço do Gerenciador de dispositivos de StorSimple Use backups](storsimple-8000-manage-backup-policies-u2.md).
2. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**. Em Olá **dispositivos** folha, vá toohello lista de dispositivos conectados ao seu serviço.
    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Selecione e clique no dispositivo de origem. dispositivo de origem de saudação tem contêineres de volume de saudação que você desejar toofail pela. Vá muito**Configurações > contêineres de Volume**.

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Selecione um contêiner de volume que deseja toofail tooanother dispositivo. Clique em Olá volume contêiner toodisplay Olá lista de volumes neste contêiner. Selecione um volume, com o botão direito e clique em **colocar Offline** tootake volume de saudação offline.

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Repita esse processo para todos os volumes de saudação no contêiner de volume hello.

     ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Etapa anterior Olá Repita para todos os contêineres de volume de Olá você gostaria que toofail de dispositivo tooanother.

7. Voltar toohello **dispositivos** folha. Na barra de comandos de saudação, clique em **failover**.

    ![Clique em Fazer failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. Em Olá **failover** folha, executar Olá etapas a seguir:
   
    1. Clique em **Fonte**. Selecione toofail de contêineres de volume Olá acima. **Olá apenas contêineres de volume com instantâneos de nuvem associados e volumes offline são exibidos.**
        ![Selecionar fonte](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Clique em **Destino**. Selecione um dispositivo de destino de nuvem na lista suspensa Olá dos dispositivos disponíveis. **Somente dispositivos de saudação que tem capacidade suficiente fonte tooaccommodate contêineres de volume são exibidos na lista de saudação.**

        ![Selecionar o destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Examine as configurações de failover de saudação em **resumo** e selecione Olá caixa de seleção que indica se os volumes de saudação em contêineres de volume selecionados estão offline. 

        ![Examinar as configurações de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Um trabalho de failover é criado. failover de saudação toomonitor de trabalho, clique em notificação de trabalho de saudação.

    ![Monitorar o trabalho de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Após a conclusão do failover Olá, volte toohello **dispositivos** folha.

    1. Selecione o dispositivo de saudação que foi usado como destino Olá Olá failover.

       ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Clique em **Contêineres de Volume**. Todos os contêineres de volume hello, junto com os volumes de saudação do dispositivo antigo do hello, devem ser listados.

       Se o contêiner de volume de saudação failover foi fixado localmente volumes, os volumes são failover como volumes em camadas. Não há suporte para volumes fixados localmente em um Dispositivo de Nuvem StorSimple.

       ![Exibir contêineres de volume de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Próximas etapas

* Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Para obter informações sobre como toouse Olá Gerenciador de dispositivos de StorSimple de serviço, visite muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

