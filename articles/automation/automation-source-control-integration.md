---
title: "aaaSource integração de controle na automação do Azure | Microsoft Docs"
description: "Este artigo descreve a integração de controle de origem com o GitHub na Automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integração de controle de origem na Automação do Azure
Integração de controle de origem permite tooassociate runbooks em seu repositório de controle de origem automação conta tooa GitHub. Controle de origem permite tooeasily colaborar com sua equipe, controlar alterações e reverter tooearlier versões dos seus runbooks. Por exemplo, o controle de origem permite a você toosync branches diferentes no controle de origem tooyour desenvolvimento, teste ou produção contas de automação, tornando fácil toopromote código que foi testado em sua produção de tooyour do ambiente de desenvolvimento automação conta.

Controle de origem permite toopush código de controle de toosource de automação do Azure ou seus runbooks do controle de origem tooAzure automação de pull. Este artigo descreve como controlar o tooset fonte em seu ambiente de automação do Azure. Vamos começar configurando a automação do Azure tooaccess seu repositório GitHub e percorrer operações diferentes que podem ser feitas usando a integração de controle de origem. 

> [!NOTE]
> O controle de origem dá suporte a efetuar pull e a enviar por push de [Runbooks de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks), bem como de [Runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks). [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks) ainda não têm suporte.<br><br>
> 
> 

Há duas etapas simples tooconfigure necessário fonte controle para sua conta de automação e somente um se você já tiver uma conta GitHub. Eles são:

## <a name="step-1--create-a-github-repository"></a>Etapa 1: Criar um repositório do GitHub
Se você já tiver uma conta do GitHub e um repositório que você deseja toolink tooAzure automação, em seguida, logon tooyour existentes de conta e começar da etapa 2 a seguir. Caso contrário, navegue muito[GitHub](https://github.com/), inscreva-se para uma nova conta e [criar um novo repositório](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Etapa 2: Configurar o controle de origem na Automação do Azure
1. Na folha de conta de automação de saudação em Olá portal do Azure, clique em **defina controle de origem.** 
   
    ![Configurar Controle de Origem](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Olá **controle de origem** folha é aberto, onde você pode configurar os detalhes da conta GitHub. Abaixo está a lista de saudação do tooconfigure de parâmetros:  
   
   | **Parâmetro** | **Descrição** |
   |:--- |:--- |
   | Escolher Origem |Selecione a fonte de saudação. No momento, apenas **GitHub** tem suporte. |
   | Autorização |Clique em Olá **autorizar** repositório GitHub tooyour de acesso do botão toogrant automação do Azure. Se você já estiver conectado tooyour conta do GitHub em uma janela diferente, Olá credenciais de conta são usadas. Após a autorização bem-sucedida, folha Olá mostrará o nome de usuário do GitHub em **autorização propriedade**. |
   | Escolher o repositório |Selecione um repositório GitHub Olá lista de repositórios disponíveis. |
   | Escolher a ramificação |Selecione um branch da lista de saudação de ramificações disponíveis. Olá somente **mestre** ramificação é mostrada se você ainda não criou nenhum ramificações. |
   | Caminho da pasta do runbook |caminho da pasta de runbook Olá Especifica o caminho de saudação no repositório do GitHub Olá da qual você deseja toopush ou receber seu código. Ela deve ser inserida no formato Olá **foldername/subfoldername**. Somente runbooks no caminho da pasta Olá runbook serão sincronizado tooyour conta de automação. Runbooks em subpastas de saudação do caminho de pasta de runbook Olá será **não** serão sincronizadas. Use ** / ** toosync todos Olá runbooks no repositório de saudação. |
3. Por exemplo, se você tiver um repositório chamado **PowerShellScripts** com uma pasta chamada **RootFolder** que contenha uma pasta chamada **SubFolder**. Você pode usar Olá toosync de cadeias de caracteres a seguir em cada nível de pasta:
   
   1. runbooks toosync **repositório**, caminho da pasta de runbook é*/*
   2. runbooks toosync **RootFolder**, caminho da pasta de runbook é */RootFolder*
   3. runbooks toosync **subpasta**, caminho da pasta de runbook é *RootFolder/subpasta*.
4. Depois de configurar os parâmetros de hello, elas são exibidas em Olá **folha defina controle de origem.**  
   
    ![Configurar Folha](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Depois de clicar em OK, a integração do controle do código-fonte estará configurada para a sua conta de automação e deverá ser atualizada com as informações do GitHub. Agora você pode clicar em tooview essa parte todos o controle de origem histórico do trabalho de sincronização.  
   
    ![Valores de Repositório](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Depois de configurar o controle de origem, hello seguintes recursos de automação serão criados na sua conta de automação:  
   Dois [ativos de variável](automation-variables.md) são criados.  
   
   * variável de saudação **Microsoft.Azure.Automation.SourceControl.Connection** contém valores de saudação de cadeia de caracteres de conexão hello, conforme mostrado abaixo.  
     
     | **Parâmetro** | **Valor** |
     |:--- |:--- |
     | Nome |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tipo |Cadeia de caracteres |
     | Valor |{"Branch":\<*Nome da sua ramificação*>,"RunbookFolderPath":\<*Caminho da pasta do runbook*>,"ProviderType":\<*tem um valor 1 para o GitHub*>,"Repository":\<*Nome do seu repositório*>,"Username":\<*O nome do seu usuário no GitHub*>} |

    * variável de saudação **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contém o valor criptografado seguro de saudação do seu OAuthToken.  

    |**Parâmetro**            |**Valor** |
    |:---|:---|
    | Nome  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tipo | Unknown(Encrypted) |
    | Valor | <*OAuthToken Criptografado*> |  

    ![variáveis](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Controle de automação de origem** é adicionado como um tooyour aplicativo autorizado conta do GitHub. aplicativo de hello tooview: home page GitHub, navegue tooyour **perfil** > **configurações** > **aplicativos**. Esse aplicativo permite toosync de automação do Azure que seu tooan do repositório GitHub conta de automação.  

    ![Aplicativo do Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Usando o controle de origem na Automação
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Check-in um runbook a partir do controle de toosource de automação do Azure
Check-in do runbook permite toopush Olá alterações tooa runbook na automação do Azure para o repositório de controle de origem. Abaixo estão as etapas de saudação toocheck em um runbook:

1. De sua Conta de Automação, [crie um novo runbook textual](automation-first-runbook-textual.md) ou [edite um runbook textual existente](automation-edit-textual-runbook.md). Esse runbook pode ser um Fluxo de Trabalho do PowerShell ou um runbook de script do PowerShell.  
2. Depois de editar o runbook, salve-o e clique em **check-in** de saudação **editar** folha.  
   
    ![Botão Check-in](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Check-in de automação do Azure substituirá código Olá que existe atualmente no controle de origem. Olá instrução de linha de comando equivalente Git toocheck-in é **git Adicionar + confirmação git + git por push**  

1. Quando você clica em **check-in**, você receberá uma mensagem de confirmação, clique em Sim toocontinue.  
   
    ![Mensagem de Check-in](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. A entrada inicia Olá runbook de controle do código-fonte: **MicrosoftAzureAutomationAccountToGitHubV1 sincronização**. Esse runbook conecta tooGitHub e envia as alterações do repositório de tooyour de automação do Azure. Olá tooview check-in do histórico do trabalho, volte toohello **integração de controle de origem** guia e clique em tooopen folha de sincronização do repositório de saudação. Essa folha mostra todos os seus trabalhos de controle de origem.  Selecione o trabalho de saudação desejado tooview e clique em detalhes de saudação tooview.  
   
    ![Fazer Check-in de Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Runbooks de controle de origem são runbooks especiais de Automação que você não pode exibir nem editar. Embora eles não apareçam em sua lista de runbooks, você verá os trabalhos de sincronização em sua lista de trabalhos.
   > 
   > 
3. nome de saudação do runbook Olá modificado é enviado como um parâmetro de entrada toohello check-in do runbook. Você pode [exibir detalhes do trabalho Olá](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) expandindo o runbook no **repositório sincronização** folha.  
   
    ![Entrada de Check-in](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Atualize seu repositório GitHub após a conclusão do trabalho Olá tooview alterações de saudação.  Deve haver uma confirmação do seu repositório com uma mensagem de confirmação: **atualizadas *nome do Runbook* na automação do Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Runbooks de sincronização do controle de origem tooAzure automação
botão de sincronização de saudação na folha de sincronização do repositório de saudação permite que você toopull todos Olá runbooks no caminho de pasta de runbook Olá de sua conta de automação de tooyour do repositório. Olá mesmo repositório pode ser sincronizado toomore que uma conta de automação. Abaixo está Olá etapas toosync um runbook:

1. Em Olá conta de automação em que você configura o controle de origem, abra Olá **folha de sincronização de integração/repositório de controle de origem** e clique em **sincronização** , em seguida, você receberá uma confirmação a mensagem, clique em **Sim** toocontinue.  
   
    ![Botão Sincronizar](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Sincronização inicia o runbook Olá: **MicrosoftAzureAutomationAccountFromGitHubV1 sincronização**. Esse runbook conecta tooGitHub e enviar alterações de saudação do seu repositório de tooAzure automação. Você verá um novo trabalho na Olá **repositório sincronização** folha para esta ação. tooview detalhes sobre o trabalho de sincronização de saudação, clique em folha de detalhes de trabalho tooopen hello.  
   
    ![Sincronizar Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Uma sincronização do controle de origem substitui a versão de rascunho Olá Olá runbooks que existem na sua conta de automação para **todos os** runbooks que estão atualmente no controle de origem. Olá Git toosync de instrução de linha de comando equivalente é **pull git**


## <a name="troubleshooting-source-control-problems"></a>Solucionando problemas do controle de origem
Se houver erros com um trabalho de check-in ou sincronização, status do trabalho Olá deve ser suspenso e você pode exibir mais detalhes sobre o erro de saudação na folha de trabalho hello.  Olá **todos os Logs** parte mostrará todos os Olá fluxos PowerShell associados ao trabalho. Isso fornecerá a que você com os detalhes de saudação necessário toohelp corrigir quaisquer problemas com seu check-in ou sincronização. Ele também mostrará Olá sequência de ações que ocorreram durante a sincronização ou verificação-em um runbook.  

![Imagem AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Desconectando o controle de origem
toodisconnect de sua conta do GitHub, abra a folha de sincronização do repositório de saudação e clique em **Disconnect**. Depois de desconectar o controle de origem, runbooks que foram sincronizados anteriormente ainda permanecerá em sua conta de automação, mas folha de sincronização do repositório de saudação não será habilitada.  

  ![Botão Desconectar](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a integração de controle de origem, consulte Olá recursos a seguir:  

* [Automação do Azure: integração de controle do código-fonte na Automação do Azure](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Vote em seu sistema de controle do código-fonte favorito](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Automação do Azure: integrando o controle do código-fonte de runbook usando o Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

