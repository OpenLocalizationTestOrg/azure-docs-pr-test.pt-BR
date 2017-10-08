---
title: "aaaIntegrate automação do Azure com o controle de origem do Visual Studio Team Services | Microsoft Docs"
description: "O cenário guia você pela configuração de integração com uma conta de Automação do Azure e o controle do código-fonte do Visual Studio Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "Azure PowerShell, VSTS, controle do código-fonte, automação"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Cenário da Automação do Azure – Integração de controle do código-fonte da Automação com o Visual Studio Team Services

Nesse cenário, você tem um projeto do Visual Studio Team Services que você está usando toomanage runbooks de automação do Azure ou as configurações de DSC sob controle de origem.
Este artigo descreve como toointegrate VSTS com seu ambiente de automação do Azure para que a integração contínua ocorre para cada check-in.

## <a name="getting-hello-scenario"></a>Obtendo o cenário de saudação

Este cenário consiste em dois runbooks do PowerShell que você pode importar diretamente da saudação [Galeria de Runbook](automation-runbook-gallery.md) Olá portal do Azure ou fazer o download de saudação [Galeria do PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Descrição| 
--------|------------|
Sync-VSTS | Importar runbooks ou configurações do controle do código-fonte do VSTS quando é feito um check-in. Se executar manualmente, importar e publicar todos os runbooks ou configurações em Olá conta de automação.| 
Sync-VSTSGit | Importar runbooks ou configurações do controle do código-fonte do VSTS sob o Git quando é feito um check-in. Se executar manualmente, importar e publicar todos os runbooks ou configurações em Olá conta de automação.|

### <a name="variables"></a>variáveis

Variável | Descrição|
-----------|------------|
VSToken | Proteger o ativo de variável, você criará que contém o token de acesso pessoal do VSTS hello. Você pode aprender como toocreate um personal VSTS acessar token em Olá [página de autenticação do VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Instalando e configurando esse cenário

Criar um [token de acesso pessoal](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) no VSTS que você usará toosync Olá runbooks ou configurações em sua conta de automação.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Criar um [variável secure](automation-variables.md) em sua saudação de toohold de conta de automação de acesso pessoal token para que Olá runbook possa autenticar tooVSTS e sincronização runbooks de saudação ou configurações em Olá conta de automação. Você pode nomear esse VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importe runbook Olá que sincronizará seus runbooks ou configurações para a conta de automação de saudação. Você pode usar o hello [runbook de exemplo do VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) ou hello [VSTS com exemplo de runbook Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) do hello PowerShellGallery.com dependendo se você usar VSTS VSTS com Git ou controle de origem e implante tooyour conta de automação.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Agora você pode [publicar](automation-creating-importing-runbook.md#publishing-a-runbook) esse runbook para que você possa criar um webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Criar um [webhook](automation-webhooks.md) para este runbook VSTS de sincronização e o preenchimento nos parâmetros de saudação conforme mostrado abaixo. Certifique-se de que copiar a url do webhook Olá pois você precisará de um gancho de serviço no VSTS. Olá VSAccessTokenVariableName é o nome de saudação (VSToken) da variável de seguro Olá que você criou o token de acesso pessoal de saudação toohold anterior. 

Integrando VSTS (sincronização VSTS.ps1) terão Olá parâmetros a seguir.
### <a name="sync-vsts-parameters"></a>Parâmetros do Sync-VSTS

Parâmetro | Descrição| 
--------|------------|
WebhookData | Isso conterá informações de check-in de saudação enviadas de gancho de serviço do VSTS hello. Você deve deixar esse parâmetro em branco.| 
ResourceGroup | Este é o nome de saudação do grupo de recursos de Olá Olá automação conta está no.|
AutomationAccountName | nome de Olá Olá da conta de automação que sincronizará com VSTS.|
VSFolder | O nome da pasta Olá no VSTS onde Olá runbooks e as configurações existem.|
VSAccount | nome de saudação do hello conta do Visual Studio Team Services.| 
VSAccessTokenVariableName | nome de Olá da saudação seguro variável (VSToken) que contém o token de acesso pessoal do VSTS Olá.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Se você estiver usando o VSTS com o GIT (sincronização VSTSGit.ps1) levará Olá parâmetros a seguir.

Parâmetro | Descrição|
--------|------------|
WebhookData | Isso conterá informações de check-in de saudação enviadas de gancho de serviço do VSTS hello. Você deve deixar esse parâmetro em branco.| ResourceGroup | Esse nome de saudação do grupo de recursos Olá Olá conta de automação está em.|
AutomationAccountName | nome de Olá Olá da conta de automação que sincronizará com VSTS.|
VSAccount | nome de saudação do hello conta do Visual Studio Team Services.|
VSProject | nome de saudação do projeto de saudação no VSTS onde Olá runbooks e as configurações existem.|
GitRepo | nome de saudação do repositório do Git de saudação.|
GitBranch | nome de saudação do branch Olá no repositório do Git do VSTS.|
Pasta | nome de saudação da pasta de saudação na ramificação do VSTS Git.|
VSAccessTokenVariableName | nome de Olá da saudação seguro variável (VSToken) que contém o token de acesso pessoal do VSTS Olá.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Crie um gancho de serviço no VSTS para pasta de toohello check-ins que dispara esse webhook no check-in do código. Selecione ganchos Web como Olá serviço toointegrate com quando você cria uma nova assinatura. Você pode aprender mais sobre os ganchos de serviço na [documentação de ganchos de serviço do VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Você deve agora ser capaz de toodo todos os check-ins de seus runbooks e configurações no VSTS e ter um automaticamente sincronizar em sua conta de automação.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Se você executar esse runbook manualmente sem sendo disparada pelo VSTS, você pode deixar o parâmetro de webhookdata hello vazio e fará uma sincronização completa da pasta do VSTS Olá especificada.

Se desejar que o cenário de saudação toouninstall, remover gancho do serviço de saudação do VSTS, exclua o runbook hello e Olá VSToken variável.
