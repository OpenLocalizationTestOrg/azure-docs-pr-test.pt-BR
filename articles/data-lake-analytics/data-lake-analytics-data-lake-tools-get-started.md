---
title: scripts de aaaDevelop U-SQL usando o Data Lake Tools para Visual Studio | Microsoft Docs
description: Saiba como tooinstall Data Lake ferramentas para Visual Studio e os scripts de U-SQL toodevelop e teste.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="77f3e-103">Desenvolvimento de scripts U-SQL usando as ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77f3e-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="77f3e-104">Saiba como contas de análise do Azure Data Lake toocreate do Visual Studio toouse, definir trabalhos em [U-SQL](data-lake-analytics-u-sql-get-started.md)e envie-o serviço de análise Data Lake toohello trabalhos.</span><span class="sxs-lookup"><span data-stu-id="77f3e-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="77f3e-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77f3e-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="77f3e-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77f3e-106">Prerequisites</span></span>

* <span data-ttu-id="77f3e-107">**Visual Studio**: há suporte para todas as edições, exceto Express.</span><span class="sxs-lookup"><span data-stu-id="77f3e-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="77f3e-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="77f3e-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="77f3e-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="77f3e-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="77f3e-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="77f3e-110">Visual Studio 2013</span></span>
* <span data-ttu-id="77f3e-111">**SDK do Microsoft Azure para .NET** versão 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="77f3e-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="77f3e-112">Instalá-lo usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="77f3e-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="77f3e-113">Uma conta do **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="77f3e-114">toocreate uma conta, consulte [Introdução à análise Azure Data Lake usando o portal do Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="77f3e-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="77f3e-115">Instale as Ferramentas do Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77f3e-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="77f3e-116">Baixe e instale o Azure Data Lake Tools para Visual Studio [do Centro de Download da saudação](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="77f3e-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="77f3e-117">Após a instalação, observe que:</span><span class="sxs-lookup"><span data-stu-id="77f3e-117">After installation, note that:</span></span>
* <span data-ttu-id="77f3e-118">Olá **Server Explorer** > **Azure** nó contém um **análise Data Lake** nó.</span><span class="sxs-lookup"><span data-stu-id="77f3e-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="77f3e-119">Olá **ferramentas** menu tem uma **Data Lake** item.</span><span class="sxs-lookup"><span data-stu-id="77f3e-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="77f3e-120">Conecte-se a conta de análise do Azure Data Lake tooan</span><span class="sxs-lookup"><span data-stu-id="77f3e-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="77f3e-121">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77f3e-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="77f3e-122">Abra o Gerenciador de servidores selecionando a **Vista** do  > **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="77f3e-123">Clique o botão direito do mouse no **Azure**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-123">Right-click **Azure**.</span></span> <span data-ttu-id="77f3e-124">Em seguida, selecione **conectar tooMicrosoft assinatura do Azure** e siga as instruções de saudação.</span><span class="sxs-lookup"><span data-stu-id="77f3e-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="77f3e-125">No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="77f3e-126">Você verá uma lista das suas contas do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="77f3e-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="77f3e-127">Escreve seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="77f3e-127">Write your first U-SQL script</span></span>

<span data-ttu-id="77f3e-128">Olá texto a seguir é um script U-SQL simples.</span><span class="sxs-lookup"><span data-stu-id="77f3e-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="77f3e-129">Ele define um conjunto de dados pequeno e gravações de repositório do conjunto de dados toohello padrão Data Lake como um arquivo chamado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="77f3e-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="77f3e-130">Enviar um trabalho da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="77f3e-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="77f3e-131">Selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="77f3e-132">Selecione Olá **projeto U-SQL** digite e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="77f3e-133">O Visual Studio cria uma solução com um arquivo **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="77f3e-134">Cole o script anterior Olá a saudação **Script.usql** janela.</span><span class="sxs-lookup"><span data-stu-id="77f3e-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="77f3e-135">No canto superior esquerdo Olá Olá **Script.usql** janela, especifique a conta da análise Data Lake de saudação.</span><span class="sxs-lookup"><span data-stu-id="77f3e-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="77f3e-137">No canto superior esquerdo Olá Olá **Script.usql** janela, selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="77f3e-138">Verifique se Olá **conta da análise**e, em seguida, selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="77f3e-139">Resultados de envio estão disponíveis em Olá Data Lake Tools para Visual Studio obter os resultados após a conclusão do envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="77f3e-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="77f3e-141">toosee hello mais recente trabalho status e a atualização de tela hello, clique em **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="77f3e-142">Quando o trabalho de saudação for bem-sucedido, ele mostra Olá **trabalho gráfico**, **operações de metadados**, **histórico de estado**, e **diagnóstico**:</span><span class="sxs-lookup"><span data-stu-id="77f3e-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Gráfico de desempenho de trabalho de Análise Data Lake do SQL-U do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="77f3e-144">**Resumo do trabalho** mostra Olá resumo do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="77f3e-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="77f3e-145">**Detalhes do trabalho** mostra informações mais específicas sobre o trabalho de hello, incluindo o script hello, recursos e vértices.</span><span class="sxs-lookup"><span data-stu-id="77f3e-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="77f3e-146">**Gráfico de trabalho** visualiza o progresso de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="77f3e-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="77f3e-147">**Operações de metadados** mostra todas as ações de saudação efetuados no catálogo de saudação U-SQL.</span><span class="sxs-lookup"><span data-stu-id="77f3e-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="77f3e-148">**Dados** mostra todas as entradas de saudação e saídas.</span><span class="sxs-lookup"><span data-stu-id="77f3e-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="77f3e-149">**Diagnósticos** fornece uma análise avançada para otimização de desempenho e a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="77f3e-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="77f3e-150">estado do trabalho toocheck</span><span class="sxs-lookup"><span data-stu-id="77f3e-150">toocheck job state</span></span>

1. <span data-ttu-id="77f3e-151">No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="77f3e-152">Expanda o nome da conta Olá análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="77f3e-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="77f3e-153">Clique duas vezes em **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="77f3e-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="77f3e-154">Selecione o trabalho de saudação enviada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="77f3e-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="77f3e-155">saída de hello toosee de um trabalho</span><span class="sxs-lookup"><span data-stu-id="77f3e-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="77f3e-156">No Gerenciador de servidores, procure toohello trabalho enviado.</span><span class="sxs-lookup"><span data-stu-id="77f3e-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="77f3e-157">Clique em Olá **dados** guia.</span><span class="sxs-lookup"><span data-stu-id="77f3e-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="77f3e-158">Em Olá **saídas do trabalho** guia, selecione Olá `"/data.csv"` arquivo.</span><span class="sxs-lookup"><span data-stu-id="77f3e-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77f3e-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77f3e-159">Next steps</span></span>

* [<span data-ttu-id="77f3e-160">Execute scripts U-SQL em sua estação de trabalho para teste e depuração</span><span class="sxs-lookup"><span data-stu-id="77f3e-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="77f3e-161">Depurar o código C# em trabalhos U-SQL</span><span class="sxs-lookup"><span data-stu-id="77f3e-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="77f3e-162">Use hello Azure Data Lake Tools para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="77f3e-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
