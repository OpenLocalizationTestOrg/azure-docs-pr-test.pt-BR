---
title: "aaaMove dados usando a atividade de cópia | Microsoft Docs"
description: "Saiba mais sobre a movimentação de dados em pipelines do Data Factory: migração de dados entre repositórios na nuvem e entre um repositório local e um repositório na nuvem. Use a Atividade de Cópia."
keywords: "copiar dados, movimentação de dados, migração de dados, transferir dados"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Mover dados usando a Atividade de Cópia
## <a name="overview"></a>Visão geral
Fábrica de dados do Azure, você pode usar dados de toocopy de atividade de cópia entre local e nuvem armazenamentos de dados. Depois de copiar dados hello, pode ser mais transformado e analisado. Você também pode usar a transformação de toopublish de atividade de cópia e os resultados da análise de business intelligence (BI) e o consumo de aplicativo.

![Função da Atividade de Cópia](media/data-factory-data-movement-activities/copy-activity.png)

A Atividade de Cópia é alimentada por um [serviço disponível globalmente](#global)seguro, confiável e escalonável. Este artigo fornece detalhes sobre a movimentação de dados no Data Factory e na Atividade de Cópia.

Primeiramente, vejamos como a migração de dados ocorre entre dois repositórios de dados na nuvem e entre um repositório de dados local e um repositório de dados na nuvem.

> [!NOTE]
> em geral, consulte toolearn sobre atividades [Noções básicas sobre pipelines e atividades](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Copiando dados entre dois armazenamentos de dados em nuvem
Quando armazenamentos de dados de origem e do coletor estão em nuvem Olá, atividade de cópia percorre Olá dados de toocopy estágios a seguir do coletor de toohello fonte hello. serviço de saudação que habilita a atividade de cópia:

1. Lê dados de repositório de dados de origem de saudação.
2. Executa a serialização/desserialização, a compactação/descompactação, o mapeamento de coluna e a conversão de tipo. Ele faz essas operações com base em configurações de saudação do conjunto de dados de entrada hello, conjunto de dados de saída e atividade de cópia.
3. Grava o repositório de dados de destino de toohello de dados.

serviço Olá escolhe automaticamente a movimentação de dados Olá região ideal tooperform hello. Esta região é geralmente Olá um mais próximo toohello coletor repositório de dados.

![Cópia de nuvem para nuvem](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copiar dados entre um armazenamento de dados local e um armazenamento de dados em nuvem
toosecurely mover dados entre um repositório de dados local e um repositório de dados de nuvem, instale o Gateway de gerenciamento de dados em seu computador local. O Gateway de Gerenciamento de Dados é um agente que possibilita a movimentação e o processamento de dados híbridos. Você pode instalá-lo em Olá mesmo computador como o repositório de dados de saudação em si, ou em um computador separado que tenha acesso toohello dados armazenar.

Nesse cenário, o Gateway de gerenciamento de dados executa Olá serialização/desserialização, compactação/descompactação, mapeamento de coluna e conversão de tipo. Dados não fluem Olá serviço do Azure Data Factory. Em vez disso, o Gateway de gerenciamento de dados grava diretamente Olá dados toohello destino repositório.

![Cópia do local para a nuvem](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Confira [Mover dados entre repositórios de dados locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para ver uma introdução e instruções passo a passo. Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter informações detalhadas sobre esse agente.

Você também pode mover dados de / armazenamentos de dados de toosupported que são hospedadas no Azure máquinas virtuais (VMs) usando o Gateway de gerenciamento de dados. Nesse caso, você pode instalar o Gateway de gerenciamento de dados em Olá mesma VM como repositório de dados de saudação em si, ou em uma VM separada que tenha acesso toohello dados armazenar.

## <a name="supported-data-stores-and-formats"></a>Fontes de dados e formatos com suporte
Atividade de cópia na fábrica de dados copia dados de um repositório de dados fonte dados repositório tooa coletor. Fábrica de dados oferece suporte a saudação armazenamentos de dados a seguir. Dados de qualquer fonte podem ser gravados tooany coletor. Clique em um toolearn de repositório de dados como toocopy tooand de dados do repositório.

> [!NOTE] 
> Se você precisar toomove dados para/de um repositório de dados que não oferece suporte a atividade de cópia, use um **atividade personalizada** na fábrica de dados com sua própria lógica para copiar/mover dados. Para obter detalhes sobre como criar e usar uma atividade personalizada, confira [Usar atividades personalizadas em um pipeline do Azure Data Factory](data-factory-use-custom-activities.md).

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Armazena dados com * pode ser local ou na IaaS do Azure e requer que você tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) em uma máquina de IaaS no local/Azure.

### <a name="supported-file-formats"></a>Formatos de arquivo com suporte
Você pode usar a atividade de cópia muito**copiar arquivos como-é** entre armazenamentos de dados baseada em arquivo, você pode ignorar Olá [Formatar seção](data-factory-create-datasets.md) no tanto Olá entrada e saída definições de conjunto de dados. dados de saudação são copiados com eficiência sem qualquer serialização/desserialização.

Atividade de cópia também lerá e grava toofiles em formatos especificados: **texto JSON, Avro, ORC e Parquet**e um codec de compactação **GZip, Deflate, BZip2 e ZipDeflate** têm suporte. Consulte [Formatos de arquivo e compactação com suporte](data-factory-supported-file-and-compression-formats.md) para obter detalhes.

Por exemplo, você pode fazer a seguir Olá copia atividades:

* Copie os dados no SQL Server no local e gravar repositório tooAzure Data Lake no formato ORC.
* Copie os arquivos no formato de texto (CSV) do sistema de arquivos local e gravar tooAzure Blob em formato Avro.
* Copiar os arquivos compactados do sistema de arquivos local e descompactar e levadas para repositório tooAzure Data Lake.
* Copiar dados em formato de texto compactado (CSV) GZip de BLOBs do Azure e gravar tooAzure banco de dados SQL.

## <a name="global"></a>Movimentação de dados globalmente disponível
A fábrica de dados do Azure está disponível apenas em regiões de saudação Oeste dos EUA, Leste dos EUA e Norte da Europa. No entanto, o serviço de saudação que habilita a atividade de cópia está disponível globalmente em Olá regiões e regiões geográficas a seguir. topologia disponível globalmente Olá garante a movimentação de dados eficiente que normalmente evita saltos entre regiões. Confira [Serviços por região](https://azure.microsoft.com/regions/#services) para ver a disponibilidade do Data Factory e da Movimentação de Dados em uma região.

### <a name="copy-data-between-cloud-data-stores"></a>Copiar dados entre armazenamentos de dados em nuvem
Quando os armazenamentos de dados de origem e do coletor na nuvem hello, fábrica de dados usa uma implantação de serviço na região hello mais próximo coletor toohello Olá mesmo dados de saudação toomove de Geografia. Consulte toohello para mapear a tabela a seguir:

| Geografia Olá repositórios de dados de destino | Região de armazenamento de dados de destino Olá | Região usada para movimentação de dados |
|:--- |:--- |:--- |
| Estados Unidos | Leste dos EUA | Leste dos EUA |
| &nbsp; | Leste dos EUA 2 | Leste dos EUA 2 |
| &nbsp; | Centro dos EUA | Centro dos EUA |
| &nbsp; | Centro-Norte dos EUA | Centro-Norte dos EUA |
| &nbsp; | Centro-Sul dos Estados Unidos | Centro-Sul dos Estados Unidos |
| &nbsp; | Centro-Oeste dos EUA | Centro-Oeste dos EUA |
| &nbsp; | Oeste dos EUA | Oeste dos EUA |
| &nbsp; | Oeste dos EUA 2 | Oeste dos EUA |
| Canadá | Leste do Canadá | Canadá Central |
| &nbsp; | Canadá Central | Canadá Central |
| Brasil | Sul do Brasil | Sul do Brasil |
| Europa | Norte da Europa | Norte da Europa |
| &nbsp; | Europa Ocidental | Europa Ocidental |
| Reino Unido | Oeste do Reino Unido | Sul do Reino Unido |
| &nbsp; | Sul do Reino Unido | Sul do Reino Unido |
| Pacífico Asiático | Sudeste Asiático | Sudeste Asiático |
| &nbsp; | Ásia Oriental | Sudeste Asiático |
| Austrália | Leste da Austrália | Leste da Austrália |
| &nbsp; | Sudeste da Austrália | Sudeste da Austrália |
| Japão | Leste do Japão | Leste do Japão |
| &nbsp; | Oeste do Japão | Leste do Japão |
| Índia | Índia Central | Índia Central |
| &nbsp; | Índia Ocidental | Índia Central |
| &nbsp; | Sul da Índia | Índia Central |

Como alternativa, você pode indicar explicitamente região de saudação do toobe do serviço de fábrica de dados usada tooperform Olá cópia especificando `executionLocation` propriedade na atividade de cópia `typeProperties`. Os valores com suporte para essa propriedade estão listados acima da coluna **Região usada para movimentação de dados**. Observe que seus dados será por meio dessa região Olá durante a cópia. Por exemplo, toocopy entre o Azure armazena em Coreia, você pode especificar `"executionLocation": "Japan East"` tooroute por meio de região Japão (consulte [JSON de exemplo](#by-using-json-scripts) como referência).

> [!NOTE]
> Se região Olá Olá destino de armazenamento de dados não está na lista anterior ou não, por padrão atividade de cópia falhar, em vez de passar por uma região alternativa, a menos que `executionLocation` for especificado. lista de regiões Olá suportada será expandida ao longo do tempo.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copiar dados entre um armazenamento de dados local e um armazenamento de dados em nuvem
Quando os dados estiverem sendo copiados entre repositórios locais (ou IaaS/máquinas virtuais do Azure) e na nuvem, o [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) executa a movimentação de dados em um computador local ou máquina virtual. Olá não fluxo de dados por meio do serviço de saudação na nuvem hello, a menos que você use Olá [preparados cópia](data-factory-copy-activity-performance.md#staged-copy) recurso. Nesse caso, os dados fluem através de Olá preparo armazenamento de BLOBs do Azure antes de serem gravado no armazenamento de dados do coletor de saudação.

## <a name="create-a-pipeline-with-copy-activity"></a>Criar um pipeline com Atividade de Cópia
Você pode criar um pipeline com uma Atividade de Cópia de duas maneiras:

### <a name="by-using-hello-copy-wizard"></a>Usando o Assistente para cópia de saudação
Olá Assistente para cópia de fábrica de dados ajuda a toocreate um pipeline com atividade de cópia. Esse pipeline permite toocopy dados de fontes suportadas toodestinations *sem escrever JSON* definições de serviços vinculados, conjuntos de dados e pipelines. Consulte [Assistente para cópia de fábrica de dados](data-factory-copy-wizard.md) para obter detalhes sobre o Assistente de saudação.  

### <a name="by-using-json-scripts"></a>Usando scripts JSON
Você pode usar o Editor de fábrica de dados no hello portal do Azure, o Visual Studio ou o Azure PowerShell toocreate uma definição de JSON para um pipeline (usando a atividade de cópia). Em seguida, você pode implantar pipeline de saudação toocreate na fábrica de dados. Confira [Tutorial: Use Copy Activity in an Azure Data Factory pipeline (Tutorial: Usar Atividade de Cópia em um pipeline do Azure Data Factory)](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para ver um tutorial com instruções detalhadas.    

As propriedades JSON (como nome, descrição, tabelas de entrada e saída, e políticas) estão disponíveis para todos os tipos de atividade. Propriedades que estão disponíveis no hello `typeProperties` seção de atividade Olá variam de acordo com cada tipo de atividade.

Para a atividade de cópia, Olá `typeProperties` seção varia de acordo com os tipos de saudação de fontes e coletores. Clique em um fonte/coletor no hello [suporte para origens e coletores](#supported-data-stores-and-formats) toolearn seção sobre propriedades de tipo que oferece suporte a atividade de cópia para o repositório de dados.

Veja um exemplo de definição JSON:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
agenda de saudação que é definida em hello saída conjunto de dados determina quando hello atividade é executada (por exemplo: **diário**, frequência como **dia**e o intervalo como **1**). Hello atividade copia os dados de um conjunto de dados de entrada (**fonte**) tooan conjunto de dados de saída (**coletor**).

Você pode especificar mais de um conjunto de dados de entrada tooCopy atividade. Eles são usados tooverify Olá dependências antes hello atividade é executada. No entanto, somente os dados de saudação do hello primeiro conjunto de dados são copiado toohello conjunto de dados de destino. Para saber mais, confira [Agendamento e execução](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Desempenho e ajuste
Consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md), que descreve os principais fatores que afetam o desempenho de saudação de movimentação de dados (Copiar atividade) no Azure Data Factory. Também lista Olá observado desempenho durante o teste interno e discute várias desempenho de saudação toooptimize maneiras de atividade de cópia.

## <a name="fault-tolerance"></a>Tolerância a falhas
Por padrão, atividade de cópia irá parar cópia de dados e retornar falha ao encontrar dados incompatíveis entre a origem e o coletor; Embora seja possível configurar explicitamente tooskip e log Olá incompatível linhas e cópia somente cópia de saudação de toomake esses dados compatíveis foi bem-sucedida. Consulte Olá [tolerância a falhas de atividade de cópia](data-factory-copy-activity-fault-tolerance.md) em mais detalhes.

## <a name="security-considerations"></a>Considerações de segurança
Consulte Olá [considerações de segurança](data-factory-data-movement-security-considerations.md), que descreve a infraestrutura de segurança que os serviços de movimentação de dados no Azure Data Factory usam toosecure seus dados.

## <a name="scheduling-and-sequential-copy"></a>Agendamento e cópia sequencial
Confira [Agendamento e execução](data-factory-scheduling-and-execution.md) para obter informações detalhadas sobre como funcionam o agendamento e a execução no Data Factory. Ele é possível toorun várias operações de cópia após o outro de forma ordenada/sequencial. Consulte Olá [copiar sequencialmente](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) seção.

## <a name="type-conversions"></a>Conversões de tipo
Armazenamentos de dados diferentes têm sistemas de tipo nativo diferentes. Copiar atividade executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:

1. Converta native tipos tooa .NET do tipo de origem.
2. Converta de um tipo de coletor nativo de tooa de tipo .NET.

mapeamento de saudação de um tipo de .NET de tooa de sistema do tipo nativo para um repositório de dados é Olá dados respectivos store artigo. (Clique link específico Olá Olá [suporte para armazenamentos de dados](#supported-data-stores) tabela). Você pode usar esses mapeamentos toodetermine os tipos apropriados ao criar tabelas, para que a atividade de cópia executa conversões de saudação à direita.

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre hello atividade de cópia mais, consulte [copiar dados de armazenamento de BLOBs do Azure tooAzure banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn sobre como mover dados de um local repositório tooa nuvem dados repositório de dados, consulte [mover dados de armazenamentos de dados local toocloud](data-factory-move-data-between-onprem-and-cloud.md).
