---
title: "Introdução: proteger VMs do Azure com um cofre de serviços de recuperação | Microsoft Docs"
description: "Proteger as VMs do Azure com um cofre de serviços de recuperação. Use backups de VMs implantadas pelo Gerenciador de recursos, implantado clássico VMs e armazenamento VMs Premium criptografado VMs, VMs em discos gerenciado tooprotect seus dados. Crie e registre um cofre de Serviços de Recuperação. Registre as VMs, crie uma política e proteger as VMs no Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Fazer backup de máquinas virtuais do Azure cofres de serviços de tooRecovery
> [!div class="op_single_selector"]
> * [Proteger VMs em um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md)
> * [Proteger VMs com um cofre de backup](backup-azure-vms-first-look.md)
>
>

Este tutorial descreve Olá etapas para criar um cofre de serviços de recuperação e backup de uma máquina virtual do Azure (VM). Os cofres dos Serviços de Recuperação protegem:

* VMs implantadas com o Azure Resource Manager
* VMs clássicas
* VMs de armazenamento Padrão
* VMs de armazenamento Premium
* VMs em execução em discos gerenciados
* VMs criptografadas usando o Azure Disk Encryption, com BEK e KEK
* Backup consistente de aplicativos de VMs do Windows que usam o VSS, e de VMs do Linux que usam scripts personalizados pré e pós-instantâneo

Para obter mais informações sobre a proteção de armazenamento Premium máquinas virtuais, consulte o artigo Olá [backup e restauração de máquinas virtuais de armazenamento Premium](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Para obter mais informações sobre o suporte para VMs de disco gerenciado, consulte [Backup e restauração de VMs em discos gerenciados](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Para saber mais sobre a estrutura pré e pós-script para backup de uma VM do Linux, confira [Backup consistente de aplicativos de VM do Linux que usam pré e pós-script] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

toofind mais sobre o que pode backup e o que não é possível, consulte [aqui](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Este tutorial presume que você já tiver uma VM em sua assinatura do Azure e que você fez medidas tooallow Olá serviço de backup tooaccess Olá VM.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Dependendo do número de saudação de máquinas virtuais que você deseja tooprotect, você pode começar de diferentes pontos de partida. Tooback backup de várias máquinas virtuais em uma única operação, vá Cofre de serviços de recuperação de toohello e [o trabalho de backup iniciar saudação do painel do cofre Olá](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Se você quiser tooback a uma única máquina virtual, você pode iniciar o trabalho de backup de saudação da folha de gerenciamento de VM.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Configurar o trabalho de backup Olá da folha de gerenciamento de VM Olá

Use Olá seguindo o trabalho de backup etapas tooconfigure Olá da folha de gerenciamento da máquina virtual no portal do Azure de saudação Olá. Essas etapas não se aplicam a máquinas virtuais de toohello no portal clássico do hello.

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **mais serviços** e, na caixa de diálogo de filtro hello, digite **máquinas virtuais**. Conforme você digita, Olá lista de filtros de recursos. Ao ver Máquinas virtuais, selecione-a.

  ![No menu Hub, clique em caixa de diálogo de texto de tooopen mais serviços e máquinas virtuais de tipo](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  Olá lista de máquinas virtuais (VM) na assinatura Olá, é exibida.

  ![Olá a lista de máquinas virtuais na assinatura de saudação é exibida.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Olá, selecione lista tooback uma VM para cima.

  ![Olá a lista de máquinas virtuais na assinatura de saudação é exibida.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Quando você seleciona Olá VM, lista de saudação de máquinas virtuais desloca toohello esquerda e folha de gerenciamento de máquina virtual hello e painel de máquina virtual hello, abrir. </br>
 ![Folha de Gerenciamento de VM](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Na folha de gerenciamento de VM hello, em Olá **configurações** seção, clique em **Backup**. </br>

  ![Opção de backup na folha de gerenciamento da VM](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  Abre a folha de backup de habilitar Hello.

  ![Opção de backup na folha de gerenciamento da VM](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Para o Cofre de serviços de recuperação de saudação, clique em **selecionar existentes** e escolha Olá cofre na lista suspensa de saudação.

  ![Habilitar o Assistente de Backup](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Se não há nenhum Cofre de serviços de recuperação, ou você deseja toouse um novo cofre, clique em **criar novo** e fornecer nome hello novo cofre de saudação. Um novo cofre é criado no hello mesmo grupo de recursos e no mesmo local da máquina virtual de saudação. Se você quiser toocreate um cofre de serviços de recuperação com valores diferentes, consulte Olá seção sobre como muito[criar um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. detalhes de saudação tooview de saudação política de Backup, clique em **política de Backup**.

  Olá **política de Backup** folha é aberta e oferece detalhes de saudação da política de saudação selecionada. Se houver outras políticas, use o menu suspenso de saudação toochoose uma política de backup diferente. Se você desejar toocreate uma política, selecione **criar novo** do menu suspenso de saudação. Para obter instruções sobre como definir uma política de backup, confira [Definindo uma política de backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). política de backup do toosave Olá alterações toohello e retorno toohello habilitar backup folha clique **Okey**.

  ![Selecionar a política de backup](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Na folha de backup de habilitar hello, clique em **habilitar Backup** toodeploy política de saudação. Implantar política Olá associa cofre hello e máquinas virtuais de saudação.

  ![Botão Habilitar Backup](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Você pode acompanhar o progresso de configuração de saudação por meio de notificações de saudação que aparecem no portal de saudação. saudação de exemplo a seguir mostra que a implantação iniciada.

  ![Habilitar a notificação de backup](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Depois de saudação configuração for concluída, na folha de gerenciamento de VM hello, clique em **Backup** folha de Item de Backup Olá tooopen e exibição Olá detalhes.

  ![Exibição de Item de Backup de VM](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Até que o backup de saudação inicial for concluída, **último status de backup** mostra como **aviso (backup inicial pendente)**. ocorre toosee quando Olá programado próximo trabalho de backup, em **política de Backup** clique Olá nome da política de saudação. folha de política de Backup Olá é aberto e mostra o tempo de saudação do backup agendado hello.

10. toorun um Backup de trabalho e criar ponto de recuperação inicial de hello, em Olá Backup cofre folha clique **Backup agora**.

  ![Clique em backup inicial do Backup agora toorun Olá](./media/backup-azure-vms-first-look-arm/backup-now.png)

  Fazer Backup agora folha Olá é aberto.

  ![mostra o Backup agora folha Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Olá Backup agora folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.

  ![conjunto Olá último dia Olá Backup agora o ponto de recuperação será mantido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notificações de implantação informar o trabalho de backup Olá foi disparado, e que você pode monitorar o progresso de saudação do trabalho de saudação na página de trabalhos de Backup hello.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Configurar o trabalho de backup de saudação do Cofre de serviços de recuperação de saudação
trabalho de backup tooconfigure hello, concluir Olá etapas a seguir.  

1. Crie um cofre dos Serviços de Recuperação para uma máquina virtual.
2. Olá Use tooselect portal do Azure um cenário, definir uma política de Backup e identificar itens tooprotect.
3. Faça backup de saudação inicial.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Criar um cofre de Serviços de Recuperação para uma VM
Um cofre de serviços de recuperação é uma entidade que armazena todos os backups de saudação e pontos de recuperação que foram criados ao longo do tempo. Olá Cofre de serviços de recuperação também contém política de backup Olá aplicada toohello protegido VMs.

> [!NOTE]
> Fazer backup das VMs é um processo local. Você não pode fazer backup de máquinas virtuais do Cofre de serviços de recuperação de tooa de um local em outro local. Portanto, para cada local do Azure com VMs toobe feito, pelo menos um cofre de serviços de recuperação deve existir no local.
>
>

toocreate um cofre de serviços de recuperação:

1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.
2. No menu de Hub hello, clique em **mais serviços** in Olá tipo de caixa de diálogo de filtro e **dos serviços de recuperação**. Conforme você digita, Olá lista de filtros de recursos. Quando você vir cofres de serviços de recuperação na lista de saudação, clique nele.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Se houver cofres dos serviços de recuperação na assinatura hello, cofres hello serão listados.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Para **nome**, insira um cofre de saudação tooidentify nome amigável. nome da saudação precisa toobe exclusivo Olá assinatura do Azure. Digite um nome que contenha de 2 a 50 caracteres. Ele deve começar com uma letra e pode conter apenas letras, números e hifens.

5. Em Olá **assinatura** seção, use Olá toochoose de menu suspenso Olá assinatura do Azure. Se você usar apenas uma assinatura, essa assinatura será exibida e você pode ignorar toohello próxima etapa. Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura. Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.

6. Em Olá **grupo de recursos** seção:

    * Selecione **criar novo** se você quiser toocreate um grupo de recursos.
    Ou
    * Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.

  Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

7. Clique em **local** tooselect Olá região para o cofre hello. Essa opção determina a região geográfica hello, onde os dados de backup são enviados.

  > [!IMPORTANT]
  > Se você tiver certeza da saudação localização na qual sua VM, feche fora da caixa de diálogo de criação de cofre hello e vá toohello a lista de máquinas virtuais no portal de saudação. Se você tiver máquinas virtuais em várias regiões, crie um cofre de Serviços de Recuperação em cada região. Crie cofre Olá no primeiro local de saudação antes de ir toohello próximo local. Não há que nenhuma conta de armazenamento necessidade toospecify Olá usado toostore Olá os dados de backup – Olá Cofre de serviços de recuperação e Olá serviço Backup do Azure automaticamente manipular o armazenamento de saudação.
  >

8. Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.

    Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação. Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação. Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.

    ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.

Agora que você criou seu cofre, saiba como tooset Olá replicação de armazenamento.

### <a name="set-storage-replication"></a>Definir replicação de armazenamento
opção de replicação de armazenamento Olá permite toochoose entre o armazenamento com redundância geográfica e o armazenamento redundante localmente. Por padrão, seu cofre tem armazenamento com redundância geográfica. Se Olá Cofre de serviços de recuperação é o backup do primário, deixe Olá replicação opção set toogeo redundância de armazenamento. Escolha o armazenamento com redundância local se quiser uma opção mais barata que não seja tão durável. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento no hello [visão geral de replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).

configuração de replicação de armazenamento de saudação tooedit:

1. De saudação **os cofres de serviços de recuperação** folha, novo cofre de saudação select.

  ![Selecione Novo cofre de saudação da lista de saudação do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Quando você seleciona o cofre hello, Olá folha de configurações (*que tem o nome do cofre Olá na parte superior da saudação*) e Olá cofre detalhes blade aberto.

  ![Exibir configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Na folha de configurações do cofre novo hello, Olá slide vertical tooscroll para baixo toohello seção gerenciar e clique em **Backup infraestrutura**.
    Abre a folha de infraestrutura de Backup Hello.
3. Na folha de infraestrutura de Backup hello, clique em **configuração de Backup** tooopen Olá **configuração de Backup** folha.

    ![Definir a configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Escolha a opção de replicação de armazenamento apropriado Olá para seu Cofre de.

    ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Por padrão, seu cofre tem armazenamento com redundância geográfica. Se você usar o Azure como um ponto de extremidade de armazenamento de backup primário, continuar toouse **georredundante**. Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure hello. Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecione uma meta de backup, defina a política e definir tooprotect itens
Antes de registrar uma VM com um cofre, execute Olá tooensure de processo de descoberta que quaisquer novas máquinas virtuais que foram adicionadas toohello assinatura são identificadas. Olá processar consultas do Azure para obter lista de saudação de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como nome de serviço de nuvem hello e região Olá. Olá portal do Azure, o cenário refere-se toowhat serão tooput no cofre de serviços de recuperação de saudação. A diretiva é agenda Olá para frequência e quando os pontos de recuperação são feitos. Política também inclui o período de retenção Olá Olá pontos de recuperação.

1. Se você já tiver um serviços de recuperação de abrir o cofre, prossiga toostep 2. Caso contrário, no menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação** e clique em **os cofres de serviços de recuperação**.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    saudação de lista de cofres de serviços de recuperação é exibida.

    ![Lista de cofres de modo de exibição de saudação dos serviços de recuperação](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Na lista de saudação de cofres de serviços de recuperação, selecione um cofre tooopen seu painel.

     ![Abrir a folha do cofre](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. No menu do painel Cofre hello, clique em **Backup** tooopen folha de Backup de saudação.

    ![Abrir a folha Backup](./media/backup-azure-arm-vms-prepare/backup-button.png)

    folhas de Backup e Backup meta Olá abrir.

    ![Abrir a folha Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Na folha de meta de Backup hello, de saudação **onde sua carga de trabalho está executando** menu suspenso, escolha o Azure. De saudação **o que fazer você deseja toobackup** lista suspensa, escolha a máquina Virtual e clique em **Okey**.

    Essas ações registrar extensão da VM Olá Olá cofre. Olá meta Backup folha fecha e hello **política de Backup** folha é aberta.

    ![Abrir a folha Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Na folha de política de Backup hello, selecione política de backup Olá deseja tooapply toohello cofre.

    ![Selecionar a política de backup](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalhes de saudação da política de padrão de saudação são listados sob o menu suspenso de saudação. Se você desejar toocreate uma política, selecione **criar novo** do menu suspenso de saudação. Para obter instruções sobre como definir uma política de backup, confira [Definindo uma política de backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Clique em **Okey** tooassociate política de backup Olá cofre hello.

    Olá fecha de folha de política de Backup e hello **selecionar máquinas virtuais** folha é aberta.
5. Em Olá **selecionar máquinas virtuais** folha, escolha Olá tooassociate de máquinas virtuais com hello especificado política e clique em **Okey**.

    ![Selecionar carga de trabalho](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de saudação selecionada é validada. Se você não vir Olá virtual máquinas que você espera que toosee, verifique se eles existem no hello mesmo local do Azure como o Cofre de serviços de recuperação de saudação. local de saudação de saudação que Cofre de serviços de recuperação é mostrado no painel do cofre hello.

6. Agora que você definiu todas as configurações para o cofre hello, na folha de Backup hello, clique em **habilitar Backup** toodeploy Olá cofre toohello de política e Olá VMs. Implantar a política de backup Olá não criar um ponto de recuperação inicial Olá para a máquina virtual de saudação.

    ![Habilitar Backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Depois de habilitar o backup de saudação com êxito, sua política de backup será executado na agenda. No entanto, continue tooinitiate Olá primeiro trabalho de backup.

## <a name="initial-backup"></a>Backup inicial
Quando uma política de backup tiver sido implantada na máquina virtual hello, o que significa que dados saudação foi feitos backup. Por padrão, Olá primeiro backup agendado (conforme definido na política de backup Olá) é backup inicial hello. Até que ocorra o backup inicial hello, Olá Status do último Backup em Olá **trabalhos de Backup** folha mostra como **aviso (backup inicial pendente)**.

![Backup pendente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A menos que o backup inicial está vencido toobegin em breve, é recomendável que você execute **backup agora**.

toorun saudação inicial trabalho de backup:

1. No painel do cofre hello, clique em número de saudação em **itens de Backup**, ou clique em Olá **itens de Backup** lado a lado. <br/>
  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Olá **itens de Backup** folha é aberta.

  ![Fazer backup de itens](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Em Olá **itens de Backup** folha, item Olá select.

  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Olá **itens de Backup** lista é aberta. <br/>

  ![Trabalho de backup iniciado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Em Olá **itens de Backup** lista, clique nas reticências de saudação **...**  tooopen menu de contexto de saudação.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu.png)

  menu de contexto de saudação aparece.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. No menu de contexto de saudação, clique em **Backup agora**.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  Fazer Backup agora folha Olá é aberto.

  ![mostra o Backup agora folha Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Olá Backup agora folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.

  ![conjunto Olá último dia Olá Backup agora o ponto de recuperação será mantido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notificações de implantação informar o trabalho de backup Olá foi disparado, e que você pode monitorar o progresso de saudação do trabalho de saudação na página de trabalhos de Backup hello. Dependendo do tamanho de saudação da VM, criar backup de saudação inicial pode demorar um pouco.

6. status de saudação tooview ou rastrear do backup inicial hello, no painel do cofre hello, em Olá **trabalhos de Backup** bloco clique **em andamento**.

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Abre a folha de trabalhos de Backup de saudação.

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Em Olá **trabalhos de Backup** folha, você pode ver o status de saudação de todos os trabalhos. Verifique se o trabalho de backup Olá para sua VM ainda está em andamento ou se ele tiver sido concluída. Quando um trabalho de backup for concluído, o status de saudação é *concluído*.

  > [!NOTE]
  > Como parte da operação de backup hello, Olá serviço Backup do Azure emite uma extensão de backup de toohello do comando em cada tooflush VM todas as gravações e tirar um instantâneo consistente.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar Olá agente de VM na máquina virtual de saudação
Essas informações são fornecidas quando necessário. Hello Azure VM Agent deve ser instalado em Olá máquina virtual do Azure para Olá toowork de extensão de Backup. No entanto, se sua VM foi criada de saudação Galeria do Azure, em seguida, Olá agente de VM já está presente na máquina virtual de saudação. Máquinas virtuais que são migrados de datacenters locais seria não Olá VM Agent instalado. Nesse caso, Olá agente de VM precisa toobe instalado. Se você tiver problemas ao fazer backup Olá VM do Azure, verifique se hello Azure VM Agent está instalado corretamente na máquina virtual de saudação (consulte Olá a tabela a seguir). Se você criar uma VM personalizada, [garantir Olá **Olá instalar agente de VM** caixa de seleção é marcada](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) antes de máquina virtual de saudação é provisionada.

Saiba mais sobre Olá [agente de VM](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) e [como tooinstall-](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Olá, a tabela a seguir fornece informações adicionais sobre Olá VM Agent para Windows e VMs do Linux.

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Olá instalar agente de VM |<li>Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisa de instalação de saudação do toocomplete de privilégios de administrador. <li>[Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. |<li> Instalar hello mais recente [agente Linux](https://github.com/Azure/WALinuxAgent) do GitHub. Você precisa de instalação de saudação do toocomplete de privilégios de administrador. <li> [Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. |
| Atualizando Olá agente de VM |Olá atualizar agente de VM é tão simple quanto a reinstalação Olá [binários de agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Certifique-se de que nenhuma operação de backup está em execução enquanto o agente de VM hello está sendo atualizado. |Siga as instruções de saudação [atualização Olá agente de VM do Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Certifique-se de que nenhuma operação de backup está em execução durante a saudação que VM Agent está sendo atualizado. |
| Validar a instalação do agente de VM Olá |<li>Navegue toohello *C:\WindowsAzure\Packages* pasta Olá VM do Azure. <li>Você deve encontrar o arquivo de WaAppAgent.exe de saudação presente.<li> Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão do produto de saudação de guia deve ser 2.6.1198.718 ou superior. |N/D |

### <a name="backup-extension"></a>Extensão de backup
Uma vez Olá que VM Agent está instalado na máquina virtual de hello, Olá serviço Backup do Azure instala Olá extensão backup toohello agente de VM. Olá serviço Backup do Azure diretamente atualizações e patches extensão de backup Olá sem intervenção do usuário adicional.

serviço de Backup Olá instala extensão de backup hello, mesmo se Olá VM não está em execução. Uma VM em execução fornece a possibilidade maior Olá da obtenção de um ponto de recuperação consistentes com aplicativos. No entanto, Olá serviço Backup do Azure continua tooback backup Olá VM mesmo se ele está desativado e não foi possível instalar a extensão de saudação. Esse tipo de backup é conhecido como VM Offline, e é o ponto de recuperação Olá *falha consistente*.

## <a name="troubleshooting-information"></a>Informações sobre solução de problemas
Se você tiver problemas para realizar algumas das tarefas de saudação neste artigo, consulte o [guia de solução de problemas](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Preços
custo de saudação do backup de máquinas virtuais do Azure é com base no número de saudação de instâncias protegidas. Para ter uma definição de uma instância protegida, confira [O que é uma instância protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Para obter um exemplo de como calcular o custo de saudação do backup de uma máquina virtual, consulte [como instâncias protegidas são calculadas](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Consulte Olá preços do Azure Backup página para obter informações sobre [de preços de Backup](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).
