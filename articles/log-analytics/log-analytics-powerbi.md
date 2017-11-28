---
title: Exportar dados do Log Analytics para o Power BI | Microsoft Docs
description: "O Power BI é um serviço de análise de negócios baseado em nuvem da Microsoft que fornece relatórios e visualizações avançadas para análise de diferentes conjuntos de dados.  O Log Analytics pode realizar exportação contínua de dados do repositório do OMS para o Power BI automaticamente para que você possa aproveitar suas visualizações e ferramentas de análise.  Este artigo descreve como configurar consultas no Log Analytics exportados automaticamente para o Power BI em intervalos regulares."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="d8752-105">Exportar dados do Log Analytics para o Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="d8752-106">Se o espaço de trabalho foi atualizado para a [nova linguagem de consulta Log Analytics](log-analytics-log-search-upgrade.md), então, esse processo para exportar dados do Log Analytics para o Power BI não irá mais funcionar.</span><span class="sxs-lookup"><span data-stu-id="d8752-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="d8752-107">Todas as agendas existentes criadas antes da atualização serão desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="d8752-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="d8752-108">Após fazer upgrade, o Azure Log Analytics utiliza a mesma plataforma do Application Insights e você usará o mesmo processo para exportar consultas do Log Analytics para o Power BI como no [processo para exportar consultas do Application Insights para o Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="d8752-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="d8752-109">É possível exportar a consulta utilizando o console do Analytics, conforme descrito nesse artigo ou selecionar o botão **Power BI** na parte superior da tela no portal de Pesquisa de Logs.</span><span class="sxs-lookup"><span data-stu-id="d8752-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="d8752-110">O [Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) é um serviço de análise de negócios baseado em nuvem da Microsoft que fornece relatórios e visualizações avançadas para análise de diferentes conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="d8752-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="d8752-111">O Log Analytics pode exportar dados do repositório do OMS para o Power BI automaticamente para que você possa aproveitar suas visualizações e ferramentas de análise.</span><span class="sxs-lookup"><span data-stu-id="d8752-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="d8752-112">Ao configurar o Power BI com o Log Analytics, você poderá criar consultas de log que exportam seus resultados para conjuntos de dados correspondentes no Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="d8752-113">A consulta e a exportação continuarão a ser executadas automaticamente em uma agenda definida por você para manter o conjunto de dados atualizado com os últimos dados coletados pelo Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d8752-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics para Power BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="d8752-115">Agendas do Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-115">Power BI Schedules</span></span>
<span data-ttu-id="d8752-116">Uma *Agenda do Power BI* inclui uma pesquisa de log que exporta um conjunto de dados do repositório do OMS para um conjunto de dados correspondente no Power BI e uma agenda que define a frequência com que essa pesquisa é executada para manter o conjunto de dados atualizado.</span><span class="sxs-lookup"><span data-stu-id="d8752-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="d8752-117">Os campos no conjunto de dados corresponderão às propriedades dos registros retornados pela pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="d8752-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="d8752-118">Se a pesquisa retornar registros de diferentes tipos, o conjunto de dados incluirá todas as propriedades de cada um dos tipos de registro incluídos.</span><span class="sxs-lookup"><span data-stu-id="d8752-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="d8752-119">É uma melhor prática usar uma consulta de pesquisa de log que retorna dados brutos em vez de executar qualquer consolidação usando comandos como [Measure](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="d8752-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="d8752-120">Você pode executar qualquer agregação e cálculo no Power BI por meio dos dados brutos.</span><span class="sxs-lookup"><span data-stu-id="d8752-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="d8752-121">Conectar o espaço de trabalho do OMS ao Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="d8752-122">Antes de exportar do Log Analytics para o Power BI, você deve conectar o seu espaço de trabalho do OMS à conta do Power BI usando o procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8752-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="d8752-123">No console do OMS, clique no bloco **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="d8752-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="d8752-124">Selecione **Contas**.</span><span class="sxs-lookup"><span data-stu-id="d8752-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="d8752-125">Na seção **Informações sobre o espaço de trabalho**, clique em **Conectar à Conta do Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d8752-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="d8752-126">Insira as credenciais da sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="d8752-127">Criar uma agenda do Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="d8752-128">Crie uma agenda do Power BI para cada conjunto de dados usando o procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8752-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="d8752-129">No console do OMS, clique no bloco **Pesquisa de Log** .</span><span class="sxs-lookup"><span data-stu-id="d8752-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="d8752-130">Digite uma nova consulta ou selecione uma pesquisa salva que retorna os dados que você deseja exportar para o **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d8752-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="d8752-131">Clique no botão **Power BI** na parte superior da página para abrir o diálogo **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d8752-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="d8752-132">Forneça as informações na tabela a seguir e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d8752-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="d8752-133">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d8752-133">Property</span></span> | <span data-ttu-id="d8752-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="d8752-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d8752-135">Nome</span><span class="sxs-lookup"><span data-stu-id="d8752-135">Name</span></span> |<span data-ttu-id="d8752-136">Nome para identificar a agenda ao exibir a lista de agendamentos do Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="d8752-137">Pesquisa Salva</span><span class="sxs-lookup"><span data-stu-id="d8752-137">Saved Search</span></span> |<span data-ttu-id="d8752-138">A pesquisa de log a ser executada.</span><span class="sxs-lookup"><span data-stu-id="d8752-138">The log search to run.</span></span>  <span data-ttu-id="d8752-139">Você pode selecionar a consulta atual ou uma pesquisa salva existente na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="d8752-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="d8752-140">Agenda</span><span class="sxs-lookup"><span data-stu-id="d8752-140">Schedule</span></span> |<span data-ttu-id="d8752-141">A frequência de execução da pesquisa salva e exportação para o conjunto de dados do Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="d8752-142">O valor deve ser entre 15 minutos e 24 horas.</span><span class="sxs-lookup"><span data-stu-id="d8752-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="d8752-143">Nome do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d8752-143">Dataset Name</span></span> |<span data-ttu-id="d8752-144">O nome do conjunto de dados no Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="d8752-145">Ele será criado se ele não existir e atualizado se existir.</span><span class="sxs-lookup"><span data-stu-id="d8752-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="d8752-146">Exibir e remover agendas do Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="d8752-147">Veja a lista de agendamentos do Power BI existentes com o procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8752-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="d8752-148">No console do OMS, clique no bloco **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="d8752-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="d8752-149">Selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d8752-149">Select **Power BI**.</span></span>

<span data-ttu-id="d8752-150">Além dos detalhes da agenda, são exibidos o número de vezes que a agenda foi executada na última semana e o status da última sincronização.</span><span class="sxs-lookup"><span data-stu-id="d8752-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="d8752-151">Se a sincronização encontrou erros, você pode clicar no link para executar uma pesquisa de log de registros com detalhes do erro.</span><span class="sxs-lookup"><span data-stu-id="d8752-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="d8752-152">É possível remover um agendamento clicando no **X** na **coluna Remover**.</span><span class="sxs-lookup"><span data-stu-id="d8752-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="d8752-153">É possível desabilitar um agendamento selecionando **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="d8752-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="d8752-154">Para modificar uma agenda, você deve removê-la e recriá-la com as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="d8752-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Agendas do Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="d8752-156">Passo a passo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d8752-156">Sample walkthrough</span></span>
<span data-ttu-id="d8752-157">A seção a seguir demonstra o passo a passo de um exemplo de como criar uma agenda do Power BI e usar seu conjunto de dados para criar um relatório simples.</span><span class="sxs-lookup"><span data-stu-id="d8752-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="d8752-158">Neste exemplo, todos os dados de desempenho para um conjunto de computadores são exportado para o Power BI e um gráfico de linha é criado para exibir a utilização do processador.</span><span class="sxs-lookup"><span data-stu-id="d8752-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="d8752-159">Criar pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="d8752-159">Create log search</span></span>
<span data-ttu-id="d8752-160">Começamos criando uma pesquisa de log para os dados que desejamos enviar para o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d8752-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="d8752-161">Neste exemplo, usaremos uma consulta que retorna todos os dados de desempenho de computadores com um nome que começa com *srv*.</span><span class="sxs-lookup"><span data-stu-id="d8752-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Agendas do Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="d8752-163">Criar a pesquisa do Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-163">Create Power BI Search</span></span>
<span data-ttu-id="d8752-164">Clicamos no botão **Power BI** para abrir o diálogo Power BI e fornecemos as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="d8752-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="d8752-165">Queremos que essa pesquisa seja executada uma vez por hora e crie um conjunto de dados chamado *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="d8752-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="d8752-166">Como já temos aberta uma pesquisa que cria os dados que queremos, mantemos a opção padrão *Usar consulta de pesquisa atual* para **Pesquisa Salva**.</span><span class="sxs-lookup"><span data-stu-id="d8752-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="d8752-168">Verifique a pesquisa do Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-168">Verify Power BI Search</span></span>
<span data-ttu-id="d8752-169">Para verificar se criamos o agendamento corretamente, exibimos a lista de Pesquisas do Power BI sob o bloco **Configurações** no painel do OMS.</span><span class="sxs-lookup"><span data-stu-id="d8752-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="d8752-170">Aguarde alguns minutos e atualize essa exibição até que ela informe que a sincronização foi executada.</span><span class="sxs-lookup"><span data-stu-id="d8752-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="d8752-172">Verificar o conjunto de dados no Power BI</span><span class="sxs-lookup"><span data-stu-id="d8752-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="d8752-173">Fazemos logon em nossa conta em [powerbi.microsoft.com](http://powerbi.microsoft.com/) e rolamos até **Conjuntos de Dados** na parte inferior do painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="d8752-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="d8752-174">Podemos observar que o conjunto de dados *Contoso Perf* é listado, indicando que nossa exportação foi executada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d8752-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Conjunto de dados do Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="d8752-176">Criar um relatório com base no conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d8752-176">Create report based on dataset</span></span>
<span data-ttu-id="d8752-177">Selecionamos o conjunto de dados **Contoso Perf** e clicamos em **Resultados** no painel **Campos** à direita para exibir os campos que fazem parte desse conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d8752-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="d8752-178">Para criar um gráfico de linha mostrando a utilização do processador para cada computador, executamos as seguintes ações.</span><span class="sxs-lookup"><span data-stu-id="d8752-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="d8752-179">Selecione a visualização de Gráfico de linha.</span><span class="sxs-lookup"><span data-stu-id="d8752-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="d8752-180">Arraste**ObjectName** para **Filtro no nível de relatório** e marque **Processor**.</span><span class="sxs-lookup"><span data-stu-id="d8752-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="d8752-181">Arraste **CounterName** para **Filtro no nível de relatório** e marque **% Processor Time**.</span><span class="sxs-lookup"><span data-stu-id="d8752-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="d8752-182">Arraste **CounterValue** para **Valores**.</span><span class="sxs-lookup"><span data-stu-id="d8752-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="d8752-183">Arraste **Computer** para **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="d8752-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="d8752-184">Arraste **TimeGenerated** para **Eixo**.</span><span class="sxs-lookup"><span data-stu-id="d8752-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="d8752-185">Podemos ver que o gráfico de linhas resultante é exibido com os dados do nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d8752-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Gráfico de linha do Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="d8752-187">Salvar o relatório</span><span class="sxs-lookup"><span data-stu-id="d8752-187">Save the report</span></span>
<span data-ttu-id="d8752-188">Salvamos o relatório clicando no botão Salvar na parte superior da tela e validamos se agora ele está listado na seção Relatórios no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="d8752-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Relatórios do Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="d8752-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8752-190">Next steps</span></span>
* <span data-ttu-id="d8752-191">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) para criar consultas que podem ser exportadas para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8752-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="d8752-192">Saiba mais sobre o [Power BI](http://powerbi.microsoft.com) para criar visualizações baseadas em exportações do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d8752-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
