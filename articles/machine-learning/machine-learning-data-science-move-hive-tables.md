---
title: aaaCreate tabelas de Hive e carregar dados do armazenamento de BLOBs do Azure | Microsoft Docs
description: Criar tabelas de Hive e carregar dados nas tabelas de toohive de blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Criar tabelas do Hive e carregar dados do Armazenamento de Blobs do Azure
Neste tópico, são apresentadas consultas genéricas do Hive que criam tabelas do Hive e carregam dados do armazenamento de blobs do Azure. Orientação também é fornecida sobre particionamento de tabelas de Hive e uso Olá linha de otimização Colunar (ORC) formatação tooimprove desempenho da consulta.

Isso **menu** links tootopics que descrevem como dados tooingest em ambientes de destino onde os dados saudação podem ser armazenados e processados durante Olá processo de ciência de dados da equipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você:

* Criou uma conta de armazenamento do Azure. Se precisar de instruções, consulte [Sobre Contas de Armazenamento do Azure](../storage/common/storage-create-storage-account.md).
* Provisionar um cluster de Hadoop personalizado com hello serviço HDInsight.  Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).
* Cluster de toohello de acesso remoto habilitado, conectado e abrir o console de linha de comando do Hadoop hello. Se você precisar de instruções, consulte [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Carregue o armazenamento de blob de tooAzure de dados
Se você tiver criado uma máquina virtual do Azure seguindo Olá instruções fornecidas na [configurar uma máquina virtual do Azure para análise avançada](machine-learning-data-science-setup-virtual-machine.md), esse arquivo de script deve ter sido baixado toohello *c:\\ Os usuários\\\<nome de usuário\>\\documentos\\Scripts de ciência de dados* diretório na máquina virtual de saudação. Essas consultas de Hive exigem apenas que você conecte seu próprio esquema de dados e a configuração de armazenamento de BLOBs do Azure no hello campos apropriados toobe pronto para envio.

Vamos supor que dados Olá para tabelas de Hive estão em um **descompactados** formato tabular e que dados saudação foi carregado toohello padrão (ou tooan adicional) contêiner Olá da conta de armazenamento usada pelo cluster de Hadoop de saudação.

Se você quiser toopractice em Olá **NYC táxi Trip dados**, você precisa:

* **baixar** Olá 24 [NYC táxi Trip dados](http://www.andresmh.com/nyctaxitrips) arquivos (arquivos de viagem 12 e arquivos de passagens 12),
* **descompactar** todos os arquivos em arquivos .csv, e
* **carregar** -los toohello padrão (ou contêiner apropriado) do hello conta de armazenamento do Azure que foi criada pelo procedimento Olá descrito Olá [clusters de Hadoop de HDInsight do Azure personalizar para o processo de análise avançada e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) tópico. Olá processo tooupload hello. csv arquivos toohello contêiner padrão na conta de armazenamento Olá pode ser encontrada neste [página](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Como consultas de Hive toosubmit
Consultas de Hive podem ser enviadas usando:

1. [Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop](#headnode)
2. [Enviar consultas Hive com hello Editor Hive](#hive-editor)
3. [Enviar consultas de Hive com comandos do PowerShell do Azure](#ps)

Consultas de Hive são semelhantes ao SQL. Se você estiver familiarizado com o SQL, você pode encontrar hello [Hive para SQL usuários Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.

Ao enviar uma consulta de Hive, você também pode controlar o destino Olá da saída de saudação de consultas de Hive, seja em Olá tela ou tooa arquivo local no nó principal hello ou tooan BLOBs do Azure.

### <a name="headnode"></a> 1. Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop
Se o Hive Olá consulta é complexa, enviando diretamente no nó principal de saudação do cluster de Hadoop de saudação normalmente leva toofaster de retorno que enviá-lo com um Editor Hive ou scripts do PowerShell do Azure.

Login toohello o nó principal do cluster de Hadoop hello, abra Olá linha de comando do Hadoop na área de trabalho de saudação do nó principal hello e digite o comando `cd %hive_home%\bin`.

Você tem três consultas de Hive toosubmit maneiras em Olá linha de comando do Hadoop:

* diretamente
* usando arquivos .hql
* com hello Hive console de comando

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Enviar consultas de Hive diretamente na Linha de Comando do Hadoop.
Você pode executar o comando como `hive -e "<your hive query>;` toosubmit consultas de Hive simples diretamente no Hadoop linha de comando. Aqui está um exemplo onde estruturas de caixa Olá vermelho Olá comando que envia a consulta de Hive hello e Olá caixa verde contornos Olá saída da consulta de Hive hello.

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Enviar consultas de Hive em arquivos de .hql
Quando a consulta de Hive Olá é mais complicada e tem várias linhas, a edição de consultas no console de comando de Hive ou de linha de comando não é prático. Uma alternativa é toouse um editor de texto no nó principal de saudação do hello Hadoop cluster toosave Olá consultas de Hive em um arquivo .hql em um diretório local do nó principal hello. E consulta de Hive Olá no arquivo de .hql Olá pode ser submetida usando Olá `-f` argumento da seguinte maneira:

    hive -f "<path toohello .hql file>"

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Suprimir a impressão da tela de status de progresso de consultas de Hive**

Por padrão, após a consulta de Hive é enviada na linha de comando do Hadoop, progresso de saudação do trabalho de mapear/reduzir Olá é impresso na tela. toosuppress Olá impressão de tela de andamento do trabalho de mapear/reduzir hello, você pode usar um argumento `-S` ("S" em letras maiusculas) em Olá linha de comando da seguinte maneira:

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Enviar consultas de Hive no console de comando de Hive.
Você pode inserir primeiro console de comando de Hive Olá executando o comando `hive` na linha de comando do Hadoop e, em seguida, enviar consultas de Hive no console de comando do Hive. Aqui está um exemplo. Neste exemplo, Olá duas caixas vermelhas realce Olá comandos usados tooenter Olá console de comando de Hive e Olá consulta de Hive enviada no console de comando de Hive, respectivamente. caixa Olá verde realça saída Olá da consulta de Hive hello.

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

exemplos anteriores Olá diretamente resultados de consulta de Hive Olá na tela de saída. Você também pode escrever um arquivo local de saudação saída tooa no nó principal do hello, ou tooan BLOBs do Azure. Em seguida, você pode usar outras ferramentas toofurther analisar a saída de saudação de consultas de Hive.

**Saída Hive consulta resultados tooa arquivo local.**
toooutput Hive consulta resultados tooa diretório local no nó principal do hello, tiver consulta de Hive Olá toosubmit em Olá Hadoop linha de comando da seguinte maneira:

    hive -e "<hive query>" > <local path in hello head node>

Em Olá exemplo a seguir, saída de saudação da consulta de Hive é gravada em um arquivo `hivequeryoutput.txt` no diretório `C:\apps\temp`.

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Saída tooan de resultados de consulta de Hive BLOBs do Azure**

Você também pode gerar Olá Hive consulta resultados tooan BLOBs do Azure, no contêiner do cluster de Hadoop de saudação padrão de saudação. consulta de Hive Olá para isso é o seguinte:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

Em Olá exemplo a seguir, saída de saudação da consulta de Hive é gravada diretório de blob tooa `queryoutputdir` no contêiner do cluster de Hadoop de saudação padrão de saudação. Aqui, você só precisa de nome do diretório tooprovide hello, sem nome de blob hello. Um erro será gerado se você fornecer os nomes do blob e do diretório, como `wasb:///queryoutputdir/queryoutput.txt`.

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Se você abrir o contêiner padrão de saudação do cluster de Hadoop hello usando o Azure Storage Explorer, você pode ver a saída Olá da consulta de Hive Olá conforme mostrado na figura a seguir de saudação. Você pode aplicar Olá filtro (realçado por caixa vermelha) tooonly recuperar Olá blob com as letras nos nomes especificadas.

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Enviar consultas Hive com hello Editor Hive
Você também pode usar o hello Console de consulta (Editor Hive) digitando uma URL do formulário de saudação *https://&#60; Nome do cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* em um navegador da web. Você deve ser registrado no hello, consulte este console e portanto você precisa de suas credenciais de cluster Hadoop aqui.

### <a name="ps"></a> 3. Enviar consultas de Hive com comandos do PowerShell do Azure
Você também pode usar consultas de Hive toosubmit PowerShell. Para obter instruções, confira [Enviar trabalhos do Hive usando o PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Criar banco de dados e tabelas Hive
Olá consultas de Hive são compartilhadas em Olá [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e pode ser baixado a partir daí.

Aqui está uma consulta de Hive Olá que cria uma tabela de Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Aqui estão descrições de saudação dos campos de saudação que você precisa tooplug no e outras configurações:

* **&#60; o nome do banco de dados >**: nome de saudação do banco de dados de saudação que você deseja toocreate. Se você quiser apenas o banco de dados padrão do toouse hello, Olá consulta *criar banco de dados...*  pode ser omitido.
* **&#60; o nome da tabela >**: nome de saudação da tabela de saudação que você deseja toocreate no banco de dados especificado hello. Se você quiser que o banco de dados do toouse saudação padrão, tabela Olá pode ser chamada diretamente por *&#60; o nome da tabela >* sem &#60; o nome do banco de dados >.
* **&#60; separador >**: separador Olá que delimita campos Olá toobe de arquivo de dados carregado toohello tabela de Hive.
* **&#60; separador de linha >**: separador Olá que delimita linhas no arquivo de dados de saudação.
* **&#60; local de armazenamento >**: Olá dados do armazenamento do Azure local toosave saudação de tabelas de Hive. Se você não especificar *local &#60; local de armazenamento >*, Olá banco de dados e hello tabelas são armazenadas em *hive/warehouse/* diretório no contêiner de padrão de saudação do cluster de Hive Olá por padrão. Se você quiser toospecify Olá armazenamento local, o local de armazenamento Olá tem toobe no contêiner do saudação padrão para o banco de dados de saudação e tabelas. Essa localização tem toobe conhecido como contêiner do local relativo toohello padrão de cluster Olá no formato de saudação do *' wasb: / / / &#60; diretório 1 > /'* ou *' wasb: / / / &#60; diretório 1 > / &#60; diretório 2 > /'*, etc. Após Olá consulta é executada, diretórios relativo Olá são criados no contêiner de padrão de saudação.
* **TBLPROPERTIES("Skip.Header.line.Count"="1")**: se o arquivo de dados de saudação tem uma linha de cabeçalho, têm tooadd essa propriedade **final Olá** de saudação *criar tabela* consulta. Caso contrário, a linha de cabeçalho de saudação é carregada como uma tabela de registro toohello. Se o arquivo de dados de saudação não tem uma linha de cabeçalho, essa configuração pode ser omitida na consulta de saudação.

## <a name="load-data"></a>Carregar dados tooHive tabelas
Aqui está uma consulta de Hive Olá que carrega dados em uma tabela de Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; dados de caminho de tooblob >**: Olá se Olá blob arquivo toobe carregado toohello Hive tabela estiver no contêiner de padrão de saudação do hello cluster HDInsight Hadoop, *&#60; dados de caminho de tooblob >* deve estar no formato de saudação *' wasb: / / / &#60; diretório neste contêiner > / &#60; o nome de arquivo do blob >'*. arquivo de blob Olá também pode estar em um recipiente adicional de saudação cluster HDInsight Hadoop. Nesse caso, *&#60; dados de caminho de tooblob >* deve estar no formato de saudação *' wasb: / / &#60; nome do contêiner > @&#60; o nome da conta de armazenamento >.blob.core.windows.net/ &#60; o nome de arquivo do blob >'*.

  > [!NOTE]
  > Olá blob dados toobe carregado tooHive tabela tem toobe no padrão de saudação ou no contêiner adicional Olá da conta de armazenamento de cluster de Hadoop hello. Caso contrário, Olá *carregar dados* indicando que ele não pode acessar dados saudação ocorre falha na consulta.
  >
  >

## <a name="partition-orc"></a>Tópicos avançados: tabela e repositório de dados Hive particionados no formato ORC
Se dados saudação forem grandes, o particionamento de tabela Olá é útil para consultas que precisam apenas tooscan algumas partições da tabela de saudação. Por exemplo, é razoável toopartition dados de log de saudação de um site da web por datas.

Em adição toopartitioning Hive tabelas, também é benéfico toostore os dados de Hive Olá no formato de linha de otimização Colunar (ORC) hello. Para obter mais informações sobre a formatação ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Usando arquivos ORC melhora o desempenho quando o Hive lê, grava e processa dados</a>.

### <a name="partitioned-table"></a>Tabela particionada
Aqui está uma consulta de Hive Olá que cria uma tabela particionada e carrega dados nele.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Ao consultar tabelas particionadas, é recomendável tooadd condição de partição Olá no hello **início** de saudação `where` cláusula como isso melhora a eficácia de saudação da pesquisa significativamente.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Armazenar dados Hive no formato ORC
Diretamente, você não pode carregar dados do armazenamento de blob em tabelas de Hive que são armazenados em formato ORC hello. Aqui estão as etapas de saudação tooHive tabelas armazenadas no formato ORC os blobs que Olá precisar de tootake tooload dados do Azure.

Crie uma tabela externa **arquivo de texto ARMAZENADO como** e carregar dados da tabela de toohello de armazenamento de blob.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Criar uma tabela interna com hello mesmo esquema da tabela externa de saudação na etapa 1, com hello mesmo delimitador de campo e armazenar Olá Hive dados no formato ORC hello.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Selecionar dados de tabela externa de saudação na etapa 1 e inserir a tabela ORC Olá

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Se tabela de arquivo de texto de saudação *&#60; o nome do banco de dados >. &#60; o nome da tabela externa do arquivo de texto >* tem partições, na etapa 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando selecionará Olá variável de partição como um campo em Olá retornou um conjunto de dados. Inseri-lo no hello *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* falhar desde *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* não tem uma variável de partição hello como um campo no esquema da tabela de saudação. Nesse caso, você precisa toospecifically Olá selecione campos toobe inserido muito*&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* da seguinte maneira:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

É seguro toodrop Olá *&#60; o nome da tabela externa do arquivo de texto >* quando usar Olá após todos os dados a seguir consulta tenha sido inserido no *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Depois de seguir este procedimento, você deve ter uma tabela com dados em toouse pronto do hello ORC formato.  
