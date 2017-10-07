---
title: "aaaCopy dados tooand de WASB em repositório Data Lake usando Distcp | Microsoft Docs"
description: "Use Distcp ferramenta toocopy dados tooand do repositório Azure armazenamento de Blobs tooData Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Usar dados de toocopy Distcp entre Blobs de armazenamento do Azure e o repositório Data Lake
> [!div class="op_single_selector"]
> * [Como usar DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Como usar AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Depois de criar um cluster de HDInsight com a conta de acesso de repositório Data Lake tooa, você pode usar ferramentas Hadoop de ecossistema como dados de toocopy Distcp **tooand de** um armazenamento de cluster do HDInsight (WASB) em uma conta do repositório Data Lake. Este artigo fornece instruções sobre como tooachieve isso.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.

## <a name="do-you-learn-fast-with-videos"></a>Você aprende rapidamente com vídeos?
[Assista a este vídeo](https://mix.office.com/watch/1liuojvdx6sie) sobre como os dados de toocopy entre Blobs de armazenamento do Azure e o repositório Data Lake usando DistCp.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Usar Distcp de um cluster HDInsight do Linux

Um cluster HDInsight vem com o utilitário de Distcp hello, que pode ser usado toocopy dados de origens diferentes em um cluster HDInsight. Se você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello como um armazenamento adicional, hello Distcp utilitário pode ser usado fora da caixa toocopy tooand de dados de uma conta de repositório Data Lake. Nesta seção, vamos examinar como toouse Olá Distcp utilitário.

1. Na área de trabalho, use SSH tooconnect toohello cluster. Consulte [conectar tooa HDInsight baseados em Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Execute comandos de saudação do prompt SSH hello.

2. Verifique se você pode acessar Olá Blobs de armazenamento do Azure (WASB). Execute Olá comando a seguir:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Isso deve fornecer uma lista de conteúdo no blob de armazenamento hello.
3. Da mesma forma, verifique se você pode acessar Olá conta do repositório Data Lake do cluster hello. Execute Olá comando a seguir:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Isso deve fornecer uma lista de arquivos/pastas Olá conta do repositório Data Lake.
4. Use dados de toocopy Distcp de WASB tooa conta do repositório Data Lake.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Isso copiará o conteúdo de saudação do hello **exemplo/data/gutenberg/** pasta WASB muito**/myfolder** em Olá conta do repositório Data Lake.
5. Da mesma forma, use dados de toocopy Distcp de tooWASB de conta do repositório Data Lake.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Isso copiará o conteúdo de saudação do **/myfolder** Olá repositório Data Lake conta muito**exemplo/data/gutenberg/** pasta em WASB.

## <a name="performance-considerations-while-using-distcp"></a>Considerações de desempenho ao usar o DistCp

Como DistCp's menor granularidade é um único arquivo, configuração Olá o número máximo de cópias simultâneas é hello mais importante parâmetro toooptimize em relação a repositório Data Lake. Isso é controlado pela configuração mapeadores de inúmeros hello (estou ') parâmetro na linha de comando hello. Esse parâmetro especifica o número de máximo de saudação de mapeadores que será usado toocopy dados. O valor padrão é 20.

**Exemplo**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Como determinar o número de saudação de mapeadores toouse?

Aqui estão algumas diretrizes que podem ser usadas.

* **Etapa 1: Determinar o total de memória YARN** -Olá primeira etapa é cluster toodetermine Olá YARN memória disponível toohello onde você executa o trabalho de DistCp hello. Essas informações estão disponíveis no portal do Ambari Olá associada Olá cluster. Navegue tooYARN e exibir configurações de saudação guia toosee Olá YARN memória. tooget Olá YARN memória total, multiplicar Olá YARN de memória por nó com número de saudação de nós ter no cluster.

* **Etapa 2: Calcular o número de saudação de mapeadores de** -Olá valor **m** é igual toohello quociente de memória total do YARN dividida por Olá tamanho do contêiner YARN. Olá informações de tamanho do contêiner YARN está disponível no portal de Ambari Olá também. Navegue tooYARN e exibição Olá configurações na guia Olá tamanho do contêiner YARN é exibido nesta janela. Olá tooarrive equação no número de saudação do mapeadores (**m**) é

        m = (number of nodes * YARN memory for each node) / YARN container size

**Exemplo**

Vamos supor que você tenha um 4 nós D14v2s cluster hello e você está tentando tootransfer 10TB de dados de 10 pastas diferentes. Cada uma das pastas de saudação contêm diferentes quantidades de dados e tamanhos de arquivo hello dentro de cada pasta são diferentes.

* Memória total do YARN - de saudação Ambari portal determinar que Olá memória YARN é 96GB para um nó D14. Portanto, o total de memória YARN para um cluster de 4 nós é: 

        YARN memory = 4 * 96GB = 384GB

* Número de mapeadores - de saudação portal Ambari você determinar que Olá tamanho do contêiner YARN é 3072 para um nó de cluster D14. Portanto, o número de mapeadores é:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Se outros aplicativos estão usando memória, em seguida, você pode escolher usar tooonly uma parte da memória YARN do cluster para DistCp.

### <a name="copying-large-datasets"></a>Copiando grandes conjuntos de dados

Ao mover o tamanho de saudação do hello toobe de conjunto de dados é muito grande (por exemplo, > 1TB) ou se você tiver muitas pastas diferentes, considere usar vários trabalhos DistCp. Provavelmente, não há nenhum ganho de desempenho, mas ele distribuirão trabalhos Olá para que se algum trabalho falhar, você só precisará toorestart esse trabalho específico, em vez de todo o trabalho de saudação.

### <a name="limitations"></a>Limitações

* DistCp tenta mapeadores de toocreate semelhantes no desempenho de toooptimize de tamanho. Aumentar o número de saudação de mapeadores não pode aumentar desempenho sempre.

* DistCp é mapeador de um tooonly limitado por arquivo. Portanto, você não deve ter mais mapeadores do que arquivos. Como DistCp só pode atribuir mapeador de um arquivo de tooa, isso limita a quantidade de saudação de simultaneidade que pode ser usado toocopy grandes arquivos.

* Se você tiver um número pequeno de arquivos grandes, você deve dividi-los em 256MB arquivo partes toogive você mais simultaneidade potencial. 
 
* Se você estiver copiando de uma conta de armazenamento de BLOBs do Azure, o trabalho de cópia pode ser acelerado no lado de armazenamento de blob hello. Isso prejudicará o desempenho de saudação do seu trabalho de cópia. toolearn mais sobre limites de saudação do armazenamento de BLOBs do Azure, consulte os limites de armazenamento do Azure em [assinatura do Azure e limites de serviço](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Consulte também
* [Copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
