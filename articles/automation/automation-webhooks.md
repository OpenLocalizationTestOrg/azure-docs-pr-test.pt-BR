---
title: "um runbook de automação do Azure com um webhook de aaaStarting | Microsoft Docs"
description: "Um webhook que permite que um cliente toostart um runbook na automação do Azure de uma chamada HTTP.  Este artigo descreve como um webhook de toocreate e como toocall uma toostart um runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Iniciar um runbook de Automação do Azure com um webhook
Um *webhook* permite toostart um determinado runbook na automação do Azure por meio de uma única solicitação HTTP. Isso permite que os serviços externos, como o Visual Studio Team Services, GitHub, análise de logs do Microsoft Operations Management Suite ou aplicativos personalizados toostart runbooks sem implementar uma solução completa usando Olá API de automação do Azure.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

Você pode comparar webhooks tooother métodos de iniciar um runbook [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Detalhes de um webhook
Olá, tabela a seguir descreve as propriedades de saudação que devem ser configuradas para um webhook.

| Propriedade | Descrição |
|:--- |:--- |
| Nome |Você pode fornecer qualquer nome desejado para um webhook como essa é não exposta toohello cliente.  Ele é usado somente para você tooidentify Olá runbook na automação do Azure. <br>  Como prática recomendada, você deve dar Olá webhook um cliente de toohello relacionados de nome que irá usá-la. |
| URL |Olá URL de webhook Olá é vinculado de endereço exclusivo de saudação que um cliente chama com um runbook de saudação do HTTP POST toostart toohello webhook.  Ele é gerado automaticamente quando você criar o webhook hello.  Você não pode especificar uma URL personalizada. <br> <br>  Olá URL contém um token de segurança que permite Olá runbook toobe invocado por um sistema de terceiros com nenhuma autenticação adicional. Por esse motivo, ele deve ser tratado como uma senha.  Por motivos de segurança, você pode apenas Olá exibição que URL no hello portal do Azure em Olá tempo Olá webhook é criado. Você deve observar Olá URL em um local seguro para uso futuro. |
| Data de validade |Como um certificado, cada webhook tem uma data de validade após a qual ele não pode mais ser usado.  A data de validade pode ser modificada depois Olá webhook é criado. |
| habilitado |Um webhook é habilitado por padrão quando ele é criado.  Se você definir tooDisabled, nenhum cliente será capaz de toouse-lo.  Você pode definir Olá **habilitado** é criado quando você criar o webhook hello ou a qualquer momento uma vez. |

### <a name="parameters"></a>parâmetros
Um webhook pode definir valores para parâmetros de runbook que são usados quando Olá runbook for iniciado por esse webhook. Olá webhook deve incluir valores para todos os parâmetros obrigatórios de runbook hello e pode incluir valores de parâmetros opcionais. Um webhook de tooa do valor configurado de parâmetro pode ser modificado até mesmo depois de criar webhoook hello. Vários webhooks vinculado tooa único runbook pode usar valores de parâmetros diferentes.

Quando um cliente inicia um runbook usando um webhook, ele não pode substituir valores de parâmetro de saudação definidos no hello webhook.  tooreceive dados de cliente hello, Olá runbook pode aceitar um parâmetro único chamado **$WebhookData** do tipo [object] que contém dados que o cliente Olá inclui na solicitação POST hello.

![Propriedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Olá **$WebhookData** objeto terá Olá propriedades a seguir:

| Propriedade | Descrição |
|:--- |:--- |
| WebhookName |nome de saudação do webhook hello. |
| RequestHeader |Tabela de hash que contém Olá cabeçalhos de solicitação POST de entrada hello. |
| RequestBody |corpo de saudação de solicitação POST de entrada hello.  Isso manterá qualquer formatação, como a cadeia de caracteres, JSON, XML ou os dados codificados de formulário. Olá runbook deve ser escrito toowork com formato de dados de saudação é esperado. |

Não há nenhuma configuração de Olá webhook toosupport necessário Olá **$WebhookData** parâmetro, e Olá runbook não é necessário tooaccept-lo.  Se o runbook Olá não define parâmetro hello, quaisquer detalhes de solicitação de saudação enviada do cliente de saudação é ignorado.

Se você especificar um valor para $WebhookData quando você cria o webhook hello, esse valor será substituída quando webhook Olá Olá runbook é iniciado com dados de saudação da solicitação POST do cliente Olá, mesmo se o cliente Olá não inclui todos os dados no corpo da solicitação de saudação.  Se você iniciar um runbook com $WebhookData usando um método que não seja um webhook, você pode fornecer um valor para $Webhookdata será reconhecido pelo runbook hello.  Esse valor deve ser um objeto com hello mesmo [propriedades](#details-of-a-webhook) como $Webhookdata para esse runbook Olá possa funcionar corretamente com ele como se ele estava trabalhando com WebhookData real passado por um webhook.

Por exemplo, se você estiver iniciando Olá após o runbook Olá Portal do Azure e deseja toopass alguns exemplos de WebhookData para teste, como WebhookData é um objeto, ele deve ser passado como JSON em Olá da interface do usuário.

![Parâmetro WebhookData da interface do usuário](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Para Olá acima runbook, se você tiver Olá seguintes propriedades para o parâmetro de WebhookData hello:

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

Em seguida, você passaria Olá valor JSON em hello da interface do usuário para o parâmetro de WebhookData hello a seguir:  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![Iniciar o parâmetro WebhookData na interface do usuário](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> os valores de todos os parâmetros de entrada Hello são registrados com o trabalho de runbook hello.  Isso significa que qualquer entrada fornecida pelo cliente Olá na solicitação de webhook hello serão tooanyone conectado e disponível com o trabalho de automação de toohello de acesso.  Por esse motivo, você deve ter cuidado ao incluir informações confidenciais em chamadas webhook.
>

## <a name="security"></a>Segurança
segurança de saudação de um webhook depende de privacidade Olá de sua URL que contém um token de segurança que lhe permite toobe invocado. Automação do Azure não executa nenhuma autenticação na solicitação Olá desde que ela se torna a URL correta do toohello. Por esse motivo, webhooks não deve ser usado para runbooks que executam funções altamente confidenciais sem usar um meio alternativo de validação de solicitação de saudação.

Você pode incluir lógica no hello runbook toodetermine que foi chamada por um webhook verificando Olá **WebhookName** propriedade do parâmetro hello $WebhookData. Olá runbook pode executar uma validação adicional, procurando por informações específicas no hello **RequestHeader** ou **RequestBody** propriedades.

Outra estratégia é toohave Olá runbook executar alguma validação de uma condição externa quando ele recebeu uma solicitação de webhook.  Por exemplo, considere um runbook que é chamado pelo GitHub sempre que há um novo repositório GitHub de tooa confirmação.  Olá runbook pode se conectar a toovalidate tooGitHub que uma nova confirmação apenas ocorreu antes de continuar.

## <a name="creating-a-webhook"></a>Criando um webhook
Use Olá seguindo o procedimento toocreate um novo runbook tooa webhook vinculado no hello portal do Azure.

1. De saudação **Runbooks folha** no hello portal do Azure, clique em runbook Olá Olá webhook iniciar tooview folha seus detalhes.
2. Clique em **Webhook** na parte superior da saudação de saudação do hello folha tooopen **Webhook adicionar** folha. <br>
   ![Botão Webhooks](media/automation-webhooks/webhooks-button.png)
3. Clique em **criar nova webhook** tooopen Olá **criar folha de webhook**.
4. Especifique um **nome**, **data de expiração** para webhook hello e se ele deve ser habilitado. Consulte [Detalhes de um webhook](#details-of-a-webhook) para obter mais informações sobre essas propriedades.
5. Clique Olá ícone para copiar e pressione Ctrl + C toocopy Olá URL de webhook hello.  Em seguida, anote-o em um local seguro.  **Depois de criar o webhook hello, você não pode recuperar a URL de saudação novamente.** <br>
   ![URL de Webhook](media/automation-webhooks/copy-webhook-url.png)
6. Clique em **parâmetros** tooprovide valores para parâmetros de runbook hello.  Se Olá runbook tiver parâmetros obrigatórios, em seguida, não será capaz de toocreate Olá webhook, a menos que os valores são fornecidos.
7. Clique em **criar** toocreate Olá webhook.

## <a name="using-a-webhook"></a>Usando um webhook
toouse um webhook após ela ter sido criada, seu aplicativo cliente deverá emitir um HTTP POST com URL Olá Olá webhook.  sintaxe de saudação do webhook Olá será em Olá formato a seguir.

    http://<Webhook Server>/token?=<Token Value>

cliente Olá receberá uma das Olá seguindo códigos de retorno da solicitação POST hello.  

| Código | Texto | Descrição |
|:--- |:--- |:--- |
| 202 |Aceita |Olá solicitação foi aceita e Olá runbook foi enfileirada com êxito. |
| 400 |Solicitação incorreta |solicitação de saudação não foi aceita para uma saudação motivos a seguir. <ul> <li>Olá webhook expirou.</li> <li>Olá webhook está desabilitado.</li> <li>token Olá Olá URL é inválido.</li>  </ul> |
| 404 |Não encontrado |solicitação de saudação não foi aceita para uma saudação motivos a seguir. <ul> <li>Olá webhook não foi encontrado.</li> <li>Olá runbook não foi encontrado.</li> <li>Olá conta não foi encontrada.</li>  </ul> |
| 500 |Erro interno do servidor |Olá URL era válida, mas ocorreu um erro.  Reenvie a solicitação de saudação. |

Supondo que Olá solicitação for bem-sucedida, resposta de webhook Olá contém id de trabalho Olá no formato JSON da seguinte maneira. Ele conterá uma id de trabalho único, mas o formato JSON de saudação permite possíveis aprimoramentos futuros.

    {"JobIds":["<JobId>"]}  

cliente Olá não pode determinar quando conclui o trabalho de runbook hello ou seu status de conclusão de webhook hello.  Ele pode determinar essas informações usando a id do trabalho Olá com outro método, como [do Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou hello [API de automação do Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Exemplo
Olá exemplo a seguir usa o Windows PowerShell toostart um runbook com um webhook.  Observe que qualquer linguagem que possa fazer uma solicitação HTTP pode usar um webhook; o Windows PowerShell é usado aqui apenas como um exemplo.

Olá runbook está esperando uma lista de máquinas virtuais formatada em JSON no corpo de saudação de solicitação de saudação. Também incluímos informações sobre quem está iniciando runbook Olá Olá e data que ele está sendo iniciado no cabeçalho de saudação de solicitação de saudação.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Olá, imagem a seguir mostra as informações de cabeçalho de saudação (usando um [Fiddler](http://www.telerik.com/fiddler) rastreamento) desta solicitação. Isso inclui cabeçalhos padrão de uma solicitação HTTP em adição toohello personalizado de data e dos cabeçalhos que foi adicionada.  Cada um desses valores é runbook toohello disponíveis no hello **RequestHeaders** propriedade **WebhookData**.

![Botão Webhooks](media/automation-webhooks/webhook-request-headers.png)

Olá, imagem a seguir mostra Olá corpo da solicitação de saudação (usando um [Fiddler](http://www.telerik.com/fiddler) rastreamento) que é toohello disponível runbook no hello **RequestBody** propriedade de **WebhookData**. Isso é formatado como JSON, pois esse era o formato de saudação que foi incluído no corpo de saudação de solicitação de saudação.     

![Botão Webhooks](media/automation-webhooks/webhook-request-body.png)

Olá imagem a seguir mostra solicitação Olá enviada do Windows PowerShell e a resposta resultante de saudação.  id do trabalho Olá é extraído da resposta hello e cadeia de caracteres tooa convertido.

![Botão Webhooks](media/automation-webhooks/webhook-request-response.png)

Olá seguinte exemplo de runbook aceita a solicitação anterior de exemplo hello e inicia a máquinas virtuais de saudação especificadas no corpo da solicitação de saudação.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>Iniciar runbooks em alertas de tooAzure de resposta
Runbooks de Webhook pode ser usado tooreact muito[alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Recursos do Azure podem ser monitorados por coletar estatísticas de saudação como desempenho, disponibilidade e o uso com a Ajuda de saudação de alertas do Azure. Você pode receber um alerta com base em métricas de monitoramento ou em eventos para seus recursos do Azure. No momento, as Contas de Automação oferecem suporte apenas para métricas. Quando o valor de saudação de uma métrica especificada excede limite Olá atribuído ou se Olá configurado evento é disparado uma notificação é enviada toohello serviço admin coadministradores tooresolve Olá alerta ou, para obter mais informações sobre as métricas e eventos, consulte muito[ Alertas do Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Além de usar os alertas do Azure como um sistema de notificação, você também pode disparar runbooks no tooalerts de resposta. Automação do Azure fornece Olá recurso toorun habilitado webhook runbooks com alertas do Azure. Quando uma métrica excede Olá configurado valor de limite de regra de alerta de saudação se torna ativa e gatilhos Olá webhook de automação que por sua vez executa runbook hello.

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Contexto do alerta
Considere um recurso do Azure como uma máquina virtual, a utilização da CPU do computador é uma métrica de desempenho chave hello. Se Olá utilização da CPU é 100% ou mais de uma determinada quantidade por longo período de tempo, talvez seja o problema de saudação do toorestart Olá máquina virtual toofix. Isso pode ser resolvido por meio da configuração de uma máquina de virtual toohello regra de alerta e essa regra usa a porcentagem de CPU como sua métrica. Porcentagem de CPU é aceito apenas como um exemplo, mas há muitas outras métricas que você pode configurar tooyour Azure recursos e reiniciar a máquina virtual de saudação é uma ação que é feito toofix esse problema, você pode configurar Olá runbook tootake outras ações.

Quando esta regra de alerta de saudação se torna ativa e gatilhos Olá runbook webhook habilitado, ele envia Olá contexto de alerta toohello runbook. [Contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contém os detalhes incluindo **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp** que são necessário para o recurso de saudação do hello runbook tooidentify em que ele irá realizar ação. Alerta de contexto é inserido na parte de corpo de saudação do hello **WebhookData** toohello enviados runbook do objeto e pode ser acessado com **Webhook.RequestBody** propriedade

### <a name="example"></a>Exemplo
Criar uma máquina virtual do Azure em sua assinatura e associar um [toomonitor CPU Porcentagem métrica de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Durante a criação de alerta de saudação Verifique se que você preencher o campo de webhook de saudação com hello URL de webhook Olá que foi gerada ao criar o webhook Olá.

seguinte exemplo de runbook Hello é disparado quando a regra de alerta de saudação se torna ativa e coleta parâmetros de contexto de alerta de saudação que são necessários para o recurso de saudação do hello runbook tooidentify em que ele irá realizar ação.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Próximas etapas
* Para obter detalhes sobre diferentes maneiras toostart um runbook, consulte [iniciando um Runbook](automation-starting-a-runbook.md).
* Para obter informações sobre Olá exibindo Status de um Runbook Job, consulte muito[execução de Runbook na automação do Azure](automation-runbook-execution.md).
* toolearn como toouse ação de tootake de automação do Azure em alertas do Azure, consulte [corrigir alertas de VM do Azure com Runbooks de automação](automation-azure-vm-alert-integration.md).
