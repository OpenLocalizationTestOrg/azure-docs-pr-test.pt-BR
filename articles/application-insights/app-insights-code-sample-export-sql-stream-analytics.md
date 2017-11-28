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
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="1a7db-103">Passo a passo: Exportar tooSQL do Application Insights usando a análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="1a7db-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="1a7db-104">Este artigo mostra como toomove seus dados de telemetria de [Azure Application Insights] [ start] em um banco de dados do SQL Azure usando [exportação contínua] [ export] e [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="1a7db-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="1a7db-105">A exportação contínua move os dados de telemetria no Armazenamento do Azure no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="1a7db-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="1a7db-106">Vamos analisar objetos JSON hello usando o Azure Stream Analytics e criar linhas em uma tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1a7db-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="1a7db-107">(Mais geralmente, a exportação contínua é Olá maneira toodo sua própria análise de telemetria Olá seus aplicativos enviar tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="1a7db-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="1a7db-108">Você pode adaptar este toodo de exemplo de código outras coisas com a telemetria hello exportada, como agregação de dados.)</span><span class="sxs-lookup"><span data-stu-id="1a7db-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="1a7db-109">Vamos começar com a suposição de saudação que você já tenha Olá aplicativo deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="1a7db-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="1a7db-110">Neste exemplo, vamos usar dados de exibição de página hello, mas hello mesmo padrão pode ser facilmente estendido tooother tipos de dados como exceções e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="1a7db-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="1a7db-111">Adicionar Application Insights tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="1a7db-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="1a7db-112">tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="1a7db-112">tooget started:</span></span>

1. <span data-ttu-id="1a7db-113">[Configurar o Application Insights para sua página da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="1a7db-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="1a7db-114">(Neste exemplo, vamos nos concentrar no processamento de dados de exibição de página de navegadores de saudação do cliente, mas você pode também definir o Application Insights para o lado do servidor de saudação do seu [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) aplicativo e o processo de solicitação dependência e outra telemetria de servidor.)</span><span class="sxs-lookup"><span data-stu-id="1a7db-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="1a7db-115">Publicar seu aplicativo e observar os dados de telemetria que aparecem em seu recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a7db-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="1a7db-116">Criar armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="1a7db-116">Create storage in Azure</span></span>
<span data-ttu-id="1a7db-117">A exportação contínua sempre gera conta de armazenamento do Azure tooan dados, portanto você precisa de armazenamento de saudação toocreate primeiro.</span><span class="sxs-lookup"><span data-stu-id="1a7db-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="1a7db-118">Criar uma conta de armazenamento em sua assinatura no hello [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="1a7db-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![No portal do Azure, escolha Novo, Dados e Armazenamento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="1a7db-122">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="1a7db-122">Create a container</span></span>
   
    ![No novo armazenamento de hello, selecionar contêineres, clique em bloco de contêineres hello e, em seguida, adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="1a7db-124">Copie a chave de acesso de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="1a7db-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="1a7db-125">Você precisará dele em breve tooset o serviço de análise de fluxo de entrada toohello hello.</span><span class="sxs-lookup"><span data-stu-id="1a7db-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![No armazenamento Olá, abra configurações, chaves e faça uma cópia da saudação chave de acesso primária](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="1a7db-127">Iniciar a exportação contínua tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="1a7db-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="1a7db-128">Na Olá portal do Azure, procure o recurso do Application Insights toohello criado para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1a7db-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="1a7db-130">Crie uma exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="1a7db-130">Create a continuous export.</span></span>
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="1a7db-132">Selecione a conta de armazenamento de saudação criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1a7db-132">Select hello storage account you created earlier:</span></span>

    ![Definir o destino de exportação de saudação](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="1a7db-134">Defina tipos de evento de saudação desejado toosee:</span><span class="sxs-lookup"><span data-stu-id="1a7db-134">Set hello event types you want toosee:</span></span>

    ![Escolher os tipos de evento](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="1a7db-136">Deixe que alguns dados sejam acumulados.</span><span class="sxs-lookup"><span data-stu-id="1a7db-136">Let some data accumulate.</span></span> <span data-ttu-id="1a7db-137">Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo.</span><span class="sxs-lookup"><span data-stu-id="1a7db-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="1a7db-138">A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1a7db-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="1a7db-139">E, além disso, dados de saudação exportará tooyour armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a7db-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="1a7db-140">Inspecionar dados hello exportada, no portal de saudação - escolha **procurar**, selecione sua conta de armazenamento e, em seguida, **contêineres** - ou no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a7db-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="1a7db-141">No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a7db-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="1a7db-142">(Se você não tiver essa opção de menu, você precisa tooinstall Olá SDK do Azure: Abrir caixa de diálogo de novo projeto hello e abra o Visual C# / nuvem / obter o Microsoft Azure SDK para .NET.)</span><span class="sxs-lookup"><span data-stu-id="1a7db-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![No Visual Studio, abra o Navegador do Servidor, Azure e Armazenamento](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="1a7db-144">Anote a parte comum Olá Olá do nome do caminho, que é derivada da chave de nome e a instrumentação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1a7db-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="1a7db-145">eventos de saudação são gravados tooblob arquivos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="1a7db-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="1a7db-146">Cada arquivo pode conter um ou mais eventos.</span><span class="sxs-lookup"><span data-stu-id="1a7db-146">Each file may contain one or more events.</span></span> <span data-ttu-id="1a7db-147">Portanto, gostaríamos de dados de evento de saudação tooread e filtrar campos Olá que desejamos.</span><span class="sxs-lookup"><span data-stu-id="1a7db-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="1a7db-148">Todos os tipos de coisas que podemos fazer com dados hello, mas nosso plano de hoje é toouse do Stream Analytics toomove Olá dados tooa banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="1a7db-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="1a7db-149">Que será mais fácil toorun muitas consultas interessantes.</span><span class="sxs-lookup"><span data-stu-id="1a7db-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="1a7db-150">Criar um Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1a7db-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="1a7db-151">Mais uma vez desde a sua assinatura no [portal do Azure][portal], criar banco de dados de saudação (e um novo servidor, a menos que você já tem um) toowhich você escreverá dados saudação.</span><span class="sxs-lookup"><span data-stu-id="1a7db-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Novo, Dados, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="1a7db-153">Verifique se que esse servidor de banco de dados de saudação permite acesso tooAzure serviços:</span><span class="sxs-lookup"><span data-stu-id="1a7db-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Procurar, servidores, seu servidor, configurações, Firewall, permitir o acesso tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="1a7db-155">Criar uma tabela no banco de dados do Azure SQL</span><span class="sxs-lookup"><span data-stu-id="1a7db-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="1a7db-156">Conecte-se toohello de banco de dados criado na seção anterior de saudação com sua ferramenta de gerenciamento preferenciais.</span><span class="sxs-lookup"><span data-stu-id="1a7db-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="1a7db-157">Neste passo a passo, usaremos as SSMS ( [Ferramentas de Gerenciamento do SQL Server](https://msdn.microsoft.com/ms174173.aspx) ).</span><span class="sxs-lookup"><span data-stu-id="1a7db-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="1a7db-158">Criar uma nova consulta e execute Olá T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a7db-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="1a7db-159">Neste exemplo, estamos usando dados de modos de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="1a7db-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="1a7db-160">toosee Olá outros dados disponíveis, inspecione a saída JSON e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="1a7db-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="1a7db-161">Criar uma instância do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a7db-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="1a7db-162">De saudação [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics hello e criar um novo trabalho de análise de fluxo:</span><span class="sxs-lookup"><span data-stu-id="1a7db-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="1a7db-163">Quando o novo trabalho de saudação é criado, expanda os detalhes:</span><span class="sxs-lookup"><span data-stu-id="1a7db-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="1a7db-164">Definir local de blob</span><span class="sxs-lookup"><span data-stu-id="1a7db-164">Set blob location</span></span>
<span data-ttu-id="1a7db-165">Defina-a entrada tootake do seu blob de exportação contínua:</span><span class="sxs-lookup"><span data-stu-id="1a7db-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="1a7db-166">Agora, você precisará Olá chave de acesso primário da conta de armazenamento, que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1a7db-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="1a7db-167">Defina como Olá chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a7db-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="1a7db-168">Definir padrão de prefixo de caminho</span><span class="sxs-lookup"><span data-stu-id="1a7db-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="1a7db-169">Também ser Olá de tooset-se de que o formato de data**AAAA-MM-DD** (com **traços**).</span><span class="sxs-lookup"><span data-stu-id="1a7db-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="1a7db-170">saudação padrão de prefixo de caminho Especifica como o Stream Analytics localiza arquivos de entrada hello no armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a7db-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="1a7db-171">Você precisa tooset-toohow toocorrespond exportação contínua armazena dados saudação.</span><span class="sxs-lookup"><span data-stu-id="1a7db-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="1a7db-172">Defina-o assim:</span><span class="sxs-lookup"><span data-stu-id="1a7db-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="1a7db-173">Neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="1a7db-173">In this example:</span></span>

* <span data-ttu-id="1a7db-174">`webapplication27`é o nome de saudação de saudação recurso do Application Insights, **em letras minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="1a7db-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="1a7db-175">`1234...`é a chave de instrumentação de saudação de saudação recurso do Application Insights **traços removido**.</span><span class="sxs-lookup"><span data-stu-id="1a7db-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="1a7db-176">`PageViews`Olá tipo de dados que desejamos tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="1a7db-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="1a7db-177">tipos disponíveis de saudação dependem de filtro Olá definido na exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="1a7db-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="1a7db-178">Examinar outros tipos disponíveis de Olá Olá de toosee dados exportados e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="1a7db-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="1a7db-179">`/{date}/{time}` um padrão escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="1a7db-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="1a7db-180">nome de saudação tooget iKey do recurso do Application Insights, abrir Essentials na sua página de visão geral e abra as configurações.</span><span class="sxs-lookup"><span data-stu-id="1a7db-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="1a7db-181">Concluir a configuração inicial</span><span class="sxs-lookup"><span data-stu-id="1a7db-181">Finish initial setup</span></span>
<span data-ttu-id="1a7db-182">Confirme o formato de serialização hello:</span><span class="sxs-lookup"><span data-stu-id="1a7db-182">Confirm hello serialization format:</span></span>

![Confirme e feche o assistente](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="1a7db-184">Fechar o Assistente de saudação e aguarde Olá toocomplete de instalação.</span><span class="sxs-lookup"><span data-stu-id="1a7db-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="1a7db-185">Use Olá toocheck de função de exemplo que você definiu o caminho de entrada hello corretamente.</span><span class="sxs-lookup"><span data-stu-id="1a7db-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="1a7db-186">Se ele falhar: verificar se há dados no armazenamento de saudação para intervalo de tempo do exemplo hello escolhido.</span><span class="sxs-lookup"><span data-stu-id="1a7db-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="1a7db-187">Editar definição de entrada hello e verificar definir Olá conta de armazenamento, o prefixo de caminho e formato de data corretamente.</span><span class="sxs-lookup"><span data-stu-id="1a7db-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="1a7db-188">Definir a consulta</span><span class="sxs-lookup"><span data-stu-id="1a7db-188">Set query</span></span>
<span data-ttu-id="1a7db-189">Abra a seção de consulta hello:</span><span class="sxs-lookup"><span data-stu-id="1a7db-189">Open hello query section:</span></span>

![No Stream Analytics, selecione Consulta](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="1a7db-191">Substitua a consulta de padrão de saudação com:</span><span class="sxs-lookup"><span data-stu-id="1a7db-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="1a7db-192">Observe que primeiro Olá algumas propriedades são dados de exibição toopage específico.</span><span class="sxs-lookup"><span data-stu-id="1a7db-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="1a7db-193">Exportações de outros tipos de telemetria terão propriedades diferentes.</span><span class="sxs-lookup"><span data-stu-id="1a7db-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="1a7db-194">Consulte Olá [detalhadas de referência de modelo de dados para tipos de propriedade hello e valores.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="1a7db-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="1a7db-195">Configurar a saída toodatabase</span><span class="sxs-lookup"><span data-stu-id="1a7db-195">Set up output toodatabase</span></span>
<span data-ttu-id="1a7db-196">Selecione SQL como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="1a7db-196">Select SQL as hello output.</span></span>

![No Stream Analytics, selecione Saídas](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="1a7db-198">Especifique o banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="1a7db-198">Specify hello SQL database.</span></span>

![Preencha os detalhes de saudação do banco de dados](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="1a7db-200">Feche o Assistente de saudação e aguarde até que uma notificação de que a saída de hello foi configurada.</span><span class="sxs-lookup"><span data-stu-id="1a7db-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="1a7db-201">Iniciar o processamento</span><span class="sxs-lookup"><span data-stu-id="1a7db-201">Start processing</span></span>
<span data-ttu-id="1a7db-202">Inicie o trabalho de saudação da barra de ação hello:</span><span class="sxs-lookup"><span data-stu-id="1a7db-202">Start hello job from hello action bar:</span></span>

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="1a7db-204">Você pode escolher se o processamento toostart Olá dados a partir de agora, ou toostart com dados anteriores.</span><span class="sxs-lookup"><span data-stu-id="1a7db-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="1a7db-205">Olá este último será útil se você teve a exportação contínua já em execução por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="1a7db-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="1a7db-207">Depois de alguns minutos, volte tooSQL ferramentas de gerenciamento de servidor e observe Olá dados fluindo em.</span><span class="sxs-lookup"><span data-stu-id="1a7db-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="1a7db-208">Por exemplo, use uma consulta como esta:</span><span class="sxs-lookup"><span data-stu-id="1a7db-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="1a7db-209">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="1a7db-209">Related articles</span></span>
* [<span data-ttu-id="1a7db-210">Exportar tooPowerBI usando a análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="1a7db-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="1a7db-211">Referência de tipos de propriedade hello e valores do modelo de dados detalhados.</span><span class="sxs-lookup"><span data-stu-id="1a7db-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="1a7db-212">Exportação Contínua no Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a7db-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="1a7db-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a7db-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

