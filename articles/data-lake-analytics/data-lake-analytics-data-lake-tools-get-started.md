---
title: Desenvolvimento de scripts U-SQL usando as ferramentas do Data Lake para Visual Studio | Microsoft Docs
description: Saiba como instalar ferramentas do Data Lake para o Visual Studio e como desenvolver e testar scripts U-SQL.
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
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="43240-103">Desenvolvimento de scripts U-SQL usando as ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43240-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="43240-104">Saiba como usar o Visual Studio para criar contas do Azure Data Lake Analytics, definir trabalhos no [U-SQL](data-lake-analytics-u-sql-get-started.md) e enviar trabalhos ao serviço do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="43240-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="43240-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43240-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="43240-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="43240-106">Prerequisites</span></span>

* <span data-ttu-id="43240-107">**Visual Studio**: há suporte para todas as edições, exceto Express.</span><span class="sxs-lookup"><span data-stu-id="43240-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="43240-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="43240-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="43240-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="43240-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="43240-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="43240-110">Visual Studio 2013</span></span>
* <span data-ttu-id="43240-111">**SDK do Microsoft Azure para .NET** versão 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="43240-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="43240-112">Instale-o usando o [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="43240-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="43240-113">Uma conta do **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="43240-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="43240-114">Para criar uma conta, confira [Introdução ao Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43240-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="43240-115">Instale as Ferramentas do Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43240-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="43240-116">Baixe e instale as Ferramentas do Azure Data Lake para Visual Studio [do Centro de Download](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="43240-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="43240-117">Após a instalação, observe que:</span><span class="sxs-lookup"><span data-stu-id="43240-117">After installation, note that:</span></span>
* <span data-ttu-id="43240-118">O nó do **Gerenciador de Servidores** > do **Azure** contém um nó do **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="43240-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="43240-119">O menu de **ferramentas** tem um item do **Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="43240-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="43240-120">Conecte-se com uma conta do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="43240-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="43240-121">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43240-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="43240-122">Abra o Gerenciador de servidores selecionando a **Vista** do  > **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="43240-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="43240-123">Clique o botão direito do mouse no **Azure**.</span><span class="sxs-lookup"><span data-stu-id="43240-123">Right-click **Azure**.</span></span> <span data-ttu-id="43240-124">Em seguida, selecione **Conectar-se com a assinatura do Microsoft Azure** e siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="43240-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="43240-125">No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="43240-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="43240-126">Você verá uma lista das suas contas do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="43240-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="43240-127">Escreve seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="43240-127">Write your first U-SQL script</span></span>

<span data-ttu-id="43240-128">O texto a seguir é um script U-SQL simples.</span><span class="sxs-lookup"><span data-stu-id="43240-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="43240-129">Ele define um pequeno conjunto de dados e grava o conjunto de dados no repositório padrão do Data Lake Store como um arquivo chamado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="43240-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="43240-130">Enviar um trabalho da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="43240-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="43240-131">Selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="43240-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="43240-132">Selecione o tipo **projeto U-SQL** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43240-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="43240-133">O Visual Studio cria uma solução com um arquivo **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="43240-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="43240-134">Cole o script anterior na janela **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="43240-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="43240-135">No canto superior esquerdo da janela **Script.usql**, especifique a conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="43240-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="43240-137">No canto superior esquerdo da janela **Script.usql**, selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="43240-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="43240-138">Verifique a **conta do Analytics** e, em seguida, selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="43240-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="43240-139">Os resultados de envio estão disponíveis nas Ferramentas do Data Lake para resultados do Visual Studio após a conclusão do envio.</span><span class="sxs-lookup"><span data-stu-id="43240-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="43240-141">Para ver a versão mais recente do status do trabalho e atualizar a tela, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="43240-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="43240-142">Quando o trabalho é bem-sucedido, ele mostra o **gráfico do trabalho**, as **operações de metadados**, o **histórico de estado** e os **diagnósticos**:</span><span class="sxs-lookup"><span data-stu-id="43240-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Gráfico de desempenho de trabalho de Análise Data Lake do SQL-U do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="43240-144">**Resumo do trabalho** mostra o resumo do trabalho.</span><span class="sxs-lookup"><span data-stu-id="43240-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="43240-145">**Detalhes do trabalho** mostra informações mais específicas sobre o trabalho, incluindo o script, os recursos e os vértices.</span><span class="sxs-lookup"><span data-stu-id="43240-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="43240-146">**Gráfico do trabalho** visualiza o andamento do trabalho.</span><span class="sxs-lookup"><span data-stu-id="43240-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="43240-147">**Operações de metadados** mostra todas as ações que foram executadas no catálogo de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="43240-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="43240-148">**Dados** mostra todas as entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="43240-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="43240-149">**Diagnósticos** fornece uma análise avançada para otimização de desempenho e a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="43240-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="43240-150">Para verificar o estado do trabalho</span><span class="sxs-lookup"><span data-stu-id="43240-150">To check job state</span></span>

1. <span data-ttu-id="43240-151">No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="43240-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="43240-152">Expanda o nome da conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="43240-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="43240-153">Clique duas vezes em **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="43240-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="43240-154">Selecione o trabalho enviado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43240-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="43240-155">Para visualizar a saída de um trabalho</span><span class="sxs-lookup"><span data-stu-id="43240-155">To see the output of a job</span></span>

1. <span data-ttu-id="43240-156">No Gerenciador de servidores, navegue até o trabalho enviado.</span><span class="sxs-lookup"><span data-stu-id="43240-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="43240-157">Clique na guia **Dados** .</span><span class="sxs-lookup"><span data-stu-id="43240-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="43240-158">Na guia **Saídas do trabalho**, selecione o arquivo `"/data.csv"`.</span><span class="sxs-lookup"><span data-stu-id="43240-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43240-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43240-159">Next steps</span></span>

* [<span data-ttu-id="43240-160">Execute scripts U-SQL em sua estação de trabalho para teste e depuração</span><span class="sxs-lookup"><span data-stu-id="43240-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="43240-161">Depurar o código C# em trabalhos U-SQL</span><span class="sxs-lookup"><span data-stu-id="43240-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="43240-162">Usar as Ferramentas do Azure Data Lake para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="43240-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
