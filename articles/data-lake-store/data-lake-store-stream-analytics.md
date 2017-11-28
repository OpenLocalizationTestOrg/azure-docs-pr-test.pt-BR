---
title: "dados de aaaStream do Stream Analytics em repositório Data Lake | Microsoft Docs"
description: "Usar dados de toostream do Stream Analytics do Azure no repositório Azure Data Lake"
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
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="24db8-103">Dados de transmissão do Blob de Armazenamento do Azure para o Repositório Data Lake usando o Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="24db8-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="24db8-104">Neste artigo, você aprenderá como toouse do Azure Data Lake armazenar como uma saída para um trabalho do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="24db8-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="24db8-105">Este artigo demonstra um cenário simples que lê dados de um blob de armazenamento do Azure (entrada) e gravações Olá dados tooData Lake repositório (saída).</span><span class="sxs-lookup"><span data-stu-id="24db8-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="24db8-106">Neste momento, criação e configuração do repositório Data Lake saída para análise de fluxo tem suporte apenas em Olá [Portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="24db8-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="24db8-107">Portanto, algumas partes deste tutorial usará Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="24db8-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="24db8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24db8-108">Prerequisites</span></span>
<span data-ttu-id="24db8-109">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="24db8-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="24db8-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="24db8-110">**An Azure subscription**.</span></span> <span data-ttu-id="24db8-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24db8-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="24db8-112">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="24db8-112">**Azure Storage account**.</span></span> <span data-ttu-id="24db8-113">Você usará um contêiner de blob de dados de tooinput essa conta para um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="24db8-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="24db8-114">Para este tutorial, suponha que você tem uma conta de armazenamento chamada **storageforasa** e um contêiner na conta Olá chamado **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="24db8-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="24db8-115">Depois de criar o contêiner de hello, carregue um tooit de arquivo de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="24db8-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="24db8-116">**Conta do Repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="24db8-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="24db8-117">Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24db8-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="24db8-118">Vamos supor que você tenha uma conta do Data Lake Store chamada **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="24db8-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="24db8-119">Criar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24db8-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="24db8-120">Você começa ao criar um trabalho do Stream Analytics, que inclui uma fonte de entrada e um destino de saída.</span><span class="sxs-lookup"><span data-stu-id="24db8-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="24db8-121">Para este tutorial, origem Olá é um contêiner de BLOBs do Azure e o destino de saudação é repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24db8-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="24db8-122">Logon toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24db8-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="24db8-123">No painel esquerdo do hello, clique em **trabalhos do Stream Analytics**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="24db8-124">![Criar um trabalho do Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Criar um trabalho do Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="24db8-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="24db8-125">Certifique-se de criar trabalho Olá mesma região que a conta de armazenamento hello, ou você incorrerá em custos adicionais de mover dados entre regiões.</span><span class="sxs-lookup"><span data-stu-id="24db8-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="24db8-126">Criar uma entrada de Blob para o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="24db8-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="24db8-127">Página abrir Olá para o trabalho de análise de fluxo hello, no painel esquerdo do hello clique Olá **entradas** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="24db8-128">![Adicionar um trabalho de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "adicionar um trabalho de entrada tooyour")</span><span class="sxs-lookup"><span data-stu-id="24db8-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="24db8-129">Em Olá **nova entrada** folha, fornecer Olá valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="24db8-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="24db8-130">![Adicionar um trabalho de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "adicionar um trabalho de entrada tooyour")</span><span class="sxs-lookup"><span data-stu-id="24db8-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="24db8-131">Para **alias de entrada**, insira um nome exclusivo para a entrada de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="24db8-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="24db8-132">Para **Tipo de fonte**, selecione **luxo de dados**.</span><span class="sxs-lookup"><span data-stu-id="24db8-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="24db8-133">Para **Fonte**, selecione **Armazenamento de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="24db8-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="24db8-134">Para **Assinatura**, selecione **Usar armazenamento de blobs da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="24db8-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="24db8-135">Para **conta de armazenamento**, selecione a conta de armazenamento de saudação que você criou como parte dos pré-requisitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="24db8-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="24db8-136">Para **contêiner**, selecione contêiner Olá que você criou na saudação selecionado conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24db8-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="24db8-137">Para **Formato de Serialização de Evento**, clique em **CSV**.</span><span class="sxs-lookup"><span data-stu-id="24db8-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="24db8-138">Para **Delimitador**, selecione **guia**.</span><span class="sxs-lookup"><span data-stu-id="24db8-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="24db8-139">Para **Codificação**, selecione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="24db8-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="24db8-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-140">Click **Create**.</span></span> <span data-ttu-id="24db8-141">portal de saudação agora adiciona entrada hello e testa Olá tooit de conexão.</span><span class="sxs-lookup"><span data-stu-id="24db8-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="24db8-142">Criar uma saída de repositório Data Lake para trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="24db8-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="24db8-143">Abra a página Olá para o trabalho de análise de fluxo de saudação, clique em Olá **saídas** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="24db8-144">![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "adicionar um trabalho de tooyour de saída")</span><span class="sxs-lookup"><span data-stu-id="24db8-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="24db8-145">Em Olá **nova saída** folha, fornecer Olá valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="24db8-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="24db8-146">![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "adicionar um trabalho de tooyour de saída")</span><span class="sxs-lookup"><span data-stu-id="24db8-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="24db8-147">Para **alias de saída**, insira uma um nome exclusivo para a saída do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="24db8-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="24db8-148">Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24db8-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="24db8-149">Para **Coletor**, selecione **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="24db8-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="24db8-150">Você será solicitado tooauthorize acessar a conta do repositório de Lake tooData.</span><span class="sxs-lookup"><span data-stu-id="24db8-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="24db8-151">Clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="24db8-152">Em Olá **nova saída** folha, continuar Olá tooprovide valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="24db8-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="24db8-153">![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "adicionar um trabalho de tooyour de saída")</span><span class="sxs-lookup"><span data-stu-id="24db8-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="24db8-154">Para **nome da conta**, selecione conta de repositório Data Lake Olá já criada onde você deseja Olá toobe de saída de trabalho enviado para.</span><span class="sxs-lookup"><span data-stu-id="24db8-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="24db8-155">Para **padrão de prefixo de caminho**, insira um toowrite de caminho usado do arquivo especificado de seus arquivos no hello conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24db8-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="24db8-156">Para **formato de data**, se você usou um token de data no caminho de prefixo Olá, você pode selecionar o formato de data de saudação na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="24db8-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="24db8-157">Para **formato de hora**, se você usou um token de tempo no caminho de prefixo hello, especificar o formato de tempo de saudação na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="24db8-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="24db8-158">Para **Formato de Serialização de Evento**, clique em **CSV**.</span><span class="sxs-lookup"><span data-stu-id="24db8-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="24db8-159">Para **Delimitador**, selecione **guia**.</span><span class="sxs-lookup"><span data-stu-id="24db8-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="24db8-160">Para **Codificação**, selecione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="24db8-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="24db8-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-161">Click **Create**.</span></span> <span data-ttu-id="24db8-162">portal de saudação agora adiciona a saída de hello e testa Olá tooit de conexão.</span><span class="sxs-lookup"><span data-stu-id="24db8-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="24db8-163">Executar trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="24db8-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="24db8-164">toorun um trabalho do Stream Analytics, você deve executar uma consulta de saudação **consulta** guia. Para este tutorial, você pode executar a consulta de exemplo hello, substituindo reservados Olá Olá trabalho aliases de entrada e saídas, conforme mostrado na captura de tela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="24db8-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="24db8-165">![Executar consulta](./media/data-lake-store-stream-analytics/run.query.png "Executar consulta")</span><span class="sxs-lookup"><span data-stu-id="24db8-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="24db8-166">Clique em **salvar** de topo de saudação da tela hello e, em seguida, de saudação **visão geral** , clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="24db8-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="24db8-167">Na caixa de diálogo hello, selecione **tempo personalizado**e, em seguida, defina Olá data e hora atuais.</span><span class="sxs-lookup"><span data-stu-id="24db8-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="24db8-168">![Definir o tempo de trabalho](./media/data-lake-store-stream-analytics/run.query.2.png "Definir o tempo de trabalho")</span><span class="sxs-lookup"><span data-stu-id="24db8-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="24db8-169">Clique em **iniciar** toostart trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="24db8-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="24db8-170">Pode levar tooa alguns minutos toostart Olá de trabalho.</span><span class="sxs-lookup"><span data-stu-id="24db8-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="24db8-171">dados tootrigger saudação trabalho toopick saudação do blob hello, copie um contêiner de blob do exemplo dados arquivo toohello.</span><span class="sxs-lookup"><span data-stu-id="24db8-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="24db8-172">Você pode obter um arquivo de dados de exemplo da saudação [repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="24db8-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="24db8-173">Para este tutorial, vamos copiar arquivo hello **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="24db8-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="24db8-174">Você pode usar vários clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contêiner de blob de tooa tooupload dados.</span><span class="sxs-lookup"><span data-stu-id="24db8-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="24db8-175">De saudação **visão geral** guia em **monitoramento**, consulte como dados saudação foi processados.</span><span class="sxs-lookup"><span data-stu-id="24db8-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="24db8-176">![Monitorar o trabalho](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorar o trabalho")</span><span class="sxs-lookup"><span data-stu-id="24db8-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="24db8-177">Por fim, você pode verificar que os dados de saída do trabalho de saudação estão disponíveis na conta do repositório Data Lake Olá.</span><span class="sxs-lookup"><span data-stu-id="24db8-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="24db8-178">![Verificar a saída](./media/data-lake-store-stream-analytics/run.query.4.png "Verificar a saída")</span><span class="sxs-lookup"><span data-stu-id="24db8-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="24db8-179">No painel do Explorador de dados de hello, observe que Olá saída caminho da pasta tooa escrito como especificado no hello configurações de saída do repositório Data Lake (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="24db8-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="24db8-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="24db8-180">See also</span></span>
* [<span data-ttu-id="24db8-181">Criar um cluster de HDInsight toouse repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="24db8-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
