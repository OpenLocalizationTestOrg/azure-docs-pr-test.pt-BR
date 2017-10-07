---
title: aaaUse Pig do Hadoop com REST no HDInsight - Azure | Microsoft Docs
description: Saiba como cluster de trabalhos de Pig latino de toorun toouse restante em um Hadoop no HDInsight do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Executar trabalhos do Pig com Hadoop no HDInsight usando o REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Saiba como toorun Pig latino trabalhos, tornando o cluster do REST solicitações tooan HDInsight do Azure. Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando Olá WebHCat REST API.

> [!NOTE]
> Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte [dicas de HDInsight baseados em Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Pré-requisitos

* Um cluster do Azure HDInsight (Hadoop no HDInsight, baseado em Windows ou Linux)

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Executar trabalhos do Pig usando Curl

> [!NOTE]
> Olá API REST é protegida por meio de [autenticação de acesso básico](http://en.wikipedia.org/wiki/Basic_access_authentication). Sempre fazem solicitações usando o HTTP seguro (HTTPS) tooensure que suas credenciais são enviadas com segurança toohello server.
>
> Ao usar os comandos de saudação nesta seção, substitua `USERNAME` com cluster do hello usuário tooauthenticate toohello e substituir `PASSWORD` com senha Olá Olá conta de usuário. Substituir `CLUSTERNAME` com nome de saudação do cluster.
>


1. De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Você deve receber Olá resposta JSON a seguir:

        {"status":"ok","version":"v1"}

    Estes são os parâmetros de saudação usados neste comando:

    * **-u**: Olá nome de usuário e senha usados tooauthenticate solicitação de saudação
    * **-G**: indica que essa solicitação é uma solicitação GET

     Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações. caminho de saudação **/status**, indica que a solicitação Olá status Olá tooreturn WebHCat (também conhecido como Templeton) para o servidor de saudação.

2. Use Olá código toosubmit um cluster de toohello de trabalho de Pig latino a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    Estes são os parâmetros de saudação usados neste comando:

    * **-d**: porque `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM. `-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.

    * **User.Name**: usuário de saudação que está executando o comando Olá
    * **executar**: Olá Pig latino instruções tooexecute
    * **statusdir**: diretório Olá Olá status para esse trabalho é gravado

    > [!NOTE]
    > Observe que os espaços de saudação em instruções de Pig latino serão substituídos por Olá `+` quando usado com a rotação de caracteres.

    Este comando deve retornar uma ID de trabalho que pode ser usado toocheck Olá status do trabalho Olá, por exemplo:

        {"id":"job_1415651640909_0026"}

3. status de Olá toocheck de trabalho Olá Olá use comandos a seguir

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Substituir `JOBID` com hello valor retornado na etapa anterior hello. Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, `JOBID` é `job_1415651640909_0026`.

    Se o trabalho de saudação tiver sido concluída, o estado de Olá é **êxito**.

    > [!NOTE]
    > Essa solicitação de ondulação retorna um JavaScript Object Notation (JSON) um documento com informações sobre o trabalho de saudação e jq é tooretrieve usado Olá somente o valor de estado.

## <a id="results"></a>Exibir resultados

Quando o estado de saudação do trabalho Olá foi alterado muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação. Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, `/example/pigcurl`.

HDInsight pode usar o armazenamento do Azure ou repositório Azure Data Lake como armazenamento de dados padrão de saudação. Há tooget de várias maneiras em dados Olá dependendo de qual delas você usar. Para obter mais informações, consulte a seção de armazenamento de saudação do hello [HDInsight baseados em Linux informações](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.

## <a id="summary"></a>Resumo

Conforme demonstrado neste documento, você pode usar um toorun de solicitação HTTP bruto, o monitor e exibir resultados de saudação de trabalhos de Pig no seu cluster HDInsight.

Para obter mais informações sobre a interface REST de saudação usado neste artigo, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre o Pig no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
