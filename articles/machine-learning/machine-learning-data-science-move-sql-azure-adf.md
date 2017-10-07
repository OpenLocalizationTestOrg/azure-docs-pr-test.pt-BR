---
title: dados de aaaMove de um tooSQL do SQL Server no local do Azure com o Azure Data Factory | Microsoft Docs
description: "Configure um pipeline do ADF que compõe duas atividades de migração de dados que juntos mover dados em uma base diária entre bancos de dados locais e na nuvem de saudação."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Mover dados de um tooSQL de servidor local no SQL Azure com o Azure Data Factory
Este tópico mostra como toomove dados de um tooa de banco de dados do SQL Server local banco de dados do SQL Azure por meio do armazenamento de Blob do Azure usando Olá fábrica de dados do Azure (AAD).

Para uma tabela que resume as várias opções para mover dados tooan banco de dados do SQL Azure, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Introdução: O que é ADF e quando ele deve ser usado toomigrate dados?
A fábrica de dados do Azure é um serviço de integração de dados totalmente gerenciado baseado em nuvem que orquestra e automatiza a movimentação de saudação e transformação de dados. conceito-chave no modelo do ADF Olá Olá é pipeline. Um pipeline é um agrupamento lógico de atividades, cada uma delas define Olá ações tooperform nos dados Olá contidos em conjuntos de dados. Serviços vinculados são informações de saudação do toodefine usado necessárias para recursos de dados do Data Factory tooconnect toohello.

Com o ADF, serviços de processamento de dados existentes podem ser compostos em pipelines de dados que são altamente disponíveis e gerenciados em nuvem hello. Desses pipelines de dados podem ser agendado tooingest, preparar, transformar, analisar e publicar dados e ADF gerencia e organiza dados complexos hello e dependências de processamento. As soluções podem ser nuvem Olá rapidamente construído e implantado no, conectar-se um número crescente de locais e fontes de dados na nuvem.

Considere usar o ADF:

* Quando dados necessidades toobe continuamente migrado em um cenário híbrido que acessa os dois locais e recursos de nuvem
* Quando dados saudação são transacionados ou necessidades toobe modificado ou tem lógica de negócios adicionado tooit quando está sendo migrado.

ADF permite Olá planejamento e monitoramento de trabalhos usando scripts JSON simples que gerencia Olá movimento de dados em uma base periódica. O ADF também possui outros recursos, como suporte para operações complexas. Para obter mais informações sobre o AAD, consulte a documentação de saudação em [fábrica de dados do Azure (AAD)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Olá cenário
Criamos um pipeline do ADF que compõe duas atividades de migração de dados. Juntos eles mover dados em uma base diária entre um banco de dados do SQL local e um banco de dados do SQL Azure na nuvem hello. Olá duas atividades são:

* copiar dados de um tooan de banco de dados do SQL Server local conta de armazenamento de Blob do Azure
* copiar dados de tooan de conta de armazenamento de BLOBs do Azure hello Azure SQL Database.

> [!NOTE]
> Olá etapas mostradas aqui foram adaptado hello mais detalhadas tutorial fornecida pela equipe do ADF Olá: [mover dados entre fontes locais e na nuvem com o Gateway de gerenciamento de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) faz referência a seções relevantes toohello desse tópico são fornecidas quando apropriado.
>
>

## <a name="prereqs"></a>Pré-requisitos
Este tutorial presume que você tenha:

* Uma **assinatura do Azure**. Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Uma **conta de armazenamento do Azure**. Você pode usar uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo. Depois que você criou a conta de armazenamento hello, você precisa de conta de saudação tooobtain chave usada tooaccess armazenamento de saudação. Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Acesso tooan **banco de dados do SQL Azure**. Se você deve configurar um banco de dados do SQL Azure, Olá tpoic [guia de Introdução ao banco de dados SQL do Microsoft Azure ](../sql-database/sql-database-get-started.md) fornece informações sobre como tooprovision uma nova instância de um banco de dados do SQL Azure.
* **Azure PowerShell** instalado e configurado localmente. Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Este procedimento usa Olá [portal do Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Carregamento Olá dados tooyour do SQL Server local
Usamos Olá [NYC táxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate processo de migração de saudação. Olá NYC táxi dataset estiver disponível, conforme observado na postagem do que, no armazenamento de BLOBs do Azure [NYC táxi dados](http://www.andresmh.com/nyctaxitrips/). dados de saudação tem dois arquivos, o arquivo de trip_data.csv de saudação que contém detalhes de processamento, e o arquivo de trip_far.csv de hello, que contém detalhes de passagens Olá pago para cada viagem. Um exemplo e uma descrição desses arquivos são fornecidos na [Descrição do Conjunto de Dados de Viagens de Táxi de NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Você pode adaptar procedimento Olá fornecido aqui tooa conjunto de seus próprios dados ou execute as etapas de saudação conforme descrito usando Olá NYC táxi dataset. Olá tooupload NYC táxi de conjunto de dados em seu banco de dados do SQL Server local, execute o procedimento de saudação descrito no [dados de importação em massa no banco de dados do SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Essas instruções são para um SQL Server em uma máquina Virtual do Azure, mas o procedimento Olá para carregar toohello local SQL Server é Olá mesmo.

## <a name="create-adf"></a> Criar uma Data Factory do Azure
Olá instruções para criar uma nova fábrica de dados do Azure e um grupo de recursos no hello [portal do Azure](https://portal.azure.com/) são fornecidos [criar uma fábrica de dados do Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Nome hello nova ADF instância *adfdsp* e o grupo de recursos de saudação do nome criado *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Instalar e configurar o hello Gateway de gerenciamento de dados
tooenable seus pipelines em um toowork da fábrica de dados do Azure com um SQL Server no local, você precisa tooadd-lo como uma fábrica de dados do serviço vinculado toohello. toocreate um serviço vinculado para um SQL Server local, você deve:

* Baixe e instale o Gateway de gerenciamento de dados do Microsoft no computador do local de saudação.
* Configure o serviço de saudação vinculado Olá local gateway de dados fonte toouse hello.

Olá Data Management Gateway serializa e desserializa os dados de origem e do coletor de saudação no computador Olá onde ele está hospedado.

Para obter instruções e detalhes de instalação sobre o Gateway de Gerenciamento de Dados, confira [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Criar serviços vinculados tooconnect toohello recursos de dados
Um serviço vinculado define informações de saudação necessárias para o recurso de dados do Azure Data Factory tooconnect tooa. procedimento passo a passo de saudação para criar serviços vinculados é fornecido em [criar serviços vinculados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Temos três recursos neste cenário para o qual os serviços vinculados são necessários.

1. [Serviço vinculado para SQL Server local](#adf-linked-service-onprem-sql)
2. [Serviço vinculado do armazenamento de blob do Azure:](#adf-linked-service-blob-store)
3. [Serviço vinculado para o banco de dados do SQL Azure](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Serviço vinculado para o banco de dados do SQL Server local
toocreate Olá vinculado serviço para Olá local do SQL Server:

* Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure
* Selecione **SQL** e digite Olá *username* e *senha* as credenciais para saudação do SQL Server local. Você precisa tooenter Olá servername como um **nome de instância de barra invertida nome totalmente qualificado do servidor (nome_do_servidor \ nome_da_instância)**. Serviço vinculado de saudação do nome *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Serviço vinculado para Blob
toocreate Olá serviço vinculado para conta de armazenamento de BLOBs do Azure hello:

* Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure
* selecione **Conta de Armazenamento do Azure**
* Digite o nome de chave e o contêiner de conta de armazenamento de BLOBs do Azure do hello. Saudação de nome de serviço vinculado *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Serviço vinculado para o banco de dados do SQL Azure
toocreate Olá serviço vinculado para hello Azure SQL Database:

* Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure
* Selecione **SQL Azure** e digite Olá *username* e *senha* credenciais para hello Azure SQL Database. Olá *username* devem ser especificados como  *user@servername* .   

## <a name="adf-tables"></a>Definir e criar tabelas toospecify como tooaccess Olá conjuntos de dados
Crie tabelas que especificam a estrutura hello, local e disponibilidade de conjuntos de dados de saudação com hello baseado no script os procedimentos a seguir. Arquivos JSON são usados toodefine Olá tabelas. Para obter mais informações sobre a estrutura Olá desses arquivos, consulte [conjuntos de dados](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Olá deve ser executada `Add-AzureAccount` cmdlet antes de executar Olá [AzureDataFactoryTable novo](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm cmdlet que Olá assinatura do Azure à direita é selecionado para execução do comando hello. Para obter a documentação desse cmdlet, consulte [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

definições de saudação JSON com base nas tabelas de saudação usam Olá nomes a seguir:

* Olá **nome de tabela** Olá local SQL server está *nyctaxi_data*
* Olá **nome do contêiner** Olá armazenamento de BLOBs do Azure conta é *containername*  

Três definições de tabela são necessárias para este pipeline do ADF:

1. [Tabela do SQL local](#adf-table-onprem-sql)
2. [Tabela de blob ](#adf-table-blob-store)
3. [Tabela do SQL Azure](#adf-table-azure-sql)

> [!NOTE]
> Esses procedimentos usam o Azure PowerShell toodefine e criar hello atividades ADF. Mas essas tarefas também podem ser realizadas usando Olá portal do Azure. Para obter detalhes, consulte [Criar conjuntos de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>Tabela do SQL local
definição da tabela Olá para Olá local do SQL Server é especificado em Olá arquivo JSON a seguir:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

nomes de coluna de saudação não foram incluídos aqui. Você pode selecionar em nomes de coluna Olá sub incluindo-os aqui (detalhes Verifique Olá [documentação ADF](../data-factory/data-factory-data-movement-activities.md) tópico.

Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *onpremtabledef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\onpremtabledef.json*). Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Tabela de blob
A definição da tabela Olá para Olá saída local de blob está no seguinte hello (isso mapeia dados Olá incluído do blob de tooAzure local):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *bloboutputtabledef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\bloboutputtabledef.json*). Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>Tabela do SQL Azure
A definição da tabela de saudação de saudação que do SQL Azure de saída está no seguinte hello (esse esquema mapeia dados Olá provenientes de blob Olá):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *AzureSqlTable.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\AzureSqlTable.json*). Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Definir e criar o pipeline de saudação
Especifique atividades Olá que pertencem a toohello pipeline e criar o pipeline de saudação com hello baseado no script os procedimentos a seguir. Um arquivo JSON é usado toodefine Olá pipeline propriedades.

* script Hello supõe que Olá **nome do pipeline** é *AMLDSProcessPipeline*.
* Observe também que definimos periodicidade Olá de saudação pipeline toobe executado em diariamente base e use Olá tempo de execução padrão para o trabalho de saudação (12: 00 UTC).

> [!NOTE]
> Hello procedimentos a seguir usam o Azure PowerShell toodefine e criar hello ADF pipeline. Mas essa tarefa também pode ser realizada pelo Portal do Azure. Para obter detalhes, consulte [Criar pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Usando definições de tabela Olá fornecidas anteriormente, definição pipeline Olá Olá que ADF é especificada da seguinte maneira:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Copie esta definição de JSON de pipeline de saudação em um arquivo chamado *pipelinedef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\pipelinedef.json*). Crie o pipeline de Olá no ADF com hello Azure PowerShell cmdlet a seguir:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Confirme que você pode ver pipeline Olá em Olá AAD no Portal clássico do Azure de saudação aparecem como a seguir (quando você clicar em um diagrama de saudação)

![Pipeline do ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Iniciar Olá Pipeline
pipeline de saudação pode agora ser executada usando Olá comando a seguir:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Olá *startdate* e *enddate* toobe substituído com datas reais de saudação entre os quais você deseja Olá pipeline toorun precisam de valores de parâmetro.

Depois que o pipeline de saudação é executada, deve ser capaz de toosee Olá dados aparecem no contêiner de saudação selecionado para blob hello, um arquivo por dia.

Observe que não utilizaram funcionalidade Olá fornecida pelos dados do ADF toopipe incrementalmente. Para obter mais informações sobre como toodo este e outros recursos fornecidos pelo AAD, consulte Olá [documentação ADF](https://azure.microsoft.com/services/data-factory/).
