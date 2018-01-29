---
title: Executar programas MapReduce personalizados - HDInsight do Azure | Microsoft Docs
description: Quando e como executar programas MapReduce personalizados no HDInsight.
services: hdinsight
documentationcenter: 
author: ashishthaps
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/04/2017
ms.author: ashishth
ms.openlocfilehash: 8e65c946d2cfcc830a1b9fa59b3f7886857f4f7d
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="run-custom-mapreduce-programs"></a>Executar programas de MapReduce personalizados

Sistemas de dados grandes com base em Hadoop como o HDInsight permitem o processamento de dados usando uma ampla variedade de ferramentas e tecnologias. A tabela a seguir descreve as principais vantagens e considerações para cada um.

| Mecanismo de consulta | Vantagens | Considerações |
| --- | --- | --- |
| **Usando o HiveQL do Hive** | <ul><li>Uma solução excelente para processamento em lotes e análise de grandes quantidades de dados imutáveis, resumo de dados e consulta sob demanda. Ele usa uma sintaxe SQL familiar.</li><li>Ele pode ser usado para produzir tabelas de dados permanentes que podem ser facilmente dividas e indexadas.</li><li>Várias tabelas e visualizações externas podem ser criadas com os mesmos dados.</li><li>Ele dá suporte a um simples data warehouse que fornece recursos de grande expansão e tolerância a falhas para processamento e armazenamento de dados.</li></ul> | <ul><li>Ele requer que os dados de origem tenham pelo menos algumas estruturas de identificação.</li><li>Não é adequado para consultas em tempo real e atualizações de nível de linha. Ele é mais adequado para trabalhos em lotes com grandes conjuntos de dados.</li><li>Ele poderá não executar alguns tipos de tarefas de processamento complexo.</li></ul> |
| **Pig usando Pig Latin** | <ul><li>Uma solução excelente para manipulação de dados como conjuntos, mesclagem e filtragem de conjuntos de dados, para aplicação de funções a registros ou grupos de registros e para reestruturação de dados com a definição de colunas, pelo agrupamento de valores ou pela conversão de colunas em linhas.</li><li>Ele pode usar uma abordagem baseada em fluxo de trabalho como uma sequência de operações nos dados.</li></ul> | <ul><li>Os usuários do SQL podem achar o Pig Latin menos familiar e mais difícil de usar do que o HiveQL.</li><li>A saída padrão é geralmente um arquivo de texto e portanto pode ser mais difícil de usar com as ferramentas de visualização como o Excel. Normalmente, você cobrirá uma tabela Hive sobre a saída.</li></ul> |
| **Mapa personalizado/redução** | <ul><li>Ele fornece controle total sobre o mapa e reduz fases e a execução.</li><li>Ele permite que as consultas sejam otimizadas para alcançar desempenho máximo do cluster, ou para reduzir a carga nos servidores e na rede.</li><li>Os componentes podem ser gravados em uma variedade de linguagens conhecidas.</li></ul> | <ul><li>É mais difícil do que usar o Pig ou o Hive porque você deve criar seu próprio mapa e reduzir os componentes.</li><li>Os processos que exigem a união de conjuntos de dados são mais difíceis de implementar.</li><li>Embora estruturas de teste estejam disponíveis, depurar códigos é mais complexo do que um aplicativo normal porque o código é executado como um trabalho em lotes sob o controle do Agendador de trabalho do Hadoop.</li></ul> |
| **HCatalog** | <ul><li>Ele abstrai os detalhes do caminho de armazenamento, facilitando a administração e removendo a necessidade dos usuários de saber onde os dados estão armazenados.</li><li>Isso possibilita a notificação de eventos como a disponibilidade de dados, permitindo que outras ferramentas, como o Oozie, detectem quando operações tiverem ocorrido.</li><li>Ele apresenta uma exibição relacional dos dados, incluindo o particionamento por chave e facilita o acesso de dados.</li></ul> | <ul><li>Ele dá suporte por padrão a formatos de arquivo RCFile, texto CSV, texto JSON, SequenceFile e ORC, mas talvez seja necessário gravar um SerDe personalizado para outros formatos.</li><li>O HCatalog não é thread-safe.</li><li>Há algumas restrições sobre os tipos de dados para colunas ao usar o carregador do HCatalog em scripts do Pig. Para obter mais informações, consulte [Tipos de Dados do HCatLoader](http://cwiki.apache.org/confluence/display/Hive/HCatalog%20LoadStore#HCatalogLoadStore-HCatLoaderDataTypes) na documentação do Apache HCatalog.</li></ul> |

Normalmente, você usa a mais simples dessas soluções que podem fornecer os resultados que você precisa. Por exemplo, você poderá obter esses resultados usando apenas o Hive, mas para cenários mais complexos pode precisar usar o Pig, ou até mesmo gravar seu próprio mapa e reduzir os componentes. Você também pode decidir, depois de testar o Hive ou o Pig, que criar um mapa personalizado e reduzir componentes podem oferecer melhor desempenho, permitindo que você ajuste e otimize o processamento.

## <a name="custom-mapreduce-components"></a>Mapa personalizado/reduzir componentes

Código de mapeamento/reduzir consiste em duas funções separadas, implementadas como **mapa** e **reduzir** componentes. O componente **mapa** é executado em paralelo em vários nós do cluster, cada nó aplicando o mapeamento para o subconjunto do nó de dados. O componente **redução** agrupa e resume os resultados de todas as funções de mapa. Para obter mais informações, consulte [Usar o MapReduce no Hadoop no HDInsight](hdinsight-use-mapreduce.md).

Na maioria dos cenários de processamento do HDInsight é mais simples e eficiente usar uma abstração de alto nível, como o Pig ou o Hive. Você também pode criar o mapa personalizado e a redução de componentes para uso em scripts do Hive para executar um processamento mais sofisticado.

Mapa personalizado/redução de componentes geralmente são gravados em Java. O Hadoop fornece uma interface de streaming que também permite que os componentes usados sejam desenvolvidos em outras linguagens, como C#, F#, Visual Basic, Python e JavaScript.

* Para uma apresentação sobre como desenvolver programas personalizados MapReduce no Java, consulte [Desenvolver programas MapReduce em Java para Hadoop no HDInsight](apache-hadoop-develop-deploy-java-mapreduce-linux.md).
* [Desenvolver programas MapReduce de streaming do Python para o HDInsight](apache-hadoop-streaming-python.md).

Considere a criação de seu próprio mapa e a redução de componentes nas seguintes condições:

* Você precisa processar dados que são completamente não estruturados analisando os dados e usando lógica personalizada para obter informações estruturadas deles.
* Você deseja realizar tarefas complexas que são difíceis (ou impossíveis) de expressar no Pig ou no Hive sem recorrer à criação de um UDF. Por exemplo, você talvez precise criar usar um serviço externo de geocodificação para converter coordenadas de latitude e longitude ou endereços IP na fonte de dados em nomes de localização geográfica.
* Você deseja reutilizar o seu código existente do .NET, do Python ou do JavaScript em mapeamento/redução de componentes usando a interface de transmissão do Hadoop.

## <a name="upload-and-run-your-custom-mapreduce-program"></a>Carregar e executar o programa MapReduce personalizado

Os programas de MapReduce mais comuns são gravados em Java e compilados em um arquivo jar.

1. Depois que você desenvolveu, compilou e testou seu programa MapReduce, use o `scp` comando para carregar o arquivo jar ao nó principal.

    ```bash
    scp mycustomprogram.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Substitua **USERNAME** com a conta de usuário SSH para o seu cluster. Substitua **CLUSTERNAME** pelo nome do cluster. Se você tiver usado uma senha para proteger a conta SSH, você precisará digitá-la. Se você tiver usado um certificado, talvez precise usar o parâmetro `-i` para especificar o arquivo da chave privada.

2. Conecte-se ao cluster usando [SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

3. Da sessão SSH, execute o programa MapReduce por meio do YARN.

    ```bash
    yarn jar mycustomprogram.jar mynamespace.myclass /example/data/sample.log /example/data/logoutput
    ```

    Esse comando envia o trabalho de MapReduce para o YARN. O arquivo de entrada é `/example/data/sample.log`, e o diretório de saída é `/example/data/logoutput`. Os arquivos de entrada e saída são armazenados no armazenamento padrão do cluster.

## <a name="next-steps"></a>Próximas etapas

* [Usar o C# com MapReduce de streaming no Hadoop no HDInsight](apache-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Desenvolver programas do Java MapReduce para o Hadoop no HDInsight](apache-hadoop-develop-deploy-java-mapreduce-linux.md)
* [Desenvolver programas MapReduce de streaming do Hadoop para o HDInsight](apache-hadoop-streaming-python.md)
* [Usar o Kit de ferramentas do Azure para Eclipse para criar aplicativos Spark para um cluster HDInsight](../spark/apache-spark-eclipse-tool-plugin.md)
* [Usar as UDF (Funções Definidas pelo Usuário) do Python com o Hive e o Pig no HDInsight](python-udf-hdinsight.md)
