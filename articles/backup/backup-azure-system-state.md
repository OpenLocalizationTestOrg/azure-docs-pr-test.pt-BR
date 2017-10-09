---
title: aaaBack backup tooAzure de estado do sistema Windows | Microsoft Docs
description: "Saiba tooback backup de estado do sistema de saudação do Windows Server e/ou tooAzure de computadores Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: como toobackup; como tooback; pastas e arquivos de backup
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Fazer backup de estado do sistema do Windows na implementação do Gerenciador de Recursos
Este artigo explica como tooback o sistema Windows Server estado tooAzure. É um tutorial toowalk pretendido você sobre conceitos básicos de saudação.

Se você quiser tooknow mais sobre o Backup do Azure, leia este [visão geral](backup-introduction-to-azure-backup.md).

Se não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/) , que permitirá o acesso a qualquer serviço do Azure.

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
tooback backup de seus arquivos e pastas, é necessário toocreate um cofre de serviços de recuperação na região Olá onde você deseja toostore Olá dados. Você também precisa toodetermine como você deseja que o armazenamento replicado.

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

    * Selecione **criar novo** se você quiser toocreate um grupo de recursos.
    Ou
    * Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.

  Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

7. Clique em **local** tooselect Olá região para o cofre hello. Essa opção determina a região geográfica hello, onde os dados de backup são enviados.

8. Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.

    Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação. Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação. Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.

    ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.

### <a name="set-storage-redundancy-for-hello-vault"></a>Definir a redundância de armazenamento para o cofre Olá
Quando você criar um cofre de serviços de recuperação, certifique-se de redundância de armazenamento é a maneira de saudação configurado desejado.

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

Agora que você criou um cofre, configure-o para fazer backup do Estado do Sistema do Windows.

## <a name="configure-hello-vault"></a>Configurar o cofre Olá
1. Olá folha de Cofre de serviços de recuperação (para Olá cofre você acabou de criar), na seção de introdução de saudação em, clique em **Backup**, em seguida, na Olá **Introdução ao Backup** folha, selecione  **Meta de backup**.

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Olá **Backup meta** folha é aberta.

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. De saudação **onde sua carga de trabalho está executando?** menu suspenso, selecione **local**.

    Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.

3. De saudação **o que fazer você deseja toobackup?** menu, selecione **o estado do sistema**e clique em **Okey**.

    ![Configuração de arquivos e pastas](./media/backup-azure-system-state/backup-goal-system-state.png)

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
> Habilitar o backup por meio de saudação portal do Azure ainda não está disponível. Use Olá Microsoft Azure Recovery Services Agent tooback backup de estado do sistema do Windows Server.
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

## <a name="back-up-windows-server-system-state-preview"></a>Fazer backup do Estado do Sistema do Windows Server (visualização prévia)
backup de saudação inicial inclui três tarefas:

* Habilitar o Backup de estado do sistema usando hello Azure Backup agent
* Agendamento de backup Olá
* Fazer backup de arquivos e pastas para Olá primeira vez

toocomplete saudação inicial fazer backup, agente de serviços de recuperação do Microsoft Azure use hello.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>backup de estado do sistema tooenable usando hello Azure Backup agent

1. Em uma sessão do PowerShell, execute Olá mecanismo de Backup do Azure do comando toostop Olá a seguir.

  ```
  PS C:\> Net stop obengine
  ```

2. Abra a saudação do registro do Windows.

  ```
  PS C:\> regedit.exe
  ```

3. Adicione Olá seguinte chave de registro com hello especificado valor DWord.

  | Caminho do registro | Chave do registro | Valor DWord |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Reinicie o mecanismo de Backup de saudação executando Olá comando em um prompt de comando a seguir.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>trabalho de backup tooschedule Olá

1. Abra o agente de serviços de recuperação do Microsoft Azure hello. Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.

    ![Inicie o agente de serviços de recuperação do Azure Olá](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. No agente de serviços de recuperação de saudação, clique em **agendamento de Backup**.

    ![Agendar um backup do Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Em Olá Introdução página do Assistente de agendamento de Backup de saudação, clique em **próximo**.

4. Na página de tooBackup do hello selecionar itens, clique em **adicionar itens**.

5. Selecione **Estado do sistema** e, em seguida, clique em **OK**.

6. Clique em **Avançar**.

7. Olá agenda de Backup de estado do sistema e de retenção é definida automaticamente tooback backup de todos os domingos às 9:00 PM, horário local e período de retenção de saudação é definido too60 dias.

   > [!NOTE]
   > A política de backup e retenção do estado do sistema é configurada automaticamente. Se você fizer backup de arquivos e pastas além toohello estado de sistema do Windows Server, especifique a única política de Backup e retenção de saudação para backups de arquivo do Assistente de saudação. 
   >

8. Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.

9. Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback backup de estado do sistema do Windows Server para Olá primeira vez

1. Certifique-se de que não existem atualizações pendentes para o Windows Server que exigem uma reinicialização.

2. No agente de serviços de recuperação de saudação, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.

    ![Fazer backup do Windows Server agora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello. Em seguida, clique em **Fazer Backup**.

4. Clique em **fechar** tooclose Assistente de saudação. Se você fechar o Assistente de saudação antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.

5. Se você fizer backup de arquivos e pastas no servidor, além de toohello estado de sistema do Windows Server, o assistente Fazer Backup agora Olá fará backup somente arquivos. tooperform um estado de sistema ad hoc backup, use Olá comando PowerShell a seguir:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.

  ![IR completo](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Perguntas frequentes

Olá perguntas e respostas a seguir fornecem informações complementares.

### <a name="what-is-hello-staging-volume"></a>O que é Olá preparo Volume?

Olá preparo Volume representa local intermediário de saudação onde Olá disponível de modo nativo, Backup do Windows Server prepara Olá Backup de estado do sistema. Agente de Backup do Azure, em seguida, compacta e criptografa esse backup intermediário e envia a que ele por meio de toohello de protocolo HTTPS seguro configurado Cofre de serviços de recuperação. **É altamente recomendável que estabelecer Olá preparo Volume em um volume não-Windows-OS. Se você observar problemas com Backups de estado do sistema, verificar o local de saudação do seu Volume de preparo é a primeira etapa de solução de problemas de saudação.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Como alterar Olá preparo caminho do Volume especificado no agente de Backup do Azure Olá?

Olá Volume de preparo está localizado na pasta de cache Olá por padrão. 

1. toochange nesse local, use Olá comando (em um prompt de comando com privilégios elevados) a seguir:
  ```
  PS C:\> Net stop obengine
  ```

2. Em seguida, atualize Olá entradas do registro com hello caminho toohello nova preparação Volume pasta a seguir.

  |Caminho do registro|Chave do registro|Valor|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | novo local do volume de preparo |

Olá preparo caminho diferencia maiusculas de minúsculas e deve ser Olá exata mesmo maiusculas e minúsculas como o que existe no servidor de saudação. 

3. Depois que você alterar o caminho do volume de preparo hello, reinicie o mecanismo de Backup de saudação:
  ```
  PS C:\> Net start obengine
  ```
4. toopick caminho Olá alterado, agente de serviços de recuperação do Microsoft Azure Olá abrir e gatilho um backup ad hoc do estado do sistema.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Por que é o estado do sistema Olá retenção padrão definido too60 dias?

vida útil de saudação de um backup de estado do sistema é Olá igual a configuração hello "tempo de desativação" para a função do Windows Server Active Directory hello. valor padrão de saudação para entrada de tempo de vida de desativação Olá é 60 dias. Esse valor pode ser definido no objeto de configuração do serviço de diretório (NTDS) hello.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Como alterar o padrão de saudação Backup e política de retenção para o estado do sistema?

padrão de saudação toochange Backup e política de retenção para o estado do sistema:
1. Pare o mecanismo de Backup de saudação. Execute Olá comando a seguir em um prompt de comando com privilégios elevados.

  ```
  PS C:\> Net stop obengine
  ```

2. Adicionar ou atualizar Olá entradas de chave de registro em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider a seguir.

  |Nome do Registro|Descrição|Valor|
  |-------------|-----------|-----|
  |SSBScheduleTime|Tempo de saudação tooconfigure usado do backup hello. O horário padrão está configurado para as 21 horas da hora local.|DWord: Formato HHMM (decimal). 2130, por exemplo, significa 21h30 da hora local.|
  |SSBScheduleDays|Dias de saudação tooconfigure usado quando o Backup de estado do sistema deve ser executada no hello especificado de tempo. Dígitos individuais especificam dias da semana hello. 0 representa domingo, 1 é a segunda-feira, e assim por diante. O dia padrão para o backup é domingo.|DWord: dias do backup toorun da semana hello (decimal), por exemplo 1230 agenda de backups na segunda-feira, terça-feira, quarta-feira e domingo.|
  |SSBRetentionDays|Backup de tooretain do tooconfigure usado Olá dias. O valor padrão é de 60. O valor máximo permitido é de 180.|DWord: Backup de tooretain dias (decimal).|

3. Use Olá mecanismo de backup do comando toorestart Olá a seguir.
    ```
    PS C:\> Net start obengine
    ```

4. Abra o agente de serviços de recuperação do Microsoft hello.

5. Clique em **agendamento de Backup** e, em seguida, clique em **próximo** até ver as alterações de saudação refletidas.

6. Clique em **concluir** tooapply alterações de saudação.


## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Próximas etapas
* Obtenha mais detalhes sobre o [backup de computadores que usam o Windows](backup-configure-vault.md).
* Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).
* Se você precisar toorestore um backup, use este artigo muito[restaurar arquivos tooa Windows máquina](backup-azure-restore-windows-server.md).
