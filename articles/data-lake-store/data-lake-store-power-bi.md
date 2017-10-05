---
title: Analisar dados no Data Lake Store usando o Power BI | Microsoft Docs
description: "Usar o Power BI para analisar os dados armazenados no Repositório Azure Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0cf7e385ef2edd650479e120f52469bc6632f2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="98a22-103">Analisar dados no Repositório Data Lake usando o Power BI</span><span class="sxs-lookup"><span data-stu-id="98a22-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="98a22-104">Neste artigo, você aprenderá a usar o Power BI Desktop para analisar e visualizar dados armazenados no Repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="98a22-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98a22-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="98a22-105">Prerequisites</span></span>
<span data-ttu-id="98a22-106">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="98a22-106">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="98a22-107">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="98a22-107">**An Azure subscription**.</span></span> <span data-ttu-id="98a22-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98a22-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="98a22-109">**Conta do Repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="98a22-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="98a22-110">Siga as instruções em [Introdução ao Repositório Azure Data Lake usando o Portal do Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98a22-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="98a22-111">Este artigo pressupõe que você já tenha criado uma conta do Data Lake Store chamada **mybidatalakestore** e carregado um arquivo de dados de exemplo (**Drivers.txt**) para ela.</span><span class="sxs-lookup"><span data-stu-id="98a22-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span></span> <span data-ttu-id="98a22-112">Esse exemplo de arquivo está disponível para download no [Repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="98a22-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="98a22-113">**Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="98a22-113">**Power BI Desktop**.</span></span> <span data-ttu-id="98a22-114">Você pode baixá-lo no [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="98a22-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="98a22-115">Criar um relatório no Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="98a22-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="98a22-116">Inicie o Power BI Desktop em seu computador.</span><span class="sxs-lookup"><span data-stu-id="98a22-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="98a22-117">Na faixa de opções **Início**, clique em **Obter Dados** e clique em Mais.</span><span class="sxs-lookup"><span data-stu-id="98a22-117">From the **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="98a22-118">Na caixa de diálogo **Obter Dados**, clique em **Azure**, clique em **Azure Data Lake Store** e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="98a22-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="98a22-119">![Conectar-se ao Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Conectar ao Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="98a22-119">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span></span>
3. <span data-ttu-id="98a22-120">Se você vir uma caixa de diálogo informando que o conector está em uma fase de desenvolvimento, escolha continuar.</span><span class="sxs-lookup"><span data-stu-id="98a22-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span></span>
4. <span data-ttu-id="98a22-121">Na caixa de diálogo **Microsoft Azure Data Lake Store**, forneça a URL da sua conta do Data Lake Store e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a22-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="98a22-122">![URL do Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL para Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="98a22-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="98a22-123">Na caixa de diálogo seguinte, clique em **Entrar** para entrar na conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="98a22-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span></span> <span data-ttu-id="98a22-124">Você será redirecionado à página de logon de sua organização.</span><span class="sxs-lookup"><span data-stu-id="98a22-124">You will be redirected to your organization's sign in page.</span></span> <span data-ttu-id="98a22-125">Siga os prompts para entrar na conta.</span><span class="sxs-lookup"><span data-stu-id="98a22-125">Follow the prompts to sign into the account.</span></span>
   
    <span data-ttu-id="98a22-126">![Entrar no Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Entrar no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="98a22-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="98a22-127">Depois de entrar com sucesso, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="98a22-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="98a22-128">![Conectar-se ao Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Conectar-se ao Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="98a22-128">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span></span>
7. <span data-ttu-id="98a22-129">A próxima caixa de diálogo mostra o arquivo carregado para sua conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="98a22-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span></span> <span data-ttu-id="98a22-130">Verifique as informações e clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="98a22-130">Verify the info and then click **Load**.</span></span>
   
    <span data-ttu-id="98a22-131">![Carregar dados no Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Carregar dados no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="98a22-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="98a22-132">Após os dados serem carregados com êxito no Power BI, você verá os seguintes campos na guia **Campos** .</span><span class="sxs-lookup"><span data-stu-id="98a22-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span></span>
   
    <span data-ttu-id="98a22-133">![Importar campos](./media/data-lake-store-power-bi/imported-fields.png "importado campos")</span><span class="sxs-lookup"><span data-stu-id="98a22-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="98a22-134">No entanto, para visualizar e analisar os dados, preferimos que eles fiquem disponíveis conforme os seguintes campos</span><span class="sxs-lookup"><span data-stu-id="98a22-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span></span>
   
    <span data-ttu-id="98a22-135">![Desejado campos](./media/data-lake-store-power-bi/desired-fields.png "desejado campos")</span><span class="sxs-lookup"><span data-stu-id="98a22-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="98a22-136">Nas próximas etapas, atualizaremos a consulta para converter os dados importados no formato desejado.</span><span class="sxs-lookup"><span data-stu-id="98a22-136">In the next steps, we will update the query to convert the imported data in the desired format.</span></span>
9. <span data-ttu-id="98a22-137">Na faixa de opções **Início**, clique em **Editar Consultas**.</span><span class="sxs-lookup"><span data-stu-id="98a22-137">From the **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="98a22-138">![Editar consultas](./media/data-lake-store-power-bi/edit-queries.png "editar consultas")</span><span class="sxs-lookup"><span data-stu-id="98a22-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="98a22-139">No Editor de Consultas, na coluna **Conteúdo**, clique em **Binário**.</span><span class="sxs-lookup"><span data-stu-id="98a22-139">In the Query Editor, under the **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="98a22-140">![Editar consultas](./media/data-lake-store-power-bi/convert-query1.png "editar consultas")</span><span class="sxs-lookup"><span data-stu-id="98a22-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="98a22-141">Você verá um ícone de arquivo que representa o arquivo **Drivers.txt** carregado.</span><span class="sxs-lookup"><span data-stu-id="98a22-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="98a22-142">Clique no arquivo com o botão direito do mouse e clique em **CSV**.</span><span class="sxs-lookup"><span data-stu-id="98a22-142">Right-click the file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="98a22-143">![Editar consultas](./media/data-lake-store-power-bi/convert-query2.png "editar consultas")</span><span class="sxs-lookup"><span data-stu-id="98a22-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="98a22-144">Você deve ver uma saída parecida com a que está abaixo.</span><span class="sxs-lookup"><span data-stu-id="98a22-144">You should see an output as shown below.</span></span> <span data-ttu-id="98a22-145">Os dados agora estão disponíveis em um formato que você pode usar para criar visualizações.</span><span class="sxs-lookup"><span data-stu-id="98a22-145">Your data is now available in a format that you can use to create visualizations.</span></span>
    
    <span data-ttu-id="98a22-146">![Editar consultas](./media/data-lake-store-power-bi/convert-query3.png "editar consultas")</span><span class="sxs-lookup"><span data-stu-id="98a22-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="98a22-147">Na faixa de opções **Início**, clique em **Fechar e Aplicar** e, em seguida, clique em **Fechar e Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="98a22-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="98a22-148">![Editar consultas](./media/data-lake-store-power-bi/load-edited-query.png "editar consultas")</span><span class="sxs-lookup"><span data-stu-id="98a22-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="98a22-149">Depois que a consulta for atualizada, a guia **Campos** mostrará os novos campos disponíveis para visualização.</span><span class="sxs-lookup"><span data-stu-id="98a22-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span></span>
    
    <span data-ttu-id="98a22-150">![Atualizado campos](./media/data-lake-store-power-bi/updated-query-fields.png "atualizado campos")</span><span class="sxs-lookup"><span data-stu-id="98a22-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="98a22-151">Vamos criar um gráfico de pizza para representar os drivers em cada cidade de um determinado país.</span><span class="sxs-lookup"><span data-stu-id="98a22-151">Let us create a pie chart to represent the drivers in each city for a given country.</span></span> <span data-ttu-id="98a22-152">Para fazer isso, faça as seleções a seguir.</span><span class="sxs-lookup"><span data-stu-id="98a22-152">To do so, make the following selections.</span></span>
    
    1. <span data-ttu-id="98a22-153">Na guia Visualizações, clique no símbolo do gráfico de pizza.</span><span class="sxs-lookup"><span data-stu-id="98a22-153">From the Visualizations tab, click the symbol for a pie chart.</span></span>
       
        <span data-ttu-id="98a22-154">![Criar um gráfico de pizza](./media/data-lake-store-power-bi/create-pie-chart.png "criar o gráfico de pizza")</span><span class="sxs-lookup"><span data-stu-id="98a22-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="98a22-155">As colunas que vamos usar são a **Coluna 4** (nome da cidade) e a **Coluna 7** (nome do país).</span><span class="sxs-lookup"><span data-stu-id="98a22-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span></span> <span data-ttu-id="98a22-156">Arraste essas colunas da guia **Campos** para a guia **Visualizações** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="98a22-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="98a22-157">![Criar visualizações](./media/data-lake-store-power-bi/create-visualizations.png "Criar visualizações")</span><span class="sxs-lookup"><span data-stu-id="98a22-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="98a22-158">O gráfico de pizza agora deve ser semelhante ao mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="98a22-158">The pie chart should now resemble like the one shown below.</span></span>
       
        <span data-ttu-id="98a22-159">![Gráfico de pizza](./media/data-lake-store-power-bi/pie-chart.png "Criar visualizações")</span><span class="sxs-lookup"><span data-stu-id="98a22-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="98a22-160">Ao selecionar um país específico nos filtros de nível de página, você poderá ver o número de drivers em cada cidade do país selecionado.</span><span class="sxs-lookup"><span data-stu-id="98a22-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span></span> <span data-ttu-id="98a22-161">Por exemplo, na guia **Visualizações**, em **Filtros de nível de página**, escolha **Brasil**.</span><span class="sxs-lookup"><span data-stu-id="98a22-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="98a22-162">![Selecione um país](./media/data-lake-store-power-bi/select-country.png "selecione um país")</span><span class="sxs-lookup"><span data-stu-id="98a22-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="98a22-163">O gráfico de pizza é atualizado automaticamente para exibir os drivers em cidades do Brasil.</span><span class="sxs-lookup"><span data-stu-id="98a22-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span></span>
    
    <span data-ttu-id="98a22-164">![Drivers em um país](./media/data-lake-store-power-bi/driver-per-country.png "Drivers por país")</span><span class="sxs-lookup"><span data-stu-id="98a22-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="98a22-165">No menu **Arquivo**, clique em **Salvar** para salvar a visualização como um arquivo do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="98a22-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-to-power-bi-service"></a><span data-ttu-id="98a22-166">Publicar o relatório no serviço Power BI</span><span class="sxs-lookup"><span data-stu-id="98a22-166">Publish report to Power BI service</span></span>
<span data-ttu-id="98a22-167">Depois de criar as visualizações no Power BI Desktop, compartilhe-as com outras pessoas publicando-as no serviço Power BI.</span><span class="sxs-lookup"><span data-stu-id="98a22-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span></span> <span data-ttu-id="98a22-168">Para obter instruções sobre como fazer isso, confira [Publicar a partir do Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span><span class="sxs-lookup"><span data-stu-id="98a22-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="98a22-169">Confira também</span><span class="sxs-lookup"><span data-stu-id="98a22-169">See also</span></span>
* [<span data-ttu-id="98a22-170">Analisar dados no Repositório Data Lake usando o Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="98a22-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

