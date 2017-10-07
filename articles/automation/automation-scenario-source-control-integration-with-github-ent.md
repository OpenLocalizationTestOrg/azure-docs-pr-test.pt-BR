---
title: "aaaAzure integração de controle de fonte de automação com GitHub corporativo | Microsoft Docs"
description: "Descreve os detalhes de como Olá integração tooconfigure com GitHub corporativo para controle de origem de runbooks de automação."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Cenário da Automação do Azure - Integração de controle de origem da Automação com o GitHub Enterprise

Automação atualmente oferece suporte à integração de controle de origem, que permite que você tooassociate runbooks em seu repositório de controle de origem automação conta tooa GitHub.  No entanto, os clientes que implantaram o [GitHub corporativo](https://enterprise.github.com/home) toosupport seus DevOps práticas, também deseja toouse-toomanage ciclo de vida de saudação de runbooks que são desenvolvidos tooautomate processos de negócios e gerenciamento de serviços operações.  

Nesse cenário, você tem um computador com Windows em seu data center configurado como um operador de Runbook híbrido com módulos do Azure Resource Manager hello e ferramentas de Git instaladas.  máquina de trabalhador híbrido Olá tem um clone do repositório do Git local hello.  Quando Olá runbook for executado no hybrid worker de hello, Olá Git directory esteja sincronizado e conteúdo do arquivo de runbook Olá é importado para Olá conta de automação.

Este artigo descreve como tooset essa configuração em seu ambiente de automação do Azure. Vamos começar configurando a automação com credenciais de segurança hello, runbooks requerido toosupport neste cenário e implantação de um operador de Runbook híbrido em seus dados center toorun Olá runbooks e acessar seu toosynchronize do repositório GitHub corporativo runbooks com sua conta de automação.  


## <a name="getting-hello-scenario"></a>Obtendo o cenário de saudação

Este cenário consiste em dois runbooks do PowerShell que você pode importar diretamente da saudação [Galeria de Runbook](automation-runbook-gallery.md) Olá portal do Azure ou fazer o download de saudação [Galeria do PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Descrição| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook exporta um certificado de executar como de um tooa hybrid worker de automação conta para que os runbooks no trabalho Olá pode autenticar com o Azure em ordem tooimport runbooks em Olá conta de automação.| 
Sync-LocalGitFolderToAutomationAccount | Sincronizações de runbook Olá pasta local do Git no computador de híbrida hello e importar arquivos de runbook de saudação (ps1) na conta de automação de saudação.|

### <a name="credentials"></a>Credenciais

Credencial | Descrição|
-----------|------------|
GitHRWCredential | Ativo de credencial de você criar toocontain Olá nome do usuário e senha para um usuário com permissões toohello híbrida de trabalho.|

## <a name="installing-and-configuring-this-scenario"></a>Instalando e configurando esse cenário

### <a name="prerequisites"></a>Pré-requisitos

1. Olá sincronização LocalGitFolderToAutomationAccount runbook autentica usando Olá [conta executar como do Azure](automation-sec-configure-azure-runas-account.md). 

2. Um espaço de trabalho do Microsoft Operations Management Suite (OMS) com hello solução de automação do Azure habilitado e configurado também é necessário.  Se você não tem que está associado a saudação automação conta usada tooinstall e configurar esse cenário, ele é criado e configurado para você quando você executar Olá **OnPremiseHybridWorker.ps1 novo** script híbrida Olá trabalho de runbook.        

    > [!NOTE]
    > No momento hello seguintes regiões só oferecem suporte à automação integração com o OMS - **Sudeste da Austrália**, **Leste dos EUA 2**, **Sudeste da Ásia**, e **Oeste Europa**. 

3. Um computador que pode servir como um operador de Runbook híbrido dedicado que hospedará o software do GitHub hello e manter os arquivos de runbook Olá também (*runbook*. ps1) em um diretório de origem no toosynchronize de sistema de arquivo hello entre GitHub e seu Conta de automação.

### <a name="import-and-publish-hello-runbooks"></a>Importar e publicar runbooks Olá

Olá tooimport *RunAsCertificateToHybridWorker de exportação* e *LocalGitFolderToAutomationAccount sincronização* runbooks do hello Galeria de Runbook da sua conta de automação no hello portal do Azure, Siga os procedimentos Olá [importar Runbook da Galeria de Runbook de saudação](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Publica runbooks Olá depois que eles foram importados com êxito para a sua conta de automação.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Implantar e configurar o Hybrid Runbook Worker

Se você não tiver um Hybrid Runbook Worker já implantado em seu data center, você deve revisar os requisitos de saudação e execute as etapas de instalação Olá automatizada usando o procedimento Olá [Azure Automation Hybrid Runbook Workers - automatizar instalar Configuração e](automation-hybrid-runbook-worker.md#automated-deployment).  Quando você instalou com êxito o trabalhador híbrido de saudação em um computador, execute Olá seguindo as etapas toocomplete toosupport sua configuração nesse cenário.

1. Logon de toohello hospedagem Olá Hybrid Runbook Worker função do computador com uma conta que tenha direitos administrativos locais e crie um diretório toohold Olá Git runbook.  Clone Olá Git repositório toohello diretório interno.
2. Se você ainda não tiver uma conta executar como criada ou se desejar toocreate um novo dedicado para essa finalidade, de saudação do portal Azure navegue tooAutomation contas, selecione sua conta de automação e criar um [ativo de credencial](automation-credentials.md) que contém a saudação de nome de usuário e senha para um usuário com permissões toohello híbrida de trabalho.  
3. De sua conta de automação, [Editar runbook Olá](automation-edit-textual-runbook.md)**RunAsCertificateToHybridWorker de exportação** e modificar o valor variável Olá Olá *$Password* com uma forte senha.    Depois de modificar o valor de saudação, clique em **publicar** toohave versão de rascunho Olá Olá runbook publicado. 
5. Iniciar runbook Olá **RunAsCertificateToHybridWorker de exportação**e em hello **iniciar Runbook** folha, na opção Olá **as configurações de execução** Selecione opção Olá **Hybrid Worker** e em Olá lista suspensa Olá selecione grupo do Hybrid worker criado anteriormente para este cenário.  

    Isso exporta um operador de híbrido toohello certificado para que os runbooks no trabalho Olá pode autenticar com o Azure usando a conexão de executar como do hello em ordem toomanage recursos do Azure (em especial para esse cenário - importar runbooks toohello conta de automação).

4. De sua conta de automação, selecione Olá grupo do Hybrid worker criado anteriormente e [especificar uma conta executar como](automation-hrw-run-runbooks.md#runas-account) para o grupo do Hybrid worker hello e escolher o ativo de credencial de Olá você apenas ou já ter criado.  Isso garante que o runbook de sincronização que Olá pode executar comandos do Git. 
5. Iniciar runbook Olá **LocalGitFolderToAutomationAccount de sincronização**, forneça a seguinte Olá necessário valores de parâmetro de entrada e no hello **iniciar Runbook** folha, na opção de saudação **executar configurações de** Selecione opção Olá **Hybrid Worker** e em Olá lista suspensa Olá selecione grupo do Hybrid worker criado anteriormente para este cenário:
    * *ResourceGroup* - Olá nome do seu grupo de recursos associado à sua conta de automação
    * *AutomationAccountName* - Olá nome da sua conta de automação
    * *GitPath* - Olá pasta local ou de arquivo no hello Hybrid Runbook Worker onde Git é configurar toopull últimas alterações em

    Isso será Olá local Git pasta Olá hybrid worker computador de sincronização e depois importe arquivos. ps1 de saudação do toohello diretório de origem Olá conta de automação.

    ![Inicie Sync-LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Exibir detalhes de resumo do trabalho de runbook Olá selecionando-Olá **Runbooks** folha em conta de automação e, em seguida, selecione Olá **trabalhos** lado a lado.  Confirme foi concluída com êxito, selecionando Olá **todos os logs** lado a lado e fluxo de log detalhado Olá revisão.  

## <a name="next-steps"></a>Próximas etapas

-  tooknow mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)
-  Para saber mais sobre o recurso de suporte de script do PowerShell, veja [Native PowerShell script support in Azure Automation (Suporte a scripts nativos do PowerShell na Automação do Azure)](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
