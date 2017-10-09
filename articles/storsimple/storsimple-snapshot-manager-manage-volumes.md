---
title: "aaaStorSimple Gerenciador de instantâneos e volumes | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in tooview e gerenciar volumes e backups tooconfigure."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Use o Gerenciador de instantâneos StorSimple tooview e gerenciar volumes
## <a name="overview"></a>Visão geral
Você pode usar o hello Gerenciador de instantâneos StorSimple **Volumes** nó (em Olá **escopo** painel) tooselect volumes e exibir informações sobre eles. Olá volumes são apresentados como unidades que correspondem a toohello volumes montados pelo host hello. Olá **Volumes** nó mostra volumes locais e tipos de volume StorSimple, incluindo volumes descobertos através do uso de saudação do iSCSI e um dispositivo com suporte. 

Para obter mais informações sobre os volumes com suporte, vá muito[suporte para vários tipos de volume](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Lista de Volumes no painel de Resultados](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Olá **Volumes** nó também lhe permite examinar novamente ou excluir os volumes depois StorSimple Snapshot Manager descobre-los. 

Este tutorial explica como montar, inicializar e formatar volumes e usar o StorSimple Snapshot Manager para:

* Exibir informações sobre volumes 
* Excluir volumes
* Examinar volumes novamente 
* Configurar um volume básico e fazer seu backup
* Configurar um volume dinâmico espelhado e fazer seu backup

> [!NOTE]
> Todos os Olá **Volume** ações de nó também estão disponíveis no hello **ações** painel.
> 
> 

## <a name="mount-volumes"></a>Montar volumes
Saudação de uso seguindo o procedimento toomount, inicializar e formatar volumes do StorSimple. Este procedimento usa o gerenciamento de disco, um utilitário do sistema para gerenciar discos e volumes correspondentes hello ou partições. Para obter mais informações sobre o gerenciamento de disco, vá muito[gerenciamento de disco](https://technet.microsoft.com/library/cc770943.aspx) no site do Microsoft TechNet hello.

#### <a name="toomount-volumes"></a>volumes toomount
1. No computador host, inicie o iniciador iSCSI da Microsoft hello.
2. Forneça um dos endereços IP da interface hello como o portal de destino de saudação ou endereço IP de descoberta e conecte o dispositivo toohello. Depois Olá dispositivo estiver conectado, volumes Olá será acessível tooyour sistema do Windows. Para obter mais informações sobre como usar o iniciador iSCSI da Microsoft hello, vá toohello seção "Conectando tooan dispositivo iSCSI de destino" [instalando e configurando o Microsoft iSCSI Initiator][1].
3. Use qualquer Olá opções toostart gerenciamento de disco a seguir:
   
   * Digite Diskmgmt.msc Olá **executar** caixa.
   * Inicie o Gerenciador do servidor, expanda Olá **armazenamento** nó e selecione **gerenciamento de disco**.
   * Iniciar **ferramentas administrativas**, expanda Olá **gerenciamento do computador** nó e selecione **gerenciamento de disco**. 
     
     > [!NOTE]
     > Você deve usar privilégios de administrador toorun gerenciamento de disco.
     > 
     > 
4. Usar volumes Olá online:
   
   1. No Gerenciamento de Disco, clique com o botão direito em qualquer volume marcado como **Offline**.
   2. Clique em **Reativar Disco**. Olá disco deve ser marcado **Online** depois Olá é reativado.
5. Inicialize volumes hello:
   
   1. Clique com botão direito volumes Olá descoberto.
   2. No menu de saudação, selecione **inicializar disco**.
   3. Em Olá **inicializar disco** caixa de diálogo, discos Olá selecione que você deseja tooinitialize e, em seguida, clique em **Okey**.
6. Formate os volumes simples:
   
   1. Clique em um volume que você deseja tooformat.
   2. No menu de saudação, selecione **Novo Volume simples**.
   3. Use o volume de Olá Olá Novo Volume simples Assistente tooformat:
      
      * Especifique o tamanho do volume hello.
      * Forneça uma letra da unidade.
      * Selecione o sistema de arquivos NTFS hello.
      * Especifique um tamanho de unidade de alocação com 64 KB.
      * Realize uma formatação rápida.
7. Formate os volumes com várias partições. Para obter instruções, vá toohello seção, "Partições e Volumes" [Implementando o gerenciamento de disco](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Exibir informações sobre os volumes
Use Olá seguintes procedimento tooview informações sobre o local e os volumes do StorSimple do Azure.

#### <a name="tooview-volume-information"></a>informações de volume tooview
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager. 
2. Em Olá **escopo** painel, clique em Olá **Volumes** nó. É exibida uma lista de volumes locais e montados, incluindo todos os volumes do StorSimple do Azure, em Olá **resultados** painel. Olá colunas Olá **resultados** painel são configuráveis. (Atalho Olá **Volumes** nó, selecione **exibição**e, em seguida, selecione **Adicionar/remover colunas**.)
   
    ![Configurar colunas de saudação](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Coluna de resultados | Descrição |
   |:--- |:--- |
   |  Nome |Olá **nome** coluna contém o volume de tooeach descoberto Olá unidade letra atribuída. |
   |  Dispositivo |Olá **dispositivo** coluna contém o endereço IP de saudação do computador host do hello dispositivo toohello conectado. |
   |  Nome do Volume do Dispositivo |Olá **nome de Volume do dispositivo** coluna contém o nome de saudação do hello dispositivo volume toowhich Olá selecionado volume pertence. Esse é o nome de volume de saudação definido no hello portal do Azure para esse volume específico. |
   |  Caminhos de acesso |Olá **caminhos de acesso** coluna exibe o volume de toohello de caminho de acesso de saudação. Isso é Olá unidade letra ou ponto de montagem no qual Olá volume é acessível no computador de host hello. |

## <a name="delete-a-volume"></a>Excluir um volume
Use Olá seguindo o procedimento toodelete um volume do Gerenciador de instantâneos do StorSimple.

> [!NOTE]
> Você não poderá excluir um volume se ele fizer parte de um grupo de volumes. (opção de exclusão de saudação não está disponível para volumes que são membros de um grupo de volume). Você deve excluir Olá todo grupo toodelete Olá volumes.

#### <a name="toodelete-a-volume"></a>toodelete um volume
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em Olá **Volumes** nó. 
3. Em Olá **resultados** painel, volume de saudação do botão direito do mouse que você deseja toodelete.
4. No menu de saudação, clique em **excluir**. 
   
    ![Excluir um volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Olá **Excluir Volume** caixa de diálogo é exibida. Tipo **confirmar** Olá caixa de texto e, em seguida, clique em **Okey**.
6. Por padrão, o StorSimple Snapshot Manager faz backup de um volume antes de excluí-lo. Essa precaução pode proteger você contra perda de dados se Olá exclusão foi involuntária. Gerenciador de instantâneos StorSimple exibe um **instantâneo automático** mensagem de progresso enquanto faz backup do volume de saudação. 
   
    ![Mensagem de instantâneo automático](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Examinar volumes novamente
Olá use volumes de saudação toorescan procedimento a seguir conectado tooStorSimple Gerenciador de instantâneos.

#### <a name="toorescan-hello-volumes"></a>volumes de saudação toorescan
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique com botão direito **Volumes**e, em seguida, clique em **examinar volumes novamente**.
   
    ![Examinar volumes novamente](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Este procedimento sincroniza a lista de volumes de saudação com o Gerenciador de instantâneos do StorSimple. Todas as alterações, como novos volumes ou volumes excluídos, serão refletidas nos resultados da saudação.

## <a name="configure-and-back-up-a-basic-volume"></a>Configurar e fazer backup de um volume básico
Use Olá seguindo o procedimento tooconfigure um backup de um volume básico e iniciar um backup imediatamente ou criar uma política para backups agendados.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar:

* Certifique-se de que hello dispositivo StorSimple e o computador host estão configurados corretamente. Para obter mais informações, vá muito[implantar seu dispositivo do StorSimple local](storsimple-deployment-walkthrough-u2.md).
* Instale e configure o StorSimple Snapshot Manager. Para obter mais informações, vá muito[implantar o Gerenciador de instantâneos do StorSimple](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure backup de um volume básico
1. Crie um volume básico no dispositivo do StorSimple hello.
2. Montar, inicializar e formatar o volume de saudação conforme descrito em [montar volumes](#mount-volumes). 
3. Clique Olá StorSimple Snapshot Manager ícone na área de trabalho. janela do Gerenciador de instantâneos StorSimple Olá é exibida. 
4. Em Olá **escopo** painel, a saudação do botão direito do mouse **Volumes** nó e selecione **examinar volumes novamente**. Quando Olá varredura é concluída, uma lista de volumes deve aparecer em Olá **resultados** painel. 
5. Em Olá **resultados** painel, volume hello e, em seguida, selecione **criar grupo de Volume**. 
   
    ![Criar Grupo de Volumes](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. Em Olá **criar grupo de Volume** caixa de diálogo, digite um nome para o grupo de volumes hello, atribuir volumes tooit e, em seguida, clique em **Okey**.
7. Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó. novo grupo de volumes Olá deve aparecer no hello **grupos de Volume** nó. 
8. Clique o nome do grupo de volume hello.
   
   * toostart um trabalho de backup (sob demanda) interativo, clique em **fazer Backup**. 
   * tooschedule um backup automático, clique em **Criar política de Backup**. Em Olá **geral** página, selecione um grupo de volume na lista de saudação. Em Olá **agenda** , insira os detalhes da agenda hello. Quando terminar, clique em **OK**. 
9. tooconfirm que Olá o trabalho de backup começou, expanda Olá **trabalhos** nó Olá **escopo** painel e, em seguida, clique em Olá **executando** nó. lista de saudação de trabalhos em execução no momento é exibida no hello **resultados** painel. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configurar e fazer backup de um volume espelhado dinâmico
Olá concluída após o backup de tooconfigure de etapas de um volume dinâmico espelhado:

* Etapa 1: Usar o gerenciamento de disco toocreate um volume dinâmico espelhado. 
* Etapa 2: Backup Use o Gerenciador de instantâneo StorSimple tooconfigure.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar:

* Certifique-se de que hello dispositivo StorSimple e o computador host estão configurados corretamente. Para obter mais informações, vá muito[implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
* Instale e configure o StorSimple Snapshot Manager. Para obter mais informações, vá muito[implantar o Gerenciador de instantâneos do StorSimple](storsimple-snapshot-manager-deployment.md).
* Configure dois volumes no dispositivo do StorSimple hello. (Nos exemplos de saudação são volumes disponíveis Olá **disco 1** e **disco 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Etapa 1: Usar o gerenciamento de disco toocreate um volume dinâmico espelhado
Gerenciamento de disco é um utilitário do sistema para gerenciar discos e volumes de saudação ou partições que eles contêm. Para obter mais informações sobre o gerenciamento de disco, vá muito[gerenciamento de disco](https://technet.microsoft.com/library/cc770943.aspx) no site do Microsoft TechNet hello.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate um volume dinâmico espelhado
1. Use qualquer Olá opções toostart gerenciamento de disco a seguir: 
   
   * Olá abrir **executar** , digite **Diskmgmt.msc**, e pressione Enter.
   * Inicie o Gerenciador do servidor, expanda Olá **armazenamento** nó e selecione **gerenciamento de disco**. 
   * Iniciar **ferramentas administrativas**, expanda Olá **gerenciamento do computador** nó e selecione **gerenciamento de disco**. 
2. Certifique-se de que você tem dois volumes disponíveis no dispositivo do StorSimple hello. (No exemplo hello, são volumes disponíveis Olá **disco 1** e **disco 2**.) 
3. Na janela de gerenciamento de disco hello, na coluna à direita de saudação do painel inferior do hello, clique com botão direito **disco 1** e selecione **Novo Volume espelhado**. 
   
    ![Novo Volume Espelhado](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Em Olá **Novo Volume espelhado** página do assistente, clique em **próximo**.
5. Em Olá **selecionar discos** , selecione **disco 2** em Olá **selecionados** painel, clique em **adicionar**e, em seguida, clique em **Avançar**. 
6. Em Olá **atribuir uma letra de unidade ou caminho** página, aceite os padrões de saudação e, em seguida, clique em **próximo**. 
7. Em Olá **Formatar Volume** página Olá **tamanho da unidade de alocação** selecione **64K**. Selecione Olá **executar uma formatação rápida** caixa de seleção e, em seguida, clique em **próximo**. 
8. Em Olá **Concluindo Olá Novo Volume espelhado** página, examine as configurações e, em seguida, clique em **concluir**. 
9. Será exibida uma mensagem tooindicate que Olá disco básico será convertido tooa dinâmico. Clique em **Sim**.
   
    ![Mensagem de conversão de disco dinâmico](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. No gerenciamento de disco, verifique se os discos 1 e 2 são mostrados como volumes dinâmicos espelhados. (**Dinâmico** devem aparecer na coluna de status Olá, e cor da barra de capacidade Olá deve alterar toored, indicando um volume espelhado.) 
    
    ![Discos dinâmicos espelhados do Gerenciamento de Disco](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Etapa 2: Use o Gerenciador de instantâneo StorSimple tooconfigure backup
Use Olá seguindo o procedimento tooconfigure um volume dinâmico espelhado e inicie um backup imediatamente ou criar uma política para backups agendados.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>tooconfigure backup de um volume dinâmico espelhado
1. Clique Olá StorSimple Snapshot Manager ícone na área de trabalho. janela do Gerenciador de instantâneos StorSimple Olá é exibida. 
2. Em Olá **escopo** painel, Olá atalho **Volumes** nó e selecione **examinar volumes novamente**. Quando Olá varredura é concluída, uma lista de volumes deve aparecer em Olá **resultados** painel. volume dinâmico espelhado da saudação é listado como um único volume. 
3. Em Olá **resultados** painel, clique com botão direito volume dinâmico espelhado da saudação e, em seguida, clique em **criar grupo de Volume**. 
4. Em Olá **criar grupo de Volume** caixa de diálogo, digite um nome para o grupo de volumes hello, atribua Olá volume dinâmico espelhado toothis grupo e, em seguida, clique em **Okey**. 
5. Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó. novo grupo de volumes Olá deve aparecer no hello **grupos de Volume** nó. 
6. Clique o nome do grupo de volume hello. 
   
   * toostart um trabalho de backup (sob demanda) interativo, clique em **fazer Backup**. 
   * tooschedule um backup automático, clique em **Criar política de Backup**. Em Olá **geral** página, grupo de volumes Olá selecione da lista de saudação. Em Olá **agenda** , insira os detalhes da agenda hello. Quando terminar, clique em **OK**. 
7. Você pode monitorar o trabalho de backup Olá conforme ele é executado. Em Olá **escopo** painel, expanda Olá **trabalhos** nó e, em seguida, clique **executando**, detalhes do trabalho Olá aparecem no hello **resultados** painel. Quando terminar o trabalho de backup Olá, detalhes de saudação são transferido toohello **últimas 24** horas de trabalho de lista. 

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar Gerenciador de instantâneos StorSimple toocreate e gerenciar grupos de volume](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
