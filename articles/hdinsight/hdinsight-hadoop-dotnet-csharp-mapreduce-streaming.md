---
title: aaaUse c# com MapReduce no Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse c# toocreate MapReduce soluções com Hadoop no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Use C# com streaming de MapReduce no Hadoop no HDInsight

Saiba como toouse c# toocreate uma solução de MapReduce no HDInsight.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).

Transmissão do Hadoop é um utilitário que permite que os trabalhos de MapReduce toorun usando um script ou executável. Neste exemplo, o .NET é usado tooimplement Olá mapeador e Redutor para uma solução de contagem de palavras.

## <a name="net-on-hdinsight"></a>.NET no HDInsight

__HDInsight baseados em Linux__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET. O Mono versão 4.2.1 está incluído no HDInsight versão 3.5. Para obter mais informações sobre a versão de saudação do Mono incluído no HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md). toouse uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.

Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Como funciona o Hadoop Streaming

Olá basic processo usado para streaming neste documento é o seguinte:

1. Hadoop passa STDIN mapeador de dados de toohello (mapper.exe neste exemplo).
2. Mapeador de saudação processa dados hello e emite tooSTDOUT de pares chave/valor delimitado por tabulação.
3. saída de Hello é lido pelo Hadoop e encaminhada toohello Redutor (reducer.exe neste exemplo) STDIN.
4. Redutor Olá lê pares de chave/valor Olá delimitado por tabulação, processa dados hello e, em seguida, emite resultados hello como pares de chave/valor delimitado por tabulação em STDOUT.
5. saída de Hello lidos por Hadoop e gravada toohello diretório de saída.

Para obter mais informações sobre streaming, consulte [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Pré-requisitos

* Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5. Olá as etapas neste documento utilizarem 2017 do Visual Studio.

* Uma maneira tooupload .exe arquivos toohello cluster. Olá etapas deste documento usam Olá Data Lake Tools para Visual Studio tooupload Olá arquivos tooprimary armazenamento Olá cluster.

* Azure PowerShell ou um cliente SSH.

* Um Hadoop no cluster do HDInsight. Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Criar mapeador Olá

No Visual Studio, crie um novo __aplicativo de console__ chamado __mapeador__. Use Olá código para o aplicativo hello a seguir:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Depois de criar o aplicativo hello, compile-Olá tooproduce `/bin/Debug/mapper.exe` arquivo no diretório de projeto hello.

## <a name="create-hello-reducer"></a>Criar Redutor Olá

No Visual Studio, crie um novo __Aplicativo de console__ chamado __redutor__. Use Olá código para o aplicativo hello a seguir:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Depois de criar o aplicativo hello, compile-Olá tooproduce `/bin/Debug/reducer.exe` arquivo no diretório de projeto hello.

## <a name="upload-toostorage"></a>Carregar toostorage

1. No Visual Studio, abra **Gerenciador de Servidores**.

2. Expanda **Azure** e expanda **HDInsight**.

3. Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.

4. Expanda o cluster de HDInsight de saudação que você deseja toodeploy este aplicativo. Uma entrada com o texto de saudação __(conta de armazenamento padrão)__ está listado.

    ![Mostrando conta de armazenamento Olá para cluster de saudação do Gerenciador de servidores](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Se essa entrada pode ser expandida, você está usando um __conta de armazenamento do Azure__ como armazenamento padrão para o cluster de saudação. arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, expanda a entrada hello e clique duas vezes Olá __(contêiner padrão)__.

    * Se essa entrada não pode ser expandida, você está usando __repositório Azure Data Lake__ como armazenamento de padrão de saudação para cluster hello. arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, clique duas vezes em Olá __(conta de armazenamento padrão)__ entrada.

5. arquivos de .exe do tooupload Olá, use um dos métodos a seguir de saudação:

    * Se usar um __conta de armazenamento do Azure__, clique ícone de carregamento Olá e, em seguida, procure toohello **bin\debug** pasta Olá **mapeador** projeto. Por fim, selecione Olá **mapper.exe** de arquivo e clique em **Okey**.

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Se usar __repositório Azure Data Lake__, uma área vazia na listagem de arquivo hello e, em seguida, selecione __carregar__. Por fim, selecione Olá **mapper.exe** de arquivo e clique em **abrir**.

    Uma vez Olá __mapper.exe__ carregamento for concluída, o processo de carregamento de repetição Olá para Olá __reducer.exe__ arquivo.

## <a name="run-a-job-using-an-ssh-session"></a>Executar um trabalho: usando uma sessão SSH

1. Use SSH tooconnect toohello HDInsight cluster. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Use uma saudação trabalho MapReduce do comando toostart Olá a seguir:

    * Se estiver usando o __Data Lake Store__ como armazenamento padrão:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Se estiver usando o __Armazenamento do Azure__ como armazenamento padrão:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Olá lista a seguir descreve o que faz cada parâmetro:

    * `hadoop-streaming.jar`: arquivo jar Olá que contém Olá MapReduce funcionalidade de streaming.
    * `-files`: Adiciona Olá `mapper.exe` e `reducer.exe` trabalho toothis de arquivos. Olá `adl:///` ou `wasb:///` antes de cada arquivo é toohello raiz do caminho do hello de armazenamento padrão para o cluster de saudação.
    * `-mapper`: Especifica qual arquivo implementa mapeador de saudação.
    * `-reducer`: Especifica qual arquivo implementa Redutor hello.
    * `-input`: dados de entrada hello.
    * `-output`: diretório de saída de hello.

3. Após a conclusão do trabalho de MapReduce hello, use Olá resultados de saudação tooview a seguir:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Olá, texto a seguir é um exemplo de dados de saudação retornados por este comando:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Executar um trabalho: usando o PowerShell

Usar Olá toorun de script do PowerShell um trabalho MapReduce a seguir e baixar os resultados de saudação.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Esse script solicita nome de conta de logon de cluster hello e a senha, juntamente com o nome do cluster HDInsight hello. Após a conclusão do trabalho hello, saída de hello é baixado toohello `output.txt` arquivo no script de saudação do diretório Olá é executado de. Olá, texto a seguir é um exemplo de dados Olá Olá `output.txt` arquivo:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o MapReduce com HDInsight, veja [Usar MapReduce com HDInsight](hdinsight-use-mapreduce.md).

Para obter informações sobre como usar C# com Hive e Pig, consulte [Usar uma função C# definida pelo usuário com Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Para obter informações sobre como usar C# com Storm no HDInsight, consulte [Desenvolver topologias C# para Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).