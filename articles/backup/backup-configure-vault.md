---
title: aaaUse tooback de agente de Backup do Azure backup de arquivos e pastas | Microsoft Docs
description: "Use Olá tooback de agente de Backup do Microsoft Azure backup tooAzure de arquivos e pastas do Windows. Crie um cofre de serviços de recuperação, instalar o agente de Backup hello, definir a política de backup hello e executar o backup inicial Olá em pastas e arquivos de saudação."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: cofre de backup; fazer backup de um Windows server; backup do windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Fazer backup de um tooAzure de cliente ou servidor do Windows usando o modelo de implantação do Gerenciador de recursos de saudação
> [!div class="op_single_selector"]
> * [Portal do Azure](backup-configure-vault.md)
> * [Portal clássico](backup-configure-vault-classic.md)
>
>

Este artigo explica como tooAzure tooback backup do Windows Server (ou o cliente do Windows) de arquivos e pastas com o Backup do Azure usando Olá modelo de implantação do Gerenciador de recursos.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Etapas do processo de backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Antes de começar
tooback backup de um servidor ou cliente tooAzure, você precisa de uma conta do Azure. Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
Um cofre de serviços de recuperação é uma entidade que armazena todos os backups de saudação e pontos de recuperação criados ao longo do tempo. Cofre de serviços de recuperação de saudação também contém Olá backup política aplicada toohello protegido arquivos e pastas. Quando você criar um cofre de serviços de recuperação, você também deve selecionar opção de redundância de armazenamento apropriado hello.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate um cofre de serviços de recuperação
1. Se você ainda não fez isso, entre no toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.
2. No menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação** e clique em **os cofres de serviços de recuperação**.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Se houver cofres de serviços de recuperação na assinatura hello, cofres hello serão listados.

3. Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Para **nome**, insira um cofre de saudação tooidentify nome amigável. nome da saudação precisa toobe exclusivo Olá assinatura do Azure. Digite um nome que contenha de 2 a 50 caracteres. Ele deve começar com uma letra e pode conter apenas letras, números e hifens.

5. Em Olá **assinatura** seção, use Olá toochoose de menu suspenso Olá assinatura do Azure. Se você usar apenas uma assinatura, essa assinatura será exibida e você pode ignorar toohello próxima etapa. Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura. Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.

6. Em Olá **grupo de recursos** seção:

    * Selecione **criar novo** se você quiser toocreate um novo grupo de recursos.
    Ou
    * Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.

  Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

7. Clique em **local** tooselect Olá região para o cofre hello. Essa opção determina a região geográfica hello, onde os dados de backup são enviados.

8. Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.

  Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação. Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação. Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.

  ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.


### <a name="set-storage-redundancy"></a>Definir redundância de armazenamento
Quando você cria um cofre dos Serviços de Recuperação, determina como o armazenamento é replicado.

1. De saudação **os cofres de serviços de recuperação** folha, clique em novo cofre de saudação.

    ![Selecione Novo cofre de saudação da lista de saudação do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Hello quando você seleciona o cofre hello, **Cofre de serviços de recuperação** restringe de folha e folha de configurações de saudação (*que tem o nome de saudação do cofre Olá na parte superior da saudação*) e Olá cofre detalhes blade aberto.

    ![Exibir configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Na folha de configurações do cofre novo hello, Olá slide vertical tooscroll para baixo toohello seção gerenciar e clique em **Backup infraestrutura**.

  Abre a folha de infraestrutura de Backup Hello.

3. Na folha de infraestrutura de Backup hello, clique em **configuração de Backup** tooopen Olá **configuração de Backup** folha.

  ![Definir a configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. Escolha a opção de replicação de armazenamento apropriado Olá para seu Cofre de.

  ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  Por padrão, seu cofre tem armazenamento com redundância geográfica. Se você usar o Azure como um ponto de extremidade de armazenamento de backup primário, continuar toouse **georredundante**. Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure hello. Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).

Agora que você criou um cofre, preparar tooback sua infraestrutura backup de arquivos e pastas, baixando e instalando o agente de serviços de recuperação do Microsoft Azure hello, baixando as credenciais do cofre e, em seguida, usar essas credenciais tooregister Olá agente Cofre de saudação.

## <a name="configure-hello-vault"></a>Configurar o cofre Olá

1. Olá folha de Cofre de serviços de recuperação (para Olá cofre você acabou de criar), na seção de introdução de saudação em, clique em **Backup**, em seguida, na Olá **Introdução ao Backup** folha, selecione  **Meta de backup**.

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Olá **Backup meta** folha é aberta. Se tiver sido configurado anteriormente Olá Cofre de serviços de recuperação, Olá **meta de Backup** folhas abre quando você clica em **Backup** em serviços de recuperação de saudação cofre folha.

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. De saudação **onde sua carga de trabalho está executando?** menu suspenso, selecione **local**.

  Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.

3. De saudação **o que fazer você deseja toobackup?** menu, selecione **arquivos e pastas**e clique em **Okey**.

  ![Configuração de arquivos e pastas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  Depois de clicar em Okey, uma marca de seleção aparece próxima muito**meta Backup**e hello **preparar infraestrutura** folha é aberta.

  ![Meta de backup configurada, prepare a infraestrutura em seguida](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Em Olá **preparar infraestrutura** folha, clique em **baixar agente para Windows Server ou Windows Client**.

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  Se você estiver usando o Windows Server essenciais, em seguida, escolha o agente de Olá de toodownload para essenciais do Windows Server. Um menu pop-up solicita toorun ou salvar MARSAgentInstaller.exe.

  ![Diálogo MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. No menu pop-up de download de saudação, clique em **salvar**.

  Por padrão, Olá **MARSagentinstaller.exe** arquivo é salvo tooyour pasta de Downloads. Quando o instalador de saudação for concluída, você verá um pop-up perguntando se deseja toorun Olá installer, ou abra a pasta de saudação.

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  Você não precisa de agente de saudação tooinstall ainda. Você pode instalar o agente de saudação depois de baixar credenciais do cofre hello.

6. Em Olá **preparar infraestrutura** folha, clique em **baixar**.

  ![baixar as credenciais do cofre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  as credenciais do cofre Olá baixam tooyour pasta de Downloads. Depois que as credenciais do cofre Olá conclusão do download, você verá um pop-up perguntando se você deseja tooopen ou salva credenciais hello. Clique em **Salvar**. Se você clicar acidentalmente **abrir**, deixe a caixa de diálogo Olá tentativas de credenciais do cofre Olá tooopen, falha. Não é possível abrir as credenciais do cofre hello. Continue toohello próxima etapa. as credenciais do cofre Olá estão na pasta de Downloads de saudação.   

  ![o download das credenciais do cofre foi concluído](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Instalar e registrar o agente Olá

> [!NOTE]
> Habilitar o backup por meio de saudação portal do Azure ainda não está disponível. Use Olá Microsoft Azure Recovery Services Agent tooback backup de seus arquivos e pastas.
>

1. Localize e clique duas vezes em Olá **MARSagentinstaller.exe** de pasta de Downloads de hello (ou outro local salvo).

  instalador de saudação fornece uma série de mensagens enquanto ele extrai, instala e registra o agente de serviços de recuperação de saudação.

  ![execute as credenciais do instalador do agente dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Olá concluir o Assistente de instalação do Microsoft Azure Recovery Services Agent. Assistente de saudação toocomplete, você precisa:

  * Escolha um local para a pasta de instalação e o cache de saudação.
  * Forneça seu proxy informações do servidor se você usar um toohello de tooconnect do servidor de proxy à internet.
  * Forneça os detalhes do seu nome de usuário e de sua senha se usar um proxy autenticado.
  * Forneça as credenciais do cofre Olá baixado
  * Salve senha de criptografia de saudação em um local seguro.

  > [!NOTE]
  > Se você perde ou esquecer a senha hello, Microsoft não pode ajudar a recuperar dados de backup hello. Salve o arquivo de saudação em um local seguro. É necessário toorestore um backup.
  >
  >

Olá agent já está instalado e o computador é registrado toohello cofre. Você está pronto tooconfigure e agenda o backup.

## <a name="network-and-connectivity-requirements"></a>Requisitos de conectividade e rede

Se sua máquina/proxy limitou o acesso à internet, verifique se as configurações do firewall no computador/proxy Olá Olá tooallow configurado seguintes URLs: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Criar política de backup Olá
política de backup Olá é agenda hello quando pontos de recuperação são realizados e Olá período de tempo que os pontos de recuperação de saudação são mantidos. Use Olá Microsoft Azure Backup agent toocreate Olá política de backup de arquivos e pastas.

### <a name="toocreate-a-backup-schedule"></a>toocreate um agendamento de backup
1. Abra o agente de Backup do Microsoft Azure hello. Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.

    ![Inicie o agente de Backup do Azure Olá](./media/backup-configure-vault/snap-in-search.png)
2. No agente de Backup a saudação **ações** painel, clique em **agendamento de Backup** toolaunch Olá Assistente de agendamento de Backup.

    ![Agendar um backup do Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. Em Olá **Introdução** página de saudação Assistente de agendamento de Backup, clique em **próximo**.
4. Em Olá **selecionar itens tooBackup** , clique em **adicionar itens**.

  Abre a caixa de diálogo Olá selecionar itens.

5. Selecione arquivos hello e as pastas que você deseja tooprotect e, em seguida, clique em **Okey**.
6. Em Olá **selecionar itens tooBackup** , clique em **próximo**.
7. Em Olá **especificar agendamento de Backup** , especifique o agendamento de backup hello e clique em **próximo**.

    Você pode agendar backups diários (com uma taxa máxima de três vezes por dia) ou backups semanais.

    ![Itens para o backup do Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Para obter mais informações sobre como toospecify Olá agendamento de backup, consulte o artigo Olá [tooreplace uso do Azure Backup sua infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Em Olá **Selecionar política de retenção** página, escolha Olá Olá de políticas de retenção específico para cópia de backup hello e clique em **próximo**.

    política de retenção de saudação especifica a duração de saudação qual backup Olá é armazenado. Em vez de especificar apenas uma "política simples" para todos os pontos de backup, você pode especificar diferentes políticas de retenção com base em quando Olá backup ocorrer. Você pode modificar toomeet de políticas de retenção diária, semanal, mensal e anual Olá suas necessidades.
9. Na página de escolher tipo de Backup inicial de saudação, escolha o tipo de backup inicial hello. Deixe a opção Olá **automaticamente pela rede Olá** selecionado e, em seguida, clique em **próximo**.

    Você pode fazer backup automaticamente pela rede hello, ou você pode fazer backup offline. restante Olá deste artigo descreve o processo de saudação para fazer backup automaticamente. Se você preferir toodo um backup offline, leia o artigo de saudação [Offline fluxo de trabalho de backup no Backup do Azure](backup-azure-backup-import-export.md) para obter informações adicionais.
10. Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.
11. Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.

### <a name="enable-network-throttling"></a>Habilitar a limitação de rede
Agente de Backup do Microsoft Azure Olá fornece a limitação de rede. A limitação controles como a largura de banda de rede é usada durante a transferência de dados. Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de Internet. Limitação se aplica a tooback backup e atividades de restauração.

> [!NOTE]
> A limitação de rede não está disponível no Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ou Windows 7 (com service packs). limitação de recurso de rede de Backup do Azure de Olá emprega qualidade de serviço (QoS) no sistema operacional local de saudação. Embora o Backup do Azure pode proteger esses sistemas operacionais, versão de saudação do QoS disponíveis nessas plataformas não funciona com a limitação de rede de Backup do Azure. A limitação de rede pode ser usada em todos os outros [sistemas operacionais com suporte](backup-azure-backup-faq.md).
>
>

**a limitação de rede tooenable**

1. No agente de Backup do Microsoft Azure hello, clique em **alterar propriedades**.

    ![Alterar Propriedades](./media/backup-configure-vault/change-properties.png)
2. Em Olá **limitação** guia, selecione Olá **habilitar limitação para operações de backup do uso de largura de banda de internet** caixa de seleção.

    ![Limitação de rede](./media/backup-configure-vault/throttling-dialog.png)
3. Depois de habilitar a limitação, especifique Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.

    os valores de largura de banda Olá começam em 512 Kbps por segundo (Kbps) e podem subir too1, 023 megabytes por segundo (MBps). Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são consideradas trabalho dias. Horas fora das horas úteis designadas são consideradas horas não úteis.
4. Clique em **OK**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback backup de arquivos e pastas para Olá primeira vez
1. No agente de backup hello, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.

    ![Fazer backup do Windows Server agora](./media/backup-configure-vault/backup-now.png)
2. Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello. Em seguida, clique em **Fazer Backup**.
3. Clique em **fechar** tooclose Assistente de saudação. Se você fizer isso, antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.

Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.

![IR completo](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como fazer backup de VMs ou de outras cargas de trabalho, confira:

* Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).
* Se você precisar toorestore um backup, use este artigo muito[restaurar arquivos tooa Windows máquina](backup-azure-restore-windows-server.md).
