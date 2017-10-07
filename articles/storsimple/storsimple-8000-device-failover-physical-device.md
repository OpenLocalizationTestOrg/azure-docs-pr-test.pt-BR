---
title: "aaaStorSimple failover, o dispositivo físico do desastre recuperação tooa StorSimple 8000 series | Microsoft Docs"
description: "Saiba como toofail em seu dispositivo físico tooanother de dispositivo físico StorSimple 8000 series."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>O failover de dispositivo físico do tooa StorSimple 8000 series

## <a name="overview"></a>Visão geral

Este tutorial descreve Olá etapas necessárias toofail em um dispositivo físico StorSimple 8000 series dispositivo físico tooanother StorSimple se houver um desastre. StorSimple usa dados saudação dispositivo failover recurso toomigrate de um dispositivo físico de origem no dispositivo físico da saudação datacenter tooanother. Guia de saudação neste tutorial se aplica a dispositivos físicos de série tooStorSimple 8000 que executam versões do software Update 3 e posterior.

toolearn mais informações sobre failover de dispositivo e como ele é usado toorecover de um desastre, ir muito[Failover e recuperação de desastres para dispositivos da série StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail em um dispositivo físico de StorSimple tooa StorSimple Appliance de nuvem, ir muito[failover tooa StorSimple Appliance de nuvem](storsimple-8000-device-failover-cloud-appliance.md). toofail em tooitself um dispositivo físico, vá muito[failover toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Pré-requisitos

- Certifique-se de ter revisado as considerações de saudação para failover de dispositivo. Para obter mais informações, vá muito[considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Você deve ter um dispositivo físico de StorSimple 8000 series implantado no datacenter hello. dispositivo Olá deve executar a atualização 3 ou versão mais recente do software. Para obter mais informações, vá muito[implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Etapas toofail de dispositivo físico tooa

Execute seu dispositivo físico do dispositivo tooa destino de Olá toorestore as etapas a seguir.

1. Verifique se o contêiner de volume Olá que desejar toofail pela associou os instantâneos em nuvem. Para obter mais informações, vá muito[toocreate de serviço do Gerenciador de dispositivos de StorSimple Use backups](storsimple-8000-manage-backup-policies-u2.md).
2. Vá tooyour Gerenciador de dispositivos do StorSimple e, em seguida, clique em **dispositivos**. Em Olá **dispositivos** folha, vá toohello lista de dispositivos conectados ao seu serviço.
    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Selecione e clique no dispositivo de origem. dispositivo de origem de saudação tem contêineres de volume de saudação que você desejar toofail pela. Vá muito**Configurações > contêineres de Volume**.
4. Selecione um contêiner de volume que deseja toofail tooanother dispositivo. Clique em Olá volume contêiner toodisplay Olá lista de volumes neste contêiner. Selecione um volume, com o botão direito e clique em **colocar Offline** tootake volume de saudação offline. Repita esse processo para todos os volumes de saudação no contêiner de volume hello.
5. Etapa anterior Olá Repita para todos os contêineres de volume de Olá você gostaria que toofail de dispositivo tooanother.
6. Voltar toohello **dispositivos** folha. Na barra de comandos de saudação, clique em **failover**.
    ![Clique em Fazer failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. Em Olá **failover** folha, executar Olá etapas a seguir:
   
   1. Clique em **Fonte**. contêineres de volume de saudação com volumes associados com instantâneos de nuvem são exibidos. Somente os contêineres de saudação exibidos estão qualificados para failover. Na lista de saudação de contêineres de volume, selecione os contêineres de volume Olá você gostaria que toofail sobre. **Olá apenas contêineres de volume com instantâneos de nuvem associados e volumes offline são exibidos.**

       ![Selecionar a origem](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Clique em **Destino**. Para contêineres de volume Olá selecionados na etapa anterior hello, selecione um dispositivo de destino na lista suspensa de saudação de dispositivos disponíveis. Somente dispositivos de saudação que tem capacidade suficiente fonte tooaccommodate contêineres de volume são exibidos na lista de saudação.

        ![Selecionar o destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Por fim, examine todas as configurações de failover de saudação em **resumo**. Depois de revisar as configurações de saudação, selecione Olá caixa de seleção que indica se os volumes de saudação em contêineres de volume selecionados estão offline. Clique em **OK**.

       ![Examinar as configurações de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. O StorSimple cria um trabalho de failover. Clique em Olá trabalho notificação toomonitor Olá trabalho de failover por meio de saudação **trabalhos** folha.

    Se o contêiner de volume de saudação failover tiver volumes locais, consulte os trabalhos de restauração individuais para cada volume local (não para volumes em camadas) no contêiner de saudação. Esses trabalhos de restauração pode levar algum tempo toocomplete. É provável que esse trabalho de failover Olá pode ser concluído anteriormente. Esses volumes terá garantia local somente depois Olá restauração trabalhos sejam concluídos.

    ![Monitorar o trabalho de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Após a conclusão do failover Olá, vá toohello **dispositivos** folha.
   
   1. Selecione o dispositivo de saudação que foi usado como dispositivo de destino Olá para o processo de failover hello.

       ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Vá toohello **contêineres de Volume** folha. Todos os contêineres de volume hello, junto com os volumes de saudação do dispositivo antigo do hello, devem ser listados.

       ![Exibir contêineres de volume de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Próximas etapas

* Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obter informações sobre como toouse Olá Gerenciador de dispositivos de StorSimple de serviço, visite muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

