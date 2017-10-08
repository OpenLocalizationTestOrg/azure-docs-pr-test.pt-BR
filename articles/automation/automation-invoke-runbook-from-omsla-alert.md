---
title: "aaaCalling um Runbook da automação do Azure de um alerta de análise de Log | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como tooinvoke um runbook de automação de um alerta de análise de Log de OMS do Microsoft."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Chamando um runbook de Automação do Azure a partir de um alerta do Log Analytics do OMS

Quando um alerta é configurado em análise de Log toocreate um registro de alerta se os resultados corresponderem a um critério específico, como um aumento prolongado na utilização do processador ou uma determinado aplicativo processo toohello crítico a funcionalidade de um aplicativo de negócios falhar e grava um evento correspondente no log de eventos do Windows hello, esse alerta pode executar automaticamente um runbook de automação em uma tentativa de tooauto-corrigir o problema de saudação.  

Há dois toocall de opções um runbook quando a configuração de alerta de saudação.  Especificamente:

1. Usando um Webhook.
   * Isso é Olá a única opção disponível se o seu espaço de trabalho do OMS não é vinculado tooan conta de automação.
   * Se você já tiver um espaço de trabalho automação conta vinculada tooan OMS, essa opção ainda está disponível.  

2. Selecione um runbook diretamente.
   * Essa opção está disponível somente quando o espaço de trabalho do hello OMS é vinculado tooan conta de automação.  

## <a name="calling-a-runbook-using-a-webhook"></a>Chamando um runbook com um webhook

Um webhook permite toostart um determinado runbook na automação do Azure por meio de uma única solicitação HTTP.  Antes de configurar Olá [alerta de análise de Log](../log-analytics/log-analytics-alerts.md#alert-rules) toocall Olá runbook usando um webhook como uma ação de alerta, você precisará toofirst criar um webhook de runbook Olá que será chamado usando esse método.  Examine e siga as etapas de Olá Olá [criar um webhook](automation-webhooks.md#creating-a-webhook) artigo e lembre-se a URL do webhook toorecord Olá para que você poderá referenciá-lo ao configurar a regra de alerta de saudação.   

## <a name="calling-a-runbook-directly"></a>Chamando um runbook diretamente

Se tiver Olá automação & oferta controle instalado e configurado em seu espaço de trabalho do OMS, ao configurar opção de ações de Runbook Olá alerta hello, você pode exibir todos os runbooks de saudação **selecionar um runbook** lista suspensa e selecione Olá runbook específico que você deseja toorun no alerta de toohello de resposta.  Olá selecionado runbook pode executar em um espaço de trabalho em Olá nuvem do Azure ou em um trabalho de runbook híbrido.  Quando o alerta de saudação é criada usando a opção de runbook hello, um webhook será criado para o runbook hello.  Você pode ver Olá webhook se você acessar a conta de automação toohello e navegue toohello webhook folha do runbook Olá selecionado.  Se você excluir o alerta hello, Olá webhook não é excluído, mas usuário Olá pode excluir o webhook Olá manualmente.  Não é um problema se Olá webhook não é excluído, ele é excluído de um item órfão que deverão toobe em ordem toomaintain uma conta de automação organizada.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Características de um runbook (para ambas as opções)

Os dois métodos para chamar hello runbook de alerta de análise de Log Olá têm características de um comportamento diferente que precisam toobe compreendido antes de configurar suas regras de alerta.  

* Você deve ter um parâmetro de entrada do runbook denominado **WebhookData** que é do tipo **Objeto**.  Pode ser obrigatório ou opcional.  alerta de saudação passa Olá pesquisa resultados toohello runbook usando o parâmetro de entrada.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Você deve ter um objeto do código tooconvert Olá WebhookData tooa do PowerShell.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* será uma matriz de objetos; cada objeto contém Olá campos com valores de um resultado de pesquisa

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData inconsistências entre a opção de webhook hello e opção de runbook

* Ao configurar um alerta toocall um Webhook, insira uma URL de webhook criado para um runbook e clique em Olá **Webhook teste** botão.  Olá WebhookData resultante enviados toohello runbook não contém um *. SearchResult* ou *. SearchResults*.

*  Se você salvar esse alerta, quando o alerta de saudação dispara e chama webhook Olá, Olá WebhookData enviados runbook toohello contém *. SearchResult*.
* Se você cria um alerta e configurá-lo toocall um runbook (que também cria um webhook), quando Olá gatilhos alertas envia WebhookData toohello runbook que contenha *. SearchResults*.

Portanto, no exemplo de código Olá acima, você precisará tooget *. SearchResult* se alerta Olá chama um webhook e será necessário tooget *. SearchResults* se o alerta Olá chamar um runbook diretamente.

## <a name="example-walkthrough"></a>Exemplo de passo a passo

Demonstraremos como isso funciona usando Olá runbook gráfico do exemplo, que inicia um serviço do Windows a seguir.<br><br> ![Iniciar Runbook Gráfico do Serviço do Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Olá runbook tem um parâmetro de entrada do tipo **objeto** que é chamado **WebhookData** e inclui dados de webhook Olá passados do hello alerta contendo *. SearchResults*.<br><br> ![Parâmetros de entrada do runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Neste exemplo, na análise de Log criamos dois campos personalizados, *SvcDisplayName_CF* e *SvcState_CF*, tooextract Olá serviço nome e hello estado de exibição do serviço hello (ou seja, em execução ou parado) do evento Olá gravado toohello log de eventos do sistema.  Em seguida, criamos uma regra de alerta com hello consulta de pesquisa a seguir: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` para que podemos pode detectar quando Olá serviço Spooler de impressão é interrompida no hello sistema Windows.  Pode ser qualquer serviço de interesse, mas para este exemplo, podemos fazem referência a um dos serviços de pré-existente Olá que acompanham a saudação sistema operacional Windows.  ação de alerta de saudação é configurado tooexecute nosso runbook usado neste exemplo e execute em Olá Hybrid Runbook Worker, que é habilitado em sistemas de destino hello.   

Hello atividade de código runbook **obter o nome do serviço de LA** converterá a cadeia de caracteres formatada em JSON de saudação em um tipo de objeto e um filtro no item de saudação *SvcDisplayName_CF* tooextract nome para exibição Olá da saudação Serviço Windows e a passa para a próxima atividade do hello verificar Olá foi interrompido antes de tentar toorestart-lo.  *SvcDisplayName_CF* é um [campo personalizado](../log-analytics/log-analytics-custom-fields.md) criado na análise de Log toodemonstrate neste exemplo.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Quando o serviço de saudação for interrompida, regra de alerta de saudação na análise de Log detectar uma correspondência e disparar o runbook Olá e enviar Olá contexto de alerta toohello runbook. Olá runbook executará a ação tooverify Olá serviço for interrompido, e então toorestart tentativa Olá serviço e verifique se ele é iniciado corretamente e resultados de saudação de saída.     

Como alternativa se você não tiver o seu espaço de trabalho automação conta vinculada tooyour OMS, você deve configurar regra de alerta de saudação com um webhook ação tootrigger Olá runbook e configurar de caracteres formatada em JSON Olá runbook tooconvert Olá e filtro em *. SearchResult* orientação Olá mencionada a seguir.    

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre alertas em análise de Log e como toocreate, consulte [alertas na análise de Log](../log-analytics/log-analytics-alerts.md).

* como ver tootrigger runbooks usando um webhook de toounderstand [webhooks de automação do Azure](automation-webhooks.md).
