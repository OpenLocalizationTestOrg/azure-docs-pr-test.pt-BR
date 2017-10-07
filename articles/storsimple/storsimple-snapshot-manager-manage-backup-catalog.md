---
title: "Catálogo de backup de instantâneo Manager aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in tooview e gerenciar o catálogo de backup hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Use o Gerenciador de instantâneo StorSimple toomanage catálogo de backup Olá

## <a name="overview"></a>Visão geral
Olá principal função do Gerenciador de instantâneos do StorSimple é tooallow você toocreate consistentes com aplicativos cópias backup de volumes do StorSimple na forma de saudação de instantâneos. Os instantâneos são listados em um arquivo XML chamado de *catálogo de backups*. Catálogo de backup Olá organiza os instantâneos por grupo de volume e, em seguida, por instantâneo local ou nuvem.

Este tutorial descreve como você pode usar o hello **catálogo de Backup** saudação do nó toocomplete tarefas a seguir:

* Restaurar um volume
* Clonar um volume ou grupo de volumes
* Excluir um conjunto de backups
* Recuperar um arquivo
* Restaurar o banco de dados do hello Gerenciador de instantâneos Storsimple

Você pode exibir o catálogo de backup Olá expandindo Olá **catálogo de Backup** nó Olá **escopo** painel e expandindo o grupo de volumes hello.

* Se você clicar em nome do grupo de volume hello, Olá **resultados** painel mostra o número de saudação de instantâneos locais e instantâneos de nuvem disponíveis para o grupo de volumes de saudação. 
* Se você clicar em **instantâneo Local** ou **instantâneo em nuvem**, Olá **resultados** painel mostra Olá seguintes informações sobre cada instantâneo de backup (dependendo de sua **Exibição** configurações):
  
  * **Nome** – Olá tempo Olá instantâneo foi tirado.
  * **Tipo** – se se trata de um instantâneo local ou de nuvem.
  * **Proprietário** – proprietário do conteúdo hello. 
  * **Disponível** – se o instantâneo hello está disponível no momento. **True** indica que esse Instantâneo hello está disponível e pode ser restaurado; **False** indica que esse Instantâneo Olá não está mais disponível. 
  * **Importado** – se Olá backup foi importado. **True** indica que o backup Olá foi importado do hello Gerenciador de dispositivos do StorSimple serviço no dispositivo Olá Olá foi configurado no Gerenciador de instantâneo do StorSimple. **False** indica que ele não foi importado, mas foi criado pelo Gerenciador de instantâneos do StorSimple. (Você pode identificar facilmente um grupo de volume importado porque é adicionado um sufixo que identifica o dispositivo de saudação da qual o grupo de volumes Olá foi importado.)
    
    ![Catálogo de backup](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Se você expandir **instantâneo Local** ou **instantâneo em nuvem**e, em seguida, clique em um nome de instantâneo individual, hello **resultados** painel mostra Olá seguintes informações sobre Olá instantâneo selecionado:
  
  * **Nome** – Olá volume identificado pela letra da unidade. 
  * **Nome local** – nome local de saudação da unidade da saudação (se disponível). 
  * **Dispositivo** – hello nome de dispositivo de saudação em qual Olá volume reside. 
  * **Disponível** – se o instantâneo hello está disponível no momento. **True** indica que esse Instantâneo hello está disponível e pode ser restaurado; **False** indica que esse Instantâneo Olá não está mais disponível. 

## <a name="restore-a-volume"></a>Restaurar um volume
Use Olá seguindo o procedimento toorestore um volume de backup.

#### <a name="prerequisites"></a>Pré-requisitos
Se você ainda não tiver feito isso, crie um volume e o grupo de volumes e, em seguida, excluir o volume de saudação. Por padrão, StorSimple Snapshot Manager faz o backup de um volume antes de permitir que ele toobe excluído. Essa precaução pode evitar a perda de dados se Olá volume for excluído acidentalmente ou se precisarem de dados de saudação toobe recuperado por qualquer motivo. 

Gerenciador de instantâneos StorSimple exibe Olá seguinte mensagem enquanto cria o backup de precaução hello.

![Mensagem de instantâneo automático](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> Você não pode excluir um volume que faz parte de um grupo de volumes. opção de exclusão de saudação não está disponível. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore um volume
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager. 
2. Em Olá **escopo** painel, expanda Olá **catálogo de Backup** nó, expanda um grupo de volumes e, em seguida, clique em **instantâneos locais** ou **instantâneos em nuvem**. É exibida uma lista de instantâneos de backup no hello **resultados** painel.
3. Localizar Olá backup que você deseja toorestore, com o botão direito e clique **restauração**.
   
    ![Restaurar o catálogo de backups](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Na página de confirmação hello, examine os detalhes hello, digite **confirmar**e, em seguida, clique em **Okey**. Gerenciador de instantâneos do StorSimple usa o volume de saudação do hello toorestore backup.
   
    ![Mensagem de confirmação de restauração](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Você pode monitorar a ação de restauração Olá conforme ele é executado. Em Olá **escopo** painel, expanda Olá **trabalhos** nó e, em seguida, clique **executando**. detalhes do trabalho Olá aparecem no hello **resultados** painel. Quando terminar o trabalho de restauração hello, detalhes do trabalho Olá são transferido toohello **últimas 24 horas** lista.

## <a name="clone-a-volume-or-volume-group"></a>Clonar um volume ou grupo de volumes
Use Olá seguindo o procedimento toocreate uma duplicata (clone) de um volume ou grupo de volumes.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone um volume ou grupo de volumes
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **catálogo de Backup** nó, expanda um grupo de volumes e, em seguida, clique em **instantâneos em nuvem**. Uma lista de backups aparece no hello **resultados** painel.
3. Localizar o volume de saudação ou o grupo de volume que você deseja tooclone, o volume de saudação do botão direito do mouse ou o nome do grupo de volume e clique em **Clone**. Olá **clonar instantâneo em nuvem** caixa de diálogo é exibida.
   
    ![Clonar um instantâneo de nuvem](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Olá completa **clonar instantâneo em nuvem** caixa de diálogo da seguinte maneira: 
   
   1. Em Olá **nome** caixa de texto, digite um nome para Olá clonar o volume. Esse nome aparecerá no hello **Volumes** nó. 
   2. (Opcional) selecione **unidade**e selecione uma letra de unidade na lista suspensa de saudação.
   3. (Opcional) selecione **pasta (NTFS)**e digite um caminho de pasta ou clique em Procurar e selecione um local para a pasta de saudação. 
   4. Clique em **Criar**.
5. Quando Olá processo de clonagem é concluída, você deverá inicializar Olá clonada volume. Inicie o Gerenciador do Servidor e inicie o gerenciamento de disco. Para obter instruções detalhadas, consulte [Montar volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Depois que ele é inicializado, Olá volume será listado sob Olá **Volumes** nó Olá **escopo** painel. Se você não vir o volume de saudação listado, atualize a lista de saudação de volumes (atalho Olá **Volumes** nó e, em seguida, clique **atualização**).

## <a name="delete-a-backup"></a>Excluir um conjunto de backups
Use Olá seguindo o procedimento toodelete um instantâneo do catálogo de backup hello. 

> [!NOTE]
> Excluir um instantâneo exclui Olá dados associados com instantâneo de saudação do backup. No entanto, o processo de saudação de limpeza de dados da nuvem Olá pode levar algum tempo.<br>


#### <a name="toodelete-a-backup"></a>toodelete um backup
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **catálogo de Backup** nó, expanda um grupo de volumes e, em seguida, clique em **instantâneos locais** ou **instantâneos em nuvem**. Uma lista de instantâneos aparece no hello **resultados** painel.
3. Instantâneo de Olá atalho você deseja toodelete e, em seguida, clique em **excluir**.
4. Quando aparece a mensagem de confirmação de saudação, clique em **Okey**.

## <a name="recover-a-file"></a>Recuperar um arquivo
Se um arquivo for excluído acidentalmente de um volume, você pode recuperar o arquivo hello ao recuperar um instantâneo que antecipa a exclusão de hello, Olá instantâneo toocreate um clone do volume de saudação e, em seguida, copiar o arquivo de saudação do hello volume do volume clonado toohello original.

#### <a name="prerequisites"></a>Pré-requisitos
Antes de começar, certifique-se de que você tenha um backup atual do grupo de volumes de saudação. Em seguida, exclua o arquivo armazenado em um dos volumes de saudação no grupo de volumes. Por fim, use Olá Olá de toorestore as etapas a seguir excluído o arquivo de backup. 

#### <a name="toorecover-a-deleted-file"></a>toorecover um arquivo excluído
1. Clique Olá StorSimple Snapshot Manager ícone na área de trabalho. janela de console do Gerenciador de instantâneos StorSimple Olá aparece. 
2. Em Olá **escopo** painel, expanda Olá **catálogo de Backup** nó e procurar tooa instantâneo que contém o arquivo hello excluído. Normalmente, você deve selecionar um instantâneo que foi criado antes de exclusão de saudação.
3. Localizar Olá volume que você deseja tooclone, com o botão direito e clique em **Clone**. Olá **clonar instantâneo em nuvem** caixa de diálogo é exibida.
   
    ![Clonar um instantâneo de nuvem](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Olá completa **clonar instantâneo em nuvem** caixa de diálogo da seguinte maneira: 
   
   1. Em Olá **nome** caixa de texto, digite um nome para Olá clonar o volume. Esse nome aparecerá no hello **Volumes** nó. 
   2. (Opcional) Selecione **unidade**e selecione uma letra de unidade na lista suspensa de saudação. 
   3. (Opcional) Selecione **pasta (NTFS)**e digite um caminho de pasta ou clique **procurar** e selecione um local para a pasta de saudação. 
   4. Clique em **Criar**. 
5. Quando Olá processo de clonagem é concluída, você deverá inicializar Olá clonada volume. Inicie o Gerenciador do Servidor e inicie o gerenciamento de disco. Para obter instruções detalhadas, consulte [Montar volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Depois que ele é inicializado, Olá volume será listado sob Olá **Volumes** nó Olá **escopo** painel. 
   
    Se você não vir o volume de saudação listado, atualize a lista de saudação de volumes (atalho Olá **Volumes** nó e, em seguida, clique **atualização**).
6. Pasta do NTFS Olá aberta que contém o volume Olá clonado, expanda Olá **Volumes** nó e, em seguida, abra Olá clonado volume. Localize arquivo hello que você deseja toorecover e copie-o volume principal toohello.
7. Depois de restaurar o arquivo hello, você pode excluir a pasta NTFS Olá que contém o volume clonada de saudação.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Restaurar o banco de dados do hello Gerenciador de instantâneos StorSimple
Regularmente, você deve fazer o banco de dados do hello StorSimple Snapshot Manager no computador de host de saudação. Se ocorrer um desastre ou computador de host Olá falha por algum motivo, você pode restaurá-lo de backup hello. Backup de banco de dados criando Olá é um processo manual.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback backup e restaurar banco de dados de saudação
1. Pare Olá serviço de gerenciamento do Microsoft StorSimple:
   
   1. Inicie o Gerenciador do Servidor.
   2. Painel do Gerenciador do servidor de saudação, na Olá **ferramentas** menu, selecione **serviços**.
   3. Em Olá **serviços** janela, selecione Olá **serviço de gerenciamento do Microsoft StorSimple**.
   4. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **parar serviço Olá**.
2. No computador de host hello, procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData é uma pasta oculta.
   > 
   > 
3. Localize arquivo XML do catálogo hello, copiar o arquivo de saudação e armazenar Olá copiar em um local seguro ou na nuvem hello. Se o host de saudação falhar, você pode usar esse arquivo de backup toohelp recuperar Olá políticas de backup que você criou no Gerenciador de instantâneos do StorSimple.
   
    ![Arquivo de catálogo de backups do Azure StorSimple](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Reinicie Olá serviço de gerenciamento do Microsoft StorSimple: 
   
   1. Painel do Gerenciador do servidor de saudação, na Olá **ferramentas** menu, selecione **serviços**.
   2. Em Olá **serviços** janela, selecione Olá **serviço de gerenciamento do Microsoft StorSimple**.
   3. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **reiniciar serviço Olá**.
5. No computador de host hello, procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Excluir o arquivo XML do catálogo hello e substituí-lo com a versão de backup de saudação que você criou. 
7. Clique em Olá área de trabalho do StorSimple Snapshot Manager ícone toostart StorSimple Snapshot Manager. 

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [usando o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* [Saiba mais sobre fluxos de trabalho e tarefas do StorSimple Snapshot Manager](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

