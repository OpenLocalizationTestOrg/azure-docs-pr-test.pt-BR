---
title: "aaaRunbook mensagens na automação do Azure e saída | Microsoft Docs"
description: "Descreve como o erro e saída toocreate e recuperar mensagens de runbooks na automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Saída e mensagens do runbook na Automação do Azure
A maioria dos runbooks de automação do Azure terá alguma forma de saída, como um usuário de toohello de mensagem de erro ou um objeto complexo destinado toobe consumido por outro fluxo de trabalho. O Windows PowerShell oferece [vários fluxos](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend saída de um script ou fluxo de trabalho. Automação do Azure funciona diferentemente com cada um desses fluxos, e você deve seguir as práticas recomendadas para como toouse cada quando você estiver criando um runbook.

Olá tabela a seguir fornece uma breve descrição de cada um dos fluxos de saudação e seus comportamentos no Portal de gerenciamento de saudação quando executar um runbook publicado e quando [testar um runbook](automation-testing-runbook.md). Serão fornecidos mais detalhes sobre cada fluxo nas seções subsequentes.

| Fluxo | Descrição | Publicado | Teste |
|:--- |:--- |:--- |:--- |
| Saída |Objetos destinados toobe consumido por outros runbooks. |Histórico de trabalho toohello escrito. |Exibido no painel de saída do teste de saudação. |
| Aviso |Mensagem de aviso destinada ao usuário hello. |Histórico de trabalho toohello escrito. |Exibido no painel de saída do teste de saudação. |
| Erro |Mensagem de erro destinado Olá usuário. Ao contrário de uma exceção, Olá runbook continua após uma mensagem de erro por padrão. |Histórico de trabalho toohello escrito. |Exibido no painel de saída do teste de saudação. |
| Detalhado |Mensagens que fornecem informações gerais ou de depuração. |Gravado toojob histórico somente se o log detalhado está ativado para o runbook hello. |No painel de saída do teste Olá só aparece se $VerbosePreference é configurada tooContinue em Olá runbook. |
| Andamento |Registros gerados automaticamente antes e depois de cada atividade no runbook hello. Olá runbook não deve tentar toocreate em seus próprios registros de progresso desde que eles são destinados a um usuário interativo. |Gravado toojob histórico somente se o log de andamento está ativado para Olá runbook. |Não é exibido no painel de saída do teste de saudação. |
| Depurar |As mensagens destinadas a um usuário interativo. Não deve ser usado em runbooks. |Não gravado toojob histórico. |Não gravado tooTest painel de saída. |

## <a name="output-stream"></a>Fluxo de saída
fluxo de saída de Hello destina-se a saída de objetos criados por um script ou fluxo de trabalho quando ele é executado corretamente. Na automação do Azure, esse fluxo é usado principalmente para objetos destinados toobe consumida por [runbooks pais que chamam o runbook atual Olá](automation-child-runbooks.md). Quando você [chamar um runbook embutido](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) de um runbook pai, ele retorna dados do pai de toohello de fluxo de saída de hello. Você deve usar apenas o usuário do hello saída fluxo toocommunicate informações gerais toohello back se você souber Olá runbook nunca será chamado por outro runbook. Como prática recomendada, no entanto, você normalmente deve usar Olá [fluxo detalhado](#Verbose) toocommunicate usuário de toohello de informações gerais.

Você pode gravar o fluxo de dados toohello saída usando [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) ou colocando o objeto de saudação em sua própria linha no runbook hello.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Saída de uma função
Quando você escreve o fluxo de saída toohello em uma função que está incluída no seu runbook, a saída de hello é passada toohello back runbook. Se Olá runbook atribui essa variável de tooa de saída, em seguida, ele não será gravado toohello fluxo de saída. Gravar tooany outros fluxos de dentro da função hello gravará toohello o fluxo correspondente para o runbook hello.

Considere Olá runbook de exemplo a seguir.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


saudação de fluxo de saída para o trabalho de runbook Olá seria:

    Output inside of function
    Output outside of function

saudação de fluxo detalhado para o trabalho de runbook Olá seria:

    Verbose outside of function
    Verbose inside of function

Depois que você publicou o runbook hello e antes de você iniciá-lo, você também deve ativar registro nas configurações de runbook Olá no hello tooget de ordem saída de fluxo detalhado detalhado.

### <a name="declaring-output-data-type"></a>Declarando o tipo de dados de saída
Um fluxo de trabalho pode especificar o tipo de dados de saudação de sua saída usando Olá [atributo OutputType](http://technet.microsoft.com/library/hh847785.aspx). Esse atributo não tem nenhum efeito em tempo de execução, mas ele fornece um autor de runbook indicação toohello em tempo de design da saída de hello esperado de runbook hello. Como Olá conjunto de ferramentas para runbooks continua tooevolve, importância de saudação da declaração de tipos de dados de saída em tempo de design aumenta. Como resultado, é uma prática recomendada tooinclude essa declaração em quaisquer runbooks criados por você.

Veja uma lista de tipos de saída de exemplo:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Olá seguinte exemplo de runbook gera um objeto de cadeia de caracteres e inclui uma declaração de seu tipo de saída. Se seu runbook gera como saída uma matriz de um determinado tipo, ainda deve especificar o tipo de saudação como tooan contrário matriz do tipo hello.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare uma saída de tipo em runbooks Grapical ou fluxo de trabalho do PowerShell gráfica, você pode selecionar Olá **de entrada e saída** opção de menu e digite o nome de saudação do hello tipo de saída.  É recomendável usar o hello toomake de nome de classe completo .NET-lo facilmente identificável ao fazer referência a ele de um runbook pai.  Isso expõe todas as propriedades de saudação do barramento de dados de toohello dessa classe no runbook hello e fornece uma grande flexibilidade quando usá-los para lógica condicional, o log e referenciando os valores de outras atividades no runbook hello.<br> ![Opção Entrada e Saída de Runbook](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

Saudação de exemplo a seguir, temos duas toodemonstrate de runbooks gráficos esse recurso.  Se conseguimos aplicar o modelo de design modular runbook hello, temos um runbook que serve como Olá *modelo autenticação Runbook* gerenciamento de autenticação com o uso do Azure Olá conta executar como.  Nosso runbook segundo, que normalmente seria executar Olá core lógica tooautomate um determinado cenário, nesse caso é vai Olá tooexecute *modelo autenticação Runbook* e exibir hello resultados tooyour **teste** painel de saída.  Em circunstâncias normais, podemos teria este runbook fazer algo em relação a uma saída de hello aproveitar recursos do runbook filho de saudação.    

Aqui está a lógica básica Olá de saudação **AuthenticateTo Azure** runbook.<br> ![Exemplo de modelo de runbook de autenticação](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Ele inclui o tipo de saída de hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, que retorna as propriedades de perfil de autenticação hello.<br> ![Exemplo de tipo de saída de runbook](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Enquanto esse runbook é muito simples e prático, há um toocall de item de configuração limite aqui.  última atividade de saudação está em execução Olá **Write-Output** cmdlet e gravações Olá variável perfil dados tooa $_ usando uma expressão do PowerShell para Olá **Inputobject** parâmetro, que é necessário para que cmdlet.  

Olá runbook segundo neste exemplo, chamado *ChildOutputType teste*, simplesmente, temos duas atividades.<br> ![Runbook de tipo de saída de exemplo filho](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

primeira atividade de saudação chama Olá **AuthenticateTo Azure** runbook e hello segunda atividade está em execução Olá **Write-Verbose** cmdlet com hello **fonte de dados** de  **Saída de atividade** e o valor Olá **caminho de campo** é **Context.Subscription.SubscriptionName**, que está especificando a saída de contexto de saudação do hello  **Azure AuthenticateTo** runbook.<br> ![Fonte de dados de parâmetro do cmdlet Write-Verbose](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

saída resultante Olá é o nome de saudação de assinatura de saudação.<br> ![Resultados do runbook Test-ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Uma observação sobre o comportamento de saudação do hello controle do tipo de saída.  Quando você digita um valor no campo de tipo de saída Olá Olá entrada e a folha de propriedades de saída, você tem tooclick fora do controle Olá depois que você digita, para que seu toobe entrada reconhecido pelo controle de saudação.  

## <a name="message-streams"></a>Fluxos de mensagens
Ao contrário do fluxo de saída de hello, fluxos de mensagens são usuário de toohello informações toocommunicate pretendido. Existem vários fluxos de mensagens para diferentes tipos de informação, e cada um deles é manipulado de forma diferente pela Automação do Azure.

### <a name="warning-and-error-streams"></a>Fluxos de aviso e de erro
fluxos de aviso e erro Olá são toolog pretendido problemas que ocorrem em um runbook. Eles são gravados toohello histórico de trabalho quando um runbook é executado e são incluídos no painel de saída do teste de saudação no Portal de gerenciamento de saudação quando um runbook é testado. Por padrão, o runbook Olá continuará a executar após um aviso ou erro. Você pode especificar esse runbook Olá deve ser suspenso em um aviso ou erro definindo uma [variável de preferência](#PreferenceVariables) em Olá runbook antes de criar a mensagem de saudação. Por exemplo, toocause toosuspend um runbook em um erro como se fosse uma exceção, defina **$ErrorActionPreference** tooStop.

Criar uma mensagem de aviso ou erro usando Olá [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) ou [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. As atividades também podem gravar fluxos toothese.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Fluxo Detalhado
fluxo de mensagem detalhada Olá é para obter informações gerais sobre a operação de runbook hello. Desde Olá [fluxo de depuração](#Debug) não está disponível em um runbook, mensagens detalhadas devem ser usadas para obter informações de depuração. Por padrão, as mensagens detalhadas de runbooks publicados não serão armazenadas no histórico de trabalho hello. toostore as mensagens detalhadas, configurar runbooks publicados tooLog registros detalhados no guia de configurar Olá Olá runbook no Portal de gerenciamento de saudação. Na maioria dos casos, você deve manter a configuração de padrão de saudação do log não registros detalhados para um runbook por motivos de desempenho. Ativar este tootroubleshoot somente da opção ou depurar um runbook.

Quando [testar um runbook](automation-testing-runbook.md), mensagens detalhadas não são exibidas, mesmo se o runbook Olá é registros detalhados toolog configurado. as mensagens detalhadas ao toodisplay [testar um runbook](automation-testing-runbook.md), você deve definir Olá $VerbosePreference tooContinue de variável. Com essa variável configurada, as mensagens detalhadas serão exibidas no hello painel de saída do teste de saudação portal do Azure.

Criar uma mensagem detalhada usando Olá [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Fluxo de Depuração
fluxo de depuração Olá destina para uso com um usuário interativo e não deve ser usado em runbooks.

## <a name="progress-records"></a>Registros de andamento
Se você configurar registros de progresso de toolog um runbook (na guia Configurar de saudação de saudação runbook no portal do Azure de saudação), um registro será gravado toohello histórico de trabalho antes e após a execução de cada atividade. Na maioria dos casos, você deve manter a configuração de padrão de saudação de log não registros de progresso de um runbook no desempenho de toomaximize de ordem. Ativar este tootroubleshoot somente da opção ou depurar um runbook. Ao testar um runbook, mensagens de progresso não são exibidas, mesmo se Olá runbook estiver configurado toolog registros de progresso.

Olá [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet não é válido em um runbook, já que isso é destinado ao uso com um usuário interativo.

## <a name="preference-variables"></a>Variáveis de preferência
O Windows PowerShell usa [variáveis de preferências](http://technet.microsoft.com/library/hh847796.aspx) toodetermine como toorespond toodata enviado toodifferent fluxos de saída. Você pode definir essas variáveis em um toocontrol runbook como ele responde toodata enviados para diferentes fluxos.

Olá tabela a seguir lista as variáveis de preferências de saudação que podem ser usadas em runbooks com seus válido e valores padrão. Observe que essa tabela inclui somente os valores de saudação que são válidos em um runbook. Valores adicionais são válidos para variáveis de preferência hello quando usados no Windows PowerShell fora da automação do Azure.

| Variável | Valor Padrão | Valores Válidos |
|:--- |:--- |:--- |
| WarningPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| ErrorActionPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continue<br>SilentlyContinue |

Olá a tabela a seguir lista o comportamento de saudação para valores de variável de preferência Olá que são válidas em runbooks.

| Valor | Comportamento |
|:--- |:--- |
| Continue |Registra a mensagem de saudação e continua executando o runbook hello. |
| SilentlyContinue |Continua executando Olá runbook sem registrar a mensagem de saudação. Isso tem o efeito de saudação de ignorar a mensagem de saudação. |
| Parar |Registra a mensagem de saudação e suspende o runbook hello. |

## <a name="retrieving-runbook-output-and-messages"></a>Recuperando saída e mensagens do runbook
### <a name="azure-portal"></a>Portal do Azure
Você pode exibir detalhes de saudação de um trabalho de runbook no portal do Azure na guia trabalhos de saudação de um runbook de saudação. Olá resumo do trabalho Olá exibirá os parâmetros de entrada hello e hello [fluxo de saída](#Output) nas informações de toogeneral de adição sobre o trabalho de saudação e todas as exceções que tenham ocorrido. Olá histórico incluirá mensagens de saudação [fluxo de saída](#Output) e [fluxos de advertência e erro](#WarningError) na adição toohello [fluxo detalhado](#Verbose) e [progresso Registros](#Progress) se Olá runbook estiver configurado toolog detalhado e registros de progresso.

### <a name="windows-powershell"></a>Windows PowerShell
No Windows PowerShell, você pode recuperar mensagens e saída de um runbook usando Olá [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. Esse cmdlet requer Olá ID do trabalho hello e tem um parâmetro chamado fluxo onde você pode especificar qual fluxo tooreturn. Você pode especificar qualquer tooreturn todos os fluxos de trabalho de saudação.

saudação de exemplo a seguir inicia um runbook de exemplo e, em seguida, aguarda-toocomplete. Depois de concluído, o fluxo de saída é coletado do trabalho hello.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Criação gráfica
Para runbooks gráficos, log adicional está disponível em forma de saudação do rastreamento em nível de atividade.  Há dois níveis de rastreamento: Básico e Detalhado.  No rastreamento básico, você pode ver Olá iniciar e hora de término de cada atividade no runbook hello, além de informações relacionadas tooany repetições de atividade, como número de tentativas e a hora de início da atividade de saudação.  No rastreamento Detalhado, você obtém o rastreamento Básico, além de dados de entrada e de saída para cada atividade.  Observe que no momento registros de rastreamento de saudação são gravados usando o fluxo detalhado do hello, habilite o log detalhado quando você ativa o rastreamento.  Para runbooks gráficos com o rastreamento ativado não é necessário toolog registros de progresso, porque serve de rastreamento básico Olá Olá mesmo propósito e é mais informativo.

![Modo de exibição Transmissões de Trabalho da criação gráfica](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Você pode ver a saudação acima captura de tela que, quando você habilita o log detalhado de log e rastreamento para runbooks gráficos, muito mais informações estão disponíveis na produção de hello que exibir fluxos de trabalho.  Essas informações extra podem ser essenciais para solucionar problemas de produção com um runbook e, portanto, você só deve habilitá-lo para essa finalidade e não como uma prática geral.    
registros de rastreamento Olá podem ser especialmente vários.  Com o runbook gráfico rastreamento que você pode obter dois registros toofour por atividade dependendo se você tiver configurado o rastreamento básico ou detalhado.  A menos que você precisar esse andamento de saudação tootrack informações de um runbook para solução de problemas, convém tookeep que rastreamento desativado.

**tooenable nível de atividade de rastreamento, execute Olá etapas a seguir.**

1. No Portal do Azure do hello, abra sua conta de automação.
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.
3. Na folha de Runbooks hello, clique em tooselect um runbook gráfico da sua lista de runbooks.
4. Na folha de configurações Olá runbook Olá selecionado, clique em **log e rastreamento**.
5. No hello log e rastreamento folha em registros detalhados de Log, clique em **na** tooenable o log detalhado e rastreamento de udner nível de atividade, alterar o nível de rastreamento Olá muito**básica** ou **detalhado**  com base no nível de saudação de rastreamento que você precisa.<br>
   
   ![Folha Log e Rastreamento da criação gráfica](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Log Analytics do OMS (Microsoft Operations Management Suite)
Automação pode enviar runbook trabalho status e o trabalho fluxos tooyour análise de logs do Microsoft Operations Management Suite (OMS) espaço de trabalho.  Com o Log Analytics, você pode

* Obter informações sobre os trabalhos de Automação 
* Disparar um email ou um alerta com base no status do trabalho de runbook (por exemplo, com falha ou suspenso) 
* Escrever consultas avançadas em seus fluxos de trabalho 
* Correlacionar trabalhos em contas de Automação 
* Visualizar o histórico de trabalho ao longo do tempo    

Para obter mais informações sobre como a integração de tooconfigure com toocollect de análise de Log, correlacionar e agir sobre dados de trabalho, consulte [encaminhar o status do trabalho e fluxos de trabalho de automação tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a execução do runbook, como trabalhos de runbook toomonitor e outros detalhes técnicos, consulte [acompanhar um trabalho de runbook](automation-runbook-execution.md)
* toounderstand como toodesign e usar runbooks filho, consulte [filho runbooks na automação do Azure](automation-child-runbooks.md)

