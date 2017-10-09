---
title: "dados de aaaCopy de Blobs de armazenamento do Azure no repositório Data Lake | Microsoft Docs"
description: "Usar dados de toocopy ferramenta AdlCopy do repositório Azure armazenamento de Blobs tooData Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Copiar dados do repositório Azure armazenamento de Blobs tooData Lake
> [!div class="op_single_selector"]
> * [Como usar DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Como usar AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Repositório Azure Data Lake fornece uma ferramenta de linha de comando, [AdlCopy](http://aka.ms/downloadadlcopy), dados de toocopy de saudação as origens a seguir:

* Dos Blobs de Armazenamento do Azure no Data Lake Store. Você não pode usar dados de toocopy AdlCopy de blobs de armazenamento do repositório Data Lake tooAzure.
* Entre duas contas do Azure Data Lake Store.

Além disso, você pode usar a ferramenta de AdlCopy de saudação em dois modos diferentes:

* **Autônomo**, onde a ferramenta Olá usa tarefa de saudação do repositório Data Lake recursos tooperform.
* **Usando uma conta da análise Data Lake**, onde unidades Olá atribuídas tooyour análise Data Lake conta são usados tooperform operação de cópia de saudação. Talvez você queira toouse essa opção quando estiver buscando a tarefas de cópia de saudação tooperform de maneira previsível.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Blobs de Armazenamento do Azure** com alguns dados.
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Análise do Azure Data Lake conta (opcional)** -consulte [Introdução à análise Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md) para obter instruções sobre como toocreate um Data Lake armazenam conta.
* **Ferramenta AdlCopy**. Instalar a ferramenta de AdlCopy de saudação do [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Sintaxe da ferramenta de AdlCopy Olá
Use Olá seguindo a sintaxe toowork com a ferramenta de AdlCopy Olá

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

parâmetros de saudação na sintaxe de saudação são descritos abaixo:

| Opção | Descrição |
| --- | --- |
| Fonte |Especifica o local de Olá Olá dos dados de origem no blob de armazenamento do Azure hello. origem de saudação pode ser um contêiner de blob, um blob ou outra conta de repositório Data Lake. |
| Dest |Especifica o toocopy de destino de repositório Data Lake Olá para. |
| SourceKey |Especifica a chave de acesso de armazenamento Olá para fonte de saudação do blob de armazenamento do Azure. Isso é necessário apenas se a origem de saudação é um contêiner de blob ou um blob. |
| Conta |**Opcional**. Use isso se desejar que o trabalho de cópia toouse análise Azure Data Lake conta toorun hello. Se você usa a opção de conta de saudação na sintaxe hello, mas não especificar uma conta da análise Data Lake, AdlCopy usa um trabalho de saudação do toorun de conta padrão. Além disso, se você usar essa opção, adicione a origem de saudação (Blob de armazenamento do Azure) e de destino (repositório Azure Data Lake) como fontes de dados para sua conta da análise Data Lake. |
| Unidades |Especifica o número de saudação de unidades de análise Data Lake que será usado para o trabalho de cópia hello. Essa opção é obrigatória se você usar o hello **/conta** opção conta de análise Data Lake toospecify hello. |
| Padrão |Especifica um padrão de regex que indica qual toocopy blobs ou arquivos. O AdlCopy usa correspondência que diferencia maiúsculas de minúsculas. padrão de saudação usado quando nenhum padrão for especificado será toocopy todos os itens. Não é possível especificar diversos padrões para os arquivos. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Usar dados de toocopy AdlCopy (como autônomo) de um blob de armazenamento do Azure
1. Abra um prompt de comando e navegue diretório toohello onde AdlCopy é instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.
2. Execute Olá toocopy de comando a seguir um blob específico de saudação fonte contêiner tooa repositório Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Por exemplo:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] sintaxe de saudação acima Especifica Olá toobe tooa copiado arquivo na conta do repositório Data Lake hello. Ferramenta de AdlCopy cria uma pasta se Olá nome de pasta especificado não existe.

    Será tooenter solicitada credenciais Olá Olá assinatura do Azure sob a qual você tem a sua conta do repositório Data Lake. Você verá uma saída semelhante toohello a seguir:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. Você também pode copiar todos os blobs de saudação da conta de repositório Data Lake toohello de um contêiner usando Olá comando a seguir:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Por exemplo:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Considerações sobre o desempenho

Se você estiver copiando de uma conta de armazenamento de BLOBs do Azure, podem ser aceleradas durante a cópia no lado de armazenamento de blob hello. Isso prejudicará o desempenho de saudação do seu trabalho de cópia. toolearn mais sobre limites de saudação do armazenamento de BLOBs do Azure, consulte os limites de armazenamento do Azure em [assinatura do Azure e limites de serviço](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Usar dados de toocopy AdlCopy (como autônomo) com outra conta de repositório Data Lake
Você também pode usar dados de toocopy AdlCopy entre duas contas do repositório Data Lake.

1. Abra um prompt de comando e navegue diretório toohello onde AdlCopy é instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.
2. Olá toocopy de comando a seguir ao execute um arquivo específico de um tooanother de conta do repositório Data Lake.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Por exemplo:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > sintaxe de saudação acima Especifica Olá toobe tooa copiado arquivo na conta de repositório Data Lake Olá destino. Ferramenta de AdlCopy cria uma pasta se Olá nome de pasta especificado não existe.
   >
   >

    Será tooenter solicitada credenciais Olá Olá assinatura do Azure sob a qual você tem a sua conta do repositório Data Lake. Você verá uma saída semelhante toohello a seguir:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Olá comando a seguir copia todos os arquivos de uma pasta específica na pasta Olá origem repositório Data Lake conta tooa no destino Olá conta do repositório Data Lake.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Considerações sobre o desempenho

Ao usar AdlCopy como uma ferramenta autônoma, cópia Olá é executada em compartilhadas, recursos gerenciados do Azure. Você pode obter nesse ambiente de desempenho de saudação depende de carga do sistema e dos recursos disponíveis. Esse modo é melhor usado para transferências ad hoc pequenas. Nenhum parâmetro necessário toobe ajustado ao usar AdlCopy como uma ferramenta autônoma.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Usar dados de toocopy AdlCopy (com a conta da análise Data Lake)
Você também pode usar a análise Data Lake conta tooData Lake armazenamento de blobs do hello toorun AdlCopy dados de toocopy do trabalho do armazenamento do Azure. Normalmente você usaria essa opção quando Olá dados toobe movido está no intervalo de saudação de gigabytes e terabytes e desejar que a taxa de transferência previsível e melhor desempenho.

toouse que sua conta da análise Data Lake com toocopy AdlCopy de um Blob de armazenamento do Azure, a origem de saudação (Blob de armazenamento do Azure) deve ser adicionada como uma fonte de dados para sua conta da análise Data Lake. Para obter instruções sobre como adicionar a conta de análise Data Lake de tooyour de fontes de dados adicionais, consulte [fontes de dados de conta de gerenciamento de análise do Data Lake](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Se você estiver copiando de uma conta do repositório Azure Data Lake como fonte de saudação usando uma conta da análise Data Lake, não é necessário tooassociate Olá conta do repositório Data Lake com hello conta da análise Data Lake. Olá Olá requisito tooassociate armazenamento de origem com hello conta da análise Data Lake é somente quando a fonte de saudação é uma conta de armazenamento do Azure.
>
>

Execute Olá toocopy de comando a seguir de uma conta de repositório Data Lake do armazenamento do Azure blob tooa usando a conta da análise Data Lake:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Por exemplo:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Da mesma forma, execute Olá toocopy de comando a seguir de uma conta de repositório Data Lake do armazenamento do Azure blob tooa usando a conta da análise Data Lake:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Considerações sobre o desempenho

Ao copiar dados no intervalo de saudação de terabytes, usar AdlCopy com sua própria conta da análise Azure Data Lake fornece desempenho melhor e mais previsível. parâmetro Hello que deve ser ajustado é o número de saudação de unidades de análise do Azure Data Lake toouse para o trabalho de cópia hello. Aumentar o número de saudação de unidades de aumentarão o desempenho de saudação do seu trabalho de cópia. Cada toobe do arquivo copiado pode usar uma unidade máxima. Especificação de mais unidades que o número de saudação de arquivos que estão sendo copiados não aumentará o desempenho.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Usar AdlCopy toocopy dados usando a correspondência de padrões
Nesta seção, você aprenderá como toouse AdlCopy toocopy dados de uma fonte (em nosso exemplo abaixo usamos o Blob de armazenamento do Azure) tooa conta de repositório Data Lake de destino usando a correspondência de padrões. Por exemplo, você pode usar o hello etapas abaixo toocopy todos os arquivos com extensão. csv do hello fonte blob toohello de destino.

1. Abra um prompt de comando e navegue diretório toohello onde AdlCopy é instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.
2. Execute Olá toocopy de comando a seguir todos os arquivos com extensão *. csv de um blob específico de saudação fonte contêiner tooa repositório Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Por exemplo:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Cobrança
* Se você usar ferramenta de AdlCopy hello como autônomo, que você será cobrado para custos de saída para a movimentação de dados, se a fonte Olá conta de armazenamento do Azure não está em Olá mesma região como Olá repositório Data Lake.
* Se você usar a ferramenta de AdlCopy Olá com sua análise Data Lake conta padrão [análise Data Lake taxas de cobrança](https://azure.microsoft.com/pricing/details/data-lake-analytics/) será aplicada.

## <a name="considerations-for-using-adlcopy"></a>Considerações para o uso do AdlCopy
* O AdlCopy (para a versão 1.0.5) permite copiar dados de origens que, juntas, têm mais de milhares de arquivos e pastas. No entanto, se você encontrar problemas ao copiar um conjunto de dados grande, distribuir Olá arquivos/pastas em subpastas diferentes e usar subpastas do hello caminho toothose como fonte de saudação em vez disso.

## <a name="performance-considerations-for-using-adlcopy"></a>Considerações de desempenho para o uso do AdlCopy

O AdlCopy dá suporte à cópia de dados que contém milhares de arquivos e pastas. No entanto, se você encontrar problemas ao copiar um conjunto de dados grande, você pode distribuir Olá arquivos/pastas em subpastas menores. O AdlCopy foi desenvolvido para cópias ad hoc. Se você estiver tentando toocopy dados de forma recorrente, você deve considerar o uso [do Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) que fornece gerenciamento completo em torno de operações de cópia de saudação.

## <a name="release-notes"></a>Notas de versão
* 1.0.13 - se você estiver copiando dados toohello mesma conta do repositório Azure Data Lake em adlcopy vários comandos, não é necessário tooreenter suas credenciais para cada mais executados. O Adlcopy agora gravará essas informações em cache entre várias execuções.

## <a name="next-steps"></a>Próximas etapas
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
