---
title: "Tolerância a falhas da atividade de cópia no Azure Data Factory | Microsoft Docs"
description: "Saiba como adicionar a tolerância a falhas na atividade de cópia no Azure Data Factory ignorando linhas incompatíveis."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
ms.openlocfilehash: 293ffb2a56ae970c71d495d7d929720ddf758307
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
#  <a name="fault-tolerance-of-copy-activity-in-azure-data-factory"></a>Tolerância a falhas da atividade de cópia no Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 – já disponível](v1/data-factory-copy-activity-fault-tolerance.md)
> * [Versão 2 – Versão prévia](copy-activity-fault-tolerance.md)

A atividade de cópia do Azure Data Factory oferece duas maneiras de manipular linhas incompatíveis ao copiar dados entre os armazenamentos de dados da origem e do coletor:

- Você pode anular e fazer com que a atividade de cópia falhe quando dados incompatíveis forem encontrados (comportamento padrão).
- Você pode continuar copiando todos os dados adicionando tolerância a falhas e ignorando linhas de dados incompatíveis. Além disso, é possível registrar em log as linhas incompatíveis no armazenamento de Blobs do Azure ou Azure Data Lake Store. Em seguida, examine o log para saber a causa da falha, corrija os dados na origem de dados e repita a atividade de cópia.

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que está com GA (disponibilidade geral), consulte a [tolerância a falhas da atividade de cópia na V1](v1/data-factory-copy-activity-fault-tolerance.md).


 ## <a name="supported-scenarios"></a>Cenários com suporte
A Atividade de Cópia dá suporte a três cenários para detectar, ignorar e registrar em log dados incompatíveis:

- **Incompatibilidade entre o tipo de dados de origem e o tipo nativo do coletor**. <br/><br/> Por exemplo: copiar dados de um arquivo CSV no Armazenamento de Blobs para um banco de dados SQL com uma definição de esquema que contenha três colunas do tipo INT. As linhas do arquivo CSV que contêm dados numéricos, como 123.456.789, são copiadas com êxito para o repositório de coletores. No entanto, as linhas que contêm valores não numéricos, como 123.456, abc, são detectadas como incompatíveis e ignoradas.
- **Incompatibilidade no número de colunas entre a origem e o coletor**. <br/><br/> Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blobs em um banco de dados SQL com uma definição de esquema que contém seis colunas. As linhas do arquivo CSV que contêm seis colunas são copiadas com êxito no armazenamento do coletor. As linhas do arquivo CSV que contêm mais ou menos de seis colunas são detectadas como incompatíveis e ignoradas.
- **Violação de chave primária ao gravar em banco de dados relacional**.<br/><br/> Por exemplo: copiar dados de um servidor SQL em um banco de dados SQL. Uma chave primária é definida no banco de dados SQL do coletor, mas nenhuma chave primária é definida no SQL Server de origem. As linhas duplicadas que existem na origem não podem ser copiadas no coletor. A Atividade de Cópia copia apenas a primeira linha dos dados de origem no coletor. As linhas da origem subsequentes que contêm o valor de chave primária duplicado são detectadas como incompatíveis e ignoradas.

>[!NOTE]
>Esse recurso não se aplica quando a atividade de cópia está configurada para invocar mecanismo de carregamento de dados externos, incluindo [SQL Data Warehouse PolyBase do Microsoft Azure](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) ou [Amazon Redshift Unload](connector-amazon-redshift.md#use-unload-to-copy-data-from-amazon-redshift). Para carregar dados no SQL Data Warehouse usando PolyBase, usar o suporte nativo a tolerância a falhas do PolyBase, especificando "[polyBaseSettings](connector-azure-sql-data-warehouse.md#azure-sql-data-warehouse-as-sink)" na atividade de cópia.

## <a name="configuration"></a>Configuração
O seguinte exemplo fornece uma definição de JSON que configura a omissão de linhas incompatíveis na Atividade de Cópia:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },
    "enableSkipIncompatibleRow": true,
    "redirectIncompatibleRowSettings": {
         "linkedServiceName": {
              "referenceName": "<Azure Storage or Data Lake Store linked service>",
              "type": "LinkedServiceReference"
            },
            "path": "redirectcontainer/erroroutput"
     }
}
```

Propriedade | DESCRIÇÃO | Valores permitidos | Obrigatório
-------- | ----------- | -------------- | -------- 
enableSkipIncompatibleRow | Especifica se deve ignorar linhas incompatíveis durante a cópia ou não. | True<br/>False (padrão) | Não 
redirectIncompatibleRowSettings | Um grupo de propriedades que poderá ser especificado quando você desejar registrar as linhas incompatíveis. | &nbsp; | Não 
linkedServiceName | O serviço vinculado do [Armazenamento do Azure](connector-azure-blob-storage.md#linked-service-properties) ou [Azure Data Lake Store](connector-azure-data-lake-store.md#linked-service-properties) para armazenar o log que contém as linhas ignoradas. | O nome de um serviço vinculado `AzureStorage` ou `AzureDataLakeStore`, que se refere à instância de armazenamento que você deseja usar para armazenar o arquivo de log. | Não 
caminho | O caminho do arquivo de log que contém as linhas ignoradas. | Especifique o caminho que você deseja usar para registrar em log os dados incompatíveis. Se você não fornecer um caminho, o serviço criará um contêiner para você. | Não 

## <a name="monitor-skipped-rows"></a>Monitorar linhas ignoradas
Depois que a execução da atividade de cópia for concluída, você verá o número de linhas ignoradas na saída da atividade de cópia:

```json
"output": {
            "dataRead": 95,
            "dataWritten": 186,
            "rowsCopied": 9,
            "rowsSkipped": 2,
            "copyDuration": 16,
            "throughput": 0.01,
            "redirectRowPath": "https://myblobstorage.blob.core.windows.net//myfolder/a84bf8d4-233f-4216-8cb5-45962831cd1b/",
            "errors": []
        },

```
Se você configurar para registrar em log as linhas incompatíveis, poderá encontrar o arquivo de log neste caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv`. 

Os arquivos de log só podem ser arquivos csv. Os dados originais ignorados serão registrados com uma vírgula como delimitador de coluna, se necessário. Mais duas colunas "ErrorCode" e "ErrorMessage" são adicionadas além dos dados de origem originais no arquivo de log, em que é possível ver a causa raiz da incompatibilidade. ErrorCode e ErrorMessage aparecerão entre aspas duplas. 

Um exemplo do conteúdo do arquivo de log é o seguinte:

```
data1, data2, data3, "UserErrorInvalidDataValue", "Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'."
data4, data5, data6, "2627", "Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4)."
```

## <a name="next-steps"></a>Próximas etapas
Consulte os outros artigos sobre atividade de cópia:

- [Visão geral da atividade de cópia](copy-activity-overview.md)
- [Desempenho da atividade de cópia](copy-activity-performance.md)


