---
title: "aaaUse Hive do Hadoop com ondulação no HDInsight - Azure | Microsoft Docs"
description: "Saiba como enviar tooremotely Pig trabalhos tooHDInsight usando rotação."
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="6b182-103">Executar consultas Hive com Hadoop no HDInsight usando REST</span><span class="sxs-lookup"><span data-stu-id="6b182-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="6b182-104">Saiba como toouse Olá WebHCat REST API toorun Hive consultas com Hadoop no cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b182-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="6b182-105">[Curl](http://curl.haxx.se/) é usado toodemonstrate como você pode interagir com o HDInsight usando solicitações HTTP brutas.</span><span class="sxs-lookup"><span data-stu-id="6b182-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="6b182-106">Olá [jq](http://stedolan.github.io/jq/) utilitário é tooprocess usados dados JSON de saudação retornados de solicitações REST.</span><span class="sxs-lookup"><span data-stu-id="6b182-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="6b182-107">Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte Olá [o que você precisa tooknow sobre Hadoop no HDInsight baseados em Linux](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="6b182-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="6b182-108"><a id="curl"></a>Executar consultas Hive</span><span class="sxs-lookup"><span data-stu-id="6b182-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="6b182-109">Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="6b182-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="6b182-110">Para comandos Olá nesta seção, substitua **USERNAME** com cluster do hello usuário tooauthenticate toohello e substituir **senha** com senha Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="6b182-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="6b182-111">Substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="6b182-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="6b182-112">Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="6b182-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="6b182-113">toohelp Verifique suas credenciais com segurança são sempre enviadas servidor toohello, fazer solicitações usando o HTTP seguro (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="6b182-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="6b182-114">De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="6b182-115">Você receberá um toohello semelhante resposta texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="6b182-116">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="6b182-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="6b182-117">**-u** -Olá nome de usuário e senha usados tooauthenticate solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="6b182-118">**-G** – Indica que essa solicitação é uma operação GET.</span><span class="sxs-lookup"><span data-stu-id="6b182-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="6b182-119">Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="6b182-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="6b182-120">caminho de saudação **/status**, indica que a solicitação Olá tooreturn um status de WebHCat (também conhecido como Templeton) para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="6b182-121">Você também pode solicitar a versão de saudação do Hive usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="6b182-122">Essa solicitação retorna um toohello semelhante resposta texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="6b182-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="6b182-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="6b182-124">Saudação de uso a seguir toocreate uma tabela denominada **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="6b182-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="6b182-125">Olá parâmetros usados com esta solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="6b182-126">**-d** - desde `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="6b182-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="6b182-127">`-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="6b182-128">**User.Name** -usuário Olá que está executando o comando hello.</span><span class="sxs-lookup"><span data-stu-id="6b182-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="6b182-129">**executar** -Olá tooexecute de declarações do HiveQL.</span><span class="sxs-lookup"><span data-stu-id="6b182-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="6b182-130">**statusdir** -diretório Olá Olá status para esse trabalho é gravado.</span><span class="sxs-lookup"><span data-stu-id="6b182-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="6b182-131">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="6b182-132">**DROP TABLE** -se Olá tabela já existir, ele será excluído.</span><span class="sxs-lookup"><span data-stu-id="6b182-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="6b182-133">**CREATE EXTERNAL TABLE** - cria uma nova tabela “externa" em Hive.</span><span class="sxs-lookup"><span data-stu-id="6b182-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="6b182-134">Tabelas externas armazenam a definição da tabela somente Olá no Hive.</span><span class="sxs-lookup"><span data-stu-id="6b182-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="6b182-135">dados de saudação são deixados no local original hello.</span><span class="sxs-lookup"><span data-stu-id="6b182-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b182-136">Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="6b182-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="6b182-137">Por exemplo, um processo de upload de dados automatizados ou outra operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6b182-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="6b182-138">Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="6b182-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="6b182-139">**FORMATO de linha** - como Olá os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="6b182-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="6b182-140">campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="6b182-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="6b182-141">**LOCAL de arquivo de texto como ARMAZENADO** - onde são armazenados dados de saudação (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.</span><span class="sxs-lookup"><span data-stu-id="6b182-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="6b182-142">**Selecione** -seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="6b182-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="6b182-143">Essa instrução retorna um valor de **3**, visto que há três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="6b182-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b182-144">Observe que os espaços de saudação entre declarações do HiveQL são substituídos por Olá `+` quando usado com a rotação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6b182-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="6b182-145">Os valores entre aspas que contêm um espaço, como o delimitador de hello, não devem ser substituídos pelo `+`.</span><span class="sxs-lookup"><span data-stu-id="6b182-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="6b182-146">**INPUT__FILE__NAME como '% 25.log'** - esses arquivos de uso instrução limites Olá pesquisa tooonly termina em. log.</span><span class="sxs-lookup"><span data-stu-id="6b182-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b182-147">Olá `%25` é a forma de codificados de URL de Olá %, para a condição de saudação real é `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="6b182-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="6b182-148">Olá % tem toobe URL codificada, como ele será tratado como um caractere especial em URLs.</span><span class="sxs-lookup"><span data-stu-id="6b182-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="6b182-149">Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="6b182-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="6b182-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="6b182-151">status de Olá toocheck de trabalho Olá Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="6b182-152">Substituir **JOBID** com hello valor retornado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6b182-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="6b182-153">Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="6b182-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="6b182-154">Se o trabalho de saudação tiver sido concluída, o estado de Olá é **êxito**.</span><span class="sxs-lookup"><span data-stu-id="6b182-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b182-155">Essa solicitação de ondulação retorna um documento de JSON JavaScript Object Notation () com informações sobre o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="6b182-156">Jq é usada tooretrieve Olá apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="6b182-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="6b182-157">Depois que o estado de saudação do trabalho Olá mudou muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b182-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="6b182-158">Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, **exemplo/ondulação**.</span><span class="sxs-lookup"><span data-stu-id="6b182-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="6b182-159">Esse endereço armazena a saída de hello em Olá **exemplo/ondulação** diretório no hello clusters de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="6b182-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="6b182-160">Você pode listar e baixar esses arquivos usando Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b182-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="6b182-161">Para obter mais informações sobre como usar o hello CLI do Azure com o armazenamento do Azure, consulte Olá [usar Azure CLI 2.0 com o armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="6b182-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="6b182-162">Olá Use seguindo as instruções toocreate uma nova tabela 'internal' nomeada **em decorrência**:</span><span class="sxs-lookup"><span data-stu-id="6b182-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="6b182-163">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="6b182-164">**CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6b182-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="6b182-165">Essa instrução cria uma tabela interna que é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="6b182-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b182-166">Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.</span><span class="sxs-lookup"><span data-stu-id="6b182-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="6b182-167">**ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC).</span><span class="sxs-lookup"><span data-stu-id="6b182-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="6b182-168">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="6b182-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="6b182-169">**INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="6b182-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="6b182-170">**Selecione** -seleciona todas as linhas de saudação novo **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="6b182-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="6b182-171">Use a ID do trabalho Olá retornada toocheck Olá status do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="6b182-172">Depois que ele foi bem-sucedida, use Olá CLI do Azure conforme descrito anteriormente toodownload e exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b182-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="6b182-173">saída de Hello deve conter três linhas, que contêm **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="6b182-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="6b182-174"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b182-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6b182-175">Para obter informações gerais sobre o Hive com HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6b182-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="6b182-176">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b182-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="6b182-177">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6b182-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="6b182-178">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b182-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6b182-179">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b182-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="6b182-180">Se você estiver usando Tez com Hive, consulte Olá documentos para as informações de depuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="6b182-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="6b182-181">Use Olá exibição Ambari Tez no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="6b182-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="6b182-182">Para obter mais informações sobre Olá API de REST usada neste documento, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.</span><span class="sxs-lookup"><span data-stu-id="6b182-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


