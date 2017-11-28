---
title: Analisar logs de sites usando o Azure Data Lake Analytics | Microsoft Docs
description: "Saiba como analisar os logs de site usando a Análise Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="bdd05-103">Analisar logs de site usando o Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="bdd05-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="bdd05-104">Saiba como analisar os logs do site usando a Análise Data Lake, principalmente para descobrir quais referenciadores resultaram em erros ao tentar visitar o site.</span><span class="sxs-lookup"><span data-stu-id="bdd05-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdd05-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bdd05-105">Prerequisites</span></span>
* <span data-ttu-id="bdd05-106">**Visual Studio 2015 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="bdd05-107">**[Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="bdd05-108">Quando as Ferramentas do Data Lake para Visual Studio estiverem instaladas, você verá um item **Data Lake** no menu **Ferramentas** do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bdd05-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="bdd05-110">**Conhecimento básico sobre o Data Lake Analytics e sobre as Ferramentas do Data Lake para o Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="bdd05-111">Para começar. confira:</span><span class="sxs-lookup"><span data-stu-id="bdd05-111">To get started, see:</span></span>

  * <span data-ttu-id="bdd05-112">[Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="bdd05-113">**Uma conta da Análise Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="bdd05-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="bdd05-114">Confira [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md) (Criar uma conta do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="bdd05-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="bdd05-115">**Carregue os dados de exemplo na conta da Análise Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="bdd05-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="bdd05-116">Confira [To copy sample data files](data-lake-analytics-get-started-portal.md) (Para copiar os arquivos de dados de exemplo).</span><span class="sxs-lookup"><span data-stu-id="bdd05-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="bdd05-117">Para executar o trabalho da Análise Data Lake, você precisará de alguns dados.</span><span class="sxs-lookup"><span data-stu-id="bdd05-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="bdd05-118">Embora as Ferramentas do Data Lake deem suporte ao carregamento de dados, você poderá usar o portal para carregar os dados de exemplo para deixar o tutorial mais fácil de acompanhar.</span><span class="sxs-lookup"><span data-stu-id="bdd05-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="bdd05-119">Conecte-se ao Azure</span><span class="sxs-lookup"><span data-stu-id="bdd05-119">Connect to Azure</span></span>
<span data-ttu-id="bdd05-120">Antes de criar e testar qualquer script U-SQL, é preciso se conectar ao Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd05-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="bdd05-121">**Para conectar-se à Análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bdd05-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="bdd05-122">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bdd05-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="bdd05-123">Clique em **Data Lake > Opções e configurações**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="bdd05-124">Clique em **Entrar** ou **Alterar Usuário**, se alguém estiver conectado, e siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="bdd05-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="bdd05-125">Clique em **OK** para fechar a caixa de diálogo Opções e Configurações.</span><span class="sxs-lookup"><span data-stu-id="bdd05-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="bdd05-126">**Para procurar suas contas da Análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bdd05-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="bdd05-127">No Visual Studio, abra o **Gerenciador de Servidores** pressionando **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="bdd05-128">No **Gerenciador de Servidores**, expanda **Azure** e **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="bdd05-129">Você deverá ver uma lista das suas contas da Análise Data Lake, caso haja alguma.</span><span class="sxs-lookup"><span data-stu-id="bdd05-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="bdd05-130">Não é possível criar contas da Análise Data Lake a partir do estúdio.</span><span class="sxs-lookup"><span data-stu-id="bdd05-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="bdd05-131">Para criar uma conta, confira [Introdução ao Azure Data Lake Analytics usando o Portal do Azure](data-lake-analytics-get-started-portal.md) ou [Introdução ao Azure Data Lake Analytics usando o Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="bdd05-132">Desenvolver aplicativos U-SQL</span><span class="sxs-lookup"><span data-stu-id="bdd05-132">Develop U-SQL application</span></span>
<span data-ttu-id="bdd05-133">Um aplicativo U-SQL é basicamente um script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bdd05-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="bdd05-134">Para saber mais sobre o U-SQL, consulte [Introdução ao U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="bdd05-135">Você pode adicionar operadores definidos pelo usuário a este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bdd05-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="bdd05-136">Para obter mais informações, veja [Desenvolver operadores U-SQL definidos pelo usuário para trabalhos da Análise do Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="bdd05-137">**Para criar e enviar um trabalho da Análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bdd05-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="bdd05-138">Clique em **Arquivo > Novo > Projeto**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="bdd05-139">Selecione o tipo Projeto do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bdd05-139">Select the U-SQL Project type.</span></span>

    ![novo projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="bdd05-141">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-141">Click **OK**.</span></span> <span data-ttu-id="bdd05-142">O Visual Studio cria uma solução com um arquivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="bdd05-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="bdd05-143">Insira o seguinte script no arquivo Script.usql:</span><span class="sxs-lookup"><span data-stu-id="bdd05-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="bdd05-144">Para entender o U-SQL, consulte [Introdução à linguagem da Análise do Date Lake U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="bdd05-145">Adicione um novo script U-SQL ao seu projeto e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bdd05-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="bdd05-146">Volte para o primeiro script U-SQL e, ao lado do botão **Enviar** , especifique a conta de análise.</span><span class="sxs-lookup"><span data-stu-id="bdd05-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="bdd05-147">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Compilar Script**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="bdd05-148">Verifique os resultados no painel Saída.</span><span class="sxs-lookup"><span data-stu-id="bdd05-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="bdd05-149">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="bdd05-150">Verifique se a **Conta do Analytics** é uma conta na qual você pode executar o trabalho e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="bdd05-151">Os resultados do envio e o link do trabalho ficarão disponíveis na janela de resultados das Ferramentas do Date Lake para Visual Studio quando o envio for concluído.</span><span class="sxs-lookup"><span data-stu-id="bdd05-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="bdd05-152">Aguarde até o trabalho ser concluído com sucesso.</span><span class="sxs-lookup"><span data-stu-id="bdd05-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="bdd05-153">Se houver falha no trabalho, é provável que esteja faltando o arquivo original.</span><span class="sxs-lookup"><span data-stu-id="bdd05-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="bdd05-154">Confira a seção Pré-requisitos deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="bdd05-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="bdd05-155">Para obter mais informações sobre solução de problemas, veja [Monitorar e solucionar problemas com trabalhos da Análise do Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="bdd05-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="bdd05-156">Quando o trabalho for concluído, você deverá ver a seguinte tela:</span><span class="sxs-lookup"><span data-stu-id="bdd05-156">When the job is completed, you shall see the following screen:</span></span>

    ![a Análise Data Lake analisa logs de site de blogs](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="bdd05-158">Agora, repita as etapas 7 a 10 para **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="bdd05-159">**Para ver a saída do trabalho**</span><span class="sxs-lookup"><span data-stu-id="bdd05-159">**To see the job output**</span></span>

1. <span data-ttu-id="bdd05-160">No **Gerenciador de Servidores**, expanda **Azure**, expanda **Data Lake Analytics**, expanda sua conta do Data Lake Analytics, expanda **Contas de Armazenamento**, clique com o botão direito do mouse na conta de Armazenamento padrão do Data Lake e clique em **Gerenciador**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="bdd05-161">Clique duas vezes em **Exemplos** para abrir a pasta e, então, clique duas vezes em **Saídas**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="bdd05-162">Clique duas vezes em **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="bdd05-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="bdd05-163">Também é possível clicar duas vezes no arquivo de saída no modo de exibição de gráficos do trabalho a fim de navegar diretamente até a saída.</span><span class="sxs-lookup"><span data-stu-id="bdd05-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="bdd05-164">Confira também</span><span class="sxs-lookup"><span data-stu-id="bdd05-164">See also</span></span>
<span data-ttu-id="bdd05-165">Para começar a usar a Análise Data Lake com ferramentas diferentes, consulte:</span><span class="sxs-lookup"><span data-stu-id="bdd05-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="bdd05-166">Introdução à Análise do Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bdd05-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="bdd05-167">Introdução à Análise Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdd05-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="bdd05-168">Introdução à Análise Data Lake usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="bdd05-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
