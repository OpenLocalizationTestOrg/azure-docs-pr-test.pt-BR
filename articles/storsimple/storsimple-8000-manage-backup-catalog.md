---
title: "aaaManage seu catálogo de backup do StorSimple | Microsoft Docs"
description: "Explica como Olá toouse toolist de página do Gerenciador de dispositivos do StorSimple serviço Catálogo de backup, selecione e excluir conjuntos de backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Usar toomanage de serviço do Gerenciador de dispositivos de StorSimple Olá seu catálogo de backup
## <a name="overview"></a>Visão geral
saudação de serviço do Gerenciador de dispositivos de StorSimple **catálogo de Backup** folha exibe todos os conjuntos de backup de saudação que são criados quando são realizados backups manuais ou agendados. Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.

Este tutorial explica como toolist, selecione e exclua um conjunto de backup. toolearn como toorestore seu dispositivo de backup, vá muito[restaurar seu dispositivo de um conjunto de backup](storsimple-8000-restore-from-backup-set-u2.md). toolearn como tooclone um volume, ir muito[clonar um volume StorSimple](storsimple-8000-clone-volume-u2.md).

![Catálogo de backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Olá **catálogo de Backup** folha fornece uma consulta toonarrow sua seleção de conjunto de backup. Você pode filtrar conjuntos de backup de saudação que são recuperados, com base em Olá parâmetros a seguir:

* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.
* **Política de backup ou Volume** – Olá a política de backup ou volume associado a este conjunto de backup.
* **De e para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.

Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:

* **Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.
* **Tamanho** – Olá tamanho real do conjunto de backup hello.
* **Criado em** – a data de saudação e a hora quando foram criados backups hello. 
* **Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação. Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Iniciado por** – backups Olá podem ser iniciados automaticamente por uma agenda ou manualmente por um usuário. Você pode usar backups de tooschedule uma política de backup. Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup manual.

## <a name="list-backup-sets-for-a-backup-policy"></a>Listar conjuntos de backup para uma política de backup
As etapas a seguir Olá completa toolist todos os backups de saudação para uma política de backup.

#### <a name="toolist-backup-sets"></a>conjuntos de backup toolist
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.

2. Filtre seleções de saudação da seguinte maneira:
   
   1. Especifique o intervalo de tempo de saudação.
   2. Selecione dispositivo de saudação apropriado.
   3. Filtrar por **política de Backup** tooview Olá backups de saudação correspondente.
   3. Na lista suspensa política de backup hello, escolha **todos os** tooview todos Olá backups em Olá selecionado dispositivo.
   4. Clique em **aplicar** tooexecute esta consulta.
      
      backups Olá associados à política de backup Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Selecione um conjunto de backup
Olá completa tooselect as etapas a seguir um backup definido para uma política de backup ou volume.

#### <a name="tooselect-a-backup-set"></a>tooselect um conjunto de backup
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.
2. Filtre seleções de saudação da seguinte maneira:
   
   1. Especifique o intervalo de tempo de saudação. 
   2. Selecione dispositivo de saudação apropriado. 
   3. Filtrar por política de backup ou volume para backup de saudação que você deseja tooselect.
   4. Clique em **aplicar** tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecione e expanda um conjunto de backups. Agora você pode ver os conjuntos de backup Olá divididos por volumes Olá que ele contém. Olá **restaurar** e **excluir** opções estão disponíveis por meio do menu de contexto (direito) Olá Olá conjunto de backup. Você pode executar qualquer uma dessas ações no conjunto de backup de saudação que você selecionou.

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Excluir um conjunto de backups
Exclua um backup quando você não deseja mais dados de saudação tooretain associados a ele. Execute Olá seguindo as etapas toodelete um conjunto de backup.

#### <a name="toodelete-a-backup-set"></a>toodelete um conjunto de backup
 Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.
2. Filtre seleções de saudação da seguinte maneira:
   
   1. Especifique o intervalo de tempo de saudação. 
   2. Selecione dispositivo de saudação apropriado. 
   3. Filtrar por política de backup ou volume para backup de saudação que você deseja tooselect.
   4. Clique em **aplicar** tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecione e expanda um conjunto de backups. Agora você pode ver os conjuntos de backup Olá divididos por volumes Olá que ele contém. Olá **restaurar** e **excluir** opções estão disponíveis por meio do menu de contexto (direito) Olá Olá conjunto de backup. Conjunto de backup Olá selecionado e Olá no menu de contexto, selecione **excluir**.

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Quando solicitado para confirmação, examine informações Olá exibido e clique em **excluir**. backup de saudação selecionado será excluído permanentemente.

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Você será notificado quando Olá exclusão está em andamento e quando ele foi concluído com êxito. Após a exclusão hello, atualize a consulta de saudação nesta página. Não, o conjunto de backup Olá excluída aparecerá na lista de saudação de conjuntos de backup.

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[use Olá toorestore do catálogo de backup de seu dispositivo de um conjunto de backup](storsimple-8000-restore-from-backup-set-u2.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

