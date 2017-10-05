---
title: Transmitir dados do Stream Analytics para o Data Lake Store | Microsoft Docs
description: "Usar o Stream Analytics do Azure para transmitir dados para o Repositório Azure Data Lake"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="36d4b-103">Dados de transmissão do Blob de Armazenamento do Azure para o Repositório Data Lake usando o Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="36d4b-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="36d4b-104">Neste artigo, você aprenderá como usar o Repositório Azure Data Lake como uma saída para um trabalho do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="36d4b-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="36d4b-105">Este artigo demonstra um cenário simples que lê dados de um blob de armazenamento do Azure (entrada) e grava os dados no Repositório Data Lake (saída).</span><span class="sxs-lookup"><span data-stu-id="36d4b-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="36d4b-106">No momento, há suporte para a criação e a configuração das saídas do Data Lake Store para o Stream Analytics apenas no [Portal Clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="36d4b-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="36d4b-107">Portanto, algumas partes deste tutorial usarão o Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="36d4b-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="36d4b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="36d4b-108">Prerequisites</span></span>
<span data-ttu-id="36d4b-109">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="36d4b-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="36d4b-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-110">**An Azure subscription**.</span></span> <span data-ttu-id="36d4b-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36d4b-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="36d4b-112">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-112">**Azure Storage account**.</span></span> <span data-ttu-id="36d4b-113">Você usará um contêiner de blob desta conta para os dados de entrada para um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="36d4b-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="36d4b-114">Para esse tutorial, suponha que você tem uma conta de armazenamento chamada **storageforasa** e um contêiner na conta chamado **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="36d4b-115">Depois de criar o contêiner, carregue um arquivo de dados de exemplo nele.</span><span class="sxs-lookup"><span data-stu-id="36d4b-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="36d4b-116">**Conta do Repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="36d4b-117">Siga as instruções em [Introdução ao Repositório Azure Data Lake usando o Portal do Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="36d4b-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="36d4b-118">Vamos supor que você tenha uma conta do Data Lake Store chamada **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="36d4b-119">Criar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="36d4b-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="36d4b-120">Você começa ao criar um trabalho do Stream Analytics, que inclui uma fonte de entrada e um destino de saída.</span><span class="sxs-lookup"><span data-stu-id="36d4b-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="36d4b-121">Para este tutorial, o código-fonte é um contêiner de blob do Azure e o destino é o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36d4b-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="36d4b-122">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36d4b-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="36d4b-123">No painel à esquerda, clique em **Trabalhos do Stream Analytics** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="36d4b-124">![Criar um trabalho do Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Criar um trabalho do Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="36d4b-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="36d4b-125">Certifique-se de criar o trabalho na mesma região que a conta de armazenamento, ou você estará sujeito a pagar pelos custos adicionais de mover os dados entre regiões.</span><span class="sxs-lookup"><span data-stu-id="36d4b-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="36d4b-126">Criar uma entrada de blob para o trabalho</span><span class="sxs-lookup"><span data-stu-id="36d4b-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="36d4b-127">Abra a página do trabalho do Stream Analytics, clique na guia **Entradas** no painel à esquerda e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="36d4b-128">![Adicionar uma entrada ao trabalho](./media/data-lake-store-stream-analytics/create.input.1.png "Adicionar uma entrada ao trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="36d4b-129">Na folha **Nova entrada**, forneça os valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="36d4b-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="36d4b-130">![Adicionar uma entrada ao trabalho](./media/data-lake-store-stream-analytics/create.input.2.png "Adicionar uma entrada ao trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="36d4b-131">Para **Alias de entrada**, insira um nome exclusivo para essa entrada de trabalho.</span><span class="sxs-lookup"><span data-stu-id="36d4b-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="36d4b-132">Para **Tipo de fonte**, selecione **luxo de dados**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="36d4b-133">Para **Fonte**, selecione **Armazenamento de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="36d4b-134">Para **Assinatura**, selecione **Usar armazenamento de blobs da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="36d4b-135">Para **Conta de armazenamento**, selecione a conta de armazenamento que você criou como parte dos pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="36d4b-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="36d4b-136">Para **Contêiner**, selecione o contêiner que você criou na conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="36d4b-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="36d4b-137">Para **Formato de Serialização de Evento**, clique em **CSV**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="36d4b-138">Para **Delimitador**, selecione **guia**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="36d4b-139">Para **Codificação**, selecione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="36d4b-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-140">Click **Create**.</span></span> <span data-ttu-id="36d4b-141">O portal agora adiciona a entrada e testa a conexão.</span><span class="sxs-lookup"><span data-stu-id="36d4b-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="36d4b-142">Criar uma saída do Repositório Data Lake para o trabalho</span><span class="sxs-lookup"><span data-stu-id="36d4b-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="36d4b-143">Abra a página do trabalho do Stream Analytics, clique na guia **Saídas** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="36d4b-144">![Adicionar uma saída ao trabalho](./media/data-lake-store-stream-analytics/create.output.1.png "Adicionar uma saída ao trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="36d4b-145">Na folha **Nova saída**, forneça os valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="36d4b-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="36d4b-146">![Adicionar uma saída ao trabalho](./media/data-lake-store-stream-analytics/create.output.2.png "Adicionar uma saída ao trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="36d4b-147">Para **Alias de saída**, insira um nome exclusivo para essa saída de trabalho.</span><span class="sxs-lookup"><span data-stu-id="36d4b-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="36d4b-148">Esse é um nome amigável utilizado em consultas para direcionar a saída da consulta para esse Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36d4b-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="36d4b-149">Para **Coletor**, selecione **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="36d4b-150">Você precisará autorizar o acesso à conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="36d4b-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="36d4b-151">Clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="36d4b-152">Na folha **Nova saída**, forneça os valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="36d4b-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="36d4b-153">![Adicionar uma saída ao trabalho](./media/data-lake-store-stream-analytics/create.output.3.png "Adicionar uma saída ao trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="36d4b-154">Para **Nome da conta**, selecione a conta do Data Lake Store criada para o qual você deseja que o trabalho de saída seja enviado.</span><span class="sxs-lookup"><span data-stu-id="36d4b-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="36d4b-155">Para **Padrão de prefixo do caminho**, insira um caminho de arquivo usado para gravar seus arquivos na conta do Data Lake Store especificada.</span><span class="sxs-lookup"><span data-stu-id="36d4b-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="36d4b-156">Para **Formato de data**, se você usou um token de data no caminho do prefixo, pode selecionar o formato de data em que os arquivos estão organizados.</span><span class="sxs-lookup"><span data-stu-id="36d4b-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="36d4b-157">Para **Formato de hora**, se você usou um token de hora no caminho do prefixo, especifique o formato de hora em que os arquivos estão organizados.</span><span class="sxs-lookup"><span data-stu-id="36d4b-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="36d4b-158">Para **Formato de Serialização de Evento**, clique em **CSV**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="36d4b-159">Para **Delimitador**, selecione **guia**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="36d4b-160">Para **Codificação**, selecione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="36d4b-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-161">Click **Create**.</span></span> <span data-ttu-id="36d4b-162">O portal agora adiciona a saída e testa a conexão.</span><span class="sxs-lookup"><span data-stu-id="36d4b-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="36d4b-163">Executar o trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="36d4b-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="36d4b-164">Para executar um trabalho do Stream Analytics, você deve executar uma consulta da guia **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="36d4b-165">Para este tutorial, você pode executar a consulta de exemplo, substituindo os espaços reservados pelos aliases de entrada e saída de trabalho, conforme mostrado na captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="36d4b-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="36d4b-166">![Executar consulta](./media/data-lake-store-stream-analytics/run.query.png "Executar consulta")</span><span class="sxs-lookup"><span data-stu-id="36d4b-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="36d4b-167">Clique em **Salvar** na parte superior da tela e, depois, em **Visão geral**, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="36d4b-168">Na caixa de diálogo, selecione **Hora Personalizada** e, em seguida, defina a data e a hora atuais.</span><span class="sxs-lookup"><span data-stu-id="36d4b-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="36d4b-169">![Definir o tempo de trabalho](./media/data-lake-store-stream-analytics/run.query.2.png "Definir o tempo de trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="36d4b-170">Clique em **Iniciar** para iniciar o teste.</span><span class="sxs-lookup"><span data-stu-id="36d4b-170">Click **Start** to start the job.</span></span> <span data-ttu-id="36d4b-171">Pode levar até dois minutos para o trabalho ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="36d4b-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="36d4b-172">Para acionar o trabalho de forma a escolher a os dados do blob, copie um arquivo de dados de exemplo para o contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="36d4b-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="36d4b-173">Você pode obter um arquivo de dados de exemplo do [Repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="36d4b-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="36d4b-174">Para este tutorial, vamos copiar o arquivo **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="36d4b-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="36d4b-175">Você pode usar vários clientes, como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/), para carregar dados em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="36d4b-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="36d4b-176">Na guia **Visão geral**, em **Monitoramento**, veja como os dados foram processados.</span><span class="sxs-lookup"><span data-stu-id="36d4b-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="36d4b-177">![Monitorar o trabalho](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorar o trabalho")</span><span class="sxs-lookup"><span data-stu-id="36d4b-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="36d4b-178">Por fim, você pode verificar se os dados de saída do trabalho estão disponíveis na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="36d4b-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="36d4b-179">![Verificar a saída](./media/data-lake-store-stream-analytics/run.query.4.png "Verificar a saída")</span><span class="sxs-lookup"><span data-stu-id="36d4b-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="36d4b-180">No painel Data Explorer, observe que a saída é gravada em uma pasta, conforme especificado nas configurações de saída do Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="36d4b-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="36d4b-181">Consulte também</span><span class="sxs-lookup"><span data-stu-id="36d4b-181">See also</span></span>
* [<span data-ttu-id="36d4b-182">Criar um cluster do HDInsight para usar o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="36d4b-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
