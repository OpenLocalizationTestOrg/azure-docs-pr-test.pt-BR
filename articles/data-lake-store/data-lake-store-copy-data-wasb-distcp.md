---
title: "aaaCopy dados tooand de WASB em repositório Data Lake usando Distcp | Microsoft Docs"
description: "Use Distcp ferramenta toocopy dados tooand do repositório Azure armazenamento de Blobs tooData Lake"
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
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="19178-103">Usar dados de toocopy Distcp entre Blobs de armazenamento do Azure e o repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="19178-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19178-104">Como usar DistCp</span><span class="sxs-lookup"><span data-stu-id="19178-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="19178-105">Como usar AdlCopy</span><span class="sxs-lookup"><span data-stu-id="19178-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="19178-106">Depois de criar um cluster de HDInsight com a conta de acesso de repositório Data Lake tooa, você pode usar ferramentas Hadoop de ecossistema como dados de toocopy Distcp **tooand de** um armazenamento de cluster do HDInsight (WASB) em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="19178-107">Este artigo fornece instruções sobre como tooachieve isso.</span><span class="sxs-lookup"><span data-stu-id="19178-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19178-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19178-108">Prerequisites</span></span>
<span data-ttu-id="19178-109">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="19178-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="19178-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="19178-110">**An Azure subscription**.</span></span> <span data-ttu-id="19178-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19178-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="19178-112">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="19178-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="19178-113">Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="19178-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="19178-114">**Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="19178-115">Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="19178-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="19178-116">Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="19178-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="19178-117">Você aprende rapidamente com vídeos?</span><span class="sxs-lookup"><span data-stu-id="19178-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="19178-118">[Assista a este vídeo](https://mix.office.com/watch/1liuojvdx6sie) sobre como os dados de toocopy entre Blobs de armazenamento do Azure e o repositório Data Lake usando DistCp.</span><span class="sxs-lookup"><span data-stu-id="19178-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="19178-119">Usar Distcp de um cluster HDInsight do Linux</span><span class="sxs-lookup"><span data-stu-id="19178-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="19178-120">Um cluster HDInsight vem com o utilitário de Distcp hello, que pode ser usado toocopy dados de origens diferentes em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="19178-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="19178-121">Se você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello como um armazenamento adicional, hello Distcp utilitário pode ser usado fora da caixa toocopy tooand de dados de uma conta de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="19178-122">Nesta seção, vamos examinar como toouse Olá Distcp utilitário.</span><span class="sxs-lookup"><span data-stu-id="19178-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="19178-123">Na área de trabalho, use SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="19178-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="19178-124">Consulte [conectar tooa HDInsight baseados em Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="19178-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="19178-125">Execute comandos de saudação do prompt SSH hello.</span><span class="sxs-lookup"><span data-stu-id="19178-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="19178-126">Verifique se você pode acessar Olá Blobs de armazenamento do Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="19178-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="19178-127">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="19178-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="19178-128">Isso deve fornecer uma lista de conteúdo no blob de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="19178-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="19178-129">Da mesma forma, verifique se você pode acessar Olá conta do repositório Data Lake do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="19178-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="19178-130">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="19178-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="19178-131">Isso deve fornecer uma lista de arquivos/pastas Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="19178-132">Use dados de toocopy Distcp de WASB tooa conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="19178-133">Isso copiará o conteúdo de saudação do hello **exemplo/data/gutenberg/** pasta WASB muito**/myfolder** em Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="19178-134">Da mesma forma, use dados de toocopy Distcp de tooWASB de conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="19178-135">Isso copiará o conteúdo de saudação do **/myfolder** Olá repositório Data Lake conta muito**exemplo/data/gutenberg/** pasta em WASB.</span><span class="sxs-lookup"><span data-stu-id="19178-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="19178-136">Considerações de desempenho ao usar o DistCp</span><span class="sxs-lookup"><span data-stu-id="19178-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="19178-137">Como DistCp's menor granularidade é um único arquivo, configuração Olá o número máximo de cópias simultâneas é hello mais importante parâmetro toooptimize em relação a repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19178-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="19178-138">Isso é controlado pela configuração mapeadores de inúmeros hello (estou ') parâmetro na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="19178-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="19178-139">Esse parâmetro especifica o número de máximo de saudação de mapeadores que será usado toocopy dados.</span><span class="sxs-lookup"><span data-stu-id="19178-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="19178-140">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="19178-140">Default value is 20.</span></span>

<span data-ttu-id="19178-141">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="19178-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="19178-142">Como determinar o número de saudação de mapeadores toouse?</span><span class="sxs-lookup"><span data-stu-id="19178-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="19178-143">Aqui estão algumas diretrizes que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="19178-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="19178-144">**Etapa 1: Determinar o total de memória YARN** -Olá primeira etapa é cluster toodetermine Olá YARN memória disponível toohello onde você executa o trabalho de DistCp hello.</span><span class="sxs-lookup"><span data-stu-id="19178-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="19178-145">Essas informações estão disponíveis no portal do Ambari Olá associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="19178-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="19178-146">Navegue tooYARN e exibir configurações de saudação guia toosee Olá YARN memória.</span><span class="sxs-lookup"><span data-stu-id="19178-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="19178-147">tooget Olá YARN memória total, multiplicar Olá YARN de memória por nó com número de saudação de nós ter no cluster.</span><span class="sxs-lookup"><span data-stu-id="19178-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="19178-148">**Etapa 2: Calcular o número de saudação de mapeadores de** -Olá valor **m** é igual toohello quociente de memória total do YARN dividida por Olá tamanho do contêiner YARN.</span><span class="sxs-lookup"><span data-stu-id="19178-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="19178-149">Olá informações de tamanho do contêiner YARN está disponível no portal de Ambari Olá também.</span><span class="sxs-lookup"><span data-stu-id="19178-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="19178-150">Navegue tooYARN e exibição Olá configurações na guia Olá tamanho do contêiner YARN é exibido nesta janela.</span><span class="sxs-lookup"><span data-stu-id="19178-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="19178-151">Olá tooarrive equação no número de saudação do mapeadores (**m**) é</span><span class="sxs-lookup"><span data-stu-id="19178-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="19178-152">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="19178-152">**Example**</span></span>

<span data-ttu-id="19178-153">Vamos supor que você tenha um 4 nós D14v2s cluster hello e você está tentando tootransfer 10TB de dados de 10 pastas diferentes.</span><span class="sxs-lookup"><span data-stu-id="19178-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="19178-154">Cada uma das pastas de saudação contêm diferentes quantidades de dados e tamanhos de arquivo hello dentro de cada pasta são diferentes.</span><span class="sxs-lookup"><span data-stu-id="19178-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="19178-155">Memória total do YARN - de saudação Ambari portal determinar que Olá memória YARN é 96GB para um nó D14.</span><span class="sxs-lookup"><span data-stu-id="19178-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="19178-156">Portanto, o total de memória YARN para um cluster de 4 nós é:</span><span class="sxs-lookup"><span data-stu-id="19178-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="19178-157">Número de mapeadores - de saudação portal Ambari você determinar que Olá tamanho do contêiner YARN é 3072 para um nó de cluster D14.</span><span class="sxs-lookup"><span data-stu-id="19178-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="19178-158">Portanto, o número de mapeadores é:</span><span class="sxs-lookup"><span data-stu-id="19178-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="19178-159">Se outros aplicativos estão usando memória, em seguida, você pode escolher usar tooonly uma parte da memória YARN do cluster para DistCp.</span><span class="sxs-lookup"><span data-stu-id="19178-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="19178-160">Copiando grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="19178-160">Copying large datasets</span></span>

<span data-ttu-id="19178-161">Ao mover o tamanho de saudação do hello toobe de conjunto de dados é muito grande (por exemplo, > 1TB) ou se você tiver muitas pastas diferentes, considere usar vários trabalhos DistCp.</span><span class="sxs-lookup"><span data-stu-id="19178-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="19178-162">Provavelmente, não há nenhum ganho de desempenho, mas ele distribuirão trabalhos Olá para que se algum trabalho falhar, você só precisará toorestart esse trabalho específico, em vez de todo o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="19178-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="19178-163">Limitações</span><span class="sxs-lookup"><span data-stu-id="19178-163">Limitations</span></span>

* <span data-ttu-id="19178-164">DistCp tenta mapeadores de toocreate semelhantes no desempenho de toooptimize de tamanho.</span><span class="sxs-lookup"><span data-stu-id="19178-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="19178-165">Aumentar o número de saudação de mapeadores não pode aumentar desempenho sempre.</span><span class="sxs-lookup"><span data-stu-id="19178-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="19178-166">DistCp é mapeador de um tooonly limitado por arquivo.</span><span class="sxs-lookup"><span data-stu-id="19178-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="19178-167">Portanto, você não deve ter mais mapeadores do que arquivos.</span><span class="sxs-lookup"><span data-stu-id="19178-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="19178-168">Como DistCp só pode atribuir mapeador de um arquivo de tooa, isso limita a quantidade de saudação de simultaneidade que pode ser usado toocopy grandes arquivos.</span><span class="sxs-lookup"><span data-stu-id="19178-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="19178-169">Se você tiver um número pequeno de arquivos grandes, você deve dividi-los em 256MB arquivo partes toogive você mais simultaneidade potencial.</span><span class="sxs-lookup"><span data-stu-id="19178-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="19178-170">Se você estiver copiando de uma conta de armazenamento de BLOBs do Azure, o trabalho de cópia pode ser acelerado no lado de armazenamento de blob hello.</span><span class="sxs-lookup"><span data-stu-id="19178-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="19178-171">Isso prejudicará o desempenho de saudação do seu trabalho de cópia.</span><span class="sxs-lookup"><span data-stu-id="19178-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="19178-172">toolearn mais sobre limites de saudação do armazenamento de BLOBs do Azure, consulte os limites de armazenamento do Azure em [assinatura do Azure e limites de serviço](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="19178-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="19178-173">Consulte também</span><span class="sxs-lookup"><span data-stu-id="19178-173">See also</span></span>
* [<span data-ttu-id="19178-174">Copiar dados do repositório Azure armazenamento de Blobs tooData Lake</span><span class="sxs-lookup"><span data-stu-id="19178-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="19178-175">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="19178-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="19178-176">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="19178-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="19178-177">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="19178-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
