---
title: "aaaBack o Windows server ou estação de trabalho tooAzure (modelo clássico) | Microsoft Docs"
description: "Fazer backup de servidores ou clientes tooa backup cofre do Windows no Azure. Percorrer Noções básicas para proteger arquivos e pastas tooa Cofre de Backup usando hello Azure Backup agent."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: cofre de backup; fazer backup de um Windows server; backup do windows;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Fazer backup de um tooAzure de servidor ou estação de trabalho do Windows usando o portal clássico Olá
> [!div class="op_single_selector"]
> * [Portal clássico](backup-configure-vault-classic.md)
> * [Portal do Azure](backup-configure-vault.md)
>
>

Este artigo aborda os procedimentos de saudação que você precisa toofollow tooprepare seu ambiente e fazer backup de um tooAzure de servidor (ou estação de trabalho) do Windows. Ele também aborda considerações para a implantação de sua solução de backup. Se você estiver interessado em testar o Backup do Azure para Olá primeira vez, este artigo rapidamente o orienta pelo processo de saudação.

O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Gerenciador de Recursos e Clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="before-you-start"></a>Antes de começar
tooback backup de um servidor ou cliente tooAzure, você precisa de uma conta do Azure. Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.

## <a name="create-a-backup-vault"></a>Criar um cofre de backup
tooback backup de arquivos e pastas de um servidor ou cliente, é necessário toocreate um cofre de backup na região geográfica hello, onde você deseja toostore Olá dados.

> [!IMPORTANT]
> A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
>
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> **15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup. <br/> **A partir de 1º de novembro de 2017**:
>- Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>


## <a name="download-hello-vault-credential-file"></a>Baixe o arquivo de credencial de cofre Olá
máquina local, Olá precisa toobe autenticado com um cofre de backup antes que ele pode fazer backup de dados tooAzure. Olá autenticação é obtida por meio de *Cofre de credenciais*. arquivo de credencial de cofre Olá é baixado por meio de um canal seguro do portal clássico do hello. chave privada do certificado Olá não persistem no portal de saudação ou serviço hello.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload Olá cofre credencial arquivo tooa máquina local
1. No painel de navegação esquerdo hello, clique em **dos serviços de recuperação**e, em seguida, selecione o Cofre de backup Olá que você criou.

    ![IR completo](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Na página início rápido hello, clique em **baixar credenciais do cofre**.

   portal clássico do Hello gera uma credencial de cofre usando uma combinação do nome do cofre hello e hello data atual. o arquivo de credenciais de cofre Olá é usado somente durante o fluxo de trabalho de registro de saudação e expira após 48 horas.

   arquivo de credencial de cofre Olá pode ser baixado do portal de saudação.
3. Clique em **salvar** toodownload Olá cofre credencial arquivo toohello pasta Downloads da conta local hello. Você também pode selecionar **Salvar como** de saudação **salvar** menu toospecify um local para o arquivo de credencial de cofre hello.

   > [!NOTE]
   > Verifique se o arquivo de credencial de cofre Olá é salvo em um local que possa ser acessado em seu computador. Se ele estiver armazenado em um bloco de mensagens de servidor ou compartilhamento de arquivo, verifique se você tem Olá permissões tooaccess-lo.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Baixar, instalar e registrar o agente de Backup Olá
Depois de criar o Cofre de backup hello e arquivo de credencial de cofre download hello, um agente deve ser instalado em cada um de seus computadores Windows.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, instalar e registrar o agente Olá
1. Clique em **dos serviços de recuperação**e, em seguida, selecione o Cofre de backup Olá que você deseja tooregister com um servidor.
2. Na página de início rápido de saudação, clique em agente Olá **agente para Windows Server ou do cliente do System Center Data Protection Manager ou Windows**. Em seguida, clique em **Salvar**.

    ![Salvar agente](./media/backup-configure-vault-classic/agent.png)
3. Depois de saudação MARSagentinstaller.exe arquivo baixado, clique em **executar** (ou clique duas vezes em **MARSAgentInstaller.exe** de local de saudação salvada).
4. Escolha a pasta de instalação de saudação e a pasta de cache que são necessários para o agente de saudação e, em seguida, clique em **próximo**. local de cache de saudação especificado deve ter tooat de espaço livre igual menos 5 por cento Olá dos dados de backup.
5. Você pode continuar tooconnect toohello da Internet por meio de configurações de proxy padrão hello.             Se você usar um toohello de tooconnect do servidor proxy da Internet, na página de configuração de Proxy de saudação, selecione Olá **usar configurações de proxy personalizadas** caixa de seleção e, em seguida, insira detalhes de saudação do servidor de proxy. Se você usar um proxy autenticado, insira os detalhes de nome e senha de usuário hello e, em seguida, clique em **próximo**.
6. Clique em **instalar** toobegin instalação do agente de saudação. Agente de Backup Olá instala o .NET Framework 4.5 e o Windows PowerShell (se ele ainda não estiver instalado) toocomplete instalação de saudação.
7. Depois de saudação agente estiver instalado, clique em **continuar tooRegistration** toocontinue ao fluxo de trabalho de saudação.
8. Na página de identificação de cofre hello, procure tooand Olá selecione cofre arquivo de credenciais que você baixou anteriormente.

    arquivo de credencial de cofre Olá é válido para apenas 48 horas após o download do portal de saudação. Se você encontrar um erro nesta página (como "credenciais de cofre arquivo fornecido expirou"), entrar no portal de toohello e baixar o arquivo de credencial de cofre Olá novamente.

    Certifique-se de que esse arquivo de credencial de cofre hello está disponível em um local que possa ser acessado pelo aplicativo de instalação hello. Se você encontrar erros relacionados a acesso, copie Olá cofre credencial tooa temporário local do arquivo no hello mesmo computador e repita a operação de saudação.

    Se você encontrar um erro de credencial de cofre, como "credenciais de Cofre inválido fornecido", o arquivo hello está danificado ou não ter Olá credenciais mais recentes associadas ao serviço de recuperação de saudação. Repita a operação Olá após o download de um novo arquivo de credencial do cofre no portal de saudação. Esse erro também poderá ocorrer se um usuário clica Olá **credencial do cofre Download** opção várias vezes em sucessão rápida. Nesse caso, somente Olá última cofre credencial arquivo é válido.
9. Na página de configuração de criptografia Olá, você pode gerar uma senha ou forneça uma frase secreta (com um mínimo de 16 caracteres). Lembre-se toosave Olá senha em um local seguro.
10. Clique em **Concluir**. Olá Assistente para registrar servidor registra o servidor de saudação com Backup.

    > [!WARNING]
    > Se você perde ou esquecer a senha hello, Microsoft não pode ajudá-lo a recuperar os dados de backup hello. Você possui Olá senha de criptografia e a Microsoft não tem visibilidade Olá frase secreta que você usa. Salve o arquivo de saudação em um local seguro, pois ela será necessária durante uma operação de recuperação.
    >
    >

11. Após a chave de criptografia de saudação é definida, deixe Olá **iniciar o Microsoft Azure Recovery Services Agent** selecionada de caixa de seleção e, em seguida, clique em **fechar**.

## <a name="complete-hello-initial-backup"></a>Backup inicial completo Olá
backup de saudação inicial inclui duas tarefas principais:

* Criar agenda de backup Olá
* Fazendo backup de arquivos e pastas para Olá primeira vez

Concluída a política de backup Olá backup inicial hello, ele cria pontos de backup que podem ser usados se você precisar toorecover Olá dados. política de backup Olá faz isso com base em agendamento Olá que você definir.

### <a name="tooschedule-hello-backup"></a>backup de saudação tooschedule
1. Abra o agente de Backup do Microsoft Azure hello. (Ela será aberta automaticamente se você deixou Olá **iniciar o Microsoft Azure Recovery Services Agent** caixa de seleção marcada quando você fechou Olá Assistente para registrar servidor.) Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.

    ![Inicie o agente de Backup do Azure Olá](./media/backup-configure-vault-classic/snap-in-search.png)
2. No agente de Backup hello, clique em **agendamento de Backup**.

    ![Agendar um backup do Windows Server](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Em Olá Introdução página do Assistente de agendamento de Backup de saudação, clique em **próximo**.
4. Na página de tooBackup do hello selecionar itens, clique em **adicionar itens**.
5. Selecione Olá arquivos e pastas que você deseja tooback backup e, em seguida, clique em **Okey**.
6. Clique em **Avançar**.
7. Em Olá **especificar agendamento de Backup** especifique Olá **agendamento de backup** e clique em **próximo**.

    Você pode agendar backups diários (com uma taxa máxima de três vezes por dia) ou backups semanais.

    ![Itens para o backup do Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Para obter mais informações sobre como toospecify Olá agendamento de backup, consulte o artigo Olá [tooreplace uso do Azure Backup sua infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Em Olá **Selecionar política de retenção** página, selecione Olá **política de retenção** para cópia de backup de saudação.

    política de retenção de saudação especifica a duração de saudação para o qual Olá backup será armazenado. Em vez de especificar apenas uma "política simples" para todos os pontos de backup, você pode especificar diferentes políticas de retenção com base em quando Olá backup ocorrer. Você pode modificar toomeet de políticas de retenção diária, semanal, mensal e anual Olá suas necessidades.
9. Na página de escolher tipo de Backup inicial de saudação, escolha o tipo de backup inicial hello. Deixe a opção Olá **automaticamente pela rede Olá** selecionado e, em seguida, clique em **próximo**.

    Você pode fazer backup automaticamente pela rede hello, ou você pode fazer backup offline. restante Olá deste artigo descreve o processo de saudação para fazer backup automaticamente. Se você preferir toodo um backup offline, leia o artigo de saudação [Offline fluxo de trabalho de backup no Backup do Azure](backup-azure-backup-import-export.md) para obter informações adicionais.
10. Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.
11. Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.

### <a name="enable-network-throttling-optional"></a>Habilitar a limitação da rede (opcional)
Agente de Backup Olá fornece a limitação de rede. A limitação controles como a largura de banda de rede é usada durante a transferência de dados. Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de Internet. Limitação se aplica a tooback backup e atividades de restauração.

**a limitação de rede tooenable**

1. No agente de Backup hello, clique em **alterar propriedades**.

    ![Alterar Propriedades](./media/backup-configure-vault-classic/change-properties.png)
2. Em Olá **limitação** guia, selecione Olá **habilitar limitação para operações de backup do uso de largura de banda de internet** caixa de seleção.

    ![Limitação de rede](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Depois de habilitar a limitação, especifique Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.

    os valores de largura de banda Olá começam em 512 Kbps por segundo (Kbps) e podem subir too1, 023 megabytes por segundo (MBps). Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são consideradas trabalho dias. Horas fora das horas úteis designadas são consideradas horas não úteis.
4. Clique em **OK**.

### <a name="tooback-up-now"></a>tooback backup agora
1. No agente de Backup hello, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.

    ![Fazer backup do Windows Server agora](./media/backup-configure-vault-classic/backup-now.png)
2. Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello. Em seguida, clique em **Fazer Backup**.
3. Clique em **fechar** tooclose Assistente de saudação. Se você fizer isso, antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.

Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.

![IR completo](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Próximas etapas
* Inscreva-se para obter uma [conta do Azure gratuita](https://azure.microsoft.com/free/).

Para saber mais sobre como fazer backup de VMs ou de outras cargas de trabalho, confira:

* [Fazer backup de VMs IaaS](backup-azure-vms-prepare.md)
* [Fazer backup de cargas de trabalho tooAzure com o Microsoft Azure Backup Server](backup-azure-microsoft-azure-backup.md)
* [Fazer backup de cargas de trabalho tooAzure com o DPM](backup-azure-dpm-introduction.md)
