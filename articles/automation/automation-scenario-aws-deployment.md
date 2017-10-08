---
title: "implantação de aaaAutomating de uma VM no Amazon Web Services | Microsoft Docs"
description: "Este artigo demonstra como toouse a criação de uma VM de serviço do Amazon Web tooautomate automação do Azure"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Cenário de Automação do Azure – provisionar uma máquina virtual do AWS
Neste artigo, demonstraremos como você pode aproveitar automação do Azure tooprovision uma máquina virtual em sua assinatura do serviço AWS (Amazon Web) e dê um nome específico – de VM que AWS refere-se tooas "marcação" hello VM.

## <a name="prerequisites"></a>Pré-requisitos
Para fins de saudação deste artigo, você precisa toohave uma conta de automação do Azure e uma assinatura AWS. Para obter mais informações sobre como configurar uma conta da Automação do Azure e configurá-la com suas credenciais de assinatura do AWS, consulte [Configurar a autenticação com a Amazon Web Services](automation-configure-aws-account.md).  Essa conta deve ser criada ou atualizada com suas credenciais de assinatura AWS antes de prosseguir, como podemos fará referência a essa conta nas etapas de saudação abaixo.

## <a name="deploy-amazon-web-services-powershell-module"></a>Implantar Módulo do PowerShell do Amazon Web Services
Nosso VM provisionamento runbook aproveitará Olá AWS PowerShell módulo toodo seu trabalho. Execute Olá etapas tooadd Olá módulo tooyour conta de automação que é configurada com as credenciais de assinatura AWS a seguir.  

1. Abra seu navegador da web e navegue toohello [Galeria do PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) e clique em Olá **implantar botão de automação de tooAzure**.<br><br> ![Importação de módulo de PS do AWS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Você será direcionado toohello página de logon do Azure e depois de autenticar, você será roteado toohello Portal do Azure e apresentada com hello folha a seguir.<br><br> ![Folha Importar Módulo](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Olá selecione grupo de recursos do hello **grupo de recursos** suspensa lista e na folha de parâmetros hello, forneça Olá informações a seguir:
   
   * De saudação **novo ou a conta de automação existente (string)** lista suspensa, selecione **existente**.  
   * Em Olá **nome de conta de automação (string)** caixa, digite nome exato de saudação do hello conta de automação que inclui credenciais Olá para sua assinatura AWS.  Por exemplo, se você tiver criado uma conta dedicada denominada **AWSAutomation**, que é o que você digita na caixa de saudação.
   * Selecione Olá região apropriada da saudação **local da conta de automação** lista suspensa.
4. Quando você concluiu a inserção de informações Olá necessárias, clique em **criar**.
   
   > [!NOTE]
   > Ao importar um módulo do PowerShell para automação do Azure, ele também extrai Olá cmdlets e essas atividades não aparecerá até que o módulo Olá completamente terminou de importar e extrair Olá cmdlets. Esse processo pode levar alguns minutos.  
   > <br>
   > 
   > 
5. No Portal do Azure do hello, abra sua conta de automação referenciada na etapa 3.
6. Clique em Olá **ativos** lado a lado e Olá **ativos** folha, selecione Olá **módulos** lado a lado.
7. Em Olá **módulos** folha, você verá Olá **AWSPowerShell** módulo na lista de saudação.

## <a name="create-aws-deploy-vm-runbook"></a>Criar runbook de implantação de VM no AWS
Uma vez Olá que AWS módulo do PowerShell foi implantado, agora pode criar um tooautomate runbook provisionar uma máquina virtual em AWS usando um script do PowerShell. etapas de saudação abaixo demonstrará como tooleverage nativo script do PowerShell na automação do Azure.  

> [!NOTE]
> Para obter mais opções e informações sobre esse script, visite Olá [Galeria do PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Fazer o download de script do PowerShell New-AwsVM Olá Olá Galeria do PowerShell abrindo uma sessão do PowerShell e digitando o seguinte hello:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. De Olá Portal do Azure, abra sua conta de automação e clique em Olá **Runbooks** lado a lado.  
3. De saudação **Runbooks** folha, selecione **adicionar um runbook**.
4. Em Olá **adicionar um runbook** folha, selecione **criação rápida** (criar um novo runbook).
5. Em Olá **Runbook** folha de propriedades, digite um nome na caixa de nome de saudação para seu runbook e de saudação **tipo de Runbook** lista suspensa, selecione **PowerShell**e, em seguida, clique em  **Criar**.<br><br> ![Folha Importar Módulo](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Quando for exibida a folha de editar Runbook do PowerShell de saudação, copie e cole o script do PowerShell Olá em tela de criação de runbook de saudação.<br><br> ![Script do PowerShell de Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Observe o seguinte Olá ao trabalhar com o exemplo hello script do PowerShell:
    > 
    > * Olá runbook contém um número de valores de parâmetro padrão. Avalie todos os valores padrão e atualize-os conforme necessário.
    > * Se você armazenou suas credenciais AWS como um ativo de credencial nomes diferentes que **AWScred**, você precisará tooupdate script hello linha 57 toomatch adequadamente.  
    > * Ao trabalhar com hello comandos AWS CLI no PowerShell, especialmente com este exemplo de runbook, você deve especificar a região AWS Olá. Caso contrário, os cmdlets Olá falhará.  Tópico do modo de exibição AWS [especificar AWS região](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) em hello AWS ferramentas para documento de PowerShell para obter mais detalhes.  
    >

7. tooretrieve uma lista de nomes de imagem de sua assinatura AWS, inicie o PowerShell ISE e importe Olá AWS módulo do PowerShell.  Autentique no AWS substituindo **Get-AutomationPSCredential** em seu ambiente do ISE por **AWScred = Get-Credential**.  Solicitará suas credenciais e você pode fornecer sua **ID da chave de acesso** Olá nome de usuário e **chave de acesso do segredo** senha hello.  Consulte o exemplo hello abaixo:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Olá saída a seguir será retornada:<br><br>
   ![Obter imagens do AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Copie e cole Olá um dos nomes de imagem de saudação em uma variável de automação referenciado no runbook hello como **$InstanceType**. Como neste exemplo, estamos usando Olá AWS livre hierárquico de assinatura, vamos usar **t2.micro** para nosso exemplo de runbook.  
9. Salvar Olá runbook e clique em **publicar** toopublish Olá runbook e, em seguida, **Sim** quando solicitado.

### <a name="testing-hello-aws-vm-runbook"></a>Olá runbook AWS VM de teste
Antes de continuar com o runbook de teste Olá, é preciso tooverify algumas coisas. Especificamente:  

* Foi criado um ativo para autenticação em AWS chamado **AWScred** ou script hello foi atualizada tooreference nome de saudação do seu ativo de credencial.    
* módulo de PowerShell AWS Olá tenha sido importado na automação do Azure  
* Foi criado um novo runbook e valores de parâmetro foram verificados e atualizados conforme necessário  
* **Registros detalhados de log** e, opcionalmente, **registros de progresso de Log** em configuração de runbook Olá **registro em log e rastreamento** definiu muito**em**.<br><br> ![Log e rastreamento de Runbook](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Podemos ser toostart Olá runbook, clique em **iniciar** e, em seguida, clique em **Okey** quando abre a folha de iniciar Runbook hello.
2. Na folha de iniciar Runbook hello, forneça um **VMname**.  Aceite valores padrão Olá Olá outros parâmetros que pré-configurado no script hello anteriormente.  Clique em **Okey** trabalho de runbook toostart hello.<br><br> ![Iniciar runbook New-AwsVM](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Um painel de trabalho é aberto para o trabalho de runbook Olá que acabou de criar. Feche esse painel.
4. Podemos pode exibir o progresso de saída de trabalho e modo de exibição de saudação **fluxos** selecionando Olá **todos os Logs** bloco de folha de trabalho de runbook hello.<br><br> ![Saída de fluxo](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. Olá tooconfirm VM está sendo provisionada, faça logon no hello AWS Console de gerenciamento se você não estiver conectado no momento.<br><br> ![VM implantada por console do AWS](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* tooknow mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)
* Para saber mais sobre o recurso de suporte de script do PowerShell, veja [Native PowerShell script support in Azure Automation (Suporte a scripts nativos do PowerShell na Automação do Azure)](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

