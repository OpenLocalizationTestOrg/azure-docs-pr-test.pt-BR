---
title: "Perguntas frequentes sobre a pesquisa de log nova análise aaaLog | Microsoft Docs"
description: "Este artigo fornece as perguntas frequentes sobre atualização de saudação de análise de Log toohello nova linguagem de consulta."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Perguntas frequentes e problemas conhecidos sobre a nova pesquisa de logs do Log Analytics

Este artigo inclui perguntas frequentes e problemas conhecidos sobre atualização de saudação do [toohello de análise de logs nova linguagem de consulta](log-analytics-log-search-upgrade.md).  Você deve ler todo este artigo antes de fazer Olá decisão tooupgrade seu espaço de trabalho.


## <a name="alerts"></a>Alertas

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Pergunta: Tenho várias regras de alerta. É necessário toocreate-los novamente em Olá novo idioma depois de atualizar?  
Não, suas regras de alerta são automaticamente convertidos toohello nova linguagem de pesquisa durante a atualização.  


## <a name="computer-groups"></a>Grupos de computadores

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Pergunta: Estou recebendo erros durante a tentativa de toouse grupos de computadores.  A sintaxe deles mudou?
Sim, sintaxe de saudação para usar o computador agrupa as alterações ao seu espaço de trabalho é atualizado.  Consulte [Grupos de computadores em pesquisas de logs do Log Analytics](log-analytics-computer-groups.md) para obter detalhes.

### <a name="known-issue-groups-imported-from-active-directory"></a>Problema conhecido: grupos importados do Active Directory
No momento, não é possível criar uma consulta que usa um grupo de computadores importado do Active Directory.  Como uma solução alternativa até que esse problema seja corrigido, criar um novo grupo de computadores usando o grupo do Active Directory Olá importado e, em seguida, usar esse novo grupo na consulta.

Uma consulta de exemplo toocreate um novo grupo de computadores que inclui um grupo do Active Directory importado é da seguinte maneira:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Painéis

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Pergunta: Ainda posso usar painéis em um espaço de trabalho atualizado?
Você pode continuar toouse qualquer blocos que você adicionou muito**meu painel** antes de seu espaço de trabalho foi atualizado, mas você não pode editar esses blocos ou adicionar novos.  Você pode continuar toocreate e editar modos de exibição com [View Designer](log-analytics-view-designer.md) e também criar painéis no hello portal do Azure.


## <a name="log-searches"></a>Pesquisas de log

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Pergunta: Tenho pesquisas salvas fora de meu espaço de trabalho atualizado. Pode convertê-los toohello nova linguagem de pesquisa automaticamente?
Você pode usar a ferramenta de conversão de linguagem Olá em tooconvert de página de pesquisa de log de saudação cada um.  Não há nenhuma conversão de tooautomatically método várias pesquisas sem atualizar o espaço de trabalho de saudação.

### <a name="question-why-are-my-query-results-not-sorted"></a>Pergunta: Por que os resultados de minha consulta não são classificados?
Não, os resultados são classificados por padrão na nova linguagem de consulta hello.  Saudação de uso [operador sort](https://go.microsoft.com/fwlink/?linkid=856079) toosort os resultados por uma ou mais propriedades.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Problema conhecido: os resultados da pesquisa em uma lista podem incluir propriedades sem dados
Os resultados da pesquisa de logs em uma lista podem exibir propriedades sem dados.  Tooupgrade anterior, essas propriedades não serão incluídas.  Esse problema será corrigido para que propriedades vazias não sejam exibidas.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Problema conhecido: a seleção de um valor em um gráfico não exibe resultados detalhados
Tooupgrade anterior, quando você selecionar um valor em um gráfico, ele retornará uma lista detalhada dos registros de correspondência do valor de saudação selecionada.  Após a atualização, apenas Olá resumidos linha é retornada.  Esse problema está sendo investigado no momento.

## <a name="log-search-api"></a>API da Pesquisa de Log

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Pergunta: Olá API de pesquisa de Log for atualizado depois de atualizar?
Olá [API de pesquisa de Log](log-analytics-log-search-api.md) ainda não foi atualizado toohello nova linguagem de pesquisa.  Continue a linguagem de consulta herdados Olá toouse com essa API, mesmo depois que você atualizar seu espaço de trabalho.  Documentação atualizada ficarão disponível para Olá API de pesquisa de Log quando ele for atualizado.


## <a name="portals"></a>Portais

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Pergunta: Devo usar Olá novo portal de análise avançada ou continuar a usar o portal de pesquisa de Log Olá?
Você pode ver uma comparação de portais Olá dois em [portais para a criação e edição de consultas de log no Azure Log Analytics](log-analytics-log-search-portals.md).  Cada um tem vantagens distintas assim você pode escolher Olá uma melhor para suas necessidades.  É consultas comuns de toowrite no portal do Advanced Analytics hello e colá-los em outros lugares, como o Designer de exibição.  Você deve ler sobre [problemas tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) quando fazer isso.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Pergunta: alguma coisa muda com a integração do PowerBI?
Sim.  Depois que seu espaço de trabalho tiver sido atualizado, em seguida, processo Olá para exportar dados de análise de Log tooPower BI deixarão de funcionar.  Todas as agendas existentes criadas antes da atualização serão desabilitadas.  Após a atualização, usa a análise de Log do Azure Olá mesma plataforma como o Application Insights e usar Olá mesmo processo tooPower de consultas de análise de Log tooexport BI como [tooexport de processo de saudação do Application Insights consultas tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Problema conhecido: limite de tamanho de solicitação do Power BI
Atualmente, há um limite de tamanho de 8 MB para uma consulta de análise de Log que pode ser exportado tooPower BI.  Esse limite será aumentado em breve.


##<a name="powershell-cmdlets"></a>Cmdlets do PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Pergunta: Cmdlet do PowerShell de pesquisa de Log de saudação for atualizado depois de atualizar?
Olá [AzureRmOperationalInsightsSearchResults Get](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) ainda não foi atualizado toohello nova linguagem de pesquisa.  Continue a linguagem de consulta herdados Olá toouse com esse cmdlet, mesmo depois que você atualizar seu espaço de trabalho.  Documentação atualizada ficarão disponível para o cmdlet hello quando ele for atualizado.


## <a name="resource-manager-templates"></a>Modelos do Gerenciador de Recursos

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Pergunta: Posso criar um espaço de trabalho atualizado com um modelo do Resource Manager?
Sim.  Você deve usar uma versão da API de 2017-03-15-visualização e incluir um **recursos** seção em seu modelo, como no exemplo a seguir de saudação.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Soluções

### <a name="question-will-my-solutions-continue-toowork"></a>Pergunta: Meu soluções continuará toowork?
Todas as soluções continuará toowork em um espaço de trabalho atualizado, embora seu desempenho melhorará se eles são convertidos toohello nova linguagem de consulta.  Há problemas conhecidos com algumas soluções existentes que são descritos nesta seção.

### <a name="known-issue-capacity-and-performance-solution"></a>Problema conhecido: solução Capacidade e Desempenho
Algumas das peças Olá Olá [capacidade e desempenho](log-analytics-capacity.md) a exibição pode ser vazia.  Um problema de toothis correção estará disponível em breve.

### <a name="known-issue-device-health-solution"></a>Problema conhecido: solução Integridade do Dispositivo
Olá [solução de integridade do dispositivo](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) não coletará dados em um espaço de trabalho atualizado.  Um problema de toothis correção estará disponível em breve.

### <a name="known-issue-application-insights-connector"></a>Problema conhecido: conector do Application Insights
Atualmente, não há suporte para perspectivas na [solução Conector do Application Insights](log-analytics-app-insights-connector.md) em um espaço de trabalho atualizado.  Um problema de toothis correção está atualmente na análise.

## <a name="upgrade-process"></a>Processo de atualização

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Pergunta: Tenho vários espaços de trabalho. É possível atualizar todos os espaços de trabalho em Olá simultaneamente?  
Não.  Atualização se aplica a tooa único espaço de trabalho cada vez. Atualmente não há nenhuma maneira de atualizar vários espaços de trabalho ao mesmo tempo. Observe que outros usuários do espaço de trabalho Olá atualizado serão afetados também.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Pergunta: os dados de logs existentes coletados em meu espaço de trabalho serão modificados se eu fizer o upgrade?  
Não. pesquisas de espaço de trabalho do Hello log dados tooyour disponível não é afetado pela atualização de saudação. Pesquisas salvas, alertas e modos de exibição serão convertidas toohello nova linguagem de pesquisa automaticamente.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Pergunta: o que acontecerá se eu não fizer o upgrade de meu espaço de trabalho?  
pesquisa de log herdados Hello será substituída em hello em meses. Os espaços de trabalho que não forem atualizados até lá serão atualizados automaticamente.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Pergunta: não escolher tooupgrade, mas o meu espaço de trabalho tiver sido atualizado assim mesmo! O que aconteceu?  
Outro administrador deste espaço de trabalho foi atualizado com espaço de trabalho de saudação. Observe que todos os espaços de trabalho serão atualizados automaticamente quando a nova linguagem de saudação alcança disponibilidade geral.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Pergunta: atualizou por engano e agora precisa toocancel-lo e tudo o que fazer a restauração. O que devo fazer?  
Sem problema.  Criamos um instantâneo do seu espaço de trabalho antes da atualização, então você pode restaurá-lo. Tenha em mente que procura, alertas ou exibições que você salvou após atualização hello serão perdida se.  toorestore seu ambiente de espaço de trabalho, no procedimento a seguir Olá [posso depois de atualizar?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Modos de exibição

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Pergunta: Como fazer para criar uma nova exibição com o Designer de Exibição?
Tooupgrade anterior, você pode criar um novo modo de exibição com o Designer de exibição de um bloco no painel principal hello.  Quando o espaço de trabalho é atualizado, esse bloco é removido.  Você pode criar um novo modo de exibição com o Designer de exibição no portal do OMS Olá clicando no botão no menu esquerdo Olá + Olá verde.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Problema conhecido: a opção Ver tudo em gráficos de linhas nas exibições não resulta em um gráfico de linhas
Quando você clica na Olá *ver todas as* opção na parte inferior de saudação de uma parte do gráfico de linha em uma exibição, você verá uma tabela.  Tooupgrade anterior, você verá um gráfico de linhas.  Esse problema está sendo analisado para uma modificação potencial.


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [atualizar seu espaço de trabalho toohello análise de logs nova linguagem de consulta](log-analytics-log-search-upgrade.md).
