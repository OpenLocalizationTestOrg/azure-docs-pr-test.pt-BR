---
title: Copiar dados para e do WASB no Data Lake Store usando o Distcp| Microsoft Docs
description: "Use a ferramenta Distcp para copiar dados de e para os Blobs de Armazenamento do Azure para o Repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="07eb2-103">Use Distcp para copiar dados entre o Repositório do Data Lake e os Blobs de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="07eb2-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07eb2-104">Como usar DistCp</span><span class="sxs-lookup"><span data-stu-id="07eb2-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="07eb2-105">Como usar AdlCopy</span><span class="sxs-lookup"><span data-stu-id="07eb2-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="07eb2-106">Depois de criar um cluster do HDInsight que tem acesso a uma conta de Repositório do Data Lake, você pode usar ferramentas do ecossistema Hadoop, como Distcp, para copiar dados **do e para** um armazenamento de cluster do HDInsight (WASB) em uma conta do Repositório do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="07eb2-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="07eb2-107">Esse artigo fornece instruções sobre como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="07eb2-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07eb2-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07eb2-108">Prerequisites</span></span>
<span data-ttu-id="07eb2-109">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="07eb2-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="07eb2-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="07eb2-110">**An Azure subscription**.</span></span> <span data-ttu-id="07eb2-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07eb2-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="07eb2-112">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="07eb2-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="07eb2-113">Para obter instruções sobre como criar uma, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="07eb2-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="07eb2-114">**Cluster HDInsight do Azure** com acesso a uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="07eb2-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="07eb2-115">Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07eb2-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="07eb2-116">Certifique-se de habilitar a área de trabalho remota para o cluster.</span><span class="sxs-lookup"><span data-stu-id="07eb2-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="07eb2-117">Você aprende rapidamente com vídeos?</span><span class="sxs-lookup"><span data-stu-id="07eb2-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="07eb2-118">[Assista a este vídeo](https://mix.office.com/watch/1liuojvdx6sie) sobre como copiar dados entre o Repositório do Data Lake e os Blobs de Armazenamento do Azure usando o DistCp.</span><span class="sxs-lookup"><span data-stu-id="07eb2-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="07eb2-119">Usar Distcp de um cluster HDInsight do Linux</span><span class="sxs-lookup"><span data-stu-id="07eb2-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="07eb2-120">Um cluster do HDInsight é fornecido com o utilitário Distcp, que pode ser usado para copiar dados de fontes diferentes em um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07eb2-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="07eb2-121">Se você tiver configurado o cluster do HDInsight para usar o Repositório do Data Lake como um armazenamento adicional, o utilitário Distcp pode ser usado prontamente para copiar dados de e para uma conta do Repositório do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="07eb2-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="07eb2-122">Nesta seção, vamos examinar como usar o utilitário Distcp.</span><span class="sxs-lookup"><span data-stu-id="07eb2-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="07eb2-123">Da sua área de trabalho, use o SSH para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="07eb2-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="07eb2-124">Confira [Conectar-se a um cluster HDInsight baseado em Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="07eb2-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="07eb2-125">Execute os comandos do prompt de SSH.</span><span class="sxs-lookup"><span data-stu-id="07eb2-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="07eb2-126">Verifique se você pode acessar os WASB (Blobs de Armazenamento do Azure).</span><span class="sxs-lookup"><span data-stu-id="07eb2-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="07eb2-127">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="07eb2-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="07eb2-128">Isso deve fornecer uma lista de conteúdo no blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="07eb2-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="07eb2-129">Da mesma forma, verifique se você pode acessar a conta de Repositório do Data Lake do cluster.</span><span class="sxs-lookup"><span data-stu-id="07eb2-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="07eb2-130">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="07eb2-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="07eb2-131">Isso deve fornecer uma lista de arquivos/pastas na conta de Repositório do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="07eb2-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="07eb2-132">Use Distcp para copiar dados do WASB para uma conta de Repositório do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="07eb2-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="07eb2-133">Isso copiará o conteúdo da pasta **/example/data/gutenberg/** do WASB em **/myfolder** na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="07eb2-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="07eb2-134">De modo semelhante, use Distcp para copiar dados da conta de Repositório do Data Lake para o WASB.</span><span class="sxs-lookup"><span data-stu-id="07eb2-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="07eb2-135">Isso copiará o conteúdo de **/myfolder** da conta do Data Lake Store na pasta **/example/data/gutenberg/** no WASB.</span><span class="sxs-lookup"><span data-stu-id="07eb2-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="07eb2-136">Considerações de desempenho ao usar o DistCp</span><span class="sxs-lookup"><span data-stu-id="07eb2-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="07eb2-137">Como a granularidade mais baixa do DistCp é um único arquivo, definir o número máximo de cópias simultâneas é o parâmetro mais importante para otimizá-lo em relação ao Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="07eb2-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="07eb2-138">Isso é controlado pela configuração do parâmetro de número de mapeadores (“m”) na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="07eb2-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="07eb2-139">Esse parâmetro especifica o número máximo de mapeadores que será usado para copiar dados.</span><span class="sxs-lookup"><span data-stu-id="07eb2-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="07eb2-140">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="07eb2-140">Default value is 20.</span></span>

<span data-ttu-id="07eb2-141">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="07eb2-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="07eb2-142">Como determino o número de mapeadores que serão usados?</span><span class="sxs-lookup"><span data-stu-id="07eb2-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="07eb2-143">Aqui estão algumas diretrizes que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="07eb2-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="07eb2-144">**Etapa 1: Determinar a memória total de YARN** ‑ A primeira etapa é determinar a memória YARN disponível para o cluster em que você executa o trabalho DistCp.</span><span class="sxs-lookup"><span data-stu-id="07eb2-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="07eb2-145">Essas informações estão disponíveis no portal do Ambari associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="07eb2-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="07eb2-146">Navegue até YARN e exiba a guia Configurações para ver a memória YARN.</span><span class="sxs-lookup"><span data-stu-id="07eb2-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="07eb2-147">Para obter a memória YARN total, multiplique a memória YARN por nó pelo número de nós que você tem no cluster.</span><span class="sxs-lookup"><span data-stu-id="07eb2-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="07eb2-148">**Etapa 2: Calcular o número de mapeadores** ‑ O valor de **m** é igual ao quociente de memória total de YARN dividida pelo tamanho do contêiner YARN.</span><span class="sxs-lookup"><span data-stu-id="07eb2-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="07eb2-149">As informações de tamanho do contêiner YARN também estão disponíveis no portal do Ambari.</span><span class="sxs-lookup"><span data-stu-id="07eb2-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="07eb2-150">Navegue até YARN e exiba a guia Configurações.</span><span class="sxs-lookup"><span data-stu-id="07eb2-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="07eb2-151">O tamanho do contêiner YARN é exibido nessa janela.</span><span class="sxs-lookup"><span data-stu-id="07eb2-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="07eb2-152">A equação para chegar até o número de mapeadores (**m**) é</span><span class="sxs-lookup"><span data-stu-id="07eb2-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="07eb2-153">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="07eb2-153">**Example**</span></span>

<span data-ttu-id="07eb2-154">Suponhamos que você tenha 4 nós D14v2s no cluster e está tentando transferir 10 TB de dados de 10 pastas diferentes.</span><span class="sxs-lookup"><span data-stu-id="07eb2-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="07eb2-155">Cada uma das pastas contêm volumes diversos de dados e os tamanhos dos arquivos em cada pasta também são diferentes.</span><span class="sxs-lookup"><span data-stu-id="07eb2-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="07eb2-156">Total de memória YARN ‑ Do portal Ambari você determina que a memória YARN é 96 GB para um nó D14.</span><span class="sxs-lookup"><span data-stu-id="07eb2-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="07eb2-157">Portanto, o total de memória YARN para um cluster de 4 nós é:</span><span class="sxs-lookup"><span data-stu-id="07eb2-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="07eb2-158">Número de mapeadores ‑ Do portal do Ambari a você determina que o tamanho do contêiner YARN é 3072 para um nó de cluster D14.</span><span class="sxs-lookup"><span data-stu-id="07eb2-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="07eb2-159">Portanto, o número de mapeadores é:</span><span class="sxs-lookup"><span data-stu-id="07eb2-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="07eb2-160">Se outros aplicativos estiverem usando memória, então você poderá usar somente uma parte da memória YARN do cluster para o DistCp.</span><span class="sxs-lookup"><span data-stu-id="07eb2-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="07eb2-161">Copiando grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="07eb2-161">Copying large datasets</span></span>

<span data-ttu-id="07eb2-162">Quando o tamanho do conjunto de dados a ser movido será muito grande (por exemplo, maior que 1 TB) ou se você tiver muitas pastas diferentes, considere usar vários trabalhos DistCp.</span><span class="sxs-lookup"><span data-stu-id="07eb2-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="07eb2-163">Provavelmente, não haverá nenhum ganho de desempenho, porém isso espalhará os trabalhos para que, se algum trabalho falhar, seja necessário reiniciar somente esse trabalho específico em vez de todo o trabalho.</span><span class="sxs-lookup"><span data-stu-id="07eb2-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="07eb2-164">Limitações</span><span class="sxs-lookup"><span data-stu-id="07eb2-164">Limitations</span></span>

* <span data-ttu-id="07eb2-165">O DistCp tenta criar mapeadores de tamanho semelhantes para otimizar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="07eb2-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="07eb2-166">Aumentar o número de mapeadores nem sempre melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="07eb2-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="07eb2-167">O DistCp é limitado a apenas um mapeador por arquivo.</span><span class="sxs-lookup"><span data-stu-id="07eb2-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="07eb2-168">Portanto, você não deve ter mais mapeadores do que arquivos.</span><span class="sxs-lookup"><span data-stu-id="07eb2-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="07eb2-169">Como DistCp só pode atribuir um mapeador para um arquivo, isso limita a quantidade de simultaneidade que pode ser usada para copiar grandes arquivos.</span><span class="sxs-lookup"><span data-stu-id="07eb2-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="07eb2-170">Se você tiver um pequeno número de grandes arquivos, divida-os em partes do arquivo de 256 MB para proporcionar um maior potencial de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="07eb2-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="07eb2-171">Se você estiver copiando de uma conta de Armazenamento de Blobs do Azure, seu trabalho de cópia poderá ficar limitado do lado do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="07eb2-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="07eb2-172">Isso poderá degradar o desempenho do seu trabalho de cópia.</span><span class="sxs-lookup"><span data-stu-id="07eb2-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="07eb2-173">Para saber mais sobre os limites do Armazenamento de Blobs do Azure, confira Limites de Armazenamento do Azure em [Limites de serviço e assinatura do Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="07eb2-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="07eb2-174">Consulte também</span><span class="sxs-lookup"><span data-stu-id="07eb2-174">See also</span></span>
* [<span data-ttu-id="07eb2-175">Copiar dados de Blobs do Armazenamento do Azure para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="07eb2-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="07eb2-176">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="07eb2-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="07eb2-177">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="07eb2-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="07eb2-178">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="07eb2-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
