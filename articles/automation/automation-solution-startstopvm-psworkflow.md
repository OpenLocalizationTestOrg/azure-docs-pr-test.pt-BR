---
title: "aaaStarting e parar máquinas virtuais com a automação do Azure - fluxo de trabalho do PowerShell | Microsoft Docs"
description: "Versão gráfica do cenário de automação do Azure, incluindo runbooks toostart e parar máquinas virtuais clássicas."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Cenário de Automação do Azure — iniciando e parando máquinas virtuais
Este cenário de automação do Azure inclui runbooks toostart e parar máquinas virtuais clássicas.  Você pode usar este cenário para qualquer um dos seguintes hello:  

* Use runbooks Olá sem modificação no seu ambiente.
* Modificar a funcionalidade do hello runbooks tooperform personalizado.  
* Chame hello runbooks de outro runbook como parte de uma solução geral.
* Use runbooks hello como tutoriais toolearn runbook conceitos de criação.

> [!div class="op_single_selector"]
> * [Gráfico](automation-solution-startstopvm-graphical.md)
> * [Fluxo de Trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

Isso é hello versão de runbook de fluxo de trabalho do PowerShell deste cenário. Ela também é disponibilizada usando [runbooks gráficos](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Obtendo o cenário de saudação
Este cenário consiste em dois runbooks de fluxo de trabalho do PowerShell que você pode baixar do hello links a seguir.  Consulte Olá [versão gráfica](automation-solution-startstopvm-graphical.md) deste cenário para links toohello gráfica runbooks.

| Runbook | Link | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Iniciar VMs clássicas do Azure](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Fluxo de Trabalho do PowerShell |Inicia todas as máquinas virtuais clássicas em uma assinatura do Azure ou em todas as máquinas virtuais com um nome de serviço específico. |
| Stop-AzureVMs |[Parar VMs clássicas do Azure](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Fluxo de Trabalho do PowerShell |Para todas as máquinas virtuais em uma conta de automação ou todas as máquinas virtuais com um nome de serviço específico. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalando e configurando o cenário de saudação
### <a name="1-install-hello-runbooks"></a>1. Instalar Olá runbooks
Depois de baixar runbooks hello, você pode importá-los usando o procedimento Olá [importar um Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Descrição de saudação de revisão e requisitos
Olá runbooks incluir texto de ajuda comentados que inclui uma descrição e os ativos necessários.  Você também pode obter Olá as mesmas informações deste artigo.

### <a name="3-configure-assets"></a>3. Configurar ativos
Olá runbooks exigem Olá ativos que você deve criar e popular com os valores apropriados a seguir.

| Tipo de Ativo | Nome do ativo | Descrição |
|:--- |:--- |:--- |:--- |
| Credencial |AzureCredential |Contém as credenciais para uma conta que tenha autoridade toostart e parar máquinas de virtuais em Olá assinatura do Azure.  Como alternativa, você pode especificar outro ativo de credencial em Olá **credencial** parâmetro hello **Add-AzureAccount** atividade. |
| Variável |AzureSubscriptionId |Contém a ID de assinatura de saudação da sua assinatura do Azure. |

## <a name="using-hello-scenario"></a>Usando o cenário de saudação
### <a name="parameters"></a>parâmetros
Olá runbooks cada têm Olá parâmetros a seguir.  Você deve fornecer valores para todos os parâmetros obrigatórios e pode, se desejar, fornecer valores para outros parâmetros de acordo com os próprios requisitos.

| Parâmetro | Tipo | Obrigatório | Descrição |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Não |Se um valor for fornecido, todas as máquinas virtuais com esse nome de serviço serão iniciadas ou paradas.  Se nenhum valor for fornecido, todas as máquinas virtuais clássicas em Olá assinatura do Azure são iniciadas ou interrompidas. |
| AzureSubscriptionIdAssetName |string |Não |Contém nome de saudação do hello [ativo variável](#installing-and-configuring-the-scenario) que contém a ID de assinatura de saudação da sua assinatura do Azure.  Se você não especificar um valor, *AzureSubscriptionId* será usado. |
| AzureCredentialAssetName |string |Não |Contém nome de saudação do hello [ativo de credencial](#installing-and-configuring-the-scenario) que contém credenciais Olá Olá runbook toouse.  Se você não especificar um valor, *AzureCredential* será usado. |

### <a name="starting-hello-runbooks"></a>Runbooks de saudação inicial
Você pode usar qualquer um dos métodos de saudação em [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md) toostart qualquer um dos runbooks Olá neste cenário.

Olá comandos de exemplo a seguir usa o Windows PowerShell toorun **StartAzureVMs** toostart todas as máquinas virtuais com o nome do serviço Olá *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Saída
Olá runbooks serão [uma mensagem de saída](automation-runbook-output-and-messages.md) para cada máquina virtual que indica se ou não Olá início ou instrução stop foi enviada com êxito.  Você pode procurar uma cadeia de caracteres específica em Olá toodetermine Olá resultado para cada runbook.  cadeias de caracteres de saída possíveis Olá são listadas na Olá a tabela a seguir.

| Runbook | Condição | Mensagem |
|:--- |:--- |:--- |
| Start-AzureVMs |A máquina virtual já está em execução |MyVM já está em execução |
| Start-AzureVMs |Solicitação de inicialização para máquina virtual enviada com êxito |MyVM foi iniciada |
| Start-AzureVMs |Falha na solicitação de inicialização para máquina virtual |Falha de MyVM toostart |
| Stop-AzureVMs |A máquina virtual já está parada |MyVM já foi parada |
| Stop-AzureVMs |Solicitação de parada da máquina virtual enviada com êxito |MyVM foi parada |
| Stop-AzureVMs |Falha na solicitação de parada da máquina virtual |Falha de MyVM toostop |

Por exemplo, Olá trecho de código a seguir de um runbook tentativas toostart todas as máquinas virtuais com o nome do serviço Olá *MyServiceName*.  Se qualquer Olá iniciar solicitações falhar, as ações de erro podem tomadas.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Divisão detalhada
A seguir está uma análise detalhada dos runbooks Olá neste cenário.  Você pode usar essas informações tooeither personalizar Olá runbooks ou apenas toolearn deles para a criação de seus próprios cenários de automação.

### <a name="parameters"></a>parâmetros
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hello fluxo de trabalho é iniciado por obter valores Olá Olá [parâmetros de entrada](#using-the-scenario).  Se não forem fornecidos nomes de recursos de saudação nomes padrão são usados.

### <a name="output"></a>Saída
    # Returns strings with status messages
    [OutputType([String])]

Essa linha declara que o resultado Olá Olá runbook será uma cadeia de caracteres.  Isso não é necessário, mas é uma prática recomendada para quando o runbook Olá é usada como um [runbook filho](automation-child-runbooks.md) para que um runbook pai saibam saída Olá tooexpect de tipo.

### <a name="authentication"></a>Autenticação
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

linhas seguintes Olá definem Olá [credenciais](automation-credentials.md) e assinatura do Azure que será usada para o restante de saudação do runbook hello.
Primeiro, usamos **Get-AutomationPSCredential** tooget ativo de saudação que mantém as credenciais de saudação com acesso toostart e parar máquinas virtuais em Olá assinatura do Azure. **Adicionar-AzureAccount** , em seguida, usa esse credenciais de saudação tooset ativo.  saída de Hello é atribuída a variável fictício tooa para que ele não está incluído na saída de runbook hello.  

ativo de variável Olá com assinatura Olá ID, em seguida, é recuperada com **Get-AutomationVariable** e assinatura Olá com **Select-AzureSubscription**.

### <a name="get-vms"></a>Obter VMs
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** é usado tooretrieve máquinas virtuais de Olá Olá runbook funcionará com.  Se um valor é fornecido no hello **ServiceName** variável, em seguida, somente as máquinas virtuais do hello com esse nome de serviço são recuperadas de entrada.  Se **ServiceName** estiver vazia, todas as máquinas virtuais serão recuperadas.

### <a name="startstop-virtual-machines-and-send-output"></a>Iniciar/parar as máquinas virtuais e enviar a saída
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

Olá Avançar linhas percorrer cada máquina virtual.  Olá primeiro **PowerState** de saudação a máquina virtual está toosee verificado se ele já está em execução ou parado, dependendo da saudação runbook.  Se ele já está em estado de destino hello, uma mensagem é enviada toooutput e Olá runbook termina.  Se não, em seguida, **Start-AzureVM** ou **Stop-AzureVM** é tooattempt usado toostart ou parar Olá máquina virtual com o resultado da saudação da variável do hello solicitação tooa armazenado.  Uma mensagem é enviada toooutput especificando se Olá solicitação toostart ou parar foi enviada com êxito.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre como trabalhar com runbooks filho, consulte [filho runbooks na automação do Azure](automation-child-runbooks.md)
* Saiba mais sobre toolearn mensagens durante a execução de runbook e registro em log toohelp solucionar problemas, consulte [Runbook mensagens na automação do Azure e saída](automation-runbook-output-and-messages.md)

