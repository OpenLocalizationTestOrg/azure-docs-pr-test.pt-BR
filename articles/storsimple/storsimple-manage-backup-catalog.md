---
title: "aaaManage seu catálogo de backup do StorSimple | Microsoft Docs"
description: "Explica como toolist toouse Olá StorSimple Manager serviço Catálogo de Backup página, selecione e excluir conjuntos de backup para um volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Usar toomanage de serviço do StorSimple Manager Olá seu catálogo de backup
## <a name="overview"></a>Visão geral
Olá serviço StorSimple Manager **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando são realizados backups manuais ou agendados. Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.

Este tutorial explica como toolist, selecione e exclua um conjunto de backup. toolearn como toorestore seu dispositivo de backup, vá muito[restaurar seu dispositivo de um conjunto de backup](storsimple-restore-from-backup-set.md). toolearn como tooclone um volume, ir muito[clonar um volume StorSimple](storsimple-clone-volume.md).

![Catálogo de backup](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Olá **catálogo de Backup** página fornece uma consulta toonarrow sua seleção de conjunto de backup. Você pode filtrar conjuntos de backup de saudação que são recuperados, com base em Olá parâmetros a seguir:

* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.
* **Volume ou política de backup** – Olá a política de backup ou volume associado a este conjunto de backup.
* **De e para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.

Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:

* **Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.
* **Tamanho** – Olá tamanho real do conjunto de backup hello.
* **Criado em** – a data de saudação e a hora quando foram criados backups hello. 
* **Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação. Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Iniciado por** – backups Olá podem ser iniciados automaticamente por uma agenda ou manualmente por um usuário. Você pode usar backups de tooschedule uma política de backup. Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup manual.

## <a name="list-backup-sets-for-a-volume"></a>Listar conjuntos de backup para um volume
As etapas a seguir Olá completa toolist todos os backups de saudação para um volume.

#### <a name="toolist-backup-sets"></a>conjuntos de backup toolist
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia.
2. Filtre seleções de saudação da seguinte maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha os tooview um volume Olá correspondente Olá backups.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      backups de saudação associados volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.

## <a name="select-a-backup-set"></a>Selecione um conjunto de backup
Olá completa tooselect as etapas a seguir um backup definido para uma política de backup ou volume.

#### <a name="tooselect-a-backup-set"></a>tooselect um conjunto de backup
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia.
2. Filtre seleções de saudação da seguinte maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
3. Selecione e expanda um conjunto de backups. Olá **restaurar** e **excluir** opções são exibidas na parte inferior da saudação da página de saudação. Você pode executar qualquer uma dessas ações no conjunto de backup de saudação que você selecionou.

## <a name="delete-a-backup-set"></a>Excluir um conjunto de backups
Exclua um backup quando você não deseja mais dados de saudação tooretain associados a ele. Execute Olá seguindo as etapas toodelete um conjunto de backup.

#### <a name="toodelete-a-backup-set"></a>toodelete um conjunto de backup
1. Na página de serviço do StorSimple Manager hello, clique em Olá **guia do catálogo de Backup**.
2. Filtre seleções de saudação da seguinte maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
3. Selecione e expanda um conjunto de backups. Olá **restaurar** e **excluir** opções são exibidas na parte inferior da saudação da página de saudação. Clique em **Excluir**.
4. Você será notificado quando Olá exclusão está em andamento e quando ele foi concluído com êxito. Após a exclusão hello, atualize a consulta de saudação nesta página. Não, o conjunto de backup Olá excluída aparecerá na lista de saudação de conjuntos de backup.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[use Olá toorestore do catálogo de backup de seu dispositivo de um conjunto de backup](storsimple-restore-from-backup-set.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

