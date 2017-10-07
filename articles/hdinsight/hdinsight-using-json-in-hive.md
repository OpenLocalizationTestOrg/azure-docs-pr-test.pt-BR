---
title: aaaAnalyze e JSON do processo de documentos com Hive no HDInsight | Microsoft Docs
description: "Saiba como toouse JSON documentos e analisá-los usando o Hive no HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="933d5-103">Processar e analisar documentos JSON usando Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="933d5-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="933d5-104">Saiba como tooprocess e analisar arquivos JSON usando Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933d5-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="933d5-105">Olá documento JSON a seguir é usado no tutorial hello:</span><span class="sxs-lookup"><span data-stu-id="933d5-105">hello following JSON document is used in hello tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="933d5-106">Olá arquivo pode ser encontrado em wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="933d5-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="933d5-107">Para obter mais informações sobre como usar o armazenamento de Blobs do Azure com o HDInsight, consulte [Usar o armazenamento de Blobs do Azure compatível com HDFS com o Hadoop no HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="933d5-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="933d5-108">Você pode copiar o contêiner do hello arquivo toohello padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="933d5-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="933d5-109">Neste tutorial, você usar o console de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="933d5-110">Para obter instruções de abrir o console de Hive hello, consulte [uso de Hive do Hadoop no HDInsight com a área de trabalho remota](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="933d5-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="933d5-111">Nivelar os documentos JSON</span><span class="sxs-lookup"><span data-stu-id="933d5-111">Flatten JSON documents</span></span>
<span data-ttu-id="933d5-112">métodos de saudação listados na próxima seção, Olá exigem documento JSON de saudação em uma única linha.</span><span class="sxs-lookup"><span data-stu-id="933d5-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="933d5-113">Portanto, você deve mesclar cadeia de caracteres da tooa documento hello JSON.</span><span class="sxs-lookup"><span data-stu-id="933d5-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="933d5-114">Se o documento JSON já é bidimensional, você pode ignorar esta etapa e vá reta toohello próxima seção dados analisando o JSON.</span><span class="sxs-lookup"><span data-stu-id="933d5-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="933d5-115">Olá arquivo bruto do JSON está localizado em  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="933d5-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="933d5-116">Olá *StudentsRaw* tabela Hive pontos toohello bruto nivelado documento JSON.</span><span class="sxs-lookup"><span data-stu-id="933d5-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="933d5-117">Olá *StudentsOneLine* tabela Hive armazena dados de saudação em Olá HDInsight sistema de arquivos padrão em Olá */json/alunos/* caminho.</span><span class="sxs-lookup"><span data-stu-id="933d5-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="933d5-118">instrução de inserção de saudação preenche a tabela de StudentOneLine de Olá com dados JSON de saudação mesclado.</span><span class="sxs-lookup"><span data-stu-id="933d5-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="933d5-119">instrução SELECT Olá deve retornar apenas uma linha.</span><span class="sxs-lookup"><span data-stu-id="933d5-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="933d5-120">Aqui está a saída de saudação da instrução SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="933d5-120">Here is hello output of hello SELECT statement:</span></span>

![Nivelamento de documento JSON hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="933d5-122">Analisar documentos JSON no Hive</span><span class="sxs-lookup"><span data-stu-id="933d5-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="933d5-123">Hive fornece três mecanismos diferentes toorun consultas em documentos JSON:</span><span class="sxs-lookup"><span data-stu-id="933d5-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="933d5-124">Use Olá GET\_JSON\_objeto UDF (função definida pelo usuário)</span><span class="sxs-lookup"><span data-stu-id="933d5-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="933d5-125">Use Olá JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="933d5-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="933d5-126">usar SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="933d5-126">use custom SerDe</span></span>
* <span data-ttu-id="933d5-127">gravar sua própria UDF usando Python ou outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="933d5-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="933d5-128">Consulte [este artigo][hdinsight-python] sobre como executar seu próprio código Python com o Hive.</span><span class="sxs-lookup"><span data-stu-id="933d5-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="933d5-129">Olá Use GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="933d5-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="933d5-130">O Hive fornece uma UDF interna chamada [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), que pode executar consultas JSON durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="933d5-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="933d5-131">Este método leva dois argumentos – nome da tabela de saudação e o nome do método que tem Olá bidimensional JSON documento e hello campo JSON que precisa toobe analisado.</span><span class="sxs-lookup"><span data-stu-id="933d5-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="933d5-132">Vamos examinar um toosee de exemplo como essa UDF funciona.</span><span class="sxs-lookup"><span data-stu-id="933d5-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="933d5-133">Obter Olá nome e sobrenome de cada aluno</span><span class="sxs-lookup"><span data-stu-id="933d5-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="933d5-134">Aqui está a saída de hello quando executar essa consulta na janela do console.</span><span class="sxs-lookup"><span data-stu-id="933d5-134">Here is hello output when running this query in console window.</span></span>

![UDF get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="933d5-136">Há algumas limitações de get-json_object Olá UDF.</span><span class="sxs-lookup"><span data-stu-id="933d5-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="933d5-137">Como cada campo na consulta Olá requer analisando consulta Olá, ele afeta o desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="933d5-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="933d5-138">OBTER\_JSON_OBJECT() retorna a representação de cadeia de caracteres de saudação de uma matriz.</span><span class="sxs-lookup"><span data-stu-id="933d5-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="933d5-139">tooconvert essa matriz tooa Hive de matriz, você tem toouse expressões regulares tooreplace Olá colchetes quadrados ' [' e ']' e, em seguida, também chamada de divisão tooget matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="933d5-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="933d5-140">É por isso Olá Hive wiki recomenda usar json_tuple.</span><span class="sxs-lookup"><span data-stu-id="933d5-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="933d5-141">Use Olá JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="933d5-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="933d5-142">Outra UDF fornecida pelo Hive é denominada [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), que é mais bem executada do que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="933d5-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="933d5-143">Esse método usa um conjunto de chaves e uma cadeia de caracteres JSON e retorna uma tupla de valores usando uma função.</span><span class="sxs-lookup"><span data-stu-id="933d5-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="933d5-144">Olá consulta a seguir retorna id do estudante hello e a classificação de saudação do documento JSON hello:</span><span class="sxs-lookup"><span data-stu-id="933d5-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="933d5-145">saída de saudação do script no console de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="933d5-145">hello output of this script in hello Hive console:</span></span>

![UDF json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="933d5-147">JSON\_TUPLA usa Olá [lateral exibição](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintaxe no Hive, que permite que o json\_tupla toocreate uma tabela virtual aplicando Olá UDT função tooeach linha da tabela original hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="933d5-148">Use JSON complexo ficar muito pesado devido a saudação repetida da exibição LATERAL.</span><span class="sxs-lookup"><span data-stu-id="933d5-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="933d5-149">Além disso, JSON_TUPLE não pode manipular JSONs aninhados.</span><span class="sxs-lookup"><span data-stu-id="933d5-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="933d5-150">Usar SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="933d5-150">Use custom SerDe</span></span>
<span data-ttu-id="933d5-151">SerDe é a melhor opção Olá para análise de documentos JSON aninhados, permite que você use Olá esquema tooparse Olá documentos e esquema JSON toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="933d5-152">Neste tutorial, você usar um dos Olá SerDe mais popular que foi desenvolvido pela [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="933d5-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="933d5-153">**toouse Olá SerDe personalizado:**</span><span class="sxs-lookup"><span data-stu-id="933d5-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="933d5-154">Instale o [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="933d5-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="933d5-155">Escolha a versão de Windows X64 de saudação do hello JDK se for toobe usando a implantação do Windows hello do HDInsight</span><span class="sxs-lookup"><span data-stu-id="933d5-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="933d5-156">O JDK 1.8 não funciona com este SerDe.</span><span class="sxs-lookup"><span data-stu-id="933d5-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="933d5-157">Após a instalação de saudação, adicione uma nova variável de ambiente do usuário:</span><span class="sxs-lookup"><span data-stu-id="933d5-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="933d5-158">Abra **exibição configurações avançadas do sistema** da tela do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="933d5-159">Clique em **Variáveis de Ambiente**.</span><span class="sxs-lookup"><span data-stu-id="933d5-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="933d5-160">Adicionar um novo **JAVA_HOME** variável de ambiente aponta muito**Files\Java\jdk1.7.0_55 C:\Program** ou onde quer que o seu JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="933d5-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Definir valores de configuração correto para o JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="933d5-162">Instale o [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="933d5-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="933d5-163">Adicionar tooyour caminho da pasta de compartimento Olá indo tooControl painel--> Editar Olá variáveis de sistema para as variáveis de ambiente de conta.</span><span class="sxs-lookup"><span data-stu-id="933d5-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="933d5-164">Olá seguinte captura de tela mostra como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="933d5-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Configurando o Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="933d5-166">Projeto de saudação do clone de [SerDe de JSON de Hive](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) site do github.</span><span class="sxs-lookup"><span data-stu-id="933d5-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="933d5-167">Você pode fazer isso clicando no botão de "Baixar Zip" hello conforme Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="933d5-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Projeto de clonagem Olá][image-hdi-hivejson-serde]

<span data-ttu-id="933d5-169">4: go toohello pasta onde você baixou este pacote e, em seguida, tipo do pacote"mvn".</span><span class="sxs-lookup"><span data-stu-id="933d5-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="933d5-170">Isso deve criar hello arquivos jar necessários que você pode copiar sobre toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="933d5-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="933d5-171">5: pasta de destino toohello go na pasta raiz de saudação onde você baixou o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="933d5-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="933d5-172">Carregar Olá arquivo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar toohead nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="933d5-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="933d5-173">Geralmente colocou na pasta de binários de hive Olá: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin ou algo semelhante.</span><span class="sxs-lookup"><span data-stu-id="933d5-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="933d5-174">6: no prompt de hive hello, digite "Adicionar jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="933d5-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="933d5-175">Como no meu caso, jar hello está na pasta de C:\apps\dist\hive-0.13.x\bin hello, posso adicionar diretamente Olá jar com nome hello conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="933d5-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Adicionar JAR tooyour projeto][image-hdi-hivejson-addjar]

<span data-ttu-id="933d5-177">Agora, você está pronto toouse Olá SerDe toorun consultas documento JSON hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="933d5-178">Olá instrução a seguir cria uma tabela com um esquema definido:</span><span class="sxs-lookup"><span data-stu-id="933d5-178">hello following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="933d5-179">toolist Olá nome e sobrenome do aluno Olá</span><span class="sxs-lookup"><span data-stu-id="933d5-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="933d5-180">Este é o resultado de saudação do console de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-180">Here is hello result from hello Hive console.</span></span>

![Consulta SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="933d5-182">soma de saudação toocalculate de pontuações de documento JSON Olá</span><span class="sxs-lookup"><span data-stu-id="933d5-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="933d5-183">Olá anterior a consulta usa [exibição lateral Detalhar](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand UDF Olá matriz de resultados para que eles podem ser somados.</span><span class="sxs-lookup"><span data-stu-id="933d5-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="933d5-184">Aqui está a saída de saudação do console de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="933d5-184">Here is hello output from hello Hive console.</span></span>

![Consulta SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="933d5-186">toofind que um determinado aluno os assuntos tem mais de 80 pontos de pontuação:</span><span class="sxs-lookup"><span data-stu-id="933d5-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="933d5-187">Olá, consulta anterior retorna uma matriz de Hive diferentemente get\_json\_objeto, que retorna uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="933d5-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Consulta SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="933d5-189">Se você quiser tooskil JSON malformado, em seguida, como explicado no hello [página wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) dessa SerDe, você pode obter que digitando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="933d5-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="933d5-190">Resumo</span><span class="sxs-lookup"><span data-stu-id="933d5-190">Summary</span></span>
<span data-ttu-id="933d5-191">Olá Concluindo, tipo de operador JSON no Hive que você escolher depende de seu cenário.</span><span class="sxs-lookup"><span data-stu-id="933d5-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="933d5-192">Se você tiver um documento JSON simple e tiver apenas um toolook de campo para cima – você pode escolher toouse Olá Hive UDF get\_json\_objeto.</span><span class="sxs-lookup"><span data-stu-id="933d5-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="933d5-193">Se você tiver mais de um toolook chave, em seguida, você pode usar json_tuple.</span><span class="sxs-lookup"><span data-stu-id="933d5-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="933d5-194">Se você tiver um documento aninhado, você deve usar Olá SerDe de JSON.</span><span class="sxs-lookup"><span data-stu-id="933d5-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="933d5-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="933d5-195">Next steps</span></span>

<span data-ttu-id="933d5-196">Para outros artigos relacionados, consulte</span><span class="sxs-lookup"><span data-stu-id="933d5-196">For other related articles, see</span></span>

* [<span data-ttu-id="933d5-197">Use o Hive e HiveQL com Hadoop no HDInsight tooanalyze um exemplo de um arquivo de log4j Apache</span><span class="sxs-lookup"><span data-stu-id="933d5-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="933d5-198">Analisar dados de atrasos de voos usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="933d5-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="933d5-199">Analisar dados do Twitter usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="933d5-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="933d5-200">Executar um trabalho do Hadoop usando o Azure Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="933d5-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
