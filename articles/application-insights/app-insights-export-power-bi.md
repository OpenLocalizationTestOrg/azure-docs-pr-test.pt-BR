---
title: aaaExport tooPower BI do Application Insights | Microsoft Docs
description: As consultas do Analytics podem ser exibidas no Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Alimentar o Power BI do Application Insights
O [Power BI](http://www.powerbi.com/) é um conjunto de ferramentas de análise de negócios que ajudam a analisar dados e a compartilhar informações. Painéis avançados estão disponíveis em cada dispositivo. Você pode combinar dados de várias fontes, incluindo consultas do Analytics do [Azure Application Insights](app-insights-overview.md).

Há três métodos recomendados de exportação tooPower de dados do Application Insights BI. Você pode usá-los separadamente ou em conjunto.

* [**Adaptador do Power BI**](#power-pi-adapter) -configure um painel completo de telemetria do seu aplicativo. conjunto de saudação de gráficos é predefinido, mas você pode adicionar suas próprias consultas de outras fontes.
* [**Exportar as consultas analíticas** ](#export-analytics-queries) -gravar qualquer consulta desejado usando a análise e exportá-lo tooPower BI. Você pode colocar essa consulta em um painel com outros dados.
* [**A exportação contínua e análise de fluxo** ](app-insights-export-stream-analytics.md) -isso envolve mais tooset de trabalho para cima. É útil se você quiser tookeep seus dados por longos períodos. Caso contrário, hello outros métodos são recomendados.

## <a name="power-bi-adapter"></a>Adaptador do Power BI
Esse método cria um painel completo de telemetria para você. o conjunto de dados inicial Olá é predefinido, mas você pode adicionar mais tooit de dados.

### <a name="get-hello-adapter"></a>Obter adaptador Olá
1. Entrar muito[Power BI](https://app.powerbi.com/).
2. Abra **Obter Dados**, **Serviços**, **Application Insights**
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Forneça detalhes de saudação do recurso do Application Insights.
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Aguarde um minuto ou dois para Olá toobe de dados importado.
   
    ![Adaptador do Power BI](./media/app-insights-export-power-bi/010.png)

Você pode editar o painel hello, a combinação de gráficos do Application Insights Olá com as outras fontes e com consultas de análise. Há uma galeria de visualização onde você pode obter mais gráficos e cada um deles possui parâmetros que podem ser definidos.

Após a importação inicial hello, painel hello e relatórios Olá continuar tooupdate diariamente. Você pode controlar o agendamento de atualização de Olá Olá conjunto de dados.

## <a name="export-analytics-queries"></a>Exportar consultas do Analytics
Ela permite que você toowrite qualquer análise de consulta que você deseja e, em seguida, exportar esse painel do Power BI tooa. (Você pode adicionar toohello painel criado pelo adaptador hello.)

### <a name="one-time-install-power-bi-desktop"></a>Uma vez: instalar o Power BI Desktop
tooimport consulta Application Insights, você usar a versão de área de trabalho de saudação do Power BI. Mas, em seguida, você poderá publicá-lo toohello web ou tooyour o espaço de trabalho do Power BI nuvem. 

Instalar o [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Exportar uma consulta do Analytics
1. [Abra o Analytics e escreva sua consulta](app-insights-analytics-tour.md).
2. Teste e ajuste a consulta Olá até que você estiver satisfeito com os resultados de saudação.

   **Verifique se essa consulta Olá é executado corretamente em análise antes de exportá-lo.**
3. Em Olá **exportar** menu, escolha **Power BI (M)**. Salve o arquivo de texto de saudação.
   
    ![Exportar a consulta do Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. No Power BI Desktop, selecione **obter dados, a consulta em branco** e, em seguida, em Olá editor de consultas, em **exibição** selecione **Editor de consulta avançada**.

    Colar hello exportada linguagem M script no hello Editor de consulta avançada.

    ![Editor avançado de consultas](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Você pode ter tooprovide credenciais tooallow Power BI tooaccess do Azure. Use 'conta organizacional' toosign com sua conta da Microsoft.
   
    ![Forneça as credenciais do Azure tooenable Power BI toorun sua consulta Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Se você precisar de credenciais de saudação tooverify, use comando de menu de configurações de fonte de dados Olá no hello Editor de consultas. Tome cuidado credenciais de saudação toospecify usadas para o Azure, que pode ser diferente das suas credenciais para o Power BI.)
2. Escolha uma visualização da consulta e selecionar campos de saudação para o eixo x, y e segmentando a dimensão.
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Publica seu espaço de trabalho de nuvem do relatório tooyour Power BI. A partir daí, você pode inserir uma versão sincronizada em outras páginas da Web.
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Atualizar relatório Olá manualmente em intervalos ou configurar uma atualização agendada na página de opções de saudação.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="401-or-403-unauthorized"></a>401 ou 403 Não Autorizado 
Isso pode acontecer se o token de atualização não foi atualizado. Tente tooensure essas etapas que você ainda terá acesso. Se você tem acesso e credenciais de saudação refershing não funcionar, abra um tíquete de suporte.

1. Faça logon no hello Portal do Azure e certificar-se de que você pode acessar o recurso de saudação
2. Tente toorefresh credenciais Olá Olá painel

### <a name="502-bad-gateway"></a>502 Gateway Incorreto
Isso geralmente é causado por uma Consulta de análise que retorna um número de dados excessivo. Você deve tentar usar um intervalo de tempo menor ou usando Olá [atrás](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) funciona apenas [projeto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Olá campos necessários.

Se reduzir Olá de conjunto de dados provenientes de consulta de análise de saudação não atender às suas necessidades considere usar Olá [API](https://dev.applicationinsights.io/documentation/overview) toopull um conjunto de dados maior. Aqui estão as instruções sobre como tooconvert Olá consulta M exportar Olá toouse API.

1. Criar uma [chave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Saudação de atualização script M do Power BI que você exportou da análise, substituindo Olá ARM URL com a API do AI (veja o exemplo abaixo)
   * Substituir **https://management.azure.com/subscriptions/...**
   * por **https://api.applicationinsights.io/beta/apps/...**
3. Finalmente, atualizar credenciais toobasic e usar sua chave de API
  

**Script existente**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Script atualizado**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Sobre amostragem
Se seu aplicativo envia um lote de dados, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria. Olá que mesmo é verdadeiro se você tiver configurado o amostragem manualmente no hello SDK ou na inclusão. [Saiba mais sobre amostragem.](app-insights-sampling.md)


## <a name="next-steps"></a>Próximas etapas
* [Power BI - Saiba mais](http://www.powerbi.com/learning/)
* [Tutorial do Analytics](app-insights-analytics-tour.md)

