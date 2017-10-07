---
title: aaaView dados de aplicativo do Azure Application Insights | Microsoft Docs
description: "Você pode usar os problemas de desempenho do hello Application Insights Connector solução toodiagnose e entender o que os usuários fazem com seu aplicativo quando monitorados com o Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Solução Conector do Application Insights (Versão Prévia) no OMS (Operations Management Suite)

![Símbolo do Application Insights](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Olá solução aplicativos Insights Connector ajuda a diagnosticar problemas de desempenho e entender o que os usuários fazem com que seu aplicativo quando ele é monitorado com [Application Insights](../application-insights/app-insights-overview.md). Exibições de saudação telemetria de aplicativo mesmo que os desenvolvedores ver no Application Insights estão disponíveis no OMS. No entanto, ao integrar os aplicativos do Application Insights ao OMS, a visibilidade dos aplicativos aumenta, pois os dados do aplicativo e da operação ficam em um único lugar. Tendo Olá mesmo exibições ajuda toocollaborate com os desenvolvedores de aplicativo. modos de exibição comuns Olá podem ajudar a reduzir Olá tempo toodetect e resolver problemas de plataforma e de aplicativo.

Quando você usar a solução de Olá, você pode:

- Exibir todos os aplicativos do Application Insights em um único lugar, mesmo quando eles estiverem em assinaturas diferentes do Azure
- Correlacionar os dados da infraestrutura com os dados do aplicativo
- Visualizar os dados do aplicativo com perspectivas na pesquisa de logs
- Tabela dinâmica de análise de Log dados tooyour Application Insights app Olá OMS e portais do Azure

## <a name="connected-sources"></a>Fontes conectadas

Ao contrário da maioria das outras soluções de análise de Log, os dados não estão coletados para Olá Application Insights Connector pelos agentes. Todos os dados usados pela solução de saudação vem diretamente do Azure.

| Fonte Conectada | Suportado | Descrição |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não | solução de saudação não coletará informações de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | solução de saudação não coletará informações de agentes do Linux. |
| [Grupo de gerenciamento do SCOM](log-analytics-om-agents.md) | Não | solução de saudação não coletará informações de agentes em um grupo de gerenciamento do SCOM conectado. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | é a solução de saudação não coleção de informações do armazenamento do Azure. |

## <a name="prerequisites"></a>Pré-requisitos

- tooaccess informações do Application Insights Connector, você deve ter uma assinatura do Azure
- É necessário ter, pelo menos, um recurso do Application Insights configurado.
- Você deve ser o proprietário de saudação ou colaborador da saudação recurso do Application Insights.

## <a name="configuration"></a>Configuração

1. Habilitar a solução de análise de aplicativos da Web do Azure de saudação do hello [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. No portal do OMS hello, clique em **configurações** &gt; **dados** &gt; **Application Insights**.
3. Em **Selecionar uma assinatura**, selecione uma assinatura que tem os recursos do Application Insights e, em seguida, em **Nome do Aplicativo**, selecione um ou mais aplicativos.
4. Clique em **Salvar**.

Em aproximadamente 30 minutos, os dados ficarão disponíveis e Olá lado a lado do Application Insights está atualizado com dados, como Olá a imagem a seguir:

![Bloco do Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Tookeep outros pontos em mente:

- Só é possível vincular o espaço de trabalho do Application Insights aplicativos tooone OMS.
- Só é possível vincular [recursos padrão ou Premium Application Insights](https://azure.microsoft.com/pricing/details/application-insights) tooOMS análise de Log. No entanto, você pode usar a camada gratuita Olá da análise de Log.

## <a name="management-packs"></a>Pacotes de gerenciamento

Essa solução não instala nenhum pacote de gerenciamento nos grupos de gerenciamento conectados.

## <a name="use-hello-solution"></a>Usar solução Olá

Olá seções a seguir descrevem como você pode usar folhas de saudação mostradas a saudação do Application Insights painel tooview e interagir com os dados de seus aplicativos.

### <a name="view-application-insights-connector-information"></a>Exibir informações do Conector do Application Insights

Clique em Olá **Application Insights** bloco tooopen Olá **Application Insights** saudação do painel toosee folhas a seguir.

![Painel do Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Painel do Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

Painel de saudação inclui folhas Olá mostradas na tabela de saudação. Cada folha lista os itens too10 correspondência critérios da folha de saudação especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que retorna todos os registros de quando você clica em **ver todos os** na parte inferior da folha de saudação ou quando você clica em cabeçalho de folha de saudação do hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Coluna** | **Descrição** |
| --- | --- |
| Aplicativos – Número de aplicativos | Mostra o número de saudação de aplicativos em recursos do aplicativo. Também lista aplicativo nomes e para cada um, Olá contagem de registros do aplicativo. Clique em toorun número Olá uma pesquisa de log para<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Clique em um nome de aplicativo toorun uma pesquisa de log de aplicativo hello que mostra os registros de aplicativos por host, registros por tipo de telemetria e todos os dados por tipo (com base em Olá último dia). |
| Volume de Dados – hosts que enviam os dados | Mostra o número de saudação de hosts do computador que está enviando dados. Também lista os hosts do computador e a contagem de registros de cada host. Clique em toorun número Olá uma pesquisa de log para<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Clique em um toorun de nome de computador uma pesquisa de log para o host de saudação que mostra os registros de aplicativos por host, registros por tipo de telemetria e todos os dados por tipo (com base em Olá último dia). |
| Disponibilidade – resultados do teste na Web | Mostra um gráfico de rosca dos resultados de teste na Web, indicando aprovação ou reprovação. Clique em Olá gráfico toorun uma pesquisa de log para<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Resultados mostram o número de saudação de passagens e falhas de todos os testes. Ele mostra todos os aplicativos Web com tráfego Olá último minuto. Clique em um tooview de nome do aplicativo uma pesquisa de log, mostrando os detalhes de testes da web com falha. |
| Solicitações do Servidor – solicitações por hora | Mostra um gráfico de linha de saudação solicitações por hora para vários aplicativos de servidor. Passe o mouse sobre uma linha em aplicativos Olá gráfico toosee Olá 3 principais receber solicitações para um ponto no tempo. Também mostra uma lista de aplicativos Olá receber solicitações e número de saudação de solicitações por período de saudação selecionado. <br><br>Clique em Olá gráfico toorun uma pesquisa de log para <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que mostra um gráfico de linhas mais detalhado de saudação solicitações por hora para vários aplicativos de servidor. <br><br> Clique em um aplicativo hello lista toorun uma pesquisa de log para <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> que mostra uma lista de solicitações, gráficos para solicitações pela duração de tempo e a solicitação e uma lista de solicitação de códigos de resposta.   |
| Falhas – solicitações com falha por hora | Mostra um gráfico de linhas das solicitações de aplicativo com falha por hora. Passe o mouse sobre Olá gráfico toosee Olá maiores 3 aplicativos com solicitações com falha para um ponto no tempo. Também mostra uma lista de aplicativos com o número de saudação de solicitações com falha para cada um. Clique em Olá gráfico toorun uma pesquisa de log para <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que mostra um gráfico de linhas mais detalhado de solicitações de aplicativo com falha. <br><br>Clique em um item no hello lista toorun uma pesquisa de log para <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> que mostra solicitações com falha, gráficos de falha nas solicitações em uma lista de códigos de resposta de solicitação com falha e a duração de tempo e a solicitação. |
| Exceções – exceções por hora | Mostra um gráfico de linhas das exceções por hora. Passe o mouse sobre Olá gráfico toosee Olá maiores 3 aplicativos com exceções para um ponto no tempo. Também mostra uma lista de aplicativos com o número de saudação de exceções para cada um. Clique em Olá gráfico toorun uma pesquisa de log para <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que mostra um gráfico de link mais detalhado de exceções. <br><br>Clique em um item no hello lista toorun uma pesquisa de log para <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> que mostra uma lista de exceções, gráficos de exceções em solicitações com falha e tempo e uma lista de tipos de exceção.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Exibir a perspectiva do Application Insights Olá com pesquisa de log

Quando você clicar em qualquer item no painel de saudação, você verá uma perspectiva do Application Insights mostrada na pesquisa. perspectiva de saudação fornece uma visualização estendida, com base no tipo de telemetria de saudação selecionado. Portanto, o conteúdo de visualização muda para tipos diferentes de telemetria.

Quando você clica em qualquer lugar na folha de aplicativos hello, você vê padrão Olá **aplicativos** perspectiva.

![Perspectiva de Aplicativos do Application Insights](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

perspectiva de saudação mostra uma visão geral do aplicativo hello que você selecionou.

Olá **disponibilidade** folha mostra uma exibição de perspectiva diferente onde você pode ver os resultados de teste da web e solicitações com falha relacionadas.

![Perspectiva de Disponibilidade do Application Insights](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Quando você clica em qualquer lugar no hello **solicitações de servidor** ou **falhas** folhas, perspectiva Olá componentes alterar toogive você uma visualização que relacionadas toorequests.

![Folha Falhas do Application Insights](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Quando você clica em qualquer lugar no hello **exceções** folha, você verá uma visualização personalizada tooexceptions.

![Folha Exceções do Application Insights](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Independentemente se você clicar em algo uma saudação **Application Insights Connector** painel dentro de saudação **pesquisa** página em si, qualquer consulta que retorna dados do Application Insights mostram Olá Perspectiva de informações do aplicativo. Por exemplo, se você estiver exibindo dados do Application Insights, um **&#42;** consulta também mostra a guia de perspectiva hello como Olá a imagem a seguir:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Componentes de perspectiva são atualizados dependendo da consulta de pesquisa de saudação. Isso significa que você pode filtrar os resultados de saudação usando qualquer campo de pesquisa que fornece Olá capacidade toosee Olá dados de:

- Todos os aplicativos
- Um único aplicativo selecionado
- Um grupo de aplicativos

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Pivot tooan aplicativo hello portal do Azure

Folhas de conector do Insights do aplicativo são projetada tooenable toohello do toopivot selecionado aplicativo Application Insights *quando você usar o portal do OMS Olá*. Você pode usar a solução hello como uma plataforma de monitoramento de alto nível que ajuda você a solucionar problemas de um aplicativo. Quando você vir um problema potencial em qualquer um dos seus aplicativos conectados, você pode o drill na pesquisa do OMS ou você pode dinamizar diretamente toohello Application Insights aplicativo.

toopivot, clique nas reticências da saudação (**...** ) que aparece no final da saudação de cada linha e selecione **aberto no Application Insights**.

>[!NOTE]
>**Abrir no Application Insights** não está disponível no portal do Azure de saudação.

![Abrir no Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Dados corrigido por amostra

Application Insights fornece  *[amostragem correção](../application-insights/app-insights-sampling.md)*  toohelp reduzir o tráfego de telemetria. Quando você habilita a amostragem no aplicativo do Application Insights, você obtém um número reduzido de entradas armazenadas no Application Insights e no OMS. Enquanto a consistência dos dados é preservada na Olá **Application Insights Connector** página e perspectivas, você deverá corrigir manualmente os dados de amostra para consultas personalizadas.

Este é um exemplo de correção de amostragem em uma consulta da pesquisa de logs:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Olá **contagem de amostra** campo está presente em todas as entradas e mostra o número de pontos de dados que representa a entrada de saudação de hello. Se você ativar a amostragem no aplicativo do Application Insights, a **Contagem Amostrada** será maior que 1. toocount Olá número real de entradas que seu aplicativo gera, Olá soma **contagem de amostra** campos.

Amostragem afeta apenas Olá número total de entradas que gera seu aplicativo. Você não precisa toocorrect de amostragem para campos de métrica como **RequestDuration** ou **AvailabilityDuration** porque esses campos aparecem média Olá para entradas representadas.

## <a name="input-data"></a>Dados de entrada

solução de saudação recebe Olá a seguir os tipos de dados de telemetria de seus aplicativos conectados do Application Insights:

- Disponibilidade
- Exceções
- Solicitações
- Exibições de página de modos de exibição de página – para tooreceive seu espaço de trabalho, você deve configurar seu toocollect aplicativos essas informações. Para obter mais informações, consulte [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Eventos personalizados – para seu espaço de trabalho tooreceive os eventos personalizados, você deve configurar seu toocollect aplicativos essas informações. Para obter mais informações, consulte [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

Os dados são recebidos pelo OMS por meio do Application Insights assim que estiverem disponíveis.

## <a name="output-data"></a>Dados de saída

Um registro com um *tipo* de *ApplicationInsights* é criado para cada tipo de dados de entrada. ApplicationInsights registros tem propriedades mostradas na Olá seções a seguir:

### <a name="generic-fields"></a>Campos genéricos

| Propriedade | Descrição |
| --- | --- |
| Tipo | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Hora do registro de saudação |
| ApplicationId | Chave de instrumentação do aplicativo do Application Insights Olá |
| ApplicationName | Nome do aplicativo do Application Insights Olá |
| RoleInstance | ID do host do servidor |
| DeviceType | Dispositivo de cliente |
| ScreenResolution |   |
| Continente | Continente que originou a solicitação de saudação |
| País | País que originou a solicitação de saudação |
| Província | Província, estado, ou a localidade onde Olá solicitação se originou |
| City | Cidade que originou a solicitação de saudação |
| isSynthetic | Indica se a solicitação de saudação foi criada por um usuário ou pelo método automatizado. True = gerado pelo usuário ou false = método automatizado |
| SamplingRate | Porcentagem de telemetria gerada por Olá SDK enviada tooportal. Intervalo 0.0-100.0. |
| SampledCount | 100/(SamplingRate). Por exemplo, 4 =&gt; 25% |
| IsAuthenticated | Verdadeiro ou falso |
| OperationID | Itens que têm Olá a mesma ID de operação são mostrados como itens relacionados no portal de saudação. ID da solicitação geralmente Olá |
| ParentOperationID | ID da operação de pai Olá |
| OperationName |   |
| SessionId | GUID toouniquely identificar a sessão de saudação em que a solicitação de saudação foi criada |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Campos específicos à disponibilidade

| Propriedade | Descrição |
| --- | --- |
| TelemetryType | Disponibilidade |
| AvailabilityTestName | Nome do teste da web de saudação |
| AvailabilityRunLocation | Origem geográfica da solicitação HTTP |
| AvailabilityResult | Indica o resultado de êxito de saudação do teste da web de saudação |
| AvailabilityMessage | mensagem de saudação anexado toohello de teste na web |
| AvailabilityCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| DataSizeMetricValue | 1.0 ou 0.0 |
| DataSizeMetricCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| AvailabilityDuration | Tempo, em milissegundos, de duração do teste da web hello |
| AvailabilityDurationCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | GUID exclusivo para o teste de web Olá |
| AvailabilityTimestamp | Carimbo de hora preciso do teste de disponibilidade Olá |
| AvailabilityDurationMin | Para registros de amostrados, este campo mostra a duração do teste Olá web mínimo (em milissegundos) Olá representado para pontos de dados |
| AvailabilityDurationMax | Para registros de amostrados, este campo mostra a duração do teste Olá web máximo (em milissegundos) Olá representado para pontos de dados |
| AvailabilityDurationStdDev | Para registros de amostrados, este campo mostra o desvio padrão de saudação entre todas as durações de teste de web (milissegundos) Olá representado para pontos de dados |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Campos específicos à exceção

| Tipo | ApplicationInsights |
| --- | --- |
| TelemetryType | Exceção |
| ExceptionType | Tipo de exceção de saudação |
| ExceptionMethod | método Hello que cria Olá exceção |
| ExceptionAssembly | Assembly inclui o framework hello e versão, bem como o token de chave pública Olá |
| ExceptionGroup | Tipo de exceção de saudação |
| ExceptionHandledAt | Indica o nível de saudação que tratou Olá exceção |
| ExceptionCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| ExceptionMessage | Mensagem de exceção Olá |
| ExceptionStack | Pilha completos de exceção Olá |
| ExceptionHasStack | Verdadeiro, se a exceção tiver uma pilha |



### <a name="request-specific-fields"></a>Campos específicos à solicitação

| Propriedade | Descrição |
| --- | --- |
| Tipo | ApplicationInsights |
| TelemetryType | Solicitação |
| ResponseCode | Tooclient de resposta enviada de HTTP |
| RequestSuccess | Indica êxito ou falha. Verdadeiro ou falso. |
| RequestID | ID toouniquely identificar solicitação Olá |
| RequestName | GET/POST + URL base |
| RequestDuration | Tempo, em segundos, de duração de solicitação Olá |
| URL | URL de solicitação de saudação não incluindo host |
| Host | Host do servidor Web |
| URLBase | URL completa da solicitação de saudação |
| ApplicationProtocol | Tipo de protocolo usado pelo aplicativo hello |
| RequestCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| RequestDurationCount | 100/(Taxa de Amostragem). Por exemplo, 4 =&gt; 25% |
| RequestDurationMin | Para registros de amostrados, este campo mostra a duração (milissegundos) do solicitações mínimas Olá Olá representado para pontos de dados. |
| RequestDurationMax | Para registros de amostrados, este campo mostra a duração (milissegundos) do máximo de solicitação Olá Olá representado para pontos de dados |
| RequestDurationStdDev | Para registros de amostrados, este campo mostra o desvio padrão de saudação entre todas as durações de solicitação (milissegundos) Olá representado para pontos de dados |

## <a name="sample-log-searches"></a>Pesquisas de log de exemplo

Essa solução não tem um conjunto de pesquisas de log de exemplo mostrado no painel de saudação. No entanto, as consultas de pesquisa de log de exemplo com descrições são mostradas na Olá [informações de exibição Application Insights Connector](#view-application-insights-connector-information) seção.

## <a name="next-steps"></a>Próximas etapas

- Use [pesquisa de Log](log-analytics-log-searches.md) tooview informações detalhadas para seus aplicativos do Application Insights.
