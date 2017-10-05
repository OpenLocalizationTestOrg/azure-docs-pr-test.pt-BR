---
title: Exportar para o SQL do Azure Application Insights | Microsoft Docs
description: Exportar dados continuamente do Application Insights para o SQL usando o Stream Analytics
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
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="d3c6e-103">Passo a passo: exportar para SQL do Application Insights usando o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3c6e-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="d3c6e-104">Este artigo mostra como mover os dados de telemetria do [Azure Application Insights][start] em um banco de dados SQL do Azure usando [Exportação Contínua][export] e [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="d3c6e-105">A exportação contínua move os dados de telemetria no Armazenamento do Azure no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="d3c6e-106">Vamos analisar objetos JSON usando o Azure Stream Analytics e criando linhas em uma tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="d3c6e-107">(Normalmente, a Exportação Contínua é a maneira de fazer sua própria análise da telemetria enviada pelos seus aplicativos ao Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="d3c6e-108">Você pode adaptar este exemplo de código para fazer outras coisas com a telemetria exportada, como agregação de dados).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="d3c6e-109">Vamos começar supondo que você já tenha o aplicativo que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="d3c6e-110">Neste exemplo, usaremos os dados de exibição de página, mas o mesmo padrão pode ser facilmente ampliado para outros tipos de dados como exceções e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="d3c6e-111">Adicione o Application Insights ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d3c6e-111">Add Application Insights to your application</span></span>
<span data-ttu-id="d3c6e-112">Introdução:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-112">To get started:</span></span>

1. <span data-ttu-id="d3c6e-113">[Configurar o Application Insights para sua página da Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="d3c6e-114">(Neste exemplo, vamos nos concentrar no processamento de dados de exibição de página de navegadores do cliente, mas você também pode configurar o Application Insights do lado do servidor do seu aplicativo [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) e processar telemetrias de solicitações, dependências e outras telemetrias do servidor.)</span><span class="sxs-lookup"><span data-stu-id="d3c6e-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="d3c6e-115">Publicar seu aplicativo e observar os dados de telemetria que aparecem em seu recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="d3c6e-116">Criar armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="d3c6e-116">Create storage in Azure</span></span>
<span data-ttu-id="d3c6e-117">Exportação contínua sempre gera dados para uma conta de armazenamento do Azure, por isso você precisa primeiro criar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="d3c6e-118">Crie uma conta de armazenamento na sua assinatura do [Portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d3c6e-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![No portal do Azure, escolha Novo, Dados e Armazenamento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="d3c6e-122">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="d3c6e-122">Create a container</span></span>
   
    ![No novo armazenamento, selecione Contêineres, clique no bloco Contêineres e, em seguida, Adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="d3c6e-124">Copie a chave de acesso de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d3c6e-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="d3c6e-125">Você precisará dela em breve para configurar a entrada para o serviço do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![No armazenamento, abra Configurações, Chaves e faça uma cópia da Chave de Acesso Primária](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="d3c6e-127">Iniciar exportação contínua no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d3c6e-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="d3c6e-128">No portal do Azure, navegue até o recurso do Application Insights que você criou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="d3c6e-130">Crie uma exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-130">Create a continuous export.</span></span>
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="d3c6e-132">Selecione a conta de armazenamento criada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-132">Select the storage account you created earlier:</span></span>

    ![Definir o destino de exportação](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="d3c6e-134">Defina os tipos de eventos que você deseja ver:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-134">Set the event types you want to see:</span></span>

    ![Escolher os tipos de evento](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="d3c6e-136">Deixe que alguns dados sejam acumulados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-136">Let some data accumulate.</span></span> <span data-ttu-id="d3c6e-137">Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="d3c6e-138">A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="d3c6e-139">E, além disso, os dados serão exportados para seu armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="d3c6e-140">Inspecione os dados exportados no portal – escolha **Procurar**, selecione sua conta de armazenamento e depois **Contêineres** – ou no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="d3c6e-141">No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="d3c6e-142">(Se você não tiver essa opção de menu, precisará instalar o Azure SDK: abra o diálogo Novo Projeto e abra Visual C#/Nuvem/Obter Microsoft Azure SDK para .NET.)</span><span class="sxs-lookup"><span data-stu-id="d3c6e-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![No Visual Studio, abra o Navegador do Servidor, Azure e Armazenamento](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="d3c6e-144">Anote a parte comum do nome do caminho, que deriva do nome do aplicativo e da chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="d3c6e-145">Os eventos são gravados em arquivos blob formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="d3c6e-146">Cada arquivo pode conter um ou mais eventos.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-146">Each file may contain one or more events.</span></span> <span data-ttu-id="d3c6e-147">Portanto, gostaríamos de escrever um código para ler os dados de evento e filtrar os campos desejados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="d3c6e-148">Podemos fazer todos os tipos de coisas com os dados, mas nosso plano para hoje é escrever um código para mover os dados para um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="d3c6e-149">Isso nos permitirá executar diversas consultas interessantes.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="d3c6e-150">Criar um Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="d3c6e-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="d3c6e-151">Mais uma vez, na sua assinatura no [portal do Azure][portal], crie o banco de dados (e um novo servidor, a menos que você já tenha um) onde você vai gravar os dados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Novo, Dados, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="d3c6e-153">Verifique se o servidor de banco de dados permite o acesso aos serviços do Azure:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-153">Make sure that the database server allows access to Azure services:</span></span>

![Navegar, Servidores, seu servidor, Configurações, Firewall, Permitir Acesso ao Azure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="d3c6e-155">Criar uma tabela no banco de dados do Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d3c6e-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="d3c6e-156">Conecte-se ao banco de dados criado na seção anterior com sua ferramenta de gerenciamento preferida.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="d3c6e-157">Neste passo a passo, usaremos as SSMS ( [Ferramentas de Gerenciamento do SQL Server](https://msdn.microsoft.com/ms174173.aspx) ).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="d3c6e-158">Crie uma nova consulta e execute o T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-158">Create a new query, and execute the following T-SQL:</span></span>

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

<span data-ttu-id="d3c6e-159">Neste exemplo, estamos usando dados de modos de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="d3c6e-160">Para ver os outros dados disponíveis, inspecione a saída JSON e veja o [modelo de exportação de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="d3c6e-161">Criar uma instância do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3c6e-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="d3c6e-162">No [Portal do Azure Clássico](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics e crie um novo trabalho do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="d3c6e-163">Quando o novo trabalho for criado, expanda seus detalhes:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="d3c6e-164">Definir local de blob</span><span class="sxs-lookup"><span data-stu-id="d3c6e-164">Set blob location</span></span>
<span data-ttu-id="d3c6e-165">Defina a entrada do seu blob de Exportação Contínua:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="d3c6e-166">Agora, você precisará da Chave de Acesso Primária da sua Conta de Armazenamento, previamente anotada.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="d3c6e-167">Defina isso como a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="d3c6e-168">Definir padrão de prefixo de caminho</span><span class="sxs-lookup"><span data-stu-id="d3c6e-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="d3c6e-169">Defina o Formato de Data como **AAAA-MM-DD** (com **traços**).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="d3c6e-170">O Padrão de Prefixo de Caminho especifica como o Stream Analytics encontra os arquivos de entrada no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="d3c6e-171">Você precisa configurá-lo para corresponder à maneira como a Exportação Contínua armazena os dados.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="d3c6e-172">Defina-o assim:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="d3c6e-173">Neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-173">In this example:</span></span>

* <span data-ttu-id="d3c6e-174">`webapplication27` é o nome do recurso do Application Insights, **todo em minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="d3c6e-175">`1234...` é a chave de instrumentação do recurso do Application Insights **com traços removidos**.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="d3c6e-176">`PageViews` é o tipo de dados que desejamos analisar.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="d3c6e-177">Os tipos disponíveis dependem do filtro definido na Exportação Contínua.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="d3c6e-178">Examine os dados exportados para ver os outros tipos disponíveis e veja o [modelo de exportação de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3c6e-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="d3c6e-179">`/{date}/{time}` um padrão escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="d3c6e-180">Para obter o nome e iKey do seu recurso do Application Insights, abra Essentials na sua página de visão geral ou abra as Configurações.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="d3c6e-181">Concluir a configuração inicial</span><span class="sxs-lookup"><span data-stu-id="d3c6e-181">Finish initial setup</span></span>
<span data-ttu-id="d3c6e-182">Confirme o formato de serialização:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-182">Confirm the serialization format:</span></span>

![Confirme e feche o assistente](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="d3c6e-184">Feche o assistente e aguarde até que a instalação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="d3c6e-185">Use a função Amostra para verificar se configurou corretamente o caminho de entrada.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="d3c6e-186">Se ele falhar: verifique se há dados no armazenamento para o intervalo de tempo de amostra que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="d3c6e-187">Edite a definição de entrada e verifique se definiu corretamente a conta de armazenamento, o prefixo de caminho e o formato de data.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="d3c6e-188">Definir a consulta</span><span class="sxs-lookup"><span data-stu-id="d3c6e-188">Set query</span></span>
<span data-ttu-id="d3c6e-189">Abra a seção de consulta:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-189">Open the query section:</span></span>

![No Stream Analytics, selecione Consulta](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="d3c6e-191">Substitua a consulta padrão por:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-191">Replace the default query with:</span></span>

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

<span data-ttu-id="d3c6e-192">Observe que as primeiras propriedades são específicas aos dados de exibição da página.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="d3c6e-193">Exportações de outros tipos de telemetria terão propriedades diferentes.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="d3c6e-194">[Referência de modelo de dados detalhados para os tipos de propriedades e valores.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="d3c6e-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="d3c6e-195">Configurar a saída para o banco de dados</span><span class="sxs-lookup"><span data-stu-id="d3c6e-195">Set up output to database</span></span>
<span data-ttu-id="d3c6e-196">Selecione SQL como a saída.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-196">Select SQL as the output.</span></span>

![No Stream Analytics, selecione Saídas](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="d3c6e-198">Especifique o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-198">Specify the SQL database.</span></span>

![Preencha os detalhes do seu banco de dados](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="d3c6e-200">Feche o assistente e aguarde uma notificação de que a saída foi configurada.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="d3c6e-201">Iniciar o processamento</span><span class="sxs-lookup"><span data-stu-id="d3c6e-201">Start processing</span></span>
<span data-ttu-id="d3c6e-202">Inicie o trabalho na barra de ação:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-202">Start the job from the action bar:</span></span>

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="d3c6e-204">Você pode optar por iniciar o processamento de dados neste momento ou iniciar com dados anteriores.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="d3c6e-205">O último é útil se você tiver Exportação Contínua já em execução por um tempo.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![No Stream Analytics, clique em Iniciar](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="d3c6e-207">Depois de alguns minutos, volte para as Ferramentas de Gerenciamento do SQL Server e observe os dados entrando.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="d3c6e-208">Por exemplo, use uma consulta como esta:</span><span class="sxs-lookup"><span data-stu-id="d3c6e-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="d3c6e-209">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="d3c6e-209">Related articles</span></span>
* [<span data-ttu-id="d3c6e-210">Exportar para Power BI usando o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3c6e-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="d3c6e-211">Referência de modelo de dados detalhados para os tipos de propriedades e valores.</span><span class="sxs-lookup"><span data-stu-id="d3c6e-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="d3c6e-212">Exportação Contínua no Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3c6e-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="d3c6e-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3c6e-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

