---
title: "alertas de aaaCreating na análise de Log do OMS | Microsoft Docs"
description: "Alertas de análise de Log identificar informações importantes no seu repositório do OMS e podem proativamente notificá-lo de problemas ou invocar ações tooattempt toocorrect-los.  Este artigo descreve como toocreate uma regra de alerta e ações diferentes de saudação de detalhes que podem executar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Trabalhar com regras de alerta no Log Analytics
Os alertas são criados por regras de alerta que executam pesquisas de log automaticamente em intervalos regulares.  Ele criarem um registro de alerta se resultados Olá correspondem a critérios específicos.  regra de saudação poderá, em seguida, executar automaticamente uma ou mais tooproactively de ações notificá-lo de alerta de saudação ou chamar outro processo.   

Este artigo descreve Olá processos toocreate e editar regras de alerta usando o portal do OMS hello.  Para obter detalhes sobre configurações diferentes hello e como tooimplement necessário lógica, consulte [Noções básicas sobre alertas em análise de Log](log-analytics-alerts.md).

>[!NOTE]
> No momento, você não pode criar ou modificar uma regra de alerta usando Olá portal do Azure. 

## <a name="create-an-alert-rule"></a>Criar uma regra de alerta

toocreate uma regra de alerta usando o portal do OMS hello, comece criando uma pesquisa de log para os registros de saudação que deve chamar o alerta de saudação.  Olá **alerta** botão estará disponível para que você pode criar e configurar a regra de alerta de saudação.

>[!NOTE]
> Atualmente, podem ser criadas no máximo 250 regras de alerta em um espaço de trabalho do OMS. 

1. Na página de visão geral do OMS hello, clique em **pesquisa de Log**.
2. Crie uma nova consulta de pesquisa de log ou selecione uma pesquisa de log salva. 
3. Clique em **alerta** na parte superior da saudação de saudação do hello página tooopen **Adicionar regra de alerta** tela.
4. Configurar regra de alerta hello usando informações em [detalhes de regras de alerta](#details-of-alert-rules) abaixo.
6. Clique em **salvar** toocomplete regra de alerta de saudação.  Ela começa a ser executada imediatamente.


## <a name="edit-an-alert-rule"></a>Editar uma regra de alerta
Você pode obter uma lista de todas as regras de alerta em Olá **alertas** menu na análise de Log **configurações**.  

![Gerenciar alertas](./media/log-analytics-alerts/configure.png)

1. Em select saudação do hello OMS console **configurações** lado a lado.
2. Selecione **Alertas**.

Você pode executar várias ações nessa exibição.

* Desabilitar uma regra selecionando **Off** tooit Avançar.
* Edite uma regra de alerta clicando Olá Lápis ícone próximo tooit.
* Remover uma regra de alerta clicando Olá **X** tooit próximo ícone. 

## <a name="details-of-alert-rules"></a>Detalhes de regras de alerta
Quando você cria ou editar uma regra de alerta no portal do OMS hello, trabalhe com hello **Adicionar regra de alerta** ou **Editar regra de alerta** página.  Olá tabelas a seguir descreve os campos de saudação nesta tela.

![Regra de Alerta](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Informações de alerta
Essas são as configurações básicas para a regra de alerta hello e alertas de saudação cria.

| Propriedade | Descrição |
|:--- |:---|
| Nome | Exclusivo nome tooidentify Olá regra de alerta. Esse nome está incluído em todos os alertas criados por regra hello.  |
| Descrição | Descrição opcional da regra de alerta de saudação. |
| Severity |Gravidade dos alertas criados por essa regra. |

### <a name="search-query-and-time-window"></a>Consulta de pesquisa e janela de tempo
janela de consulta e a hora de pesquisa Olá que retorna registros de saudação que são avaliada toodetermine se qualquer alerta deve ser criada.

| Propriedade | Descrição |
|:--- |:---|
| Consulta de pesquisa | Esta é a consulta de saudação que será executada.  registros de saudação retornados por essa consulta serão toodetermine usado se um alerta será criado.<br><br>Selecione **usar consulta de pesquisa atual** toouse Olá consulta atual ou selecione uma pesquisa salva na lista de saudação existente.  sintaxe de consulta de saudação é fornecido na caixa de texto de saudação onde você pode modificá-lo se necessário. |
| Janela de tempo |Especifica o intervalo de tempo de saudação para consulta hello.  consulta de saudação retorna somente os registros que foram criados neste intervalo de saudação hora atual.  Este pode ser qualquer valor entre 5 minutos e 24 horas.  Ele deve ser a frequência de alerta de toohello maior que ou igual.  <br><br> Por exemplo, se hello tempo janela é definida too60 minutos e consulta de saudação for executado em 1:15 PM, somente os registros criados entre 12:15 PM e 1:15 PM serão retornados. |

Quando você fornece a janela de tempo de saudação para regra de alerta Olá, Olá número de registros existentes que correspondem aos critérios de pesquisa de saudação para a janela de tempo será exibido.  Isso pode ajudar a determinar a frequência de saudação que lhe dará Olá número de resultados que você espera.

### <a name="schedule"></a>Agenda
Define a frequência hello consulta de pesquisa é executada.

| Propriedade | Descrição |
|:--- |:---|
| Frequência de alerta | Especifica com que frequência hello consulta deve ser executada. Pode ser qualquer valor entre 5 minutos e 24 horas. Deve ser igual tooor inferior a janela de tempo de saudação.  Se o valor de saudação for maior que a janela de tempo de saudação, você poderá registros que está sendo ignorados.<br><br>Por exemplo, considere uma janela de tempo de 30 minutos e uma frequência de 60 minutos.  Se Olá consulta é executada à 1:00, ele retorna registros entre 12:30 e 1:00 PM.  Olá próxima vez consulta Olá executaria é 2:00 quando ela retorna registros entre 30:1 e 2:00.  Todos os registros criados entre 1:00 e 1:30 nunca seriam avaliados. |


### <a name="generate-alert-based-on"></a>Gerar alerta com base em
Define Olá critérios que serão avaliados em relação a resultados Olá Olá toodetermine de consulta de pesquisa se um alerta devem ser criados.  Esses detalhes serão diferentes dependendo do tipo de saudação da regra de alerta que você selecionar.  Você pode obter detalhes Olá tipos diferentes de regra de alerta de [Noções básicas sobre alertas em análise de Log](log-analytics-alerts.md).

| Propriedade | Descrição |
|:--- |:---|
| Suprimir alertas | Quando você ativar a supressão de regra de alerta Olá, ações de regra Olá estão desabilitadas para um período definido depois de criar um novo alerta. regra de saudação ainda está em execução e criará registros alertas se Olá critério for atendido. Isso é tooallow tempo problema de saudação toocorrect sem executar ações duplicadas. |

#### <a name="number-of-results-alert-rules"></a>Regras de alerta de Número de resultados

| Propriedade | Descrição |
|:--- |:---|
| Número de resultados |Um alerta será criado se o número de saudação de registros retornados pela consulta Olá é **maior** ou **menor** Olá valor que você fornecer.  |

#### <a name="metric-measurement-alert-rules"></a>Regras de alerta com medição métrica

| Propriedade | Descrição |
|:--- |:---|
| Valor de agregação | Valor de limite que cada valor de agregação nos resultados da saudação deve exceder toobe considerado uma violação. |
| Disparar alerta com base em | número de saudação de violações de um alerta toobe criado.  Você pode especificar **Total de violações de** para qualquer combinação de violações em resultados de saudação do conjunto ou **falhas consecutivas** toorequire que Olá violações deve ocorrer em amostras consecutivas. |

### <a name="actions"></a>Ações
Regras de alerta sempre criará uma [registro de alerta](#alert-records) quando o limite de saudação é atingido.  Você também pode definir um ou mais toobe de respostas executar como enviar um email ou iniciar um runbook.



#### <a name="email-actions"></a>Ações de email
Ações de email enviar um email com detalhes de saudação do tooone alerta hello ou mais destinatários.

| Propriedade | Descrição |
|:--- |:---|
| Notificação por email |Especifique **Sim** se você quiser um toobe de email enviada quando Olá alerta for disparado. |
| Assunto |Assunto no email de saudação.  Não é possível modificar o corpo de saudação de mensagens de saudação. |
| Destinatários |Endereços de todos os destinatários de email.  Se você especificar mais de um endereço e endereços de saudação separada com um ponto e vírgula (;). |

#### <a name="webhook-actions"></a>Ações de Webhook
Ações de Webhook permitem tooinvoke um processo externo por meio de uma única solicitação HTTP POST.

| Propriedade | Descrição |
|:--- |:---|
| webhook |Especifique **Sim** se desejar toocall um webhook quando Olá alerta for disparado. |
| URL de Webhook |URL de saudação do webhook hello. |
| Incluir a carga JSON personalizada |Selecione esta opção se desejar que a carga do tooreplace saudação padrão com uma carga personalizada. |
| Insira sua carga JSON personalizada |carga personalizada de saudação do webhook hello.  Consulte a seção anterior para ver os detalhes. |

#### <a name="runbook-actions"></a>Ações de runbook
Ações de runbook iniciam um runbook na Automação do Azure. 

>[!NOTE]
> Você deve ter a solução de automação de saudação instalada no seu espaço de trabalho para este toobe de ação habilitado. 


| Propriedade | Descrição |
|:--- |:---|
| Runbook | Especifique **Sim** se desejar toostart um runbook de automação do Azure quando Olá alerta for disparado.  |
| Conta de automação | Especifica a saudação conta de automação runbooks selecionado de.  Essa é a conta de ação de saudação foi vinculada toohello espaço de trabalho. |
| Selecionar um runbook | Selecione Olá runbook que você deseja toostart quando um alerta é criado. |
| Executar em | Selecione **Azure** toorun Olá runbook na nuvem hello.  Selecione **Hybrid worker** toorun Olá runbook em um agente com [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.  |




## <a name="next-steps"></a>Próximas etapas
* Instalar Olá [solução de gerenciamento de alertas](log-analytics-solution-alert-management.md) tooanalyze alertas criadas na análise de Log junto com alertas coletados do System Center Operations Manager (SCOM).
* Leia mais sobre [pesquisas de log](log-analytics-log-searches.md) que podem gerar alertas.
* Conclua um passo a passo para [configurar um webhook](log-analytics-alerts-webhooks.md) com uma regra de alerta.  
* Saiba como toowrite [runbooks na automação do Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemas identificados por alertas.

