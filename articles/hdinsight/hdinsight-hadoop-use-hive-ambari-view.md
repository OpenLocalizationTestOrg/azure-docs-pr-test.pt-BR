---
title: "aaaUse Ambari exibições toowork com Hive no HDInsight (Hadoop) - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Hive exibição de suas consultas de Hive do toosubmit de navegador da web. Olá exibição Hive faz parte da saudação de que interface do usuário do Ambari Web fornecido com seu cluster HDInsight baseados em Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Use Olá exibição Hive com Hadoop no HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Saiba como toorun Hive consultas usando o modo de exibição de Hive do Ambari. O Ambari é um utilitário de monitoramento e de gerenciamento fornecido com clusters HDInsight baseados em Linux. Um dos recursos de saudação fornecidos por meio do Ambari é uma interface de usuário da Web que pode ser usado toorun consultas de Hive.

> [!NOTE]
> O Ambari possui muitos recursos que não são abordados neste documento. Para obter mais informações, consulte [HDInsight gerenciar clusters usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Pré-requisitos

* Criar um cluster HDInsight baseado em Linux. Para saber mais sobre como criar um cluster, confira [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Abrir modo de exibição de Hive Olá

Você pode Ambari exibições de saudação portal do Azure; Selecione seu cluster HDInsight e, em seguida, selecione **Ambari exibições** de saudação **Links rápidos** seção.

![seção de links rápidos do portal de saudação](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Saudação de modos de exibição, selecione lista Olá __exibição Hive__.

![Olá Hive exibição selecionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Ao acessar o Ambari, será solicitada tooauthenticate toohello site. Digite Olá administrador (padrão `admin`) conta de nome e a senha usada ao criar hello cluster.

Você verá um toohello semelhante página imagem a seguir:

![Imagem da planilha de consulta Olá para o modo de exibição do hello Hive](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Executar uma consulta

toorun uma consulta de hive, use Olá seguindo as etapas da exibição de Hive hello.

1. De saudação __consulta__ guia, cole Olá HiveQL instruções a seguir na planilha de saudação:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Essas instruções executam Olá ações a seguir:

   * `DROP TABLE`-Exclui a tabela hello e arquivo de dados hello, no caso de Olá tabela já existir.

   * `CREATE EXTERNAL TABLE` – cria uma nova tabela "externa" no Hive.
   Tabelas externas armazenam a definição da tabela somente Olá no Hive. dados de saudação são deixados no local original hello.

   * `ROW FORMAT`-Como dados de saudação são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.

   * `STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e que ela é armazenada como texto.

   * `SELECT`-Seleciona uma contagem de todas as linhas em que coluna t4 contém valor Olá [Erro].

     > [!NOTE]
     > Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa. Por exemplo, um processo de carregamento de dados automatizados ou por outra operação MapReduce. Descartar uma tabela externa *não* excluir dados hello, definição de tabela Olá somente.

    > [!IMPORTANT]
    > Deixe Olá __banco de dados__ seleção em __padrão__. exemplos de saudação neste documento usam banco de dados de padrão de saudação incluído no HDInsight.

2. consulta de saudação toostart, use Olá **Execute** botão abaixo planilha hello. Ele transforma laranja e hello alterações de texto muito**parar**.

3. Quando tiver terminado de consulta hello, Olá **resultados** guia exibe os resultados de saudação da operação de saudação. Olá texto a seguir é o resultado de saudação de consulta de saudação:

        sev       cnt
        [ERROR]   3

    Olá **Logs** guia pode ser usado tooview informações de log de Olá criadas pelo trabalho de saudação.

   > [!TIP]
   > Olá **salvar resultados** caixa de diálogo lista suspensa na Olá superior esquerdo da saudação **resultados do processo de consulta** seção permite que você toodownload ou salvar os resultados.

4. Selecione Olá quatro primeiras linhas dessa consulta, em seguida, selecione **Execute**. Observe que não há nenhum resultado quando Olá trabalho é concluído. Usando Olá **Execute** botão quando parte de consulta de saudação é selecionado, somente é executado Olá instruções selecionadas. Nesse caso, a seleção de saudação não incluir instrução final de saudação que recupera linhas da tabela de saudação. Se você selecionar apenas a linha e usar **Execute**, você deve ver os resultados de saudação esperado.

5. tooadd uma planilha, use Olá **nova planilha** botão na parte inferior de saudação do hello **Editor de consultas**. Na nova planilha de hello, digite Olá HiveQL instruções a seguir:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Essas instruções executam Olá ações a seguir:

   * **CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir. Desde Olá **externo** palavra-chave não for usado, uma tabela interna é criada. Uma tabela interna é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive. Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.

   * **ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC). Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.

   * **INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contêm `[ERROR]`, e, em seguida, insere Olá dados em Olá **em decorrência** tabela.

     Saudação de uso **Execute** botão toorun esta consulta. Olá **resultados** guia não contém todas as informações quando Olá consulta retorna zero linhas. Olá status deve aparecer como **êxito** após a conclusão da consulta de saudação.

### <a name="visual-explain"></a>Explicação visual

toodisplay uma visualização de saudação do plano de consulta, selecione Olá **explicam Visual** guia abaixo planilha hello.

Olá **explicam Visual** exibição de consulta Olá pode ser útil na compreensão do fluxo de saudação de consultas complexas. Você pode exibir um equivalente textual deste modo de exibição usando Olá **explicar** botão Olá Editor de consultas.

### <a name="tez-ui"></a>Interface de usuário do Tez

toodisplay hello Tez UI para consulta hello, selecione Olá **Tez** guia abaixo planilha hello.

> [!IMPORTANT]
> Tez é tooresolve não usado em todas as consultas. Muitas consultas de Hive podem ser resolvidas sem usar o Tez. 

Se tiver sido Tez consulta tooresolve usado Olá Olá gráfico acíclico direcionado (DAG) é exibido. Se você quiser Olá tooview DAG para consultas que você executou no hello anterior ou depura Olá Tez processo, use Olá [Tez exibição](hdinsight-debug-ambari-tez-view.md) em vez disso.

## <a name="view-job-history"></a>Exibir histórico de trabalho

Olá __trabalhos__ guia exibe um histórico das consultas de Hive.

![Imagem do histórico do trabalho Olá](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Tabelas de banco de dados

Você pode usar o hello __tabelas__ guia toowork com as tabelas em um banco de dados de Hive.

![Imagem da guia de tabelas Olá](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Consultas salvas

Guia de consulta Olá, opcionalmente, é possível salvar consultas. Uma vez salvo, você pode reutilizar a consulta de saudação do hello __consultas salvas__ guia.

![Imagem da guia Consultas Salvas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Funções definidas pelo usuário

O Hive também pode ser estendido por meio de UDFs (funções definidas pelo usuário). Um UDF permite funcionalidade tooimplement ou lógica que não é modelada facilmente no estilo.

Olá guia UDF na parte superior de saudação do hello Hive exibição permite toodeclare e salvar um conjunto de UDFs. Esses UDFs podem ser usados com hello **Editor de consultas**.

![Imagem da guia UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Depois que você adicionou um toohello UDF exibição Hive, um **inserir udfs** botão é exibido na parte inferior de saudação do hello **Editor de consultas**. Selecionar essa entrada exibe uma lista de lista suspensa de Olá UDFs definidos no hello exibição Hive. Selecionar um UDF adiciona HiveQL instruções tooyour consulta tooenable Olá UDF.

Por exemplo, se você tiver definido um UDF com hello propriedades a seguir:

* Nome de recurso: myudfs

* Caminho do recurso: /myudfs.jar

* Nome da UDF: myawesomeudf

* Nome de classe da  UDF: com.myudfs.Awesome

Usando Olá **inserir udfs** botão exibe uma entrada de chamada **myudfs**, com outra lista suspensa para cada UDF é definido para esse recurso. Nesse caso, **myawesomeudf**. Selecionar essa entrada adiciona Olá toohello início da consulta Olá a seguir:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

Em seguida, você pode usar o hello UDF em sua consulta. Por exemplo: `SELECT myawesomeudf(name) FROM people;`.

Para obter mais informações sobre como usar UDFs com Hive no HDInsight, consulte Olá documentos a seguir:

* [Usando o Python com o Hive e com o Pig no HDInsight](hdinsight-python.md)
* [Como tooadd uma tooHDInsight UDF Hive personalizada](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Configurações do Hive

As configurações podem ser usada toochange várias configurações de Hive. Por exemplo, alterando o mecanismo de execução Olá para o Hive de tooMapReduce Tez (padrão de saudação).

## <a id="nextsteps"></a>Próximas etapas

Para informações gerais sobre o Hive no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
