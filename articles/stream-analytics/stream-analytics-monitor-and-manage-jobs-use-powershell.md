---
title: aaaMonitor e gerenciar trabalhos do Stream Analytics com o PowerShell | Microsoft Docs
description: Saiba como toouse toomonitor de PowerShell do Azure e cmdlets e gerenciar trabalhos do Stream Analytics.
keywords: azure powershell, cmdlets do azure powershell, comando do powershell, scripts do powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Monitorar e gerenciar trabalhos do Stream Analytics usando cmdlets do Azure PowerShell
Saiba como toomonitor e gerenciar recursos de análise de fluxo com cmdlets do PowerShell do Azure e o script do powershell que execute tarefas básicas de análise de fluxo.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Pré-requisitos para a execução de cmdlets do PowerShell do Azure para Stream Analytics
* Crie um grupo de recursos do Azure em sua assinatura. a seguir Olá é um exemplo de script do PowerShell do Azure. Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Os trabalhos do Stream Analytics criados programaticamente não têm monitoramento habilitado por padrão.  Você pode habilitar manualmente o monitoramento no hello Portal do Azure navegando página Monitor de toohello do trabalho e clicar o botão de habilitar hello, ou você pode fazer isso programaticamente, seguindo os passos de saudação localizados em [Stream Analytics do Azure - fluxo de Monitor Trabalhos de análise de maneira programática](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Cmdlets do PowerShell do Azure para Stream Analytics
Olá cmdlets do Azure PowerShell a seguir pode ser usado toomonitor e gerenciar trabalhos do Stream Analytics do Azure. Observe que o Azure PowerShell tem diferentes versões. 
**Exemplos de Olá Olá listados primeiro comando é para o Azure PowerShell 0.9.8, Olá segundo comando é para o Azure PowerShell 1.0.** comandos de saudação do Azure PowerShell 1.0 sempre terá "AzureRM" no comando hello.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Lista todos os trabalhos de análise de fluxo definidos em Olá assinatura do Azure ou o grupo de recursos especificado, ou obtém informações sobre um trabalho específico dentro de um grupo de recursos de trabalho.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Este comando do PowerShell retorna informações sobre todos os trabalhos do Stream Analytics Olá no hello assinatura do Azure.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Este comando do PowerShell retorna informações sobre todos os trabalhos do Stream Analytics Olá no grupo de recursos de saudação StreamAnalytics-padrão-Centro dos EUA.

**Exemplo 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Este comando do PowerShell retorna informações sobre o trabalho de análise de fluxo de saudação StreamingJob no grupo de recursos de saudação StreamAnalytics-padrão-Centro dos EUA.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Lista todas as entradas de saudação que são definidas em um trabalho de análise de fluxo especificado ou obtém informações sobre uma entrada específica.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando do PowerShell retorna informações sobre todas as entradas de saudação definido no trabalho Olá StreamingJob.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Este comando do PowerShell retorna informações sobre entrada hello denominada EntryStream definido no trabalho Olá StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Lista todas as saídas de saudação que são definidas em um trabalho de análise de fluxo especificado ou obtém informações sobre uma saída específica.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando do PowerShell retorna informações sobre saídas de saudação definidas no trabalho Olá StreamingJob.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Este comando do PowerShell retorna informações sobre a saída Olá chamada de saída definida no trabalho Olá StreamingJob.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Obtém informações sobre cota de saudação do streaming unidades em uma região especificada.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Este comando do PowerShell retorna informações sobre cota de saudação e o uso de unidades de streaming na região do hello centro dos EUA.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Obtém informações sobre uma transformação específica definida no trabalho de Stream Analytics.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Este comando do PowerShell retorna informações sobre transformação Olá chamada StreamingJob no trabalho Olá StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Cria uma nova entrada dentro do trabalho do Stream Analytics ou atualiza uma entrada existente especificada.

Olá nome de entrada hello pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação. Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.

Se você especificar uma entrada que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá entrada existente.

Se você especificar hello – o parâmetro Force e especifique uma existente de nome de entrada, entrada hello será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar entrada (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] seção Olá [API de REST de gerenciamento de análise de fluxo Biblioteca de referência][stream.analytics.rest.api.reference].

**Exemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Este comando do PowerShell cria uma nova entrada de arquivo hello Input.json. Se uma entrada existente com o nome de saudação especificado no arquivo de definição de entrada hello já estiver definida, Olá cmdlet perguntará se ou não tooreplace-lo.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Este comando do PowerShell cria uma nova entrada no trabalho Olá chamado EntryStream. Se uma entrada existente com esse nome já está definida, Olá cmdlet perguntará se ou não tooreplace-lo.

**Exemplo 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Esse comando do PowerShell substitui a definição Olá Olá existente da fonte de entrada chamado EntryStream com definição de saudação do arquivo hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Cria um novo trabalho do Stream Analytics no Microsoft Azure ou atualiza a definição de saudação do trabalho especificado existente.

nome de saudação do trabalho Olá pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação. Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.

Se você especificar um nome de trabalho que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá trabalho existente.

Se você especificar hello – o parâmetro Force e especifique um nome de trabalho existente, definição de trabalho Olá será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar o trabalho do Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] seção Olá [referência de API de REST de gerenciamento de análise de fluxo Biblioteca][stream.analytics.rest.api.reference].

**Exemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Este comando do PowerShell cria um novo trabalho de definição de saudação em JobDefinition.json. Se um trabalho existente com o nome hello especificada no arquivo de definição de trabalho Olá já estiver definido, Olá cmdlet perguntará se ou não tooreplace-lo.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Este comando do PowerShell substitui a definição de trabalho Olá para StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Cria uma nova saída dentro de um trabalho de Stream Analytics ou atualiza uma saída existente.  

nome de saudação da saída de hello pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação. Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.

Se você especificar uma saída que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá saída existente.

Se você especificar hello – o parâmetro Force e especifique o nome de saída existente, saída de hello será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar saída (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] seção Olá [API de REST de gerenciamento de análise de fluxo Biblioteca de referência][stream.analytics.rest.api.reference].

**Exemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Este comando do PowerShell cria uma nova saída chamada "saída" trabalho Olá StreamingJob. Se uma saída existente com esse nome já está definida, Olá cmdlet perguntará se ou não tooreplace-lo.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Este comando do PowerShell substitui a definição de saudação de "saída" no trabalho Olá StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
Cria uma nova transformação dentro de um trabalho do Stream Analytics ou atualiza a transformação de saudação existente.

nome de saudação da transformação Olá pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação. Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.

Se você especificar uma transformação que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá transformação existente.

Se você especificar hello – o parâmetro Force e especifique um nome de transformação existente, transformação Olá será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar transformação (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] seção Olá [gerenciamento de análise de fluxo Biblioteca de referência de API REST][stream.analytics.rest.api.reference].

**Exemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Este comando do PowerShell cria uma nova transformação chamada StreamingJobTransform no trabalho Olá StreamingJob. Se uma transformação existente já está definida com esse nome, Olá cmdlet perguntará se ou não tooreplace-lo.

**Exemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Este comando do PowerShell substitui a definição de saudação do StreamingJobTransform trabalho Olá StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Exclui de maneira assíncrona uma entrada específica de um trabalho do Stream Analytics no Microsoft Azure.  
Se você especificar hello – parâmetro Force, Olá de entrada será excluído sem confirmação.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Esse comando do PowerShell remove Olá entrada EventStream trabalho Olá StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Exclui de maneira assíncrona um trabalho específico do Stream Analytics no Microsoft Azure.  
Se você especificar hello – o parâmetro Force, Olá trabalho será excluída sem confirmação.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando do PowerShell remove o trabalho de saudação StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Exclui de maneira assíncrona uma saída específica de um trabalho do Stream Analytics no Microsoft Azure.  
Se você especificar hello – o parâmetro Force, Olá saída será excluída sem confirmação.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Essa saudação do PowerShell comando remove saída saída no trabalho Olá StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Implanta de maneira assíncrona e inicia um trabalho do Stream Analytics no Microsoft Azure.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Esse comando do PowerShell inicia Olá trabalho StreamingJob com uma hora de início de saída personalizado definido tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Interrompe de maneira assíncrona um trabalho do Stream Analytics para que não seja executado no Microsoft Azure e desaloca os recursos que estavam sendo usados. Olá metadados e definição de trabalho permanecerão disponíveis dentro de sua assinatura por meio de saudação portal do Azure e APIs de gerenciamento, que hello trabalho pode ser editado e reiniciado. Você não será cobrado por um trabalho no estado de saudação interrompido.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando do PowerShell para o trabalho de saudação StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Capacidade de saudação de testes de análise de fluxo tooconnect tooa especificado de entrada.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Esse status de conexão do PowerShell comando testes Olá de saudação EntryStream no StreamingJob de entrada.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Capacidade de saudação de testes de análise de fluxo tooconnect tooa especificado de saída.

**Exemplo 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Esse status de conexão do PowerShell comando testes Olá de saudação saída saída em StreamingJob.  

## <a name="get-support"></a>Obtenha suporte
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

