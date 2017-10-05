---
title: "Introdução a um exemplo do HBase no HDInsight - Azure | Microsoft Docs"
description: "Siga este exemplo do Apache HBase para começar a usar o hadoop no HDInsight. Criar tabelas a partir do shell do HBase e consultá-las usando o Hive."
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
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="1316d-105">Introdução a um exemplo do Apache HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1316d-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="1316d-106">Saiba como criar um cluster HBase no HDInsight, criar tabelas HBase e consultar as tabelas usando o Hive.</span><span class="sxs-lookup"><span data-stu-id="1316d-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="1316d-107">Para obter informações gerais do HBase, confira [Visão geral do HBase do HDInsight][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="1316d-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="1316d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1316d-108">Prerequisites</span></span>
<span data-ttu-id="1316d-109">Antes de começar este tutorial do HBase, você deverá ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1316d-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="1316d-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="1316d-110">**An Azure subscription**.</span></span> <span data-ttu-id="1316d-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1316d-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1316d-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1316d-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="1316d-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="1316d-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="1316d-114">Nome do cluster HBase</span><span class="sxs-lookup"><span data-stu-id="1316d-114">Create HBase cluster</span></span>
<span data-ttu-id="1316d-115">O procedimento a seguir usa um modelo do Azure Resource Manager para criar um cluster do HBase baseado em Linux versão 3.4 e a conta de Armazenamento do Azure padrão dependente.</span><span class="sxs-lookup"><span data-stu-id="1316d-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="1316d-116">Para compreender os parâmetros usados no procedimento e em outros métodos de criação de cluster, consulte [Criar clusters Hadoop baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1316d-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="1316d-117">Clique na imagem a seguir para abrir o modelo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1316d-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="1316d-118">O modelo está localizado em um contêiner de blob público.</span><span class="sxs-lookup"><span data-stu-id="1316d-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="1316d-119">Na folha **Implantação personalizada**, insira os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="1316d-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="1316d-120">**Assinatura**: Selecione sua assinatura do Azure que é usada para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="1316d-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="1316d-121">**Grupo de recursos**: Crie um grupo de Gerenciamento de Recursos do Azure ou use um existente.</span><span class="sxs-lookup"><span data-stu-id="1316d-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="1316d-122">**Local**: especifique o local do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1316d-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="1316d-123">**ClusterName**: Insira um nome para o cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="1316d-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="1316d-124">**Nome e senha de logon do cluster**: o nome de logon padrão é **admin**.</span><span class="sxs-lookup"><span data-stu-id="1316d-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="1316d-125">**Nome de usuário e senha SSH**: o nome de usuário padrão é **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="1316d-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="1316d-126">Você pode renomeá-lo.</span><span class="sxs-lookup"><span data-stu-id="1316d-126">You can rename it.</span></span>
     
     <span data-ttu-id="1316d-127">Outros parâmetros são opcionais.</span><span class="sxs-lookup"><span data-stu-id="1316d-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="1316d-128">Cada cluster tem uma dependência de conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1316d-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="1316d-129">Depois que você excluir um cluster, os dados serão mantidos na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1316d-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="1316d-130">O nome de conta de armazenamento padrão do cluster é o nome do cluster com "store" acrescentado.</span><span class="sxs-lookup"><span data-stu-id="1316d-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="1316d-131">Ele é codificado na seção de variáveis do modelo.</span><span class="sxs-lookup"><span data-stu-id="1316d-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="1316d-132">Selecione **Concordo com os termos e condições declarados acima** e clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="1316d-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="1316d-133">Demora cerca de 20 minutos para criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="1316d-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1316d-134">Depois que um cluster HBase for excluído, você pode criar outro cluster HBase usando o mesmo contêiner de blob padrão.</span><span class="sxs-lookup"><span data-stu-id="1316d-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="1316d-135">O novo cluster seleciona as tabelas HBase criadas por você no cluster original.</span><span class="sxs-lookup"><span data-stu-id="1316d-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="1316d-136">É recomendável desabilitar as tabelas HBase antes de excluir o cluster para evitar inconsistências.</span><span class="sxs-lookup"><span data-stu-id="1316d-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="1316d-137">Criar tabelas e inserir dados</span><span class="sxs-lookup"><span data-stu-id="1316d-137">Create tables and insert data</span></span>
<span data-ttu-id="1316d-138">Você pode usar o SSH para se conectar aos clusters HBase e usar o Shell do HBase para criar tabelas HBase, inserir dados e consultar dados.</span><span class="sxs-lookup"><span data-stu-id="1316d-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="1316d-139">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1316d-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="1316d-140">Para a maioria das pessoas, os dados aparecem no formato de tabela:</span><span class="sxs-lookup"><span data-stu-id="1316d-140">For most people, data appears in the tabular format:</span></span>

![dados tabulares do HBase HDInsight][img-hbase-sample-data-tabular]

<span data-ttu-id="1316d-142">No HBase (uma implementação de BigTable) os mesmos dados são assim:</span><span class="sxs-lookup"><span data-stu-id="1316d-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![Dados BigTable do HBase HDInsight][img-hbase-sample-data-bigtable]


<span data-ttu-id="1316d-144">**Para usar o shell HBase**</span><span class="sxs-lookup"><span data-stu-id="1316d-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="1316d-145">No SSH, execute este comando HBase:</span><span class="sxs-lookup"><span data-stu-id="1316d-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="1316d-146">Crie um HBase com famílias de duas colunas:</span><span class="sxs-lookup"><span data-stu-id="1316d-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="1316d-147">Insira alguns dados:</span><span class="sxs-lookup"><span data-stu-id="1316d-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell do HBase do Hadoop HDInsight][img-hbase-shell]
4. <span data-ttu-id="1316d-149">Obter uma única linha</span><span class="sxs-lookup"><span data-stu-id="1316d-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="1316d-150">Você deverá ver os mesmos resultados que aqueles exibidos ao usar o comando de verificação, porque há apenas uma linha.</span><span class="sxs-lookup"><span data-stu-id="1316d-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="1316d-151">Para saber mais sobre o esquema da tabela HBase, confira [Introdução ao design de esquema HBase][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="1316d-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="1316d-152">Para obter mais comandos HBase, confira [Guia de referência do Apache HBase][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="1316d-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="1316d-153">Sair do shell</span><span class="sxs-lookup"><span data-stu-id="1316d-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="1316d-154">**Para carregar dados em massa na tabela de contatos HBase**</span><span class="sxs-lookup"><span data-stu-id="1316d-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="1316d-155">O HBase inclui vários métodos de carregamento de dados em tabelas.</span><span class="sxs-lookup"><span data-stu-id="1316d-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="1316d-156">Para obter mais informações, consulte [Carregamento em massa](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="1316d-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="1316d-157">Um arquivo de dados de exemplo pode ser encontrado em um contêiner de blobs público, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span><span class="sxs-lookup"><span data-stu-id="1316d-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="1316d-158">O conteúdo do arquivo de dados é:</span><span class="sxs-lookup"><span data-stu-id="1316d-158">The content of the data file is:</span></span>

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

<span data-ttu-id="1316d-159">Você pode, opcionalmente, criar um arquivo de texto e carregá-lo na sua própria conta de armazenamento se desejar.</span><span class="sxs-lookup"><span data-stu-id="1316d-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="1316d-160">Para obter instruções, confira [Carregar dados para trabalhos de Hadoop no HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="1316d-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="1316d-161">Este procedimento usa a tabela de contatos HBase que você criou no último procedimento.</span><span class="sxs-lookup"><span data-stu-id="1316d-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="1316d-162">No SSH, execute o seguinte comando para transformar o arquivo de dados para o StoreFiles e armazene em um caminho relativo especificado por Dimporttsv.bulk.output.</span><span class="sxs-lookup"><span data-stu-id="1316d-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="1316d-163">Se você estiver no Shell do HBase, use o comando exit para sair.</span><span class="sxs-lookup"><span data-stu-id="1316d-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="1316d-164">Execute o seguinte comando para carregar os dados de /example/data/storeDataFileOutput para a tabela do HBase:</span><span class="sxs-lookup"><span data-stu-id="1316d-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="1316d-165">Você pode abrir o shell do HBase e usar o comando de verificação para listar o conteúdo da tabela.</span><span class="sxs-lookup"><span data-stu-id="1316d-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="1316d-166">Usar o Hive para consultar o HBase</span><span class="sxs-lookup"><span data-stu-id="1316d-166">Use Hive to query HBase</span></span>

<span data-ttu-id="1316d-167">Você pode consultar os dados nas tabelas HBase usando o Hive.</span><span class="sxs-lookup"><span data-stu-id="1316d-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="1316d-168">Nesta seção você cria uma tabela Hive que faz o mapeamento para a tabela do HBase e usa-a para consultar os dados em sua tabela do HBase.</span><span class="sxs-lookup"><span data-stu-id="1316d-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="1316d-169">Abra o **PuTTY**e conecte-se ao cluster.</span><span class="sxs-lookup"><span data-stu-id="1316d-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="1316d-170">Consulte as instruções no procedimento anterior.</span><span class="sxs-lookup"><span data-stu-id="1316d-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="1316d-171">Na sessão de SSH, use o seguinte comando para iniciar o Beeline:</span><span class="sxs-lookup"><span data-stu-id="1316d-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="1316d-172">Para saber mais sobre o Beeline, consulte [Usar o Hive com Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="1316d-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="1316d-173">Execute o script do HiveQL a seguir para criar uma tabela Hive que é mapeada para a tabela do HBase.</span><span class="sxs-lookup"><span data-stu-id="1316d-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="1316d-174">Assegure-se de ter criado a tabela de amostra referenciada anteriormente neste tutorial, usando o Shell HBase antes de executar esta instrução.</span><span class="sxs-lookup"><span data-stu-id="1316d-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="1316d-175">Execute o seguinte script do HiveQL para consultar os dados na tabela do HBase:</span><span class="sxs-lookup"><span data-stu-id="1316d-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="1316d-176">Usar APIs de REST do HBase usando Curl</span><span class="sxs-lookup"><span data-stu-id="1316d-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="1316d-177">A API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="1316d-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="1316d-178">Você deve sempre fazer solicitações usando HTTPS (HTTP seguro) para ajudar a garantir que suas credenciais sejam enviadas com segurança para o servidor.</span><span class="sxs-lookup"><span data-stu-id="1316d-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="1316d-179">Use o seguinte comando para listar as tabelas HBase:</span><span class="sxs-lookup"><span data-stu-id="1316d-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="1316d-180">Use o seguinte comando para criar uma nova tabela HBase com famílias de duas colunas:</span><span class="sxs-lookup"><span data-stu-id="1316d-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="1316d-181">O esquema é fornecido no formato JSon.</span><span class="sxs-lookup"><span data-stu-id="1316d-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="1316d-182">Use o comando a seguir para inserir alguns dados:</span><span class="sxs-lookup"><span data-stu-id="1316d-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="1316d-183">Você deve codificar em base64 os valores especificados na opção -d.</span><span class="sxs-lookup"><span data-stu-id="1316d-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="1316d-184">No exemplo:</span><span class="sxs-lookup"><span data-stu-id="1316d-184">In the example:</span></span>
   
   * <span data-ttu-id="1316d-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="1316d-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="1316d-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="1316d-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="1316d-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="1316d-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="1316d-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) permite inserir diversos valores (em lote).</span><span class="sxs-lookup"><span data-stu-id="1316d-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="1316d-189">Use o comando a seguir para obter uma linha:</span><span class="sxs-lookup"><span data-stu-id="1316d-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="1316d-190">Para saber mais sobre o Rest HBase, veja [Guia de referência do Apache HBase](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="1316d-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="1316d-191">Não há suporte para thrift pelo HBase no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1316d-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="1316d-192">Ao usar o Curl ou qualquer outra comunicação do REST com WebHCat, você deve autenticar as solicitações, fornecendo o nome de usuário e a senha para o administrador do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1316d-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="1316d-193">Você também deve usar o nome do cluster como parte do Uniform Resource Identifier (URI) usado para enviar as solicitações ao servidor:</span><span class="sxs-lookup"><span data-stu-id="1316d-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="1316d-194">Você deve receber uma resposta semelhante à resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="1316d-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="1316d-195">Verificar o status do cluster</span><span class="sxs-lookup"><span data-stu-id="1316d-195">Check cluster status</span></span>
<span data-ttu-id="1316d-196">O HBase em HDInsight é fornecido com uma interface do usuário da Web para monitorar clusters.</span><span class="sxs-lookup"><span data-stu-id="1316d-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="1316d-197">Usando a interface do usuário da Web, você pode solicitar estatísticas ou informações sobre regiões.</span><span class="sxs-lookup"><span data-stu-id="1316d-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="1316d-198">**Para acessar a interface do usuário mestre HBase**</span><span class="sxs-lookup"><span data-stu-id="1316d-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="1316d-199">Entre na interface do usuário da Web do Ambari em https://&lt;Clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1316d-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="1316d-200">Clique em **HBase** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="1316d-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="1316d-201">Clique em **Links rápidos** no topo da página, aponte para o link de nó ativo do Zookeeper e, em seguida, clique em **Interface do usuário mestre HBase**.</span><span class="sxs-lookup"><span data-stu-id="1316d-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="1316d-202">A interface do usuário é aberta em outra guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="1316d-202">The UI is opened in another browser tab:</span></span>

  ![Interface do Usuário HDInsight HBase HMaster](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="1316d-204">A Interface do Usuário Mestre HBase contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="1316d-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="1316d-205">servidores de região</span><span class="sxs-lookup"><span data-stu-id="1316d-205">region servers</span></span>
  - <span data-ttu-id="1316d-206">mestres de backup</span><span class="sxs-lookup"><span data-stu-id="1316d-206">backup masters</span></span>
  - <span data-ttu-id="1316d-207">tables</span><span class="sxs-lookup"><span data-stu-id="1316d-207">tables</span></span>
  - <span data-ttu-id="1316d-208">tarefas</span><span class="sxs-lookup"><span data-stu-id="1316d-208">tasks</span></span>
  - <span data-ttu-id="1316d-209">atributos de software</span><span class="sxs-lookup"><span data-stu-id="1316d-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="1316d-210">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="1316d-210">Delete the cluster</span></span>
<span data-ttu-id="1316d-211">É recomendável desabilitar as tabelas HBase antes de excluir o cluster para evitar inconsistências.</span><span class="sxs-lookup"><span data-stu-id="1316d-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="1316d-212">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="1316d-212">Troubleshoot</span></span>

<span data-ttu-id="1316d-213">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="1316d-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1316d-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1316d-214">Next steps</span></span>
<span data-ttu-id="1316d-215">Neste artigo, você aprendeu a criar um cluster HBase, criar tabelas e exibir os dados nessas tabelas por meio do shell HBase.</span><span class="sxs-lookup"><span data-stu-id="1316d-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="1316d-216">Você também aprendeu a usar a consulta do Hive dos dados em tabelas HBase e como usar as APIs REST C# do HBase para criar uma tabela HBase e recuperar dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="1316d-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="1316d-217">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="1316d-217">To learn more, see:</span></span>

* <span data-ttu-id="1316d-218">[Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.</span><span class="sxs-lookup"><span data-stu-id="1316d-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

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
