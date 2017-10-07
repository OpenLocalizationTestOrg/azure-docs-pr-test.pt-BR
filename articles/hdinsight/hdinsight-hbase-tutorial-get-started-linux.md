---
title: aaaGet iniciada com um exemplo de HBase em HDInsight - Azure | Microsoft Docs
description: "Siga este toostart de exemplo Apache HBase com hadoop no HDInsight. Criar tabelas de saudação shell do HBase e consultá-los usando o Hive."
keywords: exemplo hbasecommand,hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="dac31-105">Introdução a um exemplo do Apache HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dac31-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="dac31-106">Saiba como toocreate um cluster HBase em HDInsight, criar tabelas HBase e consultar tabelas usando o Hive.</span><span class="sxs-lookup"><span data-stu-id="dac31-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="dac31-107">Para obter informações gerais do HBase, confira [Visão geral do HBase do HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="dac31-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="dac31-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dac31-108">Prerequisites</span></span>
<span data-ttu-id="dac31-109">Antes de tentar Este exemplo HBase, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="dac31-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dac31-110">**An Azure subscription**.</span></span> <span data-ttu-id="dac31-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="dac31-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="dac31-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dac31-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="dac31-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="dac31-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="dac31-114">Nome do cluster HBase</span><span class="sxs-lookup"><span data-stu-id="dac31-114">Create HBase cluster</span></span>
<span data-ttu-id="dac31-115">Olá procedimento a seguir usa um toocreate de modelo do Gerenciador de recursos do Azure um versão 3.4 baseados em Linux HBase cluster e hello dependentes armazenamento do Azure conta padrão.</span><span class="sxs-lookup"><span data-stu-id="dac31-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="dac31-116">parâmetros de saudação toounderstand usados no procedimento de saudação e outros métodos de criação de cluster, consulte [Hadoop baseado em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="dac31-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="dac31-117">Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dac31-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="dac31-118">Olá modelo está localizado em um contêiner de blob público.</span><span class="sxs-lookup"><span data-stu-id="dac31-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="dac31-119">De saudação **implantação personalizada** folha, digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="dac31-120">**Assinatura**: selecione sua assinatura do Azure que é usado toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="dac31-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="dac31-121">**Grupo de recursos**: Crie um grupo de Gerenciamento de Recursos do Azure ou use um existente.</span><span class="sxs-lookup"><span data-stu-id="dac31-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="dac31-122">**Local**: especificar local de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dac31-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="dac31-123">**ClusterName**: insira um nome para o cluster do HBase hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="dac31-124">**Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.</span><span class="sxs-lookup"><span data-stu-id="dac31-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="dac31-125">**SSH username e password**: nome de usuário saudação padrão é **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="dac31-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="dac31-126">Você pode renomeá-lo.</span><span class="sxs-lookup"><span data-stu-id="dac31-126">You can rename it.</span></span>
     
     <span data-ttu-id="dac31-127">Outros parâmetros são opcionais.</span><span class="sxs-lookup"><span data-stu-id="dac31-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="dac31-128">Cada cluster tem uma dependência de conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dac31-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="dac31-129">Depois de excluir um cluster, dados saudação retém na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="dac31-130">nome da conta de armazenamento para o cluster padrão de saudação é o nome de cluster de saudação com "store" acrescentada.</span><span class="sxs-lookup"><span data-stu-id="dac31-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="dac31-131">Ele é codificado na seção de variáveis de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="dac31-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="dac31-132">Selecione **concordo toohello termos e condições declaradas acima**e, em seguida, clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="dac31-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="dac31-133">Demora cerca de 20 minutos toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="dac31-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="dac31-134">Depois que um cluster HBase for excluído, você pode criar outro cluster HBase usando Olá mesmo contêiner de blob padrão.</span><span class="sxs-lookup"><span data-stu-id="dac31-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="dac31-135">cluster novo Olá seleciona tabelas de HBase Olá criado no cluster original hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="dac31-136">tooavoid inconsistências, recomendamos que você desabilite a tabelas do hello HBase antes de excluir o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="dac31-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="dac31-137">Criar tabelas e inserir dados</span><span class="sxs-lookup"><span data-stu-id="dac31-137">Create tables and insert data</span></span>
<span data-ttu-id="dac31-138">Você pode usar SSH tooconnect tooHBase clusters e, em seguida, usar tabelas do Shell do HBase toocreate HBase, inserir dados e consultar dados.</span><span class="sxs-lookup"><span data-stu-id="dac31-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="dac31-139">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dac31-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="dac31-140">Para a maioria das pessoas, os dados aparecem em um formato tabular hello:</span><span class="sxs-lookup"><span data-stu-id="dac31-140">For most people, data appears in hello tabular format:</span></span>

![dados tabulares do HBase HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="dac31-142">No HBase (uma implementação de BigTable), hello mesmo dados parece com:</span><span class="sxs-lookup"><span data-stu-id="dac31-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![Dados BigTable do HBase HDInsight][img-hbase-sample-data-bigtable]


<span data-ttu-id="dac31-144">**Olá toouse shell do HBase**</span><span class="sxs-lookup"><span data-stu-id="dac31-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="dac31-145">SSH, execute Olá HBase comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="dac31-146">Crie um HBase com famílias de duas colunas:</span><span class="sxs-lookup"><span data-stu-id="dac31-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="dac31-147">Insira alguns dados:</span><span class="sxs-lookup"><span data-stu-id="dac31-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell do HBase do Hadoop HDInsight][img-hbase-shell]
4. <span data-ttu-id="dac31-149">Obter uma única linha</span><span class="sxs-lookup"><span data-stu-id="dac31-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="dac31-150">Você deverá ver Olá mesmos resultados usando o comando de verificação de saudação porque há apenas uma linha.</span><span class="sxs-lookup"><span data-stu-id="dac31-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="dac31-151">Para obter mais informações sobre o esquema de tabela do HBase hello, consulte [tooHBase Introdução Design de esquema][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="dac31-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="dac31-152">Para obter mais comandos HBase, confira [Guia de referência do Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="dac31-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="dac31-153">Saída Olá shell</span><span class="sxs-lookup"><span data-stu-id="dac31-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="dac31-154">**toobulk carregar dados em tabela do HBase Olá contatos**</span><span class="sxs-lookup"><span data-stu-id="dac31-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="dac31-155">O HBase inclui vários métodos de carregamento de dados em tabelas.</span><span class="sxs-lookup"><span data-stu-id="dac31-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="dac31-156">Para obter mais informações, consulte [Carregamento em massa](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="dac31-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="dac31-157">Um arquivo de dados de exemplo pode ser encontrado em um contêiner de blobs público, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="dac31-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="dac31-158">conteúdo Olá Olá do arquivo de dados é:</span><span class="sxs-lookup"><span data-stu-id="dac31-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="dac31-159">Opcionalmente, você pode criar um arquivo de texto e carregar a conta de armazenamento do próprio hello arquivos tooyour.</span><span class="sxs-lookup"><span data-stu-id="dac31-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="dac31-160">Para obter instruções hello, consulte [carregar dados para trabalhos de Hadoop no HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="dac31-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="dac31-161">Esse procedimento usa a tabela do HBase contatos Olá que você criou no procedimento última Olá.</span><span class="sxs-lookup"><span data-stu-id="dac31-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="dac31-162">SSH, execute Olá Olá de tootransform comando tooStoreFiles de arquivo de dados e armazenam em um caminho relativo especificado pelo Dimporttsv.bulk.output a seguir.</span><span class="sxs-lookup"><span data-stu-id="dac31-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="dac31-163">Se você estiver no Shell do HBase, use Olá tooexit de comando de saída.</span><span class="sxs-lookup"><span data-stu-id="dac31-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="dac31-164">Execute Olá seguindo os dados de saudação do comando tooupload da tabela do HBase toohello /example/data/storeDataFileOutput:</span><span class="sxs-lookup"><span data-stu-id="dac31-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="dac31-165">Você pode abrir Olá shell do HBase e usar o conteúdo da tabela Olá verificação comando toolist hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="dac31-166">Use a seção tooquery HBase</span><span class="sxs-lookup"><span data-stu-id="dac31-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="dac31-167">Você pode consultar os dados nas tabelas HBase usando o Hive.</span><span class="sxs-lookup"><span data-stu-id="dac31-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="dac31-168">Nesta seção, você cria uma tabela Hive que mapeia a tabela do HBase toohello e usa dados de saudação tooquery em sua tabela do HBase.</span><span class="sxs-lookup"><span data-stu-id="dac31-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="dac31-169">Abra **PuTTY**e conecte-se o cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="dac31-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="dac31-170">Consulte as instruções de saudação no procedimento anterior hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="dac31-171">Da sessão SSH hello, use Olá comando toostart Beeline a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="dac31-172">Para saber mais sobre o Beeline, consulte [Usar o Hive com Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="dac31-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="dac31-173">Execute Olá HiveQL toocreate de script a seguir em uma tabela de Hive que vincula a tabela do HBase toohello.</span><span class="sxs-lookup"><span data-stu-id="dac31-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="dac31-174">Certifique-se de que você criou a tabela de exemplo hello citada anteriormente neste tutorial, usando o shell do HBase Olá antes de executar essa instrução.</span><span class="sxs-lookup"><span data-stu-id="dac31-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="dac31-175">Execute Olá HiveQL script tooquery Olá dados Olá HBase tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="dac31-176">Usar APIs de REST do HBase usando Curl</span><span class="sxs-lookup"><span data-stu-id="dac31-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="dac31-177">Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="dac31-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="dac31-178">Você sempre deve fazer solicitações usando Secure HTTP (HTTPS) toohelp Certifique-se de que suas credenciais são enviadas com segurança toohello server.</span><span class="sxs-lookup"><span data-stu-id="dac31-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="dac31-179">Use Olá comando toolist Olá HBase as tabelas existentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="dac31-180">Use Olá comando toocreate uma nova tabela do HBase com as famílias de duas colunas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="dac31-181">esquema de saudação é fornecida no formato JSon de saudação.</span><span class="sxs-lookup"><span data-stu-id="dac31-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="dac31-182">Use Olá tooinsert de comando a seguir alguns dados:</span><span class="sxs-lookup"><span data-stu-id="dac31-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="dac31-183">Você deve base64 codificar valores hello especificados na opção -d hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="dac31-184">No exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="dac31-184">In hello example:</span></span>
   
   * <span data-ttu-id="dac31-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="dac31-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="dac31-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="dac31-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="dac31-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="dac31-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="dac31-188">[chave de linha False](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert permite vários valores (em lotes).</span><span class="sxs-lookup"><span data-stu-id="dac31-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="dac31-189">Use Olá comando tooget uma linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="dac31-190">Para saber mais sobre o Rest HBase, veja [Guia de referência do Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="dac31-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="dac31-191">Não há suporte para thrift pelo HBase no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dac31-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="dac31-192">Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="dac31-193">Você também deve usar o nome do cluster hello como parte do identificador de recurso uniforme (URI) do hello usado server de toohello toosend Olá solicitações:</span><span class="sxs-lookup"><span data-stu-id="dac31-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="dac31-194">Você deve receber um toohello semelhante resposta resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="dac31-195">Verificar o status do cluster</span><span class="sxs-lookup"><span data-stu-id="dac31-195">Check cluster status</span></span>
<span data-ttu-id="dac31-196">O HBase em HDInsight é fornecido com uma interface do usuário da Web para monitorar clusters.</span><span class="sxs-lookup"><span data-stu-id="dac31-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="dac31-197">Olá IU da Web pode solicitar informações sobre regiões ou estatísticas.</span><span class="sxs-lookup"><span data-stu-id="dac31-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="dac31-198">**Olá tooaccess HBase mestre UI**</span><span class="sxs-lookup"><span data-stu-id="dac31-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="dac31-199">O logon no Olá Olá Ambari Web UI no https://&lt;Clustername >. n e t.</span><span class="sxs-lookup"><span data-stu-id="dac31-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="dac31-200">Clique em **HBase** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="dac31-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="dac31-201">Clique em **links rápidos** Olá superior da página hello, o link de nó ativo em Zookeeper toohello ponto e, em seguida, clique em **HBase mestre UI**.</span><span class="sxs-lookup"><span data-stu-id="dac31-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="dac31-202">Saudação da interface do usuário é aberta em outra guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="dac31-202">hello UI is opened in another browser tab:</span></span>

  ![Interface do Usuário HDInsight HBase HMaster](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="dac31-204">Olá UI HBase mestre contém Olá seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="dac31-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="dac31-205">servidores de região</span><span class="sxs-lookup"><span data-stu-id="dac31-205">region servers</span></span>
  - <span data-ttu-id="dac31-206">mestres de backup</span><span class="sxs-lookup"><span data-stu-id="dac31-206">backup masters</span></span>
  - <span data-ttu-id="dac31-207">tables</span><span class="sxs-lookup"><span data-stu-id="dac31-207">tables</span></span>
  - <span data-ttu-id="dac31-208">tarefas</span><span class="sxs-lookup"><span data-stu-id="dac31-208">tasks</span></span>
  - <span data-ttu-id="dac31-209">atributos de software</span><span class="sxs-lookup"><span data-stu-id="dac31-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="dac31-210">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="dac31-210">Delete hello cluster</span></span>
<span data-ttu-id="dac31-211">tooavoid inconsistências, recomendamos que você desabilite a tabelas do hello HBase antes de excluir o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="dac31-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="dac31-212">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dac31-212">Troubleshoot</span></span>

<span data-ttu-id="dac31-213">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="dac31-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dac31-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dac31-214">Next steps</span></span>
<span data-ttu-id="dac31-215">Neste artigo, você aprendeu como toocreate um cluster HBase e como o modo de exibição e tabelas toocreate Olá dados nessas tabelas de Olá shell do HBase.</span><span class="sxs-lookup"><span data-stu-id="dac31-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="dac31-216">Você também aprendeu como toouse uma seção de consulta em dados em HBase tabelas e como toouse Olá APIs de REST do HBase c# toocreate uma tabela do HBase e recuperar dados da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="dac31-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="dac31-217">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="dac31-217">toolearn more, see:</span></span>

* <span data-ttu-id="dac31-218">[Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.</span><span class="sxs-lookup"><span data-stu-id="dac31-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
