---
title: "políticas de backup de instantâneo Manager aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in toocreate e gerenciar políticas de backup Olá que controlam os backups agendados."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar políticas de backup
## <a name="overview"></a>Visão geral
Uma política de backup cria uma agenda de backup de dados de volume localmente ou na nuvem hello. Quando cria uma política de backup, você também pode especificar uma política de retenção. (Você pode manter no máximo 64 instantâneos). Para obter mais informações sobre políticas de backup, consulte [Tipos de Backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) na [StorSimple série 8000: uma solução de nuvem híbrida](storsimple-overview.md).

Este tutorial explica como:

* Criar uma política de backup
* Editar uma política de backup
* Excluir uma política de backup

## <a name="create-a-backup-policy"></a>Criar uma política de backup
Use Olá seguindo o procedimento toocreate uma nova política de backup.

#### <a name="toocreate-a-backup-policy"></a>toocreate uma política de backup
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique com botão direito **políticas de Backup**e clique em **Criar política de Backup**.

    ![Criar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Olá **criar uma política de** caixa de diálogo é exibida.

    ![Criar uma Política - guia Geral](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Em Olá **geral** guia, Olá completa informações a seguir:

   1. Em Olá **nome** caixa de texto, digite um nome para a política de saudação.
   2. Em Olá **grupo de volumes** caixa de texto, digite o nome de Olá Olá do grupo de volume associado à política de saudação.
   3. Selecione **Instantâneo Local** ou **Instantâneo em Nuvem**.
   4. Selecione o número de saudação do tooretain de instantâneos. Se você selecionar **todos os**, 64 instantâneos serão retidos (máximo de saudação).
4. Clique em Olá **agenda** guia.

    ![Criar uma política - guia Agenda](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Em Olá **agenda** guia, Olá completa informações a seguir:

   1. Clique em Olá **habilitar** próximo backup de caixa de seleção tooschedule hello.
   2. Nas **Configurações**, selecione **Uma vez**, **Diariamente**, **Semanalmente** ou **Mensalmente**.
   3. Em Olá **iniciar** caixa de texto, clique o ícone de calendário hello e selecione uma data de início.
   4. Em **Configurações Avançadas**, você pode definir cronogramas opcionais de repetição e uma data de término.
   5. Clique em **OK**.

Depois de criar uma política de backup, Olá informações a seguir aparece no hello **resultados** painel:

* **Nome** – hello nome da política de backup.
* **Tipo** – instantâneo local ou instantâneo de nuvem.
* **Grupo de volume** – hello associado à política de saudação do grupo de volumes.
* **Retenção** – hello número de instantâneos retidos; Olá máximo é 64.
* **Criada** – data de saudação que esta política foi criada.
* **Habilitado** – se a política de saudação está atualmente em vigor: **True** indica que ele está em vigor; **False** indica que ele não está em vigor.

## <a name="edit-a-backup-policy"></a>Editar uma política de backup
Use Olá seguindo o procedimento tooedit uma política de backup existente.

#### <a name="tooedit-a-backup-policy"></a>tooedit uma política de backup
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em Olá **políticas de Backup** nó. Todas as políticas de backup Olá aparecem no hello **resultados** painel.
3. Clique com botão direito política Olá que você deseja tooedit e, em seguida, clique em **editar**.

    ![Editar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Olá quando **criar uma política de** janela for exibida, insira suas alterações e, em seguida, clique em **Okey**.

## <a name="delete-a-backup-policy"></a>Excluir uma política de backup
Use Olá seguindo o procedimento toodelete uma política de backup.

#### <a name="toodelete-a-backup-policy"></a>toodelete uma política de backup
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em Olá **políticas de Backup** nó. Todas as políticas de backup Olá aparecem no hello **resultados** painel.
3. Clique com botão direito a política de backup Olá que você deseja toodelete e, em seguida, clique em **excluir**.
4. Quando aparece a mensagem de confirmação de saudação, clique em **Sim**.

    ![Excluir confirmação da política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar Gerenciador de instantâneos StorSimple tooview e gerenciar trabalhos de backup](storsimple-snapshot-manager-manage-backup-jobs.md).
