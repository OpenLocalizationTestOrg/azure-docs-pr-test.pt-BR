---
title: "trabalhos de backup de instantâneo Manager aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in tooview e gerenciar trabalhos de backup agendados, atualmente em execução e concluídos."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>Use o Gerenciador de instantâneos StorSimple tooview e gerenciar trabalhos de backup

## <a name="overview"></a>Visão geral
Olá **trabalhos** nó Olá **escopo** painel mostra Olá **agendada**, **últimas 24 horas**, e **executando**tarefas iniciadas interativamente ou por uma política de configuração de backup. 

Este tutorial explica como você pode usar o hello **trabalhos** informações do nó toodisplay sobre trabalhos de backup agendados, recentes e em execução no momento. (lista de saudação de trabalhos e as informações correspondentes aparece no hello **resultados** painel.) Além disso, você pode clicar com o botão direito em um trabalho listado e ver um menu de contexto que lista as ações disponíveis.

## <a name="view-scheduled-jobs"></a>Ver trabalhos agendados
Olá Use seguindo o procedimento tooview trabalhos de backup agendados.

#### <a name="tooview-scheduled-jobs"></a>trabalhos agendado do tooview
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager. 
2. Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **agendada**. Olá seguintes informações aparecem no hello **resultados** painel:
   
   * **Nome** – hello nome do instantâneo agendado Olá
   * **Em seguida execute** – Olá data e hora do próximo instantâneo programado de saudação
   * **Última execução** – Olá data e hora do instantâneo agendado mais recente de saudação
     
     > [!NOTE]
     > Apenas para instantâneos únicos, Olá **próxima execução** e **última execução** será Olá mesmo.
     
     ![Trabalhos de backup agendados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.

## <a name="view-recent-jobs"></a>Exibir trabalhos recentes
Use Olá backup tooview do procedimento a seguir e restaure os trabalhos que foram concluídos no hello últimas 24 horas.

#### <a name="tooview-recent-jobs"></a>trabalhos recentes tooview
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **últimas 24 horas**. Olá **resultados** painel mostra os trabalhos de backup para Olá últimas 24 horas (tooa máximo de 64 trabalhos). Olá seguintes informações aparecem no hello **resultados** painel, dependendo da saudação **exibição** opções que você especificar:
   
   * **Nome** – hello nome do instantâneo agendado hello.
   * **Iniciado** – a saudação data e a hora de início do instantâneo hello.
   * **Interrompido** – a data de saudação e a hora quando o instantâneo de saudação foi concluído ou terminado.
   * **Decorrido** – quantidade Olá de tempo entre hello **iniciado** e **parado** vezes.
   * **Status** – Olá estado de trabalho Olá concluído recentemente. **Sucesso** indica que o backup Olá foi criado com êxito. **Falha ao** indica que o trabalho Olá não foi executado com êxito.
   * **Informações** – Olá motivo da falha de saudação.
   * **Bytes processados (MB)** – quantidade Olá de dados do grupo de volumes de saudação foi processado (em MBs). 
     
     ![Trabalhos executados em Olá últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.
   
    ![Excluir um trabalho](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Exibir trabalhos em execução
Use Olá trabalhos tooview de procedimento que estão em execução a seguir.

#### <a name="tooview-currently-running-jobs"></a>tooview trabalhos em execução
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **executando**. Dependendo da saudação **exibição** opções que você especificar, Olá informações a seguir aparece no hello **resultados** painel:
   
   * **Nome** – hello nome do instantâneo agendado hello.
   * **Iniciado** – a saudação data e a hora de início do instantâneo hello.
   * **Ponto de verificação** – Olá ação atual do backup hello.
   * **Status** – Olá porcentagem de conclusão.
   * **Decorrido** – quantidade de saudação do tempo decorrido desde o início do backup hello. 
   * **Taxa de transferência média (MB)** – proporção do total de bytes de dados processados toothat do tempo total gasto para processar (MBs).
   * **Bytes processados (MB)** – total de bytes de dados processados (em MBs).
   * **Bytes gravados (MB)** – total de bytes de dados gravados (em MBs). Ele inclui dados hello, bem como metadados de saudação e, portanto, é normalmente maior Olá Bytes processados.
     
     ![Trabalhos em execução no momento](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar o catálogo de backup do Gerenciador de instantâneos StorSimple toomanage Olá](storsimple-snapshot-manager-manage-backup-catalog.md).

