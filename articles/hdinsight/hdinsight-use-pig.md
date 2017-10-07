---
title: aaaUse Pig do Hadoop no HDInsight | Microsoft Docs
description: Saiba como toouse Pig com Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Usar o Pig com Hadoop no HDInsight

Saiba como toouse [Pig Apache](http://pig.apache.org/) com HDInsight...

O Pig é uma plataforma para criar programas para o Hadoop usando uma linguagem de procedimento conhecida como *Pig Latin*. Pig é uma alternativa tooJava para a criação de *MapReduce* soluções e ele está incluído no Azure HDInsight. Use Olá Olá toodiscover de tabela que Pig pode ser usado com HDInsight de várias maneiras a seguir:

| **Use** se quiser... | ...um shell **interativo** | ...Processamento em**lotes** | ... com esse **sistema operacional de cluster** | ... desse **sistema operacional cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [API REST](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [SDK .NET para Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (por enquanto) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |
| [Área de Trabalho Remota](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>Por que usar o Pig

Um dos desafios de saudação do processamento de dados usando MapReduce no Hadoop implementa a lógica de processamento usando somente um mapa e uma função de redução. Processamento complexo, você geralmente tem toobreak processamento em várias operações de MapReduce que são encadeados juntos tooachieve resultados de saudação desejado.

Pig permite que você toodefine processamento como uma série de transformações que Olá fluxos de dados por meio da saída do tooproduce Olá desejado.

linguagem de Pig latino Olá permite que você toodescribe Olá fluxo de dados de entrada não processada, por meio de um ou mais transformações, saída de saudação desejada tooproduce. Os programas em Pig Latin seguem este padrão geral:

* **Carga**: ler dados toobe manipulado saudação do sistema de arquivos

* **Transformar**: manipular dados Olá

* **Despejar ou armazenar**: tela de toohello de dados de saída ou armazená-lo para processamento

### <a name="user-defined-functions"></a>Funções definidas pelo usuário

Latino pig também oferece suporte a funções definidas pelo usuário (UDF), que permite que você tooinvoke componentes externos que implementam a lógica que é difícil toomodel em latim Pig.

Para saber mais sobre o Pig Latin, confira o [Manual de referência do Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) e o [Manual de referência do Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Para obter um exemplo do uso de UDFs com Pig, consulte Olá documentos a seguir:

* [DataFu de uso com Pig no HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu é uma coleção de útil UDFs mantida pela Apache
* [Use o Python com o Pig e o Hive no HDInsight](hdinsight-python.md)
* [Use o C# com o Hive e com o Pig no HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Dados de exemplo

HDInsight fornece vários conjuntos de dados de exemplo, que são armazenados em Olá `/example/data` e `/HdiSamples` diretórios. São esses diretórios no armazenamento padrão da saudação para seu cluster. exemplo de Pig Hello neste documento usa Olá *log4j* arquivo `/example/data/sample.log`.

Cada log no arquivo hello consiste em uma linha de campos que contém um `[LOG LEVEL]` campo tooshow Olá tipo e hello gravidade, por exemplo:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

No exemplo anterior de saudação, o nível de log de saudação é erro.

> [!NOTE]
> Você também pode gerar um arquivo log4j usando Olá [Log4j Apache](http://en.wikipedia.org/wiki/Log4j) ferramenta de registro em log e, em seguida, carregar blob tooyour arquivo. Consulte [tooHDInsight carregar dados](hdinsight-upload-data.md) para obter instruções. Para saber mais sobre como o armazenamento de blob do Azure é usado com o HDInsight, confira [Usar armazenamento de blob do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Exemplo de trabalho

próximo trabalho de Pig latino Hello carrega Olá `sample.log` arquivo de armazenamento padrão da saudação para seu cluster HDInsight. Em seguida, ele executa uma série de transformações que resultam em uma contagem de como quantas vezes cada dados de entrada de saudação ocorreu no nível de log. resultados de saudação são gravados tooSTDOUT.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Olá imagem a seguir mostra um resumo do que cada transformação faz toohello dados.

![Representação gráfica de transformações Olá][image-hdi-pig-data-transformation]

## <a id="run"></a>Executar trabalho de Pig latino Olá

O HDInsight pode executar trabalhos de Pig Latin usando vários métodos. Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.

| **Use** se quiser... | ...um shell **interativo** | ...Processamento em**lotes** | ... com esse **sistema operacional de cluster** | ... deste **cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [SDK .NET para Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (por enquanto) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |
| [Área de Trabalho Remota](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Pig e SQL Server Integration Services

Você pode usar o SQL Server Integration Services (SSIS) toorun um trabalho de Pig. Hello Azure Feature Pack para SSIS fornece Olá componentes que funcionam com os trabalhos de Pig no HDInsight a seguir.

* [Tarefa do Pig do Azure HDInsight][pigtask]

* [Gerenciador de Conexões de Assinatura do Azure][connectionmanager]

Saiba mais sobre hello Azure Feature Pack para SSIS [aqui][ssispack].

## <a id="nextsteps"></a>Próximas etapas
Agora que você aprendeu como toouse Pig com HDInsight, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.

* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Use o Sqoop com o HDInsight](hdinsight-use-sqoop.md)
* [Usar o Oozie com o HDInsight](hdinsight-use-oozie.md)
* [Usar trabalhos do MapReduce com o HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
