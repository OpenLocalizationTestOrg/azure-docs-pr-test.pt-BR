---
title: "aaaCollecting dados de análise de Log com um runbook na automação do Azure | Microsoft Docs"
description: "Tutorial passo a passo que explica como criar um runbook em dados de toocollect de automação do Azure no repositório do OMS Olá para análise pela análise de Log."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Coletar dados no Log Analytics com um runbook na Automação do Azure
Você pode coletar uma quantidade significativa de dados no Log Analytics de uma variedade de fontes, inclusive [fontes de dados](../log-analytics/log-analytics-data-sources.md) nos agentes e também os [dados coletados do Azure](../log-analytics/log-analytics-azure-storage.md).  Há um cenários que onde você precisa toocollect dados que não está acessível por meio dessas fontes padrão.  Nesses casos, você pode usar o hello [API do coletor de dados de HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite dados tooLog análise de qualquer cliente de API REST.  Um tooperform método comuns coleta de dados está usando um runbook na automação do Azure.   

Este tutorial orienta pelo processo de saudação para criar e agendar um runbook na automação do Azure toowrite dados tooLog análise.


## <a name="prerequisites"></a>Pré-requisitos
Esse cenário requer Olá seguindo os recursos configurados em sua assinatura do Azure.  Ambos podem ser uma conta gratuita.

- [Espaço de trabalho do Log Analytics](../log-analytics/log-analytics-get-started.md).
- [Conta de automação do Azure](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Visão geral do cenário
Para este tutorial, você escreverá um runbook que coleta informações sobre trabalhos de Automação.  Runbooks na automação do Azure são implementados com o PowerShell, portanto, comece por escrever e testar um script no editor de automação do Azure hello.  Depois de confirmar que você está coletando informações de saudação necessárias, você gravar que tooLog dados análise e verifique se o tipo de dados personalizado hello.  Por fim, você criará um runbook de saudação do agendamento toostart em intervalos regulares.

> [!NOTE]
> Você pode configurar a automação do Azure toosend trabalho informações tooLog análise sem este runbook.  Este cenário é principalmente tutorial de saudação toosupport usado e é recomendável que você envie o espaço de trabalho de teste do hello dados tooa.  


## <a name="1-install-data-collector-api-module"></a>1. Instalar o módulo de API do Coletor de Dados
Cada [solicitação de saudação API de coletor de dados HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) devem ser formatados adequadamente e incluir um cabeçalho de autorização.  Você pode fazer isso no seu runbook, mas você pode reduzir a quantidade de saudação do código necessário usando um módulo que simplifica esse processo.  É um módulo que você pode usar [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) no hello Galeria do PowerShell.

toouse um [módulo](../automation/automation-integration-modules.md) em um runbook, ele deve ser instalado em sua conta de automação.  Qualquer runbook no Olá a mesma conta pode usar Olá funções no módulo hello.  Você pode instalar um novo módulo selecionando **Ativos** > **Módulos** > **Adicionar um módulo** na sua conta de Automação.  

Olá Galeria do PowerShell que lhe toodeploy uma opção rapidamente um módulo diretamente a conta de automação tooyour, portanto você pode usar essa opção para este tutorial.  

![Módulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Vá muito[Galeria do PowerShell](https://www.powershellgallery.com/).
2. Procure **OMSIngestionAPI**.
3. Clique em Olá **implantar tooAzure automação** botão.
4. Selecione sua conta de automação e clique em **Okey** tooinstall módulo de saudação.


## <a name="2-create-automation-variables"></a>2. Criar variáveis de Automação
As [variáveis de Automação](..\automation\automation-variables.md) contêm valores que podem ser usados por todos os runbooks na sua conta de Automação.  Eles tornarem runbooks mais flexível, permitindo que você toochange esses valores sem editar Olá runbook real. Todas as solicitações de saudação API do coletor de dados de HTTP requer Olá ID e a chave do espaço de trabalho do OMS hello e ativos de variável são toostore ideal essas informações.  

![variáveis](media/operations-management-suite-runbook-datacollect/variables.png)

1. No portal do Azure de Olá, navegue tooyour conta de automação.
2. Selecione **Variáveis** em **Recursos Compartilhados**.
2. Clique em **adicionar uma variável** e criar hello duas variáveis no Olá a tabela a seguir.

| Propriedade | Valor da ID do Espaço de Trabalho | Valor da Chave do Espaço de Trabalho |
|:--|:--|:--|
| Nome | WorkspaceId | WorkspaceKey |
| Tipo | Cadeia de caracteres | Cadeia de caracteres |
| Valor | Cole Olá ID do espaço de trabalho do seu espaço de trabalho de análise de Log. | Colar com hello primário ou secundário chave de seu espaço de trabalho de análise de Log. |
| Criptografado | Não | Sim |



## <a name="3-create-runbook"></a>3. Criar runbook

Automação do Azure tem um editor no portal de saudação onde você pode editar e testar seu runbook.  Você tem Olá opção toouse Olá script editor toowork com [PowerShell diretamente](../automation/automation-edit-textual-runbook.md) ou [criar um runbook gráfico](../automation/automation-graphical-authoring-intro.md).  Para este tutorial, você trabalhará com um script do PowerShell. 

![Editar runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Navegue tooyour conta de automação.  
2. Clique em **Runbooks** > **Adicionar um runbook** > **Criar um novo runbook**.
3. Nome de runbook hello, digite **trabalhos de automação de coletar**.  Para o tipo de runbook hello, selecione **PowerShell**.
4. Clique em **criar** toocreate Olá runbook e início saudação do editor.
5. Copie e cole a saudação de código a seguir no runbook hello.  Consulte toohello comentários no script hello explicação do código de saudação.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Runbook de teste
Automação do Azure inclui um ambiente muito[testar seu runbook](../automation/automation-testing-runbook.md) antes de publicá-lo.  Você pode inspecionar dados Olá coletados pelo runbook hello e verificar que ele grava tooLog análise conforme o esperado antes de publicá-la tooproduction. 
 
![Runbook de teste](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Clique em **salvar** toosave Olá runbook.
1. Clique em **painel teste** tooopen Olá runbook no ambiente de teste de saudação.
3. Desde que o runbook tiver parâmetros, você está tooenter solicitadas valores para eles.  Digite nome Olá Olá do grupo de recursos e automação Olá que seu andamento toocollect trabalho informações de conta.
4. Clique em **iniciar** toohello iniciar runbook hello.
3. Olá runbook iniciará com um status de **em fila** antes que ele fique muito**executando**.  
3. Olá runbook deve exibir a saída detalhada com trabalhos Olá coletados no formato json.  Se nenhum trabalho estiver listado, em seguida, não pode ter havido nenhuma trabalhos criados na conta de automação de saudação em Olá última hora.  Tente iniciar qualquer runbook na conta de automação hello e execute novamente o teste de saudação.
4. Certifique-se de que o saída Olá não mostra que erros Olá lançar tooLog comando análise.  Você deve ter uma mensagem semelhante toohello a seguir.

    ![Saída de postagem](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Verificar registros no Log Analytics
Depois de runbook Olá foi concluída no teste e verificar a saída de hello foi recebida com êxito, você pode verificar se os registros de saudação foram criados usando um [pesquisa de log de análise de Log](../log-analytics/log-analytics-log-searches.md).

![Saída de log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. No portal do Azure de Olá, selecione seu espaço de trabalho de análise de Log.
2. Clique em **Pesquisa de Logs**.
3. Saudação de tipo comando a seguir `Type=AutomationJob_CL` e clique em botão de pesquisa de saudação. Observe que o tipo de registro de saudação inclui _CL que não está especificado no script hello.  Esse sufixo é acrescentada automaticamente toohello log tipo tooindicate que é um tipo de log personalizado.
4. Você deve ver um ou mais registros retornados indicando que esse runbook hello está funcionando conforme o esperado.


## <a name="6-publish-hello-runbook"></a>6. Publicar o runbook Olá
Depois de ter verificado que Olá runbook está funcionando corretamente, é necessário toopublish isso, você pode executá-lo em produção.  Você pode continuar tooedit e testar o runbook Olá sem modificar a versão publicada hello.  

![Publicar runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Retorne tooyour conta de automação.
2. Clique em **Runbooks** e selecione **Collect-Automation-jobs**.
3. Clique em **Editar** e **Publicar**.
4. Clique em **Sim** quando tooverify frequentes que você deseja toooverwrite Olá anteriormente publicada versão.

## <a name="7-set-logging-options"></a>7. Definir opções de log 
Para teste, você fosse capaz de tooview [saída detalhada](../automation/automation-runbook-output-and-messages.md#message-streams) porque você definir a variável de saudação $VerbosePreference no script hello.  Para a produção, você precisa propriedades de log de saudação do tooset do runbook Olá se desejar que a saída detalhada tooview.  Para o runbook Olá usado neste tutorial, será exibido envio tooLog análise de dados json hello.

![Log e rastreamento](media/operations-management-suite-runbook-datacollect/logging.png)

1. Nas propriedades de saudação do seu runbook selecione **registro em log e rastreamento** em **as configurações de Runbook**.
2. Alterar configuração Olá **registros detalhados de Log** muito**em**.
3. Clique em **Salvar**.

## <a name="8-schedule-runbook"></a>8. Agendar runbook
Olá, toostart de maneira mais comum um runbook que coleta dados de monitoramento é tooschedule-toorun automaticamente.  Você pode fazer isso criando um [agenda na automação do Azure](../automation/automation-schedules.md) e anexá-lo tooyour runbook.

![Agendar runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Nas propriedades de saudação do seu runbook, selecione **agendas** em **recursos**.
2. Clique em **adicionar uma agenda** > **vincula um runbook do agendamento tooyour** > **criar uma nova agenda**.
5. Tipo de saudação seguintes valores para o agendamento de saudação e clique em **criar**.

| Propriedade | Valor |
|:--|:--|
| Nome | AutomationJobs-Hourly |
| Inicia | Selecione a qualquer momento pelo menos 5 minutos anterior Olá hora atual. |
| Recorrência | Recorrente |
| Repetir a cada | 1 hora |
| Definir a validade | Não |

Após Olá cronograma é criado, você precisará tooset valores de parâmetro de saudação que serão usados toda vez que essa agenda inicia o runbook de saudação.

6. Clique em **Configurar parâmetros e configurações de execução**.
7. Preencha os valores para **ResourceGroupName** e **AutomationAccountName**.
8. Clique em **OK**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Verificar se o runbook é iniciado no agendamento
Toda vez que um runbook é iniciado, [um trabalho é criado](../automation/automation-runbook-execution.md) e qualquer saída é registrada.  Na verdade, esses são Olá mesmo trabalhos Olá runbook está coletando.  Você pode verificar que esse runbook Olá iniciado como esperado por verificações trabalhos Olá Olá runbook após a hora de início de saudação de agenda Olá passou.

![Trabalhos](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Nas propriedades de saudação do seu runbook, selecione **trabalhos** em **recursos**.
2. Você deve ver que uma lista de trabalhos para cada runbook de saudação do tempo foi iniciada.
3. Clique em uma saudação trabalhos tooview seus detalhes.
4. Clique em **todos os logs** tooview Olá logs e saída de runbook hello.
5. Role toohello inferior toofind uma entrada semelhante toohello imagem a seguir.<br>![Detalhado](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Clique nesta entrada hello tooview json dados detalhados que foi enviados tooLog análise.



## <a name="next-steps"></a>Próximas etapas
- Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate exibir um modo de exibição Olá dados que você coletou toohello repositório de análise de Log.
- Empacotar seu runbook em um [solução de gerenciamento de](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Saiba mais sobre o [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).
- Saiba mais sobre a [Automação do Azure](https://docs.microsoft.com/azure/automation/).
- Saiba mais sobre Olá [API do coletor de dados de HTTP](../log-analytics/log-analytics-data-collector-api.md).
