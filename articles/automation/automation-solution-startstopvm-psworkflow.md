---
title: "Iniciando e parando máquinas virtuais com a Automação do Azure - Fluxo de Trabalho do PowerShell | Microsoft Docs"
description: "Versão gráfica do cenário da Automação do Azure, incluindo runbooks para iniciar e parar máquinas virtuais clássicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Cenário de Automação do Azure — iniciando e parando máquinas virtuais
Esse cenário de Automação do Azure inclui runbooks para iniciar e parar máquinas virtuais clássicas.  Você pode usar esse cenário para qualquer um destes objetivos:  

* Usar os runbooks sem modificação em seu próprio ambiente.
* Modificar os runbooks para executar funcionalidade personalizada.  
* Chamar os runbooks de outro runbook como parte de uma solução geral.
* Usar os runbooks como tutoriais para saber sobre os conceitos de criação do runbook.

> [!div class="op_single_selector"]
> * [Gráfico](automation-solution-startstopvm-graphical.md)
> * [Fluxo de Trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

Esta é a versão de runbook do Fluxo de Trabalho do PowerShell desse cenário. Ela também é disponibilizada usando [runbooks gráficos](automation-solution-startstopvm-graphical.md).

## <a name="getting-the-scenario"></a>Obtendo o cenário
Esse cenário é formado por dois runbooks de Fluxo de Trabalho do PowerShell, que você pode baixar dos links a seguir.  Confira a [versão gráfica](automation-solution-startstopvm-graphical.md) deste cenário para obter os links para os runbooks gráficos.

| Runbook | Link | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Iniciar VMs clássicas do Azure](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Fluxo de Trabalho do PowerShell |Inicia todas as máquinas virtuais clássicas em uma assinatura do Azure ou em todas as máquinas virtuais com um nome de serviço específico. |
| Stop-AzureVMs |[Parar VMs clássicas do Azure](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Fluxo de Trabalho do PowerShell |Para todas as máquinas virtuais em uma conta de automação ou todas as máquinas virtuais com um nome de serviço específico. |

## <a name="installing-and-configuring-the-scenario"></a>Instalando e configurando o cenário
### <a name="1-install-the-runbooks"></a>1. Instalar os runbooks
Depois de baixar os runbooks, você poderá importá-los usando o procedimento em [Importando um runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-the-description-and-requirements"></a>2. Analisar a descrição e os requisitos
Os runbooks incluem um texto de ajuda comentado que apresenta uma descrição e os ativos necessários.  Também é possível obter as mesmas informações neste artigo.

### <a name="3-configure-assets"></a>3. Configurar ativos
Os runbooks exigem os ativos a seguir, que você deverá criar e preencher com os valores apropriados.

| Tipo de Ativo | Nome do ativo | Descrição |
|:--- |:--- |:--- |:--- |
| Credencial |AzureCredential |Contém as credenciais de uma conta com autoridade para iniciar e parar máquinas virtuais na assinatura do Azure.  Como alternativa, você pode especificar outro ativo credencial no parâmetro **Credencial** da atividade **Add-AzureAccount**. |
| Variável |AzureSubscriptionId |Contém a ID da sua assinatura do Azure. |

## <a name="using-the-scenario"></a>Usando o cenário
### <a name="parameters"></a>Parâmetros
Cada um dos runbooks tem os parâmetros a seguir.  Você deve fornecer valores para todos os parâmetros obrigatórios e pode, se desejar, fornecer valores para outros parâmetros de acordo com os próprios requisitos.

| Parâmetro | Tipo | Obrigatório | Descrição |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Não |Se um valor for fornecido, todas as máquinas virtuais com esse nome de serviço serão iniciadas ou paradas.  Se nenhum valor for fornecido, todas as máquinas virtuais clássicas na assinatura do Azure serão iniciadas ou paradas. |
| AzureSubscriptionIdAssetName |string |Não |Contém o nome do [ativo variável](#installing-and-configuring-the-scenario) que contém a ID da sua assinatura do Azure.  Se você não especificar um valor, *AzureSubscriptionId* será usado. |
| AzureCredentialAssetName |string |Não |Contém o nome do [ativo de credencial](#installing-and-configuring-the-scenario) com as credenciais para o runbook a ser usado.  Se você não especificar um valor, *AzureCredential* será usado. |

### <a name="starting-the-runbooks"></a>Iniciando os runbooks
Você pode usar qualquer um dos métodos em [Iniciando um runbook na Automação do Azure](automation-starting-a-runbook.md) para iniciar qualquer um dos runbooks neste cenário.

Os comandos de exemplo a seguir usam o Windows PowerShell para executar **StartAzureClassicVM** e iniciar todas as máquinas virtuais com o nome do serviço *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Saída
Os runbooks [emitirão uma mensagem](automation-runbook-output-and-messages.md) para cada máquina virtual, indicando se a instrução de inicialização ou interrupção foi enviada com êxito.  Você pode procurar uma cadeia de caracteres específica na saída para determinar o resultado de cada runbook.  As cadeias de caracteres de saída possíveis estão listadas na tabela a seguir.

| Runbook | Condição | Mensagem |
|:--- |:--- |:--- |
| Start-AzureVMs |A máquina virtual já está em execução |MyVM já está em execução |
| Start-AzureVMs |Solicitação de inicialização para máquina virtual enviada com êxito |MyVM foi iniciada |
| Start-AzureVMs |Falha na solicitação de inicialização para máquina virtual |Falha ao iniciar a MyVM |
| Stop-AzureVMs |A máquina virtual já está parada |MyVM já foi parada |
| Stop-AzureVMs |Solicitação de parada da máquina virtual enviada com êxito |MyVM foi parada |
| Stop-AzureVMs |Falha na solicitação de parada da máquina virtual |Falha ao para a MyVM |

Por exemplo, o trecho de código a seguir de um runbook tenta iniciar todas as máquinas virtuais com o nome de serviço *MyServiceName*.  Se algumas das solicitações de inicialização falhar, as ações de erro poderão ser executadas.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Divisão detalhada
Veja a seguir uma divisão detalhada dos runbooks nesse cenário.  Você pode usar essas informações para personalizar os runbooks ou apenas para aprender a criar seus próprios cenários de automação.

### <a name="parameters"></a>Parâmetros
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

O fluxo de trabalho é iniciado obtendo os valores dos [parâmetros de entrada](#using-the-scenario).  Se os nomes do ativo não forem fornecidos, os nomes padrão serão usados.

### <a name="output"></a>Saída
    # Returns strings with status messages
    [OutputType([String])]

Essa linha declara que a saída do runbook será uma cadeia de caracteres.  Ela não é obrigatória, mas é uma prática recomendada para quando o runbook for usado como um [runbook filho](automation-child-runbooks.md) , de modo que o runbook pai saiba que tipo de saída esperar.

### <a name="authentication"></a>Autenticação
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

As próximas linhas definem as [credenciais](automation-credentials.md) e a assinatura do Azure que serão usadas para o restante do runbook.
Primeiro, usamos **Get-AutomationPSCredential** para obter o ativo que mantém as credenciais com acesso para iniciar e parar máquinas virtuais na assinatura do Azure. **Add-AzureAccount** usa esse ativo para definir as credenciais.  A saída é atribuída a uma variável fictícia para que ela não seja incluída na saída do runbook.  

O ativo variável com a ID da assinatura é recuperado com **Get-AutomationVariable** e a assinatura definida com **Select-AzureSubscription**.

### <a name="get-vms"></a>Obter VMs
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** é usado para recuperar as máquinas virtuais com as quais o runbook trabalhará.  Se um valor for fornecido na variável de entrada **ServiceName** , apenas as máquinas virtuais com esse nome de serviço serão recuperadas.  Se **ServiceName** estiver vazia, todas as máquinas virtuais serão recuperadas.

### <a name="startstop-virtual-machines-and-send-output"></a>Iniciar/parar as máquinas virtuais e enviar a saída
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

As próximas linhas exploram cada máquina virtual.  Primeiro o **PowerState** da máquina virtual é verificado para confirmar se ela já está em execução ou está parada, dependendo do runbook.  Se já estiver no estado desejado, uma mensagem será enviada para a saída e o runbook será encerrado.  Caso contrário, **Start-AzureVM** ou **Stop-AzureVM** será usado para tentar iniciar ou parar a máquina virtual com o resultado da solicitação armazenado em uma variável.  Uma mensagem é enviada para a saída especificando se a solicitação para iniciar ou parar foi enviada com êxito.

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre como trabalhar com runbooks filho, consulte [Runbooks filho na Automação do Azure](automation-child-runbooks.md)
* Para saber mais sobre mensagens de saída durante a execução de runbook e registro em log para ajudar a solucionar problemas, consulte [Saída e mensagens de runbook na Automação do Azure](automation-runbook-output-and-messages.md)

