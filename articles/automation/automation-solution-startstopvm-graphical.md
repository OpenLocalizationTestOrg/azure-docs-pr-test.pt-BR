---
title: "aaaStarting e VMs parando - gráfico | Microsoft Docs"
description: "Versão de fluxo de trabalho do PowerShell do cenário de automação do Azure, incluindo runbooks toostart e parar máquinas virtuais clássicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
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

Esta é a versão de runbook gráfico de saudação deste cenário. Ela também pode ser disponibilizada usando os [runbooks de Fluxo de Trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Obtendo o cenário de saudação
Este cenário consiste em dois dois runbooks gráficos que você pode baixar do hello links a seguir.  Consulte Olá [versão de fluxo de trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md) deste cenário para links toohello runbooks do fluxo de trabalho do PowerShell.

| Runbook | Link | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Runbook gráfico Iniciar VM clássica do Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Gráfico |Inicia todas as máquinas virtuais clássicas em uma assinatura do Azure ou todas as máquinas virtuais com um nome de serviço específico. |
| StopAzureClassicVM |[Runbook gráfico Parar VM clássica do Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Gráfico |Para todas as máquinas virtuais em uma conta de automação ou todas as máquinas virtuais com um nome de serviço específico. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalando e configurando o cenário de saudação
### <a name="1-install-hello-runbooks"></a>1. Instalar Olá runbooks
Depois de baixar runbooks hello, você pode importá-los usando o procedimento Olá [procedimentos de runbook gráfico](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Descrição de saudação de revisão e requisitos
Olá runbooks incluem uma atividade chamada **leia-Me** que inclui uma descrição e os ativos necessários.  Você pode exibir essas informações selecionando Olá **leia-Me** atividade e, em seguida, hello **Script de fluxo de trabalho** parâmetro.  Você também pode obter Olá as mesmas informações deste artigo.

### <a name="3-configure-assets"></a>3. Configurar ativos
Olá runbooks exigem Olá ativos que você deve criar e popular com os valores apropriados a seguir.  nomes de saudação são padrão.  Você pode usar ativos com nomes diferentes se você especificar esses nomes em Olá [parâmetros de entrada](#using-the-runbooks) ao iniciar o runbook hello.

| Tipo de Ativo | Nome padrão | Descrição |
|:--- |:--- |:--- |:--- |
| [Credencial](automation-credentials.md) |AzureCredential |Contém as credenciais para uma conta que tenha autoridade toostart e parar máquinas de virtuais em Olá assinatura do Azure. |
| [Variable](automation-variables.md) |AzureSubscriptionId |Contém a ID de assinatura de saudação da sua assinatura do Azure. |

## <a name="using-hello-scenario"></a>Usando o cenário de saudação
### <a name="parameters"></a>parâmetros
runbooks cada Hello têm seguinte Olá [parâmetros de entrada](automation-starting-a-runbook.md#runbook-parameters).  Você deve fornecer valores para todos os parâmetros obrigatórios e pode, se desejar, fornecer valores para outros parâmetros de acordo com os próprios requisitos.

| Parâmetro | Tipo | Obrigatório | Descrição |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Não |Se um valor for fornecido, todas as máquinas virtuais com esse nome de serviço serão iniciadas ou paradas.  Se nenhum valor for fornecido, todas as máquinas virtuais clássicas em Olá assinatura do Azure são iniciadas ou interrompidas. |
| AzureSubscriptionIdAssetName |string |Não |Contém nome de saudação do hello [ativo variável](#installing-and-configuring-the-scenario) que contém a ID de assinatura de saudação da sua assinatura do Azure.  Se você não especificar um valor, *AzureSubscriptionId* será usado. |
| AzureCredentialAssetName |string |Não |Contém nome de saudação do hello [ativo de credencial](#installing-and-configuring-the-scenario) que contém credenciais Olá Olá runbook toouse.  Se você não especificar um valor, *AzureCredential* será usado. |

### <a name="starting-hello-runbooks"></a>Runbooks de saudação inicial
Você pode usar qualquer um dos métodos de saudação em [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md) toostart qualquer um dos runbooks Olá neste artigo.

Olá comandos de exemplo a seguir usa o Windows PowerShell toorun **StartAzureClassicVM** toostart todas as máquinas virtuais com o nome do serviço Olá *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Saída
Olá runbooks serão [uma mensagem de saída](automation-runbook-output-and-messages.md) para cada máquina virtual que indica se ou não Olá início ou instrução stop foi enviada com êxito.  Você pode procurar uma cadeia de caracteres específica em Olá toodetermine Olá resultado para cada runbook.  cadeias de caracteres de saída possíveis Olá são listadas na Olá a tabela a seguir.

| Runbook | Condição | Mensagem |
|:--- |:--- |:--- |
| StartAzureClassicVM |A máquina virtual já está em execução |MyVM já está em execução |
| StartAzureClassicVM |Solicitação de inicialização para máquina virtual enviada com êxito |MyVM foi iniciada |
| StartAzureClassicVM |Falha na solicitação de inicialização para máquina virtual |Falha de MyVM toostart |
| StopAzureClassicVM |A máquina virtual já está em execução |MyVM já foi parada |
| StopAzureClassicVM |Solicitação de inicialização para máquina virtual enviada com êxito |MyVM foi iniciada |
| StopAzureClassicVM |Falha na solicitação de inicialização para máquina virtual |Falha de MyVM toostart |

A seguir é uma imagem do uso de saudação **StartAzureClassicVM** como um [runbook filho](automation-child-runbooks.md) em um exemplo de runbook gráfico.  Isso usa links condicionais Olá em Olá a tabela a seguir.

| Link | Critérios |
|:--- |:--- |
| Link de êxito |$ActivityOutput['StartAzureClassicVM'] -like "\* foi iniciada" |
| Link de erro |$ActivityOutput['StartAzureClassicVM'] -notlike "\* foi iniciada" |

![Exemplo de runbook filho](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Divisão detalhada
A seguir está uma análise detalhada dos runbooks Olá neste cenário.  Você pode usar essas informações tooeither personalizar Olá runbooks ou apenas toolearn deles para a criação de seus próprios cenários de automação.

### <a name="authentication"></a>Autenticação
![Autenticação](media/automation-solution-startstopvm/graphical-authentication.png)

Olá runbook inicia com hello de tooset atividades [credenciais](automation-credentials.md) e assinatura do Azure que será usada para o restante de saudação do runbook hello.

Olá primeiro duas atividades, **obter Id de assinatura** e **obter credenciais do Azure**, recuperar Olá [ativos](#installing-the-runbook) que são usados por atividades de dois hello.  Essas atividades podem especificar diretamente ativos Olá, mas precisam de nomes de recursos de saudação.  Já que estamos permitindo Olá usuário toospecify esses nomes em Olá [parâmetros de entrada](#using-the-runbooks), precisamos esses ativos de saudação tooretrieve atividades com o nome especificado pelo parâmetro de entrada.

**Adicionar-AzureAccount** Olá de conjuntos de credenciais que serão usadas para o restante de saudação do runbook hello.  ativo de credencial de saudação recuperar da **obter credenciais do Azure** devem ter acessar toostart e parar as máquinas virtuais em Olá assinatura do Azure.  Olá assinatura que é usada é selecionada por **Select-AzureSubscription** que usa a Id de assinatura de saudação do **obter Id de assinatura**.

### <a name="get-virtual-machines"></a>Obter máquinas virtuais
![Obter VMs](media/automation-solution-startstopvm/graphical-getvms.png)

Olá runbook precisa toodetermine quais máquinas virtuais ele trabalhará com e se eles já estão iniciados ou interrompidos (dependendo da saudação runbook).   Uma das duas atividades recuperará Olá VMs.  **Obter máquinas virtuais no serviço** será executada se hello *ServiceName* parâmetro de entrada hello runbook contém um valor.  **Obter todas as VMs** será executada se hello *ServiceName* parâmetro de entrada hello runbook não contém um valor.  Essa lógica é executada por links condicionais de saudação precede cada atividade.

As duas atividades usam Olá **Get-AzureVM** cmdlet.  **Obter todas as VMs** usa Olá **ListAllVMs** parâmetro definido tooreturn todas as máquinas virtuais.  **Obter máquinas virtuais no serviço** usa Olá **GetVMByServiceAndVMName** parâmetro definido e fornece Olá **ServiceName** parâmetro de entrada para Olá **ServiceName**parâmetro.  

### <a name="merge-vms"></a>Mesclar VMs
![Mesclar VMs](media/automation-solution-startstopvm/graphical-mergevms.png)

Olá **VMs mesclar** atividade é necessário tooprovide entrada muito**Start-AzureVM** que precisa de nome de saudação e nome do serviço de saudação VMs toostart.  Essa entrada pode ser originada em **Obter Todas as VMs** ou **Obter VMs em Serviço**, mas **Start-AzureVM** pode apenas especificar uma atividade para sua entrada.   

cenário de saudação é toocreate **VMs mesclar** que é executado Olá **Write-Output** cmdlet.  Olá **InputObject** parâmetro desse cmdlet é uma expressão do PowerShell que combina entrada hello de atividades de saudação dois anterior.  Apenas uma dessas atividades será executada, de modo que apenas um conjunto de saída é esperado.  **Start-AzureVM** pode usar essa saída para seus parâmetros de entrada.

### <a name="startstop-virtual-machines"></a>Iniciar/parar máquinas virtuais
![Iniciar VMs](media/automation-solution-startstopvm/graphical-startvm.png) ![Parar VMs](media/automation-solution-startstopvm/graphical-stopvm.png)

Dependendo runbook hello, atividades Avançar Olá tentativa toostart ou parar de usar o runbook Olá **Start-AzureVM** ou **Stop-AzureVM**.  Desde que a atividade de saudação é precedida por um link de pipeline, ele será executado uma vez para cada objeto retornado de **VMs mesclar**.  Olá link é condicional para que a atividade de saudação só será executada se hello *RunningState* de saudação máquina virtual é *parado* para **Start-AzureVM** e  *Iniciado* para **Stop-AzureVM**. Se essa condição não for atendida, em seguida, **notificar já iniciado** ou **notificar já parado** é executado toosend uma mensagem usando **Write-Output**.

### <a name="send-output"></a>Enviar saída
![Notificar Iniciar VMs](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notificar Parar VMs](media/automation-solution-startstopvm/graphical-notifystop.png)

etapa final Olá Olá runbook é toosend saída se Olá início ou parada de solicitação para cada máquina virtual foi enviada com êxito. Há um separado **Write-Output** atividade para cada um, e é determinar quais um toorun com links condicionais.  **Notificar VM Iniciada** ou **Notificar VM Parada** será executada se *OperationStatus* for *Êxito*.  Se *OperationStatus* for qualquer outro valor, em seguida, **notificar falha tooStart** ou **tooStop notificar falha** é executado.

## <a name="next-steps"></a>Próximas etapas
* [Criação gráfica na Automação do Azure](automation-graphical-authoring-intro.md)
* [Runbooks filhos na Automação do Azure](automation-child-runbooks.md)
* [Saída de runbook e mensagens na Automação do Azure](automation-runbook-output-and-messages.md)
