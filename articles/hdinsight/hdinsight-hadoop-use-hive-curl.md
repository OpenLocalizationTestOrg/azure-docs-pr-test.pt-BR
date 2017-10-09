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
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Executar consultas Hive com Hadoop no HDInsight usando REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Saiba como toouse Olá WebHCat REST API toorun Hive consultas com Hadoop no cluster HDInsight do Azure.

[Curl](http://curl.haxx.se/) é usado toodemonstrate como você pode interagir com o HDInsight usando solicitações HTTP brutas. Olá [jq](http://stedolan.github.io/jq/) utilitário é tooprocess usados dados JSON de saudação retornados de solicitações REST.

> [!NOTE]
> Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte Olá [o que você precisa tooknow sobre Hadoop no HDInsight baseados em Linux](hdinsight-hadoop-linux-information.md) documento.

## <a id="curl"></a>Executar consultas Hive

> [!NOTE]
> Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello.
>
> Para comandos Olá nesta seção, substitua **USERNAME** com cluster do hello usuário tooauthenticate toohello e substituir **senha** com senha Olá Olá conta de usuário. Substituir **CLUSTERNAME** com nome de saudação do cluster.
>
> Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp Verifique suas credenciais com segurança são sempre enviadas servidor toohello, fazer solicitações usando o HTTP seguro (HTTPS).

1. De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Você receberá um toohello semelhante resposta texto a seguir:

        {"status":"ok","version":"v1"}

    Estes são os parâmetros de saudação usados neste comando:

   * **-u** -Olá nome de usuário e senha usados tooauthenticate solicitação de saudação.
   * **-G** – Indica que essa solicitação é uma operação GET.

     Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações. caminho de saudação **/status**, indica que a solicitação Olá tooreturn um status de WebHCat (também conhecido como Templeton) para o servidor de saudação. Você também pode solicitar a versão de saudação do Hive usando Olá comando a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Essa solicitação retorna um toohello semelhante resposta texto a seguir:

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. Saudação de uso a seguir toocreate uma tabela denominada **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Olá parâmetros usados com esta solicitação a seguir:

   * **-d** - desde `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM. `-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.

     * **User.Name** -usuário Olá que está executando o comando hello.
     * **executar** -Olá tooexecute de declarações do HiveQL.
     * **statusdir** -diretório Olá Olá status para esse trabalho é gravado.

     Essas instruções executam Olá ações a seguir:
   * **DROP TABLE** -se Olá tabela já existir, ele será excluído.
   * **CREATE EXTERNAL TABLE** - cria uma nova tabela “externa" em Hive. Tabelas externas armazenam a definição da tabela somente Olá no Hive. dados de saudação são deixados no local original hello.

     > [!NOTE]
     > Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa. Por exemplo, um processo de upload de dados automatizados ou outra operação MapReduce.
     >
     > Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.

   * **FORMATO de linha** - como Olá os dados são formatados. campos de saudação em cada log são separados por um espaço.
   * **LOCAL de arquivo de texto como ARMAZENADO** - onde são armazenados dados de saudação (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.
   * **Selecione** -seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**. Essa instrução retorna um valor de **3**, visto que há três linhas que contêm esse valor.

     > [!NOTE]
     > Observe que os espaços de saudação entre declarações do HiveQL são substituídos por Olá `+` quando usado com a rotação de caracteres. Os valores entre aspas que contêm um espaço, como o delimitador de hello, não devem ser substituídos pelo `+`.

   * **INPUT__FILE__NAME como '% 25.log'** - esses arquivos de uso instrução limites Olá pesquisa tooonly termina em. log.

     > [!NOTE]
     > Olá `%25` é a forma de codificados de URL de Olá %, para a condição de saudação real é `like '%.log'`. Olá % tem toobe URL codificada, como ele será tratado como um caractere especial em URLs.

     Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação.

       {"id":"job_1415651640909_0026"}

3. status de Olá toocheck de trabalho Olá Olá use comandos a seguir:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Substituir **JOBID** com hello valor retornado na etapa anterior hello. Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.

    Se o trabalho de saudação tiver sido concluída, o estado de Olá é **êxito**.

   > [!NOTE]
   > Essa solicitação de ondulação retorna um documento de JSON JavaScript Object Notation () com informações sobre o trabalho de saudação. Jq é usada tooretrieve Olá apenas o valor de estado.

4. Depois que o estado de saudação do trabalho Olá mudou muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure. Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, **exemplo/ondulação**. Esse endereço armazena a saída de hello em Olá **exemplo/ondulação** diretório no hello clusters de armazenamento padrão.

    Você pode listar e baixar esses arquivos usando Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Para obter mais informações sobre como usar o hello CLI do Azure com o armazenamento do Azure, consulte Olá [usar Azure CLI 2.0 com o armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.

5. Olá Use seguindo as instruções toocreate uma nova tabela 'internal' nomeada **em decorrência**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Essas instruções executam Olá ações a seguir:

   * **CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir. Essa instrução cria uma tabela interna que é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.

     > [!NOTE]
     > Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.

   * **ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC). Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.
   * **INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.
   * **Selecione** -seleciona todas as linhas de saudação novo **em decorrência** tabela.

6. Use a ID do trabalho Olá retornada toocheck Olá status do trabalho de saudação. Depois que ele foi bem-sucedida, use Olá CLI do Azure conforme descrito anteriormente toodownload e exibir resultados de saudação. saída de Hello deve conter três linhas, que contêm **[Erro]**.

## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre o Hive com HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Se você estiver usando Tez com Hive, consulte Olá documentos para as informações de depuração a seguir:

* [Use Olá exibição Ambari Tez no HDInsight baseados em Linux](hdinsight-debug-ambari-tez-view.md)

Para obter mais informações sobre Olá API de REST usada neste documento, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.

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


