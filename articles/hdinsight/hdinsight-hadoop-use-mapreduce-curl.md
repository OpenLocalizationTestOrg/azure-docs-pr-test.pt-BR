---
title: aaaUse MapReduce e Curl com Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como tooremotely executar trabalhos de MapReduce com Hadoop no HDInsight usando a rotação."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Executar trabalhos MapReduce com Hadoop no HDInsight usando REST

Saiba como toouse Olá WebHCat REST API toorun MapReduce trabalhos em um Hadoop no cluster HDInsight. Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando bruto toorun de solicitações HTTP trabalhos MapReduce.

> [!NOTE]
> Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas são tooHDInsight novo, consulte Olá [o que você precisa tooknow sobre baseados em Linux Hadoop no HDInsight](hdinsight-hadoop-linux-information.md) documento.


## <a id="prereq"></a>Pré-requisitos

* Um Hadoop no cluster HDInsight
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Executar trabalhos MapReduce usando o Curl

> [!NOTE]
> Quando você usa Ondulação ou quaisquer outras comunicações do REST com WebHCat, você deve autenticar solicitações de hello, fornecendo a senha e nome de usuário do administrador de cluster de HDInsight hello. Você deve usar o nome do cluster hello como parte do URI é usado toosend Olá solicitações toohello servidor de saudação.
>
> Para comandos Olá nesta seção, substitua **USERNAME** com cluster de toohello tooauthenticate do usuário Olá, e **senha** com senha Olá Olá conta de usuário. Substituir **CLUSTERNAME** com nome de saudação do cluster.
>
> Olá API REST é protegida usando [autenticação de acesso básico](http://en.wikipedia.org/wiki/Basic_access_authentication). Você sempre deve fazer solicitações usando HTTPS tooensure que suas credenciais são enviadas com segurança toohello server.


1. De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Você deve receber um toohello semelhante de resposta JSON a seguir:

        {"status":"ok","version":"v1"}

    Estes são os parâmetros de saudação usados neste comando:

   * **-u**: indica Olá nome de usuário e a senha usada tooauthenticate solicitação de saudação
   * **-G**: indica que essa operação é uma solicitação GET

     Olá a partir de saudação URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações.

2. toosubmit um trabalho de MapReduce, use Olá comando a seguir:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    fim de saudação do hello URI (mapreduce/jar) informa WebHCat que essa solicitação inicia um trabalho de MapReduce de uma classe em um arquivo jar. Estes são os parâmetros de saudação usados neste comando:

   * **-d**: `-G` não é usado, então a solicitação Olá padrão é o método POST de toohello. `-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.
    * **User.Name**: usuário de saudação que está executando o comando Olá
    * **JAR**: local de saudação do arquivo jar Olá que contém a classe toobe foi executado
    * **classe**: Olá classe que contém a lógica de MapReduce Olá
    * **arg**: Olá toobe de argumentos passado toohello trabalho de MapReduce. Nesse caso, o diretório de arquivo e hello de texto que são usados para saída de hello de entrada hello

     Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação:

       {"id":"job_1415651640909_0026"}

3. status de Olá toocheck de trabalho Olá Olá use comandos a seguir:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Substituir saudação **JOBID** com hello valor retornado na etapa anterior hello. Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, Olá JOBID seria `job_1415651640909_0026`.

    Se o trabalho de saudação for concluído, o estado de saudação retornado é `SUCCEEDED`.

   > [!NOTE]
   > Essa solicitação de ondulação retorna um documento JSON com informações sobre o trabalho de saudação. Jq é usada tooretrieve Olá apenas o valor de estado.

4. Quando o estado de saudação do trabalho Olá foi alterado muito`SUCCEEDED`, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure. Olá `statusdir` parâmetro que é passado com hello consulta contém o local de Olá Olá do arquivo de saída. Neste exemplo, o local de saudação é `/example/curl`. Esse endereço armazena a saída de saudação do trabalho Olá no armazenamento padrão da saudação clusters em `/example/curl`.

Você pode listar e baixar esses arquivos usando Olá [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Para obter mais informações sobre como trabalhar com blobs de saudação CLI do Azure, consulte Olá [usando Olá 2.0 do CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.

## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:

* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter mais informações sobre a interface REST Olá que é usada neste artigo, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
