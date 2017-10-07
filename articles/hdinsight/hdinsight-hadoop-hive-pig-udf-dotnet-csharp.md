---
title: aaaUse c# com Hive e Pig no Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse c# definida pelo usuário (UDF) de funções com Hive e Pig no HDInsight do Azure de streaming."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>Usar funções definidas pelo usuário do C# com streaming de Hive e Pig no Hadoop no HDInsight

Saiba como toouse c# funções definidas pelo usuário (UDF) com o Apache Hive e Pig no HDInsight.

> [!IMPORTANT]
> etapas de saudação neste documento funcionam com clusters de HDInsight com base em Linux e em Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).

Ambos Hive e Pig pode transmitir aplicativos de tooexternal de dados para processamento. Este processo é conhecido como _streaming_. Ao usar um aplicativo .NET, Olá transferência dos dados toohello aplicativo STDIN e aplicativo hello retorna resultados de saudação em STDOUT. tooread e gravação de STDIN e STDOUT, você pode usar `Console.ReadLine()` e `Console.WriteLine()` de um aplicativo de console.

## <a name="prerequisites"></a>Pré-requisitos

* Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5.

    * Use o IDE que preferir. Recomendamos o [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 ou o [Visual Studio Code](https://code.visualstudio.com/). Olá as etapas neste documento utilizarem 2017 do Visual Studio.

* Uma maneira tooupload .exe arquivos toohello cluster e executados trabalhos de Pig e Hive. É recomendável Olá Data Lake Tools para Visual Studio, o Azure PowerShell e a CLI do Azure. Hello etapas deste documento usam Olá Data Lake Tools para arquivos do Visual Studio tooupload hello e execute a consulta de Hive do exemplo hello.

    Para obter informações sobre outros trabalhos de Pig e consultas de Hive toorun maneiras, consulte Olá documentos a seguir:

    * [Usar o Apache Hive com o HDInsight](hdinsight-use-hive.md)

    * [Usar o Apache Pig com o HDInsight](hdinsight-use-pig.md)

* Um Hadoop no cluster do HDInsight. Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET no HDInsight

* __HDInsight baseados em Linux__ clusters usando [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET. O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.

    Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.

* __HDInsight baseados em Windows__ clusters usam aplicativos de .NET Olá Microsoft .NET CLR toorun.

Para obter mais informações sobre a versão de saudação do hello .NET framework e Mono incluídos com versões de HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Criar hello C\# projetos

### <a name="hive-udf"></a>UDF do Hive

1. Abra o Visual Studio e crie uma solução. Para o tipo de projeto hello, selecione **aplicativo de Console (.NET Framework)**e o novo projeto do nome hello **HiveCSharp**.

    > [!IMPORTANT]
    > Selecione __.NET Framework 4.5__ se estiver usando um cluster HDInsight baseado em Linux. Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Substitua o conteúdo de saudação do **Program.cs** com os seguintes hello:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Compile o projeto de saudação.

### <a name="pig-udf"></a>UDF do Pig

1. Abra o Visual Studio e crie uma solução. Para o tipo de projeto hello, selecione **aplicativo de Console**e o novo projeto do nome hello **PigUDF**.

2. Substitua o conteúdo de saudação do hello **Program.cs** arquivo com hello código a seguir:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Este aplicativo analisa linhas Olá enviadas do Pig e reformatar linhas que começam com `java.lang.Exception`.

3. Salvar **Program.cs**e, em seguida, compilar o projeto de saudação.

## <a name="upload-toostorage"></a>Carregar toostorage

1. No Visual Studio, abra **Gerenciador de Servidores**.

2. Expanda **Azure** e expanda **HDInsight**.

3. Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.

4. Expanda o cluster de HDInsight de saudação que você deseja toodeploy este aplicativo. Uma entrada com o texto de saudação __(conta de armazenamento padrão)__ está listado.

    ![Mostrando conta de armazenamento Olá para cluster de saudação do Gerenciador de servidores](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Se essa entrada pode ser expandida, você está usando um __conta de armazenamento do Azure__ como armazenamento padrão para o cluster de saudação. arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, expanda a entrada hello e clique duas vezes Olá __(contêiner padrão)__.

    * Se essa entrada não pode ser expandida, você está usando __repositório Azure Data Lake__ como armazenamento de padrão de saudação para cluster hello. arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, clique duas vezes em Olá __(conta de armazenamento padrão)__ entrada.

6. arquivos de .exe do tooupload Olá, use um dos métodos a seguir de saudação:

    * Se usar um __conta de armazenamento do Azure__, clique ícone de carregamento Olá e, em seguida, procure toohello **bin\debug** pasta Olá **HiveCSharp** projeto. Por fim, selecione Olá **HiveCSharp.exe** de arquivo e clique em **Okey**.

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Se usar __repositório Azure Data Lake__, uma área vazia na listagem de arquivo hello e, em seguida, selecione __carregar__. Por fim, selecione Olá **HiveCSharp.exe** de arquivo e clique em **abrir**.

    Uma vez Olá __HiveCSharp.exe__ carregamento for concluída, o processo de carregamento de repetição Olá para Olá __PigUDF.exe__ arquivo.

## <a name="run-a-hive-query"></a>Executar um trabalho do Hive

1. No Visual Studio, abra **Gerenciador de Servidores**.

2. Expanda **Azure** e expanda **HDInsight**.

3. Cluster de Olá atalho que você implantou Olá **HiveCSharp** aplicativo e, em seguida, selecione **escrever uma consulta de Hive**.

4. Use Olá texto de consulta de Hive Olá a seguir:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Remova os comentários Olá `add file` instrução que corresponde ao tipo de saudação de armazenamento padrão usado para o cluster.

    Essa consulta seleciona Olá `clientid`, `devicemake`, e `devicemodel` os campos do `hivesampletable`e passa campos Olá toohello HiveCSharp.exe aplicativo. espera de consulta Olá Olá tooreturn três campos de aplicativo, que são armazenados como `clientid`, `phoneLabel`, e `phoneHash`. consulta de saudação também espera toofind HiveCSharp.exe na raiz de Olá Olá padrão do contêiner de armazenamento.

5. Clique em **enviar** cluster HDInsight do toosubmit Olá trabalho toohello. Olá **resumo do trabalho de Hive** janela será aberta.

6. Clique em **atualizar** toorefresh Olá resumo até **Status do trabalho** muda muito**concluído**. trabalho de saudação tooview de saída, clique em **saída de trabalho**.

## <a name="run-a-pig-job"></a>Executar um trabalho Pig

1. Use uma saudação cluster do HDInsight métodos tooconnect tooyour a seguir:

    * Se você estiver usando um cluster HDInsight __baseado em Linux__, use SSH. Por exemplo: `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Para obter mais informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Se você estiver usando um __baseados no Windows__ cluster HDInsight, [conectar toohello cluster usando a área de trabalho remota](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Use uma saudação seguinte linha de comando do comando toostart Olá Pig:

        pig

    > [!IMPORTANT]
    > Se você estiver usando um cluster baseado no Windows, use Olá comandos a seguir em vez disso:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Um prompt de `grunt>` é exibido.

3. Digite hello toorun um trabalho de Pig que usa o aplicativo do .NET Framework hello a seguir:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Olá `DEFINE` instrução cria um alias de `streamer` para aplicativos de pigudf.exe Olá, e `CACHE` carrega do armazenamento padrão para o cluster de saudação. Posteriormente, `streamer` é usado com hello `STREAM` tooprocess operador Olá único linhas contidas no LOG e dados de retorno hello como uma série de colunas.

    > [!NOTE]
    > nome do aplicativo Hello que é usado para streaming deve estar entre Olá \` (apóstrofo) de caractere quando um alias, e ' (aspa simples) quando usado com `SHIP`.

4. Depois de inserir a última linha do hello, trabalho Olá deve começar. Ele retorna a saída toohello semelhante texto a seguir:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu como toouse um aplicativo do .NET Framework do Hive e Pig no HDInsight. Se você quiser toolearn como toouse Python com Hive e Pig, consulte [uso Python com Hive e Pig no HDInsight](hdinsight-python.md).

Para outras maneiras toouse Pig e Hive e toolearn sobre o uso de MapReduce, consulte Olá documentos a seguir:

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
