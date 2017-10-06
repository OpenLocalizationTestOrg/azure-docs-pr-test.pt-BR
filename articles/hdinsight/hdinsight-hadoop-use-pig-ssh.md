---
title: aaaUse Pig do Hadoop com SSH em um cluster HDInsight - Azure | Microsoft Docs
description: "Saiba como se conectar tooa cluster de Hadoop baseado em Linux com SSH, e, em seguida, usar Olá Pig comando toorun Pig latino instruções interativamente ou como um lote de trabalho."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Executar trabalhos de Pig em um cluster baseado em Linux com hello comando Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Saiba como toointeractively executar trabalhos de Pig de um cluster de HDInsight de tooyour de conexão SSH. Olá linguagem de programação de Pig latino permite toodescribe transformações que são aplicadas toohello entrada dados tooproduce Olá desejado saída.

> [!IMPORTANT]
> Olá, as etapas neste documento exigem um cluster HDInsight baseados em Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>Conexão com o SSH

Use SSH tooconnect tooyour HDInsight cluster. exemplo a seguir Hello conecta tooa cluster denominado **myhdinsight** como Olá conta denominada **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Se você forneceu uma chave de certificado para autenticação de SSH** quando você criou o cluster do HDInsight hello, talvez seja necessário toospecify local de saudação da chave privada Olá no sistema cliente.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Se você forneceu uma senha para autenticação de SSH** quando você criou o cluster do HDInsight hello, forneça a senha de saudação quando solicitado.

Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Use o comando de Pig de saudação

1. Uma vez conectado, inicie interface de linha de comando de Pig de saudação (CLI) usando Olá comando a seguir:

        pig

    Após um momento, você deverá ver um prompt `grunt>` .

2. Digite hello instrução a seguir:

        LOGS = LOAD '/example/data/sample.log';

    Esse comando carrega o conteúdo de saudação do arquivo de sample.log Olá nos LOGS. Você pode exibir o conteúdo de saudação do arquivo hello usando Olá instrução a seguir:

        DUMP LOGS;

3. Em seguida, transformar dados saudação aplicando um nível de log de saudação somente tooextract de expressão regular de cada registro usando Olá instrução a seguir:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Você pode usar **DESPEJAR** dados de saudação tooview após a transformação de saudação. Nesse caso, use `DUMP LEVELS;`.

4. Continue a aplicar transformações usando instruções Olá em Olá a tabela a seguir:

    | Instrução de Pig Latin | O demonstrativo de saudação não diz |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Remove as linhas que contêm um valor nulo para o nível de log hello e armazena os resultados de saudação em `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Olá grupos linhas por nível de log e armazena os resultados de saudação em `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Cria um conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre. Olá conjunto de dados é armazenado em `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Ordena os níveis de log Olá por contagem (decrescente) e armazena em `RESULT`. |

    > [!TIP]
    > Use `DUMP` tooview resultados de saudação da transformação Olá depois de cada etapa.

5. Você também pode salvar os resultados de saudação de uma transformação usando Olá `STORE` instrução. Por exemplo, a saudação instrução a seguir salva Olá `RESULT` toohello `/example/data/pigout` diretório no armazenamento padrão da saudação para seu cluster:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Olá dados são armazenados no diretório especificado do hello nos arquivos denominados `part-nnnnn`. Se já existe um diretório de saudação, você receberá um erro.

6. Olá tooexit pesado prompt, digite Olá instrução a seguir:

        QUIT;

### <a name="pig-latin-batch-files"></a>Arquivos de lote do Pig Latin

Você também pode usar o hello Pig comando toorun Pig latino contido em um arquivo.

1. Depois de sair do prompt de pesado Olá, uso a seguir Olá comando toopipe STDIN em um arquivo denominado `pigbatch.pig`. Esse arquivo é criado no diretório base Olá Olá conta de usuário SSH.

        cat > ~/pigbatch.pig

2. Digite ou cole Olá linhas a seguir e, em seguida, use Ctrl + D quando terminar.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Olá toorun do comando de uso a seguir de saudação `pigbatch.pig` arquivo usando o comando de Pig de saudação.

        pig ~/pigbatch.pig

    Quando termina de trabalho em lotes de saudação, você verá Olá saída a seguir:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre Pig no HDInsight, consulte Olá documento a seguir:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter mais informações sobre outra maneiras toowork com Hadoop no HDInsight, consulte Olá documentos a seguir:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
