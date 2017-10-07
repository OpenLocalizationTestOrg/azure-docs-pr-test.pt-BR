---
title: tutorial backup do Azure StorSimple Virtual Array aaaMicrosoft | Microsoft Docs
description: Descreve como tooback matriz Virtual StorSimple compartilhamentos e volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Fazer backup de volumes ou compartilhamentos no StorSimple Virtual Array

## <a name="overview"></a>Visão geral

Olá matriz Virtual StorSimple é um híbrido nuvem armazenamento no dispositivo virtual local que pode ser configurado como um servidor de arquivos ou um servidor iSCSI. matriz virtual Olá permite Olá usuário toocreate backups agendados e manuais de todos os volumes ou compartilhamentos Olá Olá dispositivo. Quando configurado como um servidor de arquivos, ele também permite a recuperação em nível de item. Este tutorial descreve como toocreate agendados e backups manuais e executar a recuperação em nível de item toorestore a exclusão de um arquivo em sua matriz virtual.

Este tutorial aplica toohello StorSimple Virtual matrizes somente. Para obter informações sobre a 8000 série, vá muito[criar um backup para o dispositivo da 8000 série](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Fazer backup de compartilhamentos e volumes

Backups oferecem proteção pontual, melhoram a capacidade de recuperação e minimizam os tempos de compartilhamentos e volumes. É possível fazer backup de um compartilhamento ou volume em seu dispositivo StorSimple de duas maneiras: **Agendada** ou **Manual**. Cada um dos métodos de saudação é abordada em Olá seções a seguir.

## <a name="change-hello-backup-start-time"></a>Altere a hora de início de backup Olá

> [!NOTE]
> Nesta versão, os backups agendados são criados por uma política padrão que é executada diariamente em um período especificado e faz backup de todos os volumes ou compartilhamentos Olá no dispositivo de saudação. Não é possível toocreate políticas personalizadas para backups agendados no momento.


A matriz de Virtual do StorSimple tem uma política de backup padrão que inicia em um determinado horário do dia (22:30) e faz o backup de todos os volumes ou compartilhamentos Olá no dispositivo Olá uma vez por dia. Você pode alterar o tempo de saudação em que início do backup hello, mas frequência hello e Olá retenção (que especifica o número de saudação de backups tooretain) não pode ser alterada. Durante esses backups, o dispositivo virtual inteira de saudação é feito backup. Potencialmente, isso pode afetar o desempenho de saudação do dispositivo hello e afetam as cargas de trabalho Olá implantadas no dispositivo de saudação. Portanto, recomendamos agendar esses backups fora do horário de pico.

 backup de padrão de saudação toochange hora de início, execute Olá etapas Olá [portal do Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>Olá toochange hora de início para política de backup saudação padrão

1. Vá muito**dispositivos**. Olá lista de dispositivos registrados com o serviço do Gerenciador de dispositivos de StorSimple será exibida. 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Selecione e clique em seu dispositivo. Olá **configurações** folha será exibida. Vá muito**Gerenciar > políticas de Backup**.
   
    ![selecionar o dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. Em Olá **as políticas de Backup** folha, hora de início do saudação padrão é 22:30. Você pode especificar a nova hora de início Olá para agendamento diário Olá no fuso horário do dispositivo.
   
    ![Navegue toobackup políticas](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Clique em **Salvar**.

### <a name="take-a-manual-backup"></a>Fazer um backup manual

Além disso tooscheduled backups, você pode fazer um backup manual do (sob demanda) dos dados de dispositivo a qualquer momento.

#### <a name="toocreate-a-manual-backup"></a>toocreate um backup manual

1. Vá muito**dispositivos**. Selecione o dispositivo e clique **...**  em hello mais à direita na linha selecionada da saudação. No menu de contexto hello, selecione **fazer backup**.
   
    ![Navegue tootake backup](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. Em Olá **fazer backup** folha, clique em **fazer backup**. Isto fará backup de todos os compartilhamentos de saudação no servidor de arquivos de saudação ou todos os volumes de saudação em seu servidor do iSCSI. 
   
    ![backup iniciando](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Um backup sob demanda é iniciado e você verá que um trabalho de backup foi iniciado.
   
    ![backup iniciando](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Depois que o trabalho de saudação for concluída com êxito, você será notificado novamente. em seguida, inicia o processo de backup Hello.
   
    ![trabalho de backup criado](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. progresso de saudação tootrack de backups de saudação e examinar os detalhes do trabalho hello, clique em notificação hello. Isso leva muito **detalhes do trabalho**.
   
     ![detalhes do trabalho de backup](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Após a conclusão do backup hello, ir muito**gerenciamento > Catálogo de Backup**. Você verá um instantâneo de nuvem de todos os compartilhamentos hello (ou volumes) em seu dispositivo.
   
    ![Backup concluído](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Exibir os backups existentes
backups existentes do tooview hello, executar Olá etapas Olá portal do Azure.

#### <a name="tooview-existing-backups"></a>backups existentes tooview

1. Vá muito**dispositivos** folha. Selecione e clique em seu dispositivo. Em Olá **configurações** folha, ir muito**gerenciamento > Catálogo de Backup**.
   
    ![Navegue toobackup catálogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Especifique Olá toobe critérios usado para filtrar a seguir:
   
    - **Intervalo de tempo** – pode ser **Última hora**, **Últimas 24 horas**, **Últimos 7 dias**, **Últimos 30 dias**, **Ano passado** e **Data personalizada**.
    
    - **Dispositivos** – selecione na lista de saudação de servidores de arquivos ou iSCSI servidores registrados com o serviço do Gerenciador de dispositivos do StorSimple.
   
    - **Iniciado** – pode ser **Agendado** automaticamente (por uma política de backup) ou iniciado **Manualmente** (por você).
   
    ![Backups de filtro](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Clique em **Aplicar**. Olá lista filtrada de backups é exibida no hello **catálogo de Backup** folha. Observe que apenas 100 elementos de backup podem ser exibidos de cada vez.
   
    ![Catálogo de backup atualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

