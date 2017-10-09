---
title: "tolerância a falhas aaaAdd na atividade de cópia de fábrica de dados do Azure, ignorando linhas incompatíveis | Microsoft Docs"
description: "Saiba como tooadd a tolerância a falhas na atividade de cópia de fábrica de dados do Azure, ignorando linhas incompatíveis durante a cópia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Adicionar tolerância a falhas na Atividade de Cópia ignorando linhas incompatíveis

O Azure Data Factory [atividade de cópia](data-factory-data-movement-activities.md) oferece linhas incompatível de toohandle de duas maneiras ao copiar dados entre armazenamentos de dados de origem e do coletor:

- Você pode anular e falhar cópia hello atividade quando dados incompatíveis encontrado (comportamento padrão).
- Você pode continuar toocopy todos os dados de saudação adicionando a tolerância a falhas e ignorar as linhas de dados incompatíveis. Além disso, você pode registrar linhas incompatível Olá no armazenamento de BLOBs do Azure. Em seguida, você pode examinar Olá log toolearn Olá causa falha hello, corrigir dados saudação na fonte de dados de saudação e repita a atividade de cópia de saudação.

## <a name="supported-scenarios"></a>Cenários com suporte
A Atividade de Cópia dá suporte a três cenários para detectar, ignorar e registrar em log dados incompatíveis:

- **Incompatibilidade entre o tipo de dados de origem hello e tipo nativo do coletor Olá**

    Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blob tooa SQL de banco de dados com uma definição de esquema que contém três **INT** colunas de tipo. Olá linhas do arquivo CSV que contêm dados numéricos, como `123,456,789` são copiados com êxito toohello repositório de coletor. No entanto, Olá linhas que contêm valores não numéricos, como `123,456,abc` são detectados como incompatíveis e são ignorados.

- **Incompatibilidade no número de saudação de colunas entre a origem de saudação e do coletor de saudação**

    Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blob tooa SQL de banco de dados com uma definição de esquema que contém seis colunas. Hello arquivo CSV linhas que contêm seis colunas são copiados com êxito toohello repositório de coletor. linhas do arquivo CSV Olá que contêm menos de seis ou mais colunas são detectadas como incompatíveis e são ignoradas.

- **Violação de chave primária ao gravar o banco de dados relacional tooa**

    Por exemplo: copiar dados de um banco de dados do SQL server tooa SQL. Uma chave primária seja definida no banco de dados do SQL Olá coletor, mas nenhuma chave primária é definida no SQL server de origem hello. linhas de saudação duplicada que existem na fonte de saudação não podem ser copiado toohello coletor. Atividade de cópia copia apenas Olá primeira linha dos dados de origem Olá coletor hello. Hello subsequentes origem nas linhas que contêm o valor de chave primária Olá duplicado é detectadas como incompatíveis e é ignoradas.

## <a name="configuration"></a>Configuração
Olá, exemplo a seguir fornece uma tooconfigure de definição de JSON ignorar as linhas de saudação incompatível na atividade de cópia:

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
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Habilite ou não a omissão das linhas incompatíveis durante a cópia. | True <br/>False (padrão) | Não |
| **redirectIncompatibleRowSettings** | Um grupo de propriedades que pode ser especificado quando você quiser linhas incompatível do toolog hello. | &nbsp; | Não |
| **linkedServiceName** | Olá vinculado de serviço de log de saudação do armazenamento do Azure toostore que contém linhas de saudação ignorada. | nome de saudação de um [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [o AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) serviço, que se refere a instância de armazenamento de toohello que você deseja que o arquivo de log toouse toostore Olá vinculado. | Não |
| **path** | caminho de Olá Olá do arquivo de log que contém a saudação ignorada linhas. | Especifique o caminho de armazenamento de Blob Olá cujos dados incompatíveis do toouse toolog hello. Se você não fornecer um caminho, o serviço de saudação cria um contêiner para você. | Não |

## <a name="monitoring"></a>Monitoramento
Após a conclusão da execução da atividade de cópia de saudação, você pode ver o número de saudação de linhas ignoradas na seção monitoramento de saudação:

![Monitorar linhas incompatíveis ignoradas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Se você configurar linhas incompatível do toolog Olá, você pode encontrar o arquivo de log de saudação no seguinte caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` no arquivo de log Olá, você pode ver Olá linhas que foram ignoradas e Olá causa raiz de incompatibilidade de saudação.

Dados originais hello e o erro correspondente Olá são registradas no arquivo hello. Um exemplo do conteúdo do arquivo de log de saudação é da seguinte maneira:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a atividade de cópia de fábrica de dados do Azure, consulte [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md).
