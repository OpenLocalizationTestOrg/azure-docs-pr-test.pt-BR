---
title: aaaDeactivate e excluir um dispositivo StorSimple | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço primeiro desativá-lo e, em seguida, excluí-lo."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Desativar e excluir um dispositivo StorSimple série 8000 por meio do serviço StorSimple Manager
## <a name="overview"></a>Visão geral
Talvez você queira tootake um dispositivo StorSimple fora de serviço (por exemplo, se você estiver substituindo ou atualizando seu dispositivo ou se você não estiver usando o StorSimple). Se esse for o caso de Olá, você precisará toodeactivate dispositivo de saudação antes de excluí-lo. Desativar os servidores de conexão Olá entre Olá dispositivo e o serviço StorSimple Manager correspondente de saudação. Este tutorial explica como tooremove um dispositivo StorSimple do serviço primeiro desativá-lo e, em seguida, excluí-lo. 

Quando você desativa um dispositivo, todos os dados que foram armazenados localmente no dispositivo de saudação não poderá ser acessados. Somente os dados de saudação associados Olá dispositivo que foi armazenado na nuvem Olá podem ser recuperados.  

> [!WARNING]
> A desativação é uma operação PERMANENTE e não pode ser desfeita. Um dispositivo desativado não pode ser registrado com o serviço StorSimple Manager hello, a menos que ele seja primeiro redefinir configurações padrão de fábrica toohello. 
> 
> a redefinição de fábrica Olá processo exclui todos os dados de saudação que foi armazenados localmente no seu dispositivo. Por isso, é essencial fazer um instantâneo de nuvem de todos os dados antes de desativar um dispositivo. Isso permitirá que você toorecover todos Olá dados em um estágio posterior.
> 
> 

Este tutorial explica como:

* Desativar um dispositivo e excluir dados de saudação
* Desativar um dispositivo e reter os dados de saudação

Ele também explica como funcionam a desativação e a exclusão em um dispositivo virtual StorSimple.

> [!NOTE]
> Antes de desativar um dispositivo físico ou virtual do StorSimple, certifique-se de que toostop ou exclua os clientes e hosts que dependem desse dispositivo.
> 
> 

## <a name="deactivate-and-delete-data"></a>Desativar e excluir dados
Se você quiser excluir dispositivo Olá completamente e não quiser tooretain Olá dados no dispositivo hello, conclua Olá etapas a seguir.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>dados de saudação toodeactivate Olá dispositivo e delete
1. Anterior toodeactivating um dispositivo, você deve excluir todos os Olá volume contêineres (e Olá volumes) associados a saudação dispositivo. Você pode excluir contêineres de volume somente depois que você excluiu backups Olá associado.
2. Desative o dispositivo de saudação da seguinte maneira:
   
   1. Em Olá serviço StorSimple Manager **dispositivos** página, o dispositivo Olá selecione que você deseja toodeactivate e, final Olá Olá página, clique em **desativar**.
   2. Será exibida uma mensagem de confirmação. Clique em **Sim** toocontinue. Olá desativar processo irá iniciar e executar toocomplete de alguns minutos.
3. Após a desativação, você pode excluir dispositivo Olá completamente. Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço. serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído. Use Olá dispositivo de saudação do toodelete as etapas a seguir:
   
   1. Em Olá serviço StorSimple Manager **dispositivos** , selecione um dispositivo desativado que você deseja toodelete.
   2. Na parte inferior de saudação na página de saudação, clique em **excluir**.
   3. Será solicitada a sua confirmação. Clique em **Sim** toocontinue.
      
      Ele pode levar alguns minutos para Olá dispositivo toobe excluído.

## <a name="deactivate-and-retain-data"></a>Desativar e reter dados
Se você está interessado em Excluir dispositivo Olá mas deseja tooretain Olá dados, conclua Olá etapas a seguir.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate um dispositivo e reter dados Olá
1. Desative o dispositivo de saudação. Todos os contêineres de volume de hello e instantâneos de saudação do dispositivo Olá permanecerá.
   
   1. Em Olá serviço StorSimple Manager **dispositivos** página, o dispositivo Olá selecione que você deseja toodeactivate e, final Olá Olá página, clique em **desativar**.
   2. Será exibida uma mensagem de confirmação. Clique em **Sim** toocontinue. Olá desativar processo irá iniciar e executar toocomplete de alguns minutos.
2. Agora, você pode fazer failover contêineres de volume hello e instantâneos de saudação associado. Para procedimentos, vá muito[Failover e recuperação de desastres para seu dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Após a desativação e failover, você pode excluir dispositivo Olá completamente. Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço. serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído. Concluir Olá dispositivo de saudação do toodelete as etapas a seguir:
   
   1. Em Olá serviço StorSimple Manager **dispositivos** , selecione um dispositivo desativado que você deseja toodelete.
   2. Na parte inferior de saudação na página de saudação, clique em **excluir**.
   3. Será solicitada a sua confirmação. Clique em **Sim** toocontinue.
      
      Ele pode levar alguns minutos para Olá dispositivo toobe excluído.

## <a name="deactivate-and-delete-a-virtual-device"></a>Desativar e excluir um dispositivo virtual
Para um dispositivo virtual StorSimple, desativação desaloca Olá VM. Você pode excluir máquina virtual de saudação e recursos de saudação criados quando ele foi provisionado. Depois que o dispositivo virtual hello está desativado, ele não pode ser restaurado estado anterior tooits. 

Resultados de desativação no hello ações a seguir:

* o dispositivo virtual StorSimple Olá é removido.
* Olá OSDisk e os discos de dados criados para o dispositivo virtual StorSimple Olá são removidos.
* Hello serviço hospedado e a rede Virtual que foram criadas durante o provisionamento são mantidos. Se você não estiver usando as entidades, deverá excluí-las manualmente.
* Instantâneos de nuvem criados pelo dispositivo virtual do StorSimple Olá são mantidos.

## <a name="next-steps"></a>Próximas etapas
* toorestore Olá dispositivo desativado toofactory padrões, vá muito[redefinir as configurações padrão do hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Para obter assistência técnica, [contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md).
* Saiba mais sobre toolearn como toouse Olá serviço StorSimple Manager, vá muito[Use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md). 

