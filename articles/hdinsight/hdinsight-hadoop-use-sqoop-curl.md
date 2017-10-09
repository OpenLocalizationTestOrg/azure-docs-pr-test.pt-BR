---
title: "aaaUse Hadoop Sqoop com ondulação no HDInsight - Azure | Microsoft Docs"
description: "Saiba como tooremotely enviar Sqoop trabalhos tooHDInsight usando rotação."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Executar trabalhos do Sqoop com Hadoop no HDInsight com Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como cluster de toouse ondulação toorun Sqoop trabalhos em um Hadoop no HDInsight.

Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando toorun bruto de solicitações HTTP, o monitor e recuperar resultados de saudação de trabalhos de Sqoop. Isso funciona usando Olá WebHCat REST API (anteriormente conhecido como Templeton) fornecida pelo seu cluster HDInsight.

> [!NOTE]
> Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte [informações sobre como usar o HDInsight no Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello:

* Um Hadoop no cluster HDInsight (baseado em Linux ou Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Enviar trabalhos do Sqoop usando o Curl
> [!NOTE]
> Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello. Você também deve usar o nome do cluster hello como parte do identificador de recurso uniforme (URI) do hello usado server de toohello toosend Olá solicitações.
> 
> Para comandos Olá nesta seção, substitua **USERNAME** com cluster do hello usuário tooauthenticate toohello e substituir **senha** com senha Olá Olá conta de usuário. Substituir **CLUSTERNAME** com nome de saudação do cluster.
> 
> Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication). Você sempre deve fazer solicitações usando Secure HTTP (HTTPS) toohelp Certifique-se de que suas credenciais são enviadas com segurança toohello server.
> 
> 

1. De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Você deve receber uma resposta semelhante toohello a seguir:
   
        {"status":"ok","version":"v1"}
   
    Estes são os parâmetros de saudação usados neste comando:
   
   * **-u** -Olá nome de usuário e senha usados tooauthenticate solicitação de saudação.
   * **-G** - indica que se trata de uma solicitação GET.
     
     Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será hello mesmo para todas as solicitações. caminho de saudação **/status**, indica que a solicitação Olá tooreturn um status de WebHCat (também conhecido como Templeton) para o servidor de saudação. 
2. Use Olá toosubmit um trabalho de sqoop a seguir:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Estes são os parâmetros de saudação usados neste comando:

    * **-d** - desde `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM. `-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.

        * **User.Name** -usuário Olá que está executando o comando hello.

        * **comando** -Olá Sqoop tooexecute de comando.

        * **statusdir** -diretório Olá Olá status para esse trabalho será gravada.

    Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação.

        {"id":"job_1415651640909_0026"}

1. status de saudação toocheck de trabalho de hello, Olá use comandos a seguir. Substituir **JOBID** com hello valor retornado na etapa anterior hello. Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Se o trabalho de saudação tiver sido concluída, o estado de Olá será **êxito**.
   
   > [!NOTE]
   > Essa solicitação de ondulação retorna um documento JSON JavaScript Object Notation () com informações sobre o trabalho de saudação; jq é usada tooretrieve Olá apenas o valor de estado.
   > 
   > 
2. Depois que o estado de saudação do trabalho Olá mudou muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure. Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, **wasb: / / / exemplo/ondulação**. Esse endereço armazena saída de saudação do trabalho de saudação em Olá **exemplo/ondulação** diretório no contêiner de armazenamento padrão de saudação usada por seu cluster HDInsight.
   
    Você pode listar e baixar esses arquivos usando Olá [CLI do Azure](../cli-install-nodejs.md). Por exemplo, arquivos toolist **exemplo/ondulação**, use Olá comando a seguir:
   
        azure storage blob list <container-name> example/curl
   
    toodownload um arquivo, use a seguinte hello:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Você deve especificar nome de conta de armazenamento Olá que contém o blob hello usando Olá `-a` e `-k` parâmetros ou conjunto Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave** variáveis de ambiente. Consulte <a href="hdinsight-upload-data.md" target="_blank"para obter mais informações.
   > 
   > 

## <a name="limitations"></a>Limitações
* A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.
* Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executará várias inserções em vez de envio em lote as operações de inserção hello.

## <a name="summary"></a>Resumo
Conforme demonstrado neste documento, você pode usar um toorun de solicitação HTTP bruto, o monitor e exibir os resultados dos trabalhos de Sqoop Olá no seu cluster HDInsight.

Para obter mais informações sobre a interface REST de saudação usado neste artigo, consulte Olá <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guia Sqoop REST API</a>.

## <a name="next-steps"></a>Próximas etapas
Para obter informações gerais sobre o Hive com HDInsight:

* [Usar o Sqoop com o Hadoop no HDInsight](hdinsight-use-sqoop.md)

Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

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


