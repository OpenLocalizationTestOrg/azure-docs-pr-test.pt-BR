---
title: "Usar o Hive do Hadoop com Curl no HDInsight – Azure | Microsoft Docs"
description: Saiba como enviar remotamente trabalhos do Pig para o HDInsight usando o Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="83a3c-103">Executar consultas Hive com Hadoop no HDInsight usando REST</span><span class="sxs-lookup"><span data-stu-id="83a3c-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="83a3c-104">Saiba como usar a API REST do WebHCat para executar consultas Hive com o Hadoop no cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="83a3c-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="83a3c-105">O [Curl](http://curl.haxx.se/) é usado para demonstrar como você pode interagir com o HDInsight usando solicitações HTTP brutas.</span><span class="sxs-lookup"><span data-stu-id="83a3c-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="83a3c-106">O utilitário [jq](http://stedolan.github.io/jq/) é usado para processar os dados JSON retornados de solicitações REST.</span><span class="sxs-lookup"><span data-stu-id="83a3c-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="83a3c-107">Se você já estiver familiarizado com o uso de servidores Hadoop baseados em Linux, mas for iniciante no HDInsight, consulte o documento [O que você precisa saber sobre o Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="83a3c-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="83a3c-108"><a id="curl"></a>Executar consultas Hive</span><span class="sxs-lookup"><span data-stu-id="83a3c-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="83a3c-109">Ao usar o cURL ou qualquer outra comunicação REST com WebHCat, você deve autenticar as solicitações, fornecendo o nome de usuário e a senha para o administrador do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83a3c-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="83a3c-110">Para os comandos nesta seção, substitua **USERNAME** pelo usuário para autenticar o cluster e substitua **PASSWORD** pela senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="83a3c-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="83a3c-111">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="83a3c-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="83a3c-112">A API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="83a3c-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="83a3c-113">Para ajudar a garantir que suas credenciais sejam enviadas com segurança para o servidor, sempre faça solicitações usando HTTPS (HTTP seguro).</span><span class="sxs-lookup"><span data-stu-id="83a3c-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="83a3c-114">De uma linha de comando, use o seguinte comando para verificar se você pode se conectar ao cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="83a3c-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="83a3c-115">Você deve receber uma resposta semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="83a3c-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="83a3c-116">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="83a3c-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="83a3c-117">**-u** - o nome de usuário e a senha usada para autenticar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="83a3c-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="83a3c-118">**-G** – Indica que essa solicitação é uma operação GET.</span><span class="sxs-lookup"><span data-stu-id="83a3c-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="83a3c-119">O início da URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será o mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="83a3c-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="83a3c-120">O caminho, **/status**, indica que a solicitação é para retornar o status de WebHCat (também conhecido como Templeton) ao servidor.</span><span class="sxs-lookup"><span data-stu-id="83a3c-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="83a3c-121">Você também pode solicitar a versão do Hive usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="83a3c-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="83a3c-122">Essa solicitação retorna uma resposta semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="83a3c-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="83a3c-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="83a3c-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="83a3c-124">Use o seguinte para criar uma tabela chamada **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="83a3c-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="83a3c-125">Os seguintes parâmetros são usados com esta solicitação:</span><span class="sxs-lookup"><span data-stu-id="83a3c-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="83a3c-126">**-d** – uma vez que `-G` não é usado; a solicitação padrão é o método POST.</span><span class="sxs-lookup"><span data-stu-id="83a3c-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="83a3c-127">`-d` especifica os valores de dados que são enviados com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="83a3c-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="83a3c-128">**user.name** - o usuário que está executando o comando.</span><span class="sxs-lookup"><span data-stu-id="83a3c-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="83a3c-129">**execute** - as instruções do HiveQL a executar.</span><span class="sxs-lookup"><span data-stu-id="83a3c-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="83a3c-130">**statusdir** – O diretório no qual o status deste trabalho será gravado.</span><span class="sxs-lookup"><span data-stu-id="83a3c-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="83a3c-131">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="83a3c-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="83a3c-132">**DROP TABLE** – Se a tabela já existir, ela será excluída.</span><span class="sxs-lookup"><span data-stu-id="83a3c-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="83a3c-133">**CREATE EXTERNAL TABLE** - cria uma nova tabela “externa" em Hive.</span><span class="sxs-lookup"><span data-stu-id="83a3c-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="83a3c-134">As tabelas externas armazenam apenas a definição da tabela no Hive.</span><span class="sxs-lookup"><span data-stu-id="83a3c-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="83a3c-135">Os dados são mantidos no local original.</span><span class="sxs-lookup"><span data-stu-id="83a3c-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="83a3c-136">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="83a3c-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="83a3c-137">Por exemplo, um processo de upload de dados automatizados ou outra operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="83a3c-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="83a3c-138">Remover uma tabela externa **não** exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="83a3c-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="83a3c-139">**ROW FORMAT** – O modo como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="83a3c-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="83a3c-140">Os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="83a3c-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="83a3c-141">**STORED AS TEXTFILE LOCATION** – Onde os dados são armazenados (o diretório de exemplos/dados) e que estão armazenados como texto.</span><span class="sxs-lookup"><span data-stu-id="83a3c-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="83a3c-142">**SELECT** - Seleciona uma contagem de todas as linhas em que a coluna **t4** contém o valor **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="83a3c-143">Essa instrução retorna um valor de **3**, visto que há três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="83a3c-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="83a3c-144">Observe que os espaços entre as instruções HiveQL são substituídos pelo caractere `+` quando usados com o Curl.</span><span class="sxs-lookup"><span data-stu-id="83a3c-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="83a3c-145">Os valores entre aspas que contêm um espaço, como o delimitador, não devem ser substituídos por `+`.</span><span class="sxs-lookup"><span data-stu-id="83a3c-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="83a3c-146">**INPUT__FILE__NAME LIKE '%25.log'** – Essa instrução limita a pesquisa a usar somente os arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="83a3c-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="83a3c-147">Observe que `%25` é o formato de % codificado para URL, então, a condição real é `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="83a3c-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="83a3c-148">O % deve ser codificado em URL, pois será tratado como um caractere especial em URLs.</span><span class="sxs-lookup"><span data-stu-id="83a3c-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="83a3c-149">Esse comando deve retornar uma ID de trabalho que pode ser usada para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="83a3c-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="83a3c-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="83a3c-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="83a3c-151">Para verificar o status do trabalho, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="83a3c-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="83a3c-152">Substitua **JOBID** pelo valor retornado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="83a3c-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="83a3c-153">Por exemplo, se o valor retornado for **, `{"id":"job_1415651640909_0026"}`JOBID** será `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="83a3c-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="83a3c-154">Se o trabalho foi concluído, o estado será **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="83a3c-155">Essa solicitação de Curl retorna um documento JSON (JavaScript Object Notation) com informações sobre o trabalho.</span><span class="sxs-lookup"><span data-stu-id="83a3c-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="83a3c-156">Jq é usado para recuperar apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="83a3c-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="83a3c-157">Depois que o estado do trabalho for alterado para **SUCCEEDED**, você poderá recuperar os resultados do trabalho no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="83a3c-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="83a3c-158">O parâmetro `statusdir` transmitido com a consulta contém o local do arquivo de saída; nesse caso, **/example/curl**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="83a3c-159">Esse endereço armazena a saída do diretório **exemplo/curl** no armazenamento padrão de clusters.</span><span class="sxs-lookup"><span data-stu-id="83a3c-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="83a3c-160">Você pode listar e baixar esses arquivos usando a [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="83a3c-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="83a3c-161">Para obter mais informações sobre como usar a CLI do Azure com o Armazenamento do Azure, consulte o armazenamento [Usar a CLI 2.0 do Azure com o Armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="83a3c-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="83a3c-162">Use as instruções a seguir para criar uma nova tabela "interna" chamada **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="83a3c-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="83a3c-163">Essas instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="83a3c-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="83a3c-164">**CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="83a3c-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="83a3c-165">Esta instrução cria uma tabela interna, que é armazenada no data warehouse do Hive e é totalmente gerenciada por ele.</span><span class="sxs-lookup"><span data-stu-id="83a3c-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="83a3c-166">Diferentemente de tabelas externas, o descarte de uma tabela interna excluirá também os dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="83a3c-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="83a3c-167">**STORES AS ORC** : armazena os dados no formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="83a3c-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="83a3c-168">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="83a3c-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="83a3c-169">**INSERT OVERWRITE ... SELECT** - seleciona linhas da tabela **log4jLogs** que contêm **[ERROR]** e insere os dados na tabela **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="83a3c-170">**SELECT** – Seleciona todas as linhas da nova tabela **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="83a3c-171">Use a ID de trabalho retornada para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="83a3c-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="83a3c-172">Assim que tiver êxito, use a CLI do Azure, conforme descrito anteriormente, para baixar e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="83a3c-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="83a3c-173">A saída deve conter três linhas, todos os quais contêm **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="83a3c-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="83a3c-174"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83a3c-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="83a3c-175">Para obter informações gerais sobre o Hive com HDInsight:</span><span class="sxs-lookup"><span data-stu-id="83a3c-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="83a3c-176">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="83a3c-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="83a3c-177">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="83a3c-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="83a3c-178">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="83a3c-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="83a3c-179">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="83a3c-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="83a3c-180">Se você estiver usando o Tez com o Hive, consulte os seguintes documentos para as informações de depuração:</span><span class="sxs-lookup"><span data-stu-id="83a3c-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="83a3c-181">Usar a exibição de Ambari Tez no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="83a3c-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="83a3c-182">Para obter mais informações sobre a API REST usada nesse documento, consulte o documento [Referência de WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="83a3c-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


