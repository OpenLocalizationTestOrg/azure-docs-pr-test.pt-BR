---
title: "logs de aaaAnalyze site usando a análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como o site tooanalyze registra usando análise Data Lake. "
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
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="bc0e2-103">Analisar logs de site usando o Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="bc0e2-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="bc0e2-104">Saiba como tooanalyze site logs usando a análise Data Lake, especialmente em descobrir quais Referenciadores resultou em erros quando a tentativa de site de saudação toovisit.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc0e2-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc0e2-105">Prerequisites</span></span>
* <span data-ttu-id="bc0e2-106">**Visual Studio 2015 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="bc0e2-107">**[Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="bc0e2-108">Depois que o Data Lake Tools para Visual Studio está instalado, você verá um **Data Lake** item Olá **ferramentas** menu do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="bc0e2-110">**Um conhecimento básico de análise Data Lake e hello Data Lake Tools para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="bc0e2-111">tooget iniciado, consulte:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-111">tooget started, see:</span></span>

  * <span data-ttu-id="bc0e2-112">[Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="bc0e2-113">**Uma conta da Análise Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="bc0e2-114">Confira [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md) (Criar uma conta do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="bc0e2-115">**Carregar a conta do hello exemplo dados toohello análise Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="bc0e2-116">Consulte [toocopy arquivos de dados de exemplo](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="bc0e2-117">toorun um trabalho de análise Data Lake, você precisará de alguns dados.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="bc0e2-118">Embora Olá Data Lake Tools oferece suporte ao carregamento de dados, você usará toomake de dados de exemplo do hello tooupload portal Olá este tutorial toofollow mais fácil.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="bc0e2-119">Conecte-se tooAzure</span><span class="sxs-lookup"><span data-stu-id="bc0e2-119">Connect tooAzure</span></span>
<span data-ttu-id="bc0e2-120">Antes de compilar e testar qualquer script U-SQL, primeiro você deve conectar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="bc0e2-121">**tooconnect tooData análise Lake**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="bc0e2-122">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="bc0e2-123">Clique em **Data Lake > Opções e configurações**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="bc0e2-124">Clique em **entrar**, ou **Alterar usuário** se alguém tiver se conectado e siga as instruções de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="bc0e2-125">Clique em **Okey** tooclose Olá opções e configurações de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="bc0e2-126">**toobrowse suas contas da análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="bc0e2-127">No Visual Studio, abra o **Gerenciador de Servidores** pressionando **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="bc0e2-128">No **Gerenciador de Servidores**, expanda **Azure** e **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="bc0e2-129">Você deverá ver uma lista das suas contas da Análise Data Lake, caso haja alguma.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="bc0e2-130">Você não pode criar contas de análise Data Lake studio hello.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="bc0e2-131">toocreate uma conta, consulte [Introdução à análise Azure Data Lake usando o Portal do Azure](data-lake-analytics-get-started-portal.md) ou [começar a usar o Azure PowerShell de análise do Azure Data Lake](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="bc0e2-132">Desenvolver aplicativos U-SQL</span><span class="sxs-lookup"><span data-stu-id="bc0e2-132">Develop U-SQL application</span></span>
<span data-ttu-id="bc0e2-133">Um aplicativo U-SQL é basicamente um script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="bc0e2-134">toolearn mais sobre U-SQL, consulte [começar com U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="bc0e2-135">Você pode adicionar o aplicativo de toohello adição operadores definidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="bc0e2-136">Para obter mais informações, veja [Desenvolver operadores U-SQL definidos pelo usuário para trabalhos da Análise do Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="bc0e2-137">**toocreate e enviar um trabalho de análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="bc0e2-138">Clique em Olá **arquivo > Novo > projeto**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="bc0e2-139">Selecione o tipo de projeto de U-SQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-139">Select hello U-SQL Project type.</span></span>

    ![novo projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="bc0e2-141">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-141">Click **OK**.</span></span> <span data-ttu-id="bc0e2-142">O Visual Studio cria uma solução com um arquivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="bc0e2-143">Digite hello script a seguir no arquivo de Script.usql hello:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
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

    <span data-ttu-id="bc0e2-144">Olá toounderstand U-SQL, consulte [Introdução à linguagem Data Lake análise U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="bc0e2-145">Adicionar um novo projeto de tooyour de script U-SQL e digite Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="bc0e2-146">Alternar o script U-SQL da primeira toohello voltar e Avançar toohello **enviar** botão, especifique a conta da análise.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="bc0e2-147">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Compilar Script**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="bc0e2-148">Verificar os resultados de saudação no painel de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="bc0e2-149">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Enviar Script**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="bc0e2-150">Verifique se Olá **conta da análise** é hello onde deseja toorun Olá trabalho e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="bc0e2-151">Resultados de envio e o link de trabalho estão disponíveis em hello Data Lake Tools para a janela de resultados do Visual Studio quando o envio de saudação é concluído.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="bc0e2-152">Aguarde até que o trabalho de saudação é concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="bc0e2-153">Se o trabalho de saudação falhou, o arquivo de origem Olá provavelmente está ausente.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="bc0e2-154">Consulte a seção pré-requisitos Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="bc0e2-155">Para obter mais informações sobre solução de problemas, veja [Monitorar e solucionar problemas com trabalhos da Análise do Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="bc0e2-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="bc0e2-156">Quando o trabalho de saudação for concluído, você deverá ver Olá tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![a Análise Data Lake analisa logs de site de blogs](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="bc0e2-158">Agora, repita as etapas 7 a 10 para **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="bc0e2-159">**saída de trabalho hello toosee**</span><span class="sxs-lookup"><span data-stu-id="bc0e2-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="bc0e2-160">De **Server Explorer**, expanda **Azure**, expanda **análise Data Lake**, expanda sua conta da análise Data Lake, expanda **ascontasdearmazenamento**, clique em conta de armazenamento do Data Lake saudação padrão e, em seguida, clique em **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="bc0e2-161">Clique duas vezes em **exemplos** tooopen Olá pasta e, em seguida, clique duas vezes em **saídas**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="bc0e2-162">Clique duas vezes em **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="bc0e2-163">Você pode também clique duas vezes em arquivo de saída de hello dentro do modo de exibição de gráfico de saudação do trabalho de saudação em ordem toonavigate diretamente toohello de saída.</span><span class="sxs-lookup"><span data-stu-id="bc0e2-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc0e2-164">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bc0e2-164">See also</span></span>
<span data-ttu-id="bc0e2-165">tooget iniciado com análise Data Lake usando ferramentas diferentes, consulte:</span><span class="sxs-lookup"><span data-stu-id="bc0e2-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="bc0e2-166">Introdução à Análise do Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc0e2-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="bc0e2-167">Introdução à Análise Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc0e2-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="bc0e2-168">Introdução à Análise Data Lake usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="bc0e2-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
