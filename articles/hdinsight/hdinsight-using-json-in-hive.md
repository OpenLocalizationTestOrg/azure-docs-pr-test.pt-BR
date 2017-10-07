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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Processar e analisar documentos JSON usando Hive no HDInsight

Saiba como tooprocess e analisar arquivos JSON usando Hive no HDInsight. Olá documento JSON a seguir é usado no tutorial hello:

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

Olá arquivo pode ser encontrado em wasb://processjson@hditutorialdata.blob.core.windows.net/. Para obter mais informações sobre como usar o armazenamento de Blobs do Azure com o HDInsight, consulte [Usar o armazenamento de Blobs do Azure compatível com HDFS com o Hadoop no HDInsight](hdinsight-hadoop-use-blob-storage.md). Você pode copiar o contêiner do hello arquivo toohello padrão do cluster.

Neste tutorial, você usar o console de Hive hello.  Para obter instruções de abrir o console de Hive hello, consulte [uso de Hive do Hadoop no HDInsight com a área de trabalho remota](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Nivelar os documentos JSON
métodos de saudação listados na próxima seção, Olá exigem documento JSON de saudação em uma única linha. Portanto, você deve mesclar cadeia de caracteres da tooa documento hello JSON. Se o documento JSON já é bidimensional, você pode ignorar esta etapa e vá reta toohello próxima seção dados analisando o JSON.

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

Olá arquivo bruto do JSON está localizado em  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Olá *StudentsRaw* tabela Hive pontos toohello bruto nivelado documento JSON.

Olá *StudentsOneLine* tabela Hive armazena dados de saudação em Olá HDInsight sistema de arquivos padrão em Olá */json/alunos/* caminho.

instrução de inserção de saudação preenche a tabela de StudentOneLine de Olá com dados JSON de saudação mesclado.

instrução SELECT Olá deve retornar apenas uma linha.

Aqui está a saída de saudação da instrução SELECT hello:

![Nivelamento de documento JSON hello.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Analisar documentos JSON no Hive
Hive fornece três mecanismos diferentes toorun consultas em documentos JSON:

* Use Olá GET\_JSON\_objeto UDF (função definida pelo usuário)
* Use Olá JSON_TUPLE UDF
* usar SerDe personalizado
* gravar sua própria UDF usando Python ou outras linguagens. Consulte [este artigo][hdinsight-python] sobre como executar seu próprio código Python com o Hive.

### <a name="use-hello-getjsonobject-udf"></a>Olá Use GET\_JSON_OBJECT UDF
O Hive fornece uma UDF interna chamada [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), que pode executar consultas JSON durante o tempo de execução. Este método leva dois argumentos – nome da tabela de saudação e o nome do método que tem Olá bidimensional JSON documento e hello campo JSON que precisa toobe analisado. Vamos examinar um toosee de exemplo como essa UDF funciona.

Obter Olá nome e sobrenome de cada aluno

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Aqui está a saída de hello quando executar essa consulta na janela do console.

![UDF get_json_object][image-hdi-hivejson-getjsonobject]

Há algumas limitações de get-json_object Olá UDF.

* Como cada campo na consulta Olá requer analisando consulta Olá, ele afeta o desempenho de saudação.
* OBTER\_JSON_OBJECT() retorna a representação de cadeia de caracteres de saudação de uma matriz. tooconvert essa matriz tooa Hive de matriz, você tem toouse expressões regulares tooreplace Olá colchetes quadrados ' [' e ']' e, em seguida, também chamada de divisão tooget matriz de saudação.

É por isso Olá Hive wiki recomenda usar json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Use Olá JSON_TUPLE UDF
Outra UDF fornecida pelo Hive é denominada [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), que é mais bem executada do que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Esse método usa um conjunto de chaves e uma cadeia de caracteres JSON e retorna uma tupla de valores usando uma função. Olá consulta a seguir retorna id do estudante hello e a classificação de saudação do documento JSON hello:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

saída de saudação do script no console de Hive hello:

![UDF json_tuple][image-hdi-hivejson-jsontuple]

JSON\_TUPLA usa Olá [lateral exibição](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintaxe no Hive, que permite que o json\_tupla toocreate uma tabela virtual aplicando Olá UDT função tooeach linha da tabela original hello.  Use JSON complexo ficar muito pesado devido a saudação repetida da exibição LATERAL. Além disso, JSON_TUPLE não pode manipular JSONs aninhados.

### <a name="use-custom-serde"></a>Usar SerDe personalizado
SerDe é a melhor opção Olá para análise de documentos JSON aninhados, permite que você use Olá esquema tooparse Olá documentos e esquema JSON toodefine hello. Neste tutorial, você usar um dos Olá SerDe mais popular que foi desenvolvido pela [Roberto Congiu](https://github.com/rcongiu).

**toouse Olá SerDe personalizado:**

1. Instale o [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Escolha a versão de Windows X64 de saudação do hello JDK se for toobe usando a implantação do Windows hello do HDInsight
   
   > [!WARNING]
   > O JDK 1.8 não funciona com este SerDe.
   > 
   > 
   
    Após a instalação de saudação, adicione uma nova variável de ambiente do usuário:
   
   1. Abra **exibição configurações avançadas do sistema** da tela do Windows hello.
   2. Clique em **Variáveis de Ambiente**.  
   3. Adicionar um novo **JAVA_HOME** variável de ambiente aponta muito**Files\Java\jdk1.7.0_55 C:\Program** ou onde quer que o seu JDK está instalado.
      
      ![Definir valores de configuração correto para o JDK][image-hdi-hivejson-jdk]
2. Instale o [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Adicionar tooyour caminho da pasta de compartimento Olá indo tooControl painel--> Editar Olá variáveis de sistema para as variáveis de ambiente de conta. Olá seguinte captura de tela mostra como toodo isso.
   
    ![Configurando o Maven][image-hdi-hivejson-maven]
3. Projeto de saudação do clone de [SerDe de JSON de Hive](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) site do github. Você pode fazer isso clicando no botão de "Baixar Zip" hello conforme Olá captura de tela a seguir.
   
    ![Projeto de clonagem Olá][image-hdi-hivejson-serde]

4: go toohello pasta onde você baixou este pacote e, em seguida, tipo do pacote"mvn". Isso deve criar hello arquivos jar necessários que você pode copiar sobre toohello cluster.

5: pasta de destino toohello go na pasta raiz de saudação onde você baixou o pacote de saudação. Carregar Olá arquivo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar toohead nós do cluster. Geralmente colocou na pasta de binários de hive Olá: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin ou algo semelhante.

6: no prompt de hive hello, digite "Adicionar jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar". Como no meu caso, jar hello está na pasta de C:\apps\dist\hive-0.13.x\bin hello, posso adicionar diretamente Olá jar com nome hello conforme mostrado:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Adicionar JAR tooyour projeto][image-hdi-hivejson-addjar]

Agora, você está pronto toouse Olá SerDe toorun consultas documento JSON hello.

Olá instrução a seguir cria uma tabela com um esquema definido:

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

toolist Olá nome e sobrenome do aluno Olá

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Este é o resultado de saudação do console de Hive hello.

![Consulta SerDe 1][image-hdi-hivejson-serde_query1]

soma de saudação toocalculate de pontuações de documento JSON Olá

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Olá anterior a consulta usa [exibição lateral Detalhar](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand UDF Olá matriz de resultados para que eles podem ser somados.

Aqui está a saída de saudação do console de Hive hello.

![Consulta SerDe 2][image-hdi-hivejson-serde_query2]

toofind que um determinado aluno os assuntos tem mais de 80 pontos de pontuação:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Olá, consulta anterior retorna uma matriz de Hive diferentemente get\_json\_objeto, que retorna uma cadeia de caracteres.

![Consulta SerDe 3][image-hdi-hivejson-serde_query3]

Se você quiser tooskil JSON malformado, em seguida, como explicado no hello [página wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) dessa SerDe, você pode obter que digitando Olá código a seguir:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Resumo
Olá Concluindo, tipo de operador JSON no Hive que você escolher depende de seu cenário. Se você tiver um documento JSON simple e tiver apenas um toolook de campo para cima – você pode escolher toouse Olá Hive UDF get\_json\_objeto. Se você tiver mais de um toolook chave, em seguida, você pode usar json_tuple. Se você tiver um documento aninhado, você deve usar Olá SerDe de JSON.

## <a name="next-steps"></a>Próximas etapas

Para outros artigos relacionados, consulte

* [Use o Hive e HiveQL com Hadoop no HDInsight tooanalyze um exemplo de um arquivo de log4j Apache](hdinsight-use-hive.md)
* [Analisar dados de atrasos de voos usando o Hive no HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analisar dados do Twitter usando o Hive no HDInsight](hdinsight-analyze-twitter-data.md)
* [Executar um trabalho do Hadoop usando o Azure Cosmos DB e o HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
