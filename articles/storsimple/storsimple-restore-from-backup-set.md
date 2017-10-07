---
title: aaaRestore um volume StorSimple de backup | Microsoft Docs
description: "Explica como toouse Olá toorestore de página do Gerenciador do StorSimple serviço Catálogo de Backup a um volume StorSimple um conjunto de backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restaurar um volume do StorSimple de um conjunto de backup
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Visão geral
Olá **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.

 ![Página Catálogo de Backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Este tutorial explica como Olá toouse **catálogo de Backup** página toorestore um volume no dispositivo de um conjunto de backup.

## <a name="how-toouse-hello-backup-catalog"></a>Como toouse Olá catálogo de backup
Olá **catálogo de Backup** página fornece uma consulta que ajuda você a toonarrow sua seleção de conjunto de backup. Você pode filtrar Olá conjuntos de backup que são recuperados com base em Olá parâmetros a seguir:

* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.
* **Política de backup** ou **volume** – Olá a política de backup ou volume associado a este conjunto de backup.
* **De** e **para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.

Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:

* **Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.
* **Tamanho** – Olá tamanho real do conjunto de backup hello.
* **Criado em** – a data de saudação e a hora quando foram criados backups hello. 
* **Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação. Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Iniciado por** – backups Olá podem ser iniciados automaticamente de acordo com o agendamento de tooa ou manualmente por um usuário. (Você pode usar backups de tooschedule uma política de backup. Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup interativo.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Como toorestore seu volume StorSimple de um backup
Você pode usar o hello **catálogo de Backup** página toorestore seu volume StorSimple de um backup específico. 

> [!WARNING]
> Restauração de um backup substituirá os volumes existentes de backup Olá Olá. Isso pode causar perda de saudação de todos os dados gravados após Olá backup foi feito.
> 
> 

Antes de iniciar uma restauração em um volume, certifique-se de que o volume de saudação está offline. Será necessário volume de saudação do tootake offline no host Olá primeiro e, em seguida, Olá dispositivo. Siga as etapas de saudação em [colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline). Execute Olá seguir etapas toorestore um volume de um conjunto de backup.

### <a name="toorestore-from-a-backup-set"></a>toorestore um conjunto de backup
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia.
   
    ![Catálogo de backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Selecione um conjunto de backup desta maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
3. Expanda Olá conjunto de backup tooview Olá associado volumes. Esses volumes devem ser colocados offline no host hello e no dispositivo antes de restaurá-los. Siga as etapas de saudação em [colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Certifique-se de que você colocou Olá volumes offline no host Olá primeiro, antes de colocar Olá volumes offline no dispositivo de saudação. Se você não colocar volumes de Olá offline no host hello, isso pode levar potencialmente toodata corrupção.
   > 
   > 
4. Selecione um conjunto de backup. Clique em **restaurar** final Olá Olá página.
5. Será solicitada a sua confirmação. 
   
    ![Página de confirmação](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Examinar as informações de restauração hello e clique no ícone de verificação Olá ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Isso iniciará um trabalho de restauração que você pode exibir acessando Olá **trabalhos** página. 
7. Após a conclusão da restauração hello, você pode verificar se conteúdo Olá de seus volumes é substituído por volumes de backup hello.

![Vídeo disponível](./media/storsimple-restore-from-backup-set/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como você pode usar o clone hello e restaurar recursos no StorSimple toorecover excluído arquivos, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[StorSimple gerenciar volumes](storsimple-manage-volumes.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

