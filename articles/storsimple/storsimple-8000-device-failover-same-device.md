---
title: "aaaStorSimple failover, recuperação de desastres para dispositivos da 8000 série | Microsoft Docs"
description: Saiba como toofail sobre seu toohello de dispositivo StorSimple mesmo dispositivo.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>O failover de seu dispositivo de toosame do dispositivo físico StorSimple

## <a name="overview"></a>Visão geral

Este tutorial descreve Olá etapas necessárias toofail em um tooitself de dispositivo físico StorSimple 8000 series se houver um desastre. StorSimple usa dados saudação dispositivo failover recurso toomigrate de um dispositivo físico de origem no dispositivo físico da saudação datacenter tooanother. Guia de saudação neste tutorial se aplica a dispositivos físicos de série tooStorSimple 8000 que executam versões do software Update 3 e posterior.

toolearn mais informações sobre failover de dispositivo e como ele é usado toorecover de um desastre, ir muito[Failover e recuperação de desastres para dispositivos da série StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail em um dispositivo físico do tooanother de dispositivo físico, vá muito[failover toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md). toofail em um dispositivo físico de StorSimple tooa StorSimple Appliance de nuvem, ir muito[failover tooa StorSimple Appliance de nuvem](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Pré-requisitos

- Certifique-se de ter revisado as considerações de saudação para failover de dispositivo. Para obter mais informações, vá muito[considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Etapas toofail sobre toohello mesmo dispositivo

Executar Olá etapas a seguir se precisar de toofail toohello mesmo dispositivo.

1. Tire instantâneos em nuvem de todos os volumes de saudação em seu dispositivo. Para obter mais informações, vá muito[toocreate de serviço do Gerenciador de dispositivos de StorSimple Use backups](storsimple-8000-manage-backup-policies-u2.md).
2. Redefina o dispositivo toofactory padrão. Siga Olá detalhadas instruções [como configurações de padrão tooreset um toofactory de dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Serviço de Gerenciador de dispositivos de StorSimple toohello go e, em seguida, selecione **dispositivos**. Em Olá **dispositivos** folha, dispositivo antigo Olá deve aparecer como **Offline**.

    ![Dispositivo de origem offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Configure o seu dispositivo e registre-o novamente no serviço do Gerenciador de Dispositivos do StorSimple. Olá dispositivo registrado recentemente deve aparecer como **pronto tooset backup**. nome do dispositivo Olá para o novo dispositivo de saudação é hello igual ao dispositivo antigo Olá mas anexado com um numeral tooindicate dispositivo Olá era redefinição toofactory padrão e registrados novamente.

    ![Dispositivo registrado recentemente a tooset pronto para cima](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Para o novo dispositivo de hello, conclua a configuração de dispositivo de saudação. Para obter mais informações, vá muito[etapa 4: concluir a configuração mínima do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). Em Olá **dispositivos** folha, status de saudação do dispositivo Olá muda muito**Online**.

   > [!IMPORTANT]
   > **Concluir a configuração mínima de saudação pela primeira vez ou a recuperação de desastres pode falhar.**

    ![Dispositivo recém-registrado online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Selecione o dispositivo antigo da saudação (status offline) e na barra de comandos de saudação, clique em **failover**. Em Olá **failover** folha, selecione antigo dispositivo como origem de saudação e especifique o dispositivo de destino hello como Olá dispositivo registrado recentemente.

    ![Resumo de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Para obter instruções detalhadas, consulte muito[failover de dispositivo físico tooanother](#fail-over-to-another-physical-device).

7. Um trabalho de restauração do dispositivo é criado que você pode monitorar de saudação **trabalhos** folha.

8. Depois que o trabalho de saudação for concluída com êxito, acessar o novo dispositivo de saudação e navegar toohello **contêineres de Volume** folha. Verifique se todos os contêineres de volume de saudação do dispositivo antigo Olá foram migradas toohello novo dispositivo.

   ![Contêineres de volume migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Após a conclusão do failover hello, você pode desativar e excluir dispositivo antigo saudação do portal de saudação. Selecione Olá antigo dispositivo (offline), com o botão direito e, em seguida, selecione **desativar**. Depois que o dispositivo hello está desativado, status de saudação do dispositivo Olá é atualizado.

     ![Dispositivo de origem desativado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Selecione Olá desativado dispositivo, com o botão direito e selecione **excluir**. Isso exclui o dispositivo Olá da lista de saudação de dispositivos.

    ![Dispositivo de origem excluído](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Próximas etapas

* Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Para obter informações sobre como toouse Olá Gerenciador de dispositivos de StorSimple de serviço, visite muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

