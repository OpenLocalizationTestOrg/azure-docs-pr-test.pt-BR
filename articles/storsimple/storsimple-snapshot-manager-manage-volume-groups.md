---
title: "grupos de volumes do Gerenciador de instantâneos aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in toocreate e gerenciar grupos de volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar grupos de volume
## <a name="overview"></a>Visão geral
Você pode usar o hello **grupos de Volume** nó Olá **escopo** painel tooassign volumes toovolume grupos exibir informações sobre um grupo de volumes, agendar backups e editar grupos de volume.

Grupos de volume são pools de volumes relacionados usados tooensure que os backups sejam consistentes com o aplicativo. Para saber mais, consulte [Volumes e grupos de volumes](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Todos os volumes em um grupo de volumes devem vir de um único provedor de serviço de nuvem.
> * Quando você configura grupos de volume, não misture volumes compartilhados de cluster (CSVs) e não CSVs no hello mesmo grupo de volumes. Gerenciador de instantâneos do StorSimple não suporta uma mistura de CSVs e não CSVs no hello mesmo instantâneo.

![Nó Grupos de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Figura 1: Nó Grupos de Volumes do StorSimple Snapshot Manager** 

Este tutorial explica como você pode usar o StorSimple Snapshot Manager para:

* Exibir informações sobre os grupos de volumes
* Criar um grupo de volumes
* Fazer backup de um grupo de volumes
* Editar um grupo de volumes
* Excluir um grupo de volumes

Todas essas ações também estão disponíveis em Olá **ações** painel.

## <a name="view-volume-groups"></a>Exibir grupos de volumes
Se você clicar em Olá **grupos de Volume** nó, Olá **resultados** painel mostra Olá informações sobre cada grupo de volume a seguir, dependendo das seleções de coluna Olá feitas. (Olá colunas Olá **resultados** painel são configuráveis. Saudação de atalho **Volumes** nó, selecione **exibição**e, em seguida, selecione **Adicionar/remover colunas**.)

| Coluna de resultados | Descrição |
|:--- |:--- |
| Nome |Olá **nome** coluna contém o nome de Olá Olá do grupo de volume. |
| Aplicativo |Olá **aplicativos** coluna mostra o número de saudação de gravadores VSS atualmente instalados e em execução no hello host do Windows. |
| Selecionado |Olá **selecionados** coluna mostra o número de saudação de volumes que estão contidos no grupo de volumes de saudação. Um zero (0) indica que nenhum aplicativo está associado a volumes de saudação no grupo de volumes de saudação. |
| Importado |Olá **importado** coluna mostra o número de saudação de volumes importados. Quando definido muito**True**, esta coluna indica que um grupo de volumes foi importado do hello portal do Azure e não foi criado no Gerenciador de instantâneos do StorSimple. |

> [!NOTE]
> Grupos de volumes do StorSimple Snapshot Manager também são exibidos na Olá **políticas de Backup** guia Olá portal do Azure.
> 
> 

## <a name="create-a-volume-group"></a>Criar um grupo de volumes
Use Olá seguindo o procedimento toocreate um grupo de volumes.

#### <a name="toocreate-a-volume-group"></a>toocreate um grupo de volumes
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique com botão direito **grupos de Volume**e, em seguida, clique em **criar grupo de Volume**.
   
    ![Criar Grupo de Volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Olá **criar um grupo de volumes** caixa de diálogo é exibida.
   
    ![Criar uma caixa de diálogo de grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Digite hello informações a seguir:
   
   1. Em Olá **nome** , digite um nome exclusivo para o novo grupo de volumes hello.
   2. Em Olá **aplicativos** caixa, selecione os aplicativos associados com volumes de saudação que estará adicionando o grupo de volume toohello.
      
       Olá **aplicativos** caixa de lista somente os aplicativos que usam volumes do StorSimple e tenham gravadores VSS habilitados para eles. Um gravador VSS é habilitado somente se todos os volumes de Olá Olá gravador está ciente de volumes do StorSimple. Se Olá aplicativos caixa estiver vazia, nenhum aplicativo que use volumes do StorSimple do Azure e tem suporte para gravadores VSS está instalado. (Atualmente, o Azure StorSimple dá suporte ao Microsoft Exchange e ao SQL Server.) Para obter mais informações sobre os gravadores VSS, veja [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Se você selecionar um aplicativo, todos os volumes associados a ele serão selecionados automaticamente. Por outro lado, se você selecionar volumes associados a um aplicativo específico, aplicativo hello é selecionado automaticamente no hello **aplicativos** caixa. 
   3. Em Olá **Volumes** , selecione o grupo de volumes do StorSimple volumes tooadd toohello. 
      
      * É possível incluir volumes com partições simples ou múltiplas. (Volumes com partições múltiplas podem ser discos dinâmicos ou básicos com várias partições.) Um volume que contém partições múltiplas é tratado como uma única unidade. Consequentemente, se você adicionar apenas uma saudação partições tooa do grupo de volume, Olá todas as outras partições são toothat adicionado automaticamente o grupo de volumes no hello mesmo tempo. Depois de adicionar um grupo de volumes tooa vários partição volume, hello volume de múltiplas partições continuará toobe tratado como uma única unidade.
      * Você pode criar grupos de volume vazio, não atribuindo nenhum toothem de volumes. 
      * Não misture volumes compartilhados de cluster (CSVs) e não CSVs no hello mesmo grupo de volumes. Gerenciador de instantâneos do StorSimple não oferece suporte a uma mistura de volumes CSV e Olá de volumes não CSV no mesmo instantâneo.
4. Clique em **Okey** toosave grupo de volumes de saudação.

## <a name="back-up-a-volume-group"></a>Fazer backup de um grupo de volumes
Use Olá seguindo o procedimento tooback um grupo de volume.

#### <a name="tooback-up-a-volume-group"></a>tooback um grupo de volume
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **fazer Backup**.
   
    ![Fazer imediatamente o backup do grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. Em Olá **fazer Backup** caixa de diálogo, selecione **instantâneo Local** ou **instantâneo em nuvem**e, em seguida, clique em **criar**.
   
    ![Caixa de diálogo Fazer backup](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. tooconfirm Olá backup está em execução, expanda Olá **trabalhos** nó e, em seguida, clique **executando**. Olá backup deve ser listado.
5. Olá tooview concluída de instantâneo, expanda Olá **catálogo de Backup** nó, expanda o nome do grupo de volume hello e, em seguida, clique em **instantâneo Local** ou **instantâneo em nuvem**. Olá backup será listado se for concluído com êxito.

## <a name="edit-a-volume-group"></a>Editar um grupo de volumes
Use Olá seguindo o procedimento tooedit um grupo de volumes.

#### <a name="tooedit-a-volume-group"></a>tooedit um grupo de volumes
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **editar**.
3. Olá * * criar um grupo de volumes * * caixa de diálogo é exibida. Você pode alterar Olá **nome**, **aplicativos**, e **Volumes** entradas.
4. Clique em **Okey** toosave suas alterações.

## <a name="delete-a-volume-group"></a>Excluir um grupo de volumes
Use Olá seguindo o procedimento toodelete um grupo de volumes. 

> [!WARNING]
> Isso também exclui todos os backups de saudação associados com o grupo de volumes de saudação.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete um grupo de volumes
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **excluir**.
3. Olá **excluir grupo de Volume** caixa de diálogo é exibida. Tipo **confirmar** Olá caixa de texto e, em seguida, clique em **Okey**.
   
    grupo de volumes Olá excluído desaparece da lista Olá Olá **resultados** painel e todos os backups que estão associados esse grupo de volume são excluídos do catálogo de backup hello.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple toocreate e gerenciar políticas de backup](storsimple-snapshot-manager-manage-backup-policies.md).

