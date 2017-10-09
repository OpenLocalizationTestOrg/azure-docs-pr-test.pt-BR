---
title: "aaaDeactivate e excluir um dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como o dispositivo StorSimple tooremove do serviço primeiro desativá-lo e, em seguida, excluí-lo."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Desativar e excluir um dispositivo StorSimple

## <a name="overview"></a>Visão geral

Este artigo descreve como toodeactivate e excluir um dispositivo StorSimple que é conectado tooa serviço do Gerenciador de dispositivos do StorSimple. diretrizes de saudação neste artigo se aplicam apenas tooStorSimple dispositivos da série 8000 incluindo Olá StorSimple nuvem dispositivos. Se você estiver usando uma matriz Virtual StorSimple, em seguida, acesse muito[desativar e excluir uma matriz Virtual StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

A desativação servidores conexão Olá entre Olá dispositivo e o serviço de Gerenciador de dispositivos do StorSimple correspondente Olá. Talvez você queira tootake um dispositivo StorSimple fora de serviço (por exemplo, se você estiver substituindo ou atualizando seu dispositivo ou se você não estiver usando o StorSimple). Nesse caso, é necessário que toodeactivate Olá dispositivo antes de excluí-lo.

Quando você desativa um dispositivo, todos os dados que foram armazenados localmente no dispositivo de saudação não estão mais acessíveis. Somente os dados de saudação associados Olá dispositivo que foi armazenado na nuvem Olá podem ser recuperados.

> [!WARNING]
> A desativação é uma operação PERMANENTE e não pode ser desfeita. Um dispositivo desativado não pode ser registrado com hello serviço do Gerenciador de dispositivos de StorSimple, a menos que ele seja Redefinir padrões toofactory.
>
> a redefinição de fábrica Olá processo exclui todos os dados de saudação que foi armazenados localmente no seu dispositivo. Por isso, é necessário criar um instantâneo de nuvem de todos os dados antes de desativar um dispositivo. Esse instantâneo de nuvem permite que você toorecover todos Olá dados em um estágio posterior.

Depois de ler este tutorial, você poderá:

* Desativar um dispositivo e excluir dados de saudação.
* Desativar um dispositivo e reter os dados de saudação.

> [!NOTE]
> Antes de desativar um dispositivo físico ou da nuvem StorSimple, interrompa ou exclua os clientes e hosts que dependem dele.


## <a name="deactivate-and-delete-data"></a>Desativar e excluir dados

Se você quiser excluir dispositivo Olá completamente e não quiser tooretain Olá dados no dispositivo hello, conclua Olá etapas a seguir.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>dados de saudação toodeactivate Olá dispositivo e delete

1. Antes de desativar um dispositivo, você deve excluir todos os Olá volume contêineres (e Olá volumes) associados a saudação de dispositivo. Você pode excluir contêineres de volume somente depois que você excluiu backups Olá associado.

    > [!NOTE]
    > Antes de desativar um dispositivo físico StorSimple ou um dispositivo de nuvem, certifique-se de que dados de saudação do contêiner de volume Olá excluído realmente seja excluídos do dispositivo hello. Você pode monitorar os gráficos de consumo de nuvem hello e quando você vir a utilização de nuvem Olá descartar devido a backups Olá que você excluiu, pode prosseguir toodeactivate dispositivo de saudação. Se você desativar o dispositivo de saudação antes de queda ocorre, Olá dados é perdidos na conta de armazenamento hello e acumula encargos.

2. Desative o dispositivo de saudação da seguinte maneira:
   
   1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione que você deseja toodeactivate, com o botão direito e clique **desativar**.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Em Olá **desativar** folha, digite Olá tooconfirm de nome de dispositivo e, em seguida, clique em **desativar**. Olá desativar o início do processo e leva toocomplete de alguns minutos.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Após a desativação, você pode excluir dispositivo Olá completamente. Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço. serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído. Use Olá dispositivo de saudação do toodelete as etapas a seguir:
   
   1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione desativado que você deseja toodelete, com o botão direito e clique **excluir**.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Em Olá **excluir** folha, digite Olá tooconfirm de nome de dispositivo e, em seguida, clique em **excluir**. exclusão de saudação leva toocomplete de alguns minutos.

        ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Após a exclusão de saudação foi concluído com êxito, você será notificado. lista de dispositivos Olá também atualiza a exclusão de saudação tooreflect.

## <a name="deactivate-and-retain-data"></a>Desativar e reter dados

Se você está interessado em Excluir dispositivo Olá mas deseja tooretain Olá dados, conclua Olá etapas a seguir:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate um dispositivo e reter dados Olá
1. Desative o dispositivo de saudação. Todos os contêineres de volume de hello e instantâneos de saudação do dispositivo Olá permanecem.
   
   1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione que você deseja toodeactivate, com o botão direito e clique **desativar**.

         ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Em Olá **desativar** folha, digite Olá tooconfirm de nome de dispositivo e, em seguida, clique em **desativar**. Olá desativar o início do processo e leva toocomplete de alguns minutos.

         ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Agora, você pode fazer failover contêineres de volume hello e instantâneos de saudação associado. Para procedimentos, vá muito[Failover e recuperação de desastres para seu dispositivo StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Após a desativação e failover, você pode excluir dispositivo Olá completamente. Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço. serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído. dispositivo de saudação toodelete, Olá concluir as etapas a seguir:
   
   1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione desativado que você deseja toodelete, com o botão direito e clique **excluir**.

       ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Em Olá **excluir** folha, digite Olá tooconfirm de nome de dispositivo e, em seguida, clique em **excluir**. exclusão de saudação leva toocomplete de alguns minutos.

       ![Desativar o dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Após a exclusão de saudação foi concluído com êxito, você será notificado. lista de dispositivos Olá também atualiza a exclusão de saudação tooreflect.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Desativar e excluir uma dispositivo de nuvem

Para um dispositivo StorSimple de nuvem, a desativação do portal Olá desaloca e exclui Olá a máquina virtual e recursos de saudação criados quando ele foi provisionado. Depois que o dispositivo de nuvem hello está desativado, ele não pode ser restaurado estado anterior tooits.

![Desativar um Dispositivo de Nuvem StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Resultados de desativação no hello ações a seguir:

* Olá StorSimple Appliance de nuvem é removido do serviço de saudação.
* máquina virtual Olá Olá StorSimple Appliance de nuvem é excluída.
* disco do sistema operacional Hello e discos de dados criados para Olá StorSimple Appliance de nuvem são removidos.
* serviço Olá hospedado e a rede Virtual que foram criadas durante o provisionamento são mantidos. Se você não estiver usando as entidades, deverá excluí-las manualmente.
* Instantâneos de nuvem criados pelo Olá StorSimple Appliance de nuvem são mantidos.

Depois que o dispositivo de nuvem Olá é desativado, você poderá excluí-la da lista de saudação de dispositivos. Selecione Olá desativado dispositivo, o botão direito do mouse e clique **excluir**. StorSimple notifica quando o dispositivo Olá é excluído Olá a lista de atualizações de dispositivos.

## <a name="next-steps"></a>Próximas etapas

* toorestore Olá dispositivo desativado toofactory padrões, vá muito[redefinir as configurações padrão do hello dispositivo toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obter assistência técnica, [contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md).
* toolearn mais sobre como Olá toouse serviço do Gerenciador de dispositivos de StorSimple, ir muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

