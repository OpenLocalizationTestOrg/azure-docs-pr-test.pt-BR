---
title: aaaDeactivate e excluir uma matriz do Microsoft Azure StorSimple Virtual | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço primeiro desativá-lo e, em seguida, excluí-lo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Desativar e excluir uma Matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

Quando você desativa uma matriz Virtual StorSimple, você interromper a conexão de saudação entre Olá dispositivo e o serviço de Gerenciador de dispositivos do StorSimple correspondente Olá. Este tutorial explica como:

* Desativar um dispositivo 
* Excluir um dispositivo desativado

informações de Olá neste artigo aplicam-se somente a matrizes Virtual tooStorSimple. Para obter informações sobre a 8000 série, vá toohow muito[desativar ou excluir um dispositivo](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Quando toodeactivate?

A desativação é uma operação PERMANENTE e não pode ser desfeita. Você não pode registrar um dispositivo desativado com hello serviço do Gerenciador de dispositivos de StorSimple novamente. Você pode precisar toodeactivate e excluir uma matriz Virtual do StorSimple no hello os seguintes cenários:

* **Failover planejado** : seu dispositivo está online e planejar toofail em seu dispositivo. Se você estiver planejando tooupgrade tooa maior do dispositivo, talvez seja necessário toofail em seu dispositivo. Depois que propriedade Olá dos dados é transferida e Olá failover estiver concluído, o dispositivo de origem Olá é excluído automaticamente.
* **Failover não planejado** : seu dispositivo está offline e precisar de toofail dispositivo hello. Esta situação pode ocorrer durante um desastre quando houver uma interrupção no datacenter hello e seu dispositivo primário está inativo. Planejar toofail sobre Olá dispositivo tooa secundário dispositivo. Depois que propriedade Olá dos dados é transferida e Olá failover estiver concluído, o dispositivo de origem Olá é excluído automaticamente.
* **Encerrar** : toodecommission Olá dispositivo. Isso exige que você toofirst desativar dispositivo hello e, em seguida, excluí-lo. Ao desativar um dispositivo, não é mais possível acessar os dados que foram armazenados localmente. Você pode apenas acesso e recupere Olá os dados armazenados na nuvem hello. Se você planejar os dados do dispositivo Olá tookeep após a desativação, você deve executar um instantâneo de nuvem de todos os dados antes de desativar um dispositivo. Esse instantâneo de nuvem permite que você toorecover todos Olá dados em um estágio posterior.

## <a name="deactivate-a-device"></a>Desativar um dispositivo

toodeactivate seu dispositivo, execute Olá etapas a seguir.

#### <a name="toodeactivate-hello-device"></a>dispositivo de saudação toodeactivate

1. No seu serviço, vá muito**gerenciamento > dispositivos**. Em Olá **dispositivos** folha, clique em e dispositivo Olá selecione que você deseja toodeactivate.
   
    ![Selecione o dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. No seu **painel dispositivo** folha, clique em **... Mais** e selecione lista de saudação **desativar**.
   
    ![Clique em desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. Em Olá **desativar** folha, nome do tipo de dispositivo hello e clique **desativar**. 
   
    ![Confirme desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Olá desativar o início do processo e leva toocomplete de alguns minutos.
   
    ![Desativação em andamento](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Após a desativação Olá lista de atualizações de dispositivos.
   
    ![Desativação concluída](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Agora você pode excluir este dispositivo.

## <a name="delete-hello-device"></a>Excluir dispositivo Olá

Um dispositivo tem toodelete desativadas do primeiro toobe-lo. Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço. serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído. No entanto, dados de saudação associados ao dispositivo Olá permanecem na nuvem de saudação. Esses dados acumulam encargos.

dispositivo de saudação toodelete, executar Olá etapas a seguir.

#### <a name="toodelete-hello-device"></a>dispositivo de saudação toodelete

1. No Gerenciador de dispositivos seu StorSimple, ir muito**gerenciamento > dispositivos**. Em Olá **dispositivos** folha, selecione um dispositivo desativado que você deseja toodelete.
2. Em Olá **painel dispositivo** folha, clique em **... Mais** e, em seguida, clique em **excluir**.
   
   ![Selecione o dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. Em Olá **excluir** folha, digite o nome de saudação de sua exclusão do dispositivo tooconfirm hello e clique **excluir**. Excluindo dispositivos de saudação não exclui dados de nuvem Olá associados Olá dispositivo. 
   
   ![Confirmar exclusão](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. exclusão de saudação é iniciado e leva toocomplete de alguns minutos.
   
   ![Exclusão em andamento](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Depois que o dispositivo de saudação é excluído, você pode exibir a lista de saudação atualizada de dispositivos.

## <a name="next-steps"></a>Próximas etapas

* Para obter informações sobre como toofail, ir muito[Failover e recuperação de desastres de sua matriz Virtual StorSimple](storsimple-virtual-array-failover-dr.md).

* toolearn mais sobre como Olá toouse serviço do Gerenciador de dispositivos de StorSimple, ir muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple sua matriz Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md). 

