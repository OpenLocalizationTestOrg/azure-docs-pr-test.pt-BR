---
title: Exportar tooSQL do Azure Application Insights | Microsoft Docs
description: "Exporte continuamente tooSQL de dados do Application Insights usando a análise de fluxo."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Passo a passo: Exportar tooSQL do Application Insights usando a análise de fluxo
Este artigo mostra como toomove seus dados de telemetria de [Azure Application Insights] [ start] em um banco de dados do SQL Azure usando [exportação contínua] [ export] e [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). 

A exportação contínua move os dados de telemetria no Armazenamento do Azure no formato JSON. Vamos analisar objetos JSON hello usando o Azure Stream Analytics e criar linhas em uma tabela de banco de dados.

(Mais geralmente, a exportação contínua é Olá maneira toodo sua própria análise de telemetria Olá seus aplicativos enviar tooApplication Insights. Você pode adaptar este toodo de exemplo de código outras coisas com a telemetria hello exportada, como agregação de dados.)

Vamos começar com a suposição de saudação que você já tenha Olá aplicativo deseja toomonitor.

Neste exemplo, vamos usar dados de exibição de página hello, mas hello mesmo padrão pode ser facilmente estendido tooother tipos de dados como exceções e eventos personalizados. 

## <a name="add-application-insights-tooyour-application"></a>Adicionar Application Insights tooyour aplicativo
tooget iniciado:

1. [Configurar o Application Insights para sua página da Web](app-insights-javascript.md). 
   
    (Neste exemplo, vamos nos concentrar no processamento de dados de exibição de página de navegadores de saudação do cliente, mas você pode também definir o Application Insights para o lado do servidor de saudação do seu [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) aplicativo e o processo de solicitação dependência e outra telemetria de servidor.)
2. Publicar seu aplicativo e observar os dados de telemetria que aparecem em seu recurso Application Insights.

## <a name="create-storage-in-azure"></a>Criar armazenamento no Azure
A exportação contínua sempre gera conta de armazenamento do Azure tooan dados, portanto você precisa de armazenamento de saudação toocreate primeiro.

1. Criar uma conta de armazenamento em sua assinatura no hello [portal do Azure][portal].
   
    ![No portal do Azure, escolha Novo, Dados e Armazenamento. Selecione Clássica, escolha Criar. Forneça um nome de armazenamento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Criar um contêiner
   
    ![No novo armazenamento de hello, selecionar contêineres, clique em bloco de contêineres hello e, em seguida, adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Copie a chave de acesso de armazenamento Olá
   
    Você precisará dele em breve tooset o serviço de análise de fluxo de entrada toohello hello.
   
    ![No armazenamento Olá, abra configurações, chaves e faça uma cópia da saudação chave de acesso primária](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Iniciar a exportação contínua tooAzure armazenamento
1. Na Olá portal do Azure, procure o recurso do Application Insights toohello criado para o seu aplicativo.
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Crie uma exportação contínua.
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Selecione a conta de armazenamento de saudação criado anteriormente:

    ![Definir o destino de exportação de saudação](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Defina tipos de evento de saudação desejado toosee:

    ![Escolher os tipos de evento](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Deixe que alguns dados sejam acumulados. Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo. A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md). 
   
    E, além disso, dados de saudação exportará tooyour armazenamento. 
2. Inspecionar dados hello exportada, no portal de saudação - escolha **procurar**, selecione sua conta de armazenamento e, em seguida, **contêineres** - ou no Visual Studio. No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento. (Se você não tiver essa opção de menu, você precisa tooinstall Olá SDK do Azure: Abrir caixa de diálogo de novo projeto hello e abra o Visual C# / nuvem / obter o Microsoft Azure SDK para .NET.)
   
    ![No Visual Studio, abra o Navegador do Servidor, Azure e Armazenamento](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Anote a parte comum Olá Olá do nome do caminho, que é derivada da chave de nome e a instrumentação do aplicativo hello. 

eventos de saudação são gravados tooblob arquivos no formato JSON. Cada arquivo pode conter um ou mais eventos. Portanto, gostaríamos de dados de evento de saudação tooread e filtrar campos Olá que desejamos. Todos os tipos de coisas que podemos fazer com dados hello, mas nosso plano de hoje é toouse do Stream Analytics toomove Olá dados tooa banco de dados SQL. Que será mais fácil toorun muitas consultas interessantes.

## <a name="create-an-azure-sql-database"></a>Criar um Banco de Dados SQL do Azure
Mais uma vez desde a sua assinatura no [portal do Azure][portal], criar banco de dados de saudação (e um novo servidor, a menos que você já tem um) toowhich você escreverá dados saudação.

![Novo, Dados, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Verifique se que esse servidor de banco de dados de saudação permite acesso tooAzure serviços:

![Procurar, servidores, seu servidor, configurações, Firewall, permitir o acesso tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Criar uma tabela no banco de dados do Azure SQL
Conecte-se toohello de banco de dados criado na seção anterior de saudação com sua ferramenta de gerenciamento preferenciais. Neste passo a passo, usaremos as SSMS ( [Ferramentas de Gerenciamento do SQL Server](https://msdn.microsoft.com/ms174173.aspx) ).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Criar uma nova consulta e execute Olá T-SQL a seguir:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

Neste exemplo, estamos usando dados de modos de exibição de página. toosee Olá outros dados disponíveis, inspecione a saída JSON e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Criar uma instância do Azure Stream Analytics
De saudação [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics hello e criar um novo trabalho de análise de fluxo:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Quando o novo trabalho de saudação é criado, expanda os detalhes:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Definir local de blob
Defina-a entrada tootake do seu blob de exportação contínua:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

Agora, você precisará Olá chave de acesso primário da conta de armazenamento, que você anotou anteriormente. Defina como Olá chave da conta de armazenamento.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Definir padrão de prefixo de caminho
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

Também ser Olá de tooset-se de que o formato de data**AAAA-MM-DD** (com **traços**).

saudação padrão de prefixo de caminho Especifica como o Stream Analytics localiza arquivos de entrada hello no armazenamento de saudação. Você precisa tooset-toohow toocorrespond exportação contínua armazena dados saudação. Defina-o assim:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Neste exemplo:

* `webapplication27`é o nome de saudação de saudação recurso do Application Insights, **em letras minúsculas**. 
* `1234...`é a chave de instrumentação de saudação de saudação recurso do Application Insights **traços removido**. 
* `PageViews`Olá tipo de dados que desejamos tooanalyze. tipos disponíveis de saudação dependem de filtro Olá definido na exportação contínua. Examinar outros tipos disponíveis de Olá Olá de toosee dados exportados e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).
* `/{date}/{time}` um padrão escrito literalmente.

nome de saudação tooget iKey do recurso do Application Insights, abrir Essentials na sua página de visão geral e abra as configurações.

#### <a name="finish-initial-setup"></a>Concluir a configuração inicial
Confirme o formato de serialização hello:

![Confirme e feche o assistente](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Fechar o Assistente de saudação e aguarde Olá toocomplete de instalação.

> [!TIP]
> Use Olá toocheck de função de exemplo que você definiu o caminho de entrada hello corretamente. Se ele falhar: verificar se há dados no armazenamento de saudação para intervalo de tempo do exemplo hello escolhido. Editar definição de entrada hello e verificar definir Olá conta de armazenamento, o prefixo de caminho e formato de data corretamente.
> 
> 

## <a name="set-query"></a>Definir a consulta
Abra a seção de consulta hello:

![No Stream Analytics, selecione Consulta](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Substitua a consulta de padrão de saudação com:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Observe que primeiro Olá algumas propriedades são dados de exibição toopage específico. Exportações de outros tipos de telemetria terão propriedades diferentes. Consulte Olá [detalhadas de referência de modelo de dados para tipos de propriedade hello e valores.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Configurar a saída toodatabase
Selecione SQL como saída de hello.

![No Stream Analytics, selecione Saídas](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Especifique o banco de dados SQL hello.

![Preencha os detalhes de saudação do banco de dados](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Feche o Assistente de saudação e aguarde até que uma notificação de que a saída de hello foi configurada.

## <a name="start-processing"></a>Iniciar o processamento
Inicie o trabalho de saudação da barra de ação hello:

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

Você pode escolher se o processamento toostart Olá dados a partir de agora, ou toostart com dados anteriores. Olá este último será útil se você teve a exportação contínua já em execução por algum tempo.

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Depois de alguns minutos, volte tooSQL ferramentas de gerenciamento de servidor e observe Olá dados fluindo em. Por exemplo, use uma consulta como esta:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Artigos relacionados
* [Exportar tooPowerBI usando a análise de fluxo](app-insights-export-power-bi.md)
* [Referência de tipos de propriedade hello e valores do modelo de dados detalhados.](app-insights-export-data-model.md)
* [Exportação Contínua no Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

