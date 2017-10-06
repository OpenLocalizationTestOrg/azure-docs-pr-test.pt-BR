---
title: aaaMove tooor de dados do armazenamento de BLOBs do Azure usando conectores SSIS | Microsoft Docs
description: Mova dados tooor do armazenamento de BLOBs do Azure usando conectores do SSIS.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Mover dados tooor do armazenamento de BLOBs do Azure usando conectores do SSIS
Olá [SQL Server Integration Services Feature Pack para Azure](https://msdn.microsoft.com/library/mt146770.aspx) fornece componentes tooconnect tooAzure, transferir dados entre fontes de dados do Azure e no local e processar dados armazenados no Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Depois que os clientes tem movido os dados locais em nuvem hello, eles podem acessá-lo de qualquer serviço do Azure tooleverage Olá todo o poder do pacote de saudação de tecnologias do Azure. Ele pode ser usado, por exemplo, no Azure Machine Learning ou em um cluster HDInsight.

Esse costuma ser Olá primeira etapa para Olá [SQL](machine-learning-data-science-process-sql-walkthrough.md) e [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) explicações passo a passo.

Para uma discussão de cenários canônicos que usam comercial do SSIS tooaccomplish precisa comum em cenários de integração de dados híbrido, consulte [fazendo mais com o SQL Server Integration Services Feature Pack para Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.

> [!NOTE]
> Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
tarefas de saudação tooperform descrito neste artigo, você deve ter uma assinatura do Azure e uma conta de armazenamento do Azure configurada. Você deve saber o armazenamento do Azure conta nome e a conta chave tooupload ou baixar os dados.

* tooset a uma **assinatura do Azure**, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obter instruções sobre como criar uma **conta de armazenamento** e para obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).

Olá toouse **conectores SSIS**, você deve baixar:

* **SQL Server 2014 ou 2016 Standard (ou mais recente)**: a instalação inclui os SQL Server Integration Services.
* **Microsoft SQL Server 2014 ou 2016 Integration Services Feature Pack para Azure**: eles podem ser baixados, respectivamente, do hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) e [integração do SQL Server 2016 Serviços](https://www.microsoft.com/download/details.aspx?id=49492) páginas.

> [!NOTE]
> O SSIS é instalado com o SQL Server, mas não está incluído na versão do hello Express. Para obter informações sobre quais aplicativos estão incluídos nas várias edições do SQL Server, veja [Edições do SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Para obter os materiais de treinamento sobre o SSIS, veja [Treinamento prático sobre o SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Para obter informações sobre como tooget up-e-em execução usando extração simple de toobuild SISS, transformação e carregamento (ETL) de pacotes, consulte [Tutorial do SSIS: Criando um pacote ETL simples](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Baixar o conjunto de dados NYC Taxi
Olá exemplo descrito aqui usa um conjunto de dados disponível publicamente – hello [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados. saudação de conjunto de dados consiste em distâncias de táxi sobre 173 milhões em NYC no ano Olá 2013. Há dois tipos de dados: dados sobre detalhes da corrida e dados sobre tarifas. Como há um arquivo para cada mês, temos 24 arquivos no total, cada um deles com aproximadamente 2 GB descompactados.

## <a name="upload-data-tooazure-blob-storage"></a>Carregue o armazenamento de blob de tooAzure de dados
dados toomove usando Olá SSIS feature pack a partir de armazenamento de blob tooAzure local, usamos uma instância do hello [ **tarefa de carregamento de BLOBs do Azure**](https://msdn.microsoft.com/library/mt146776.aspx), mostrado aqui:

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

parâmetros de Olá Olá usa tarefas são descritos aqui:

| Campo | Descrição |
| --- | --- |
| **AzureStorageConnection** |Especifica um Gerenciador de Conexão de armazenamento do Azure existente ou cria um novo que refere-se a conta de armazenamento do Azure tooan que aponte os arquivos de blob Olá toowhere estão hospedados. |
| **BlobContainer** |Especifica o nome de Olá Olá do contêiner de blob que mantêm arquivos Olá carregado como blobs. |
| **BlobDirectory** |Especifica o diretório de blob Olá onde o arquivo carregado Olá é armazenado como um blob de bloco. diretório de blob de saudação é uma estrutura hierárquica virtual. Se já existir um blob hello, it ia substituído. |
| **LocalDirectory** |Especifica o diretório de local de saudação que contém a saudação arquivos toobe carregado. |
| **FileName** |Especifica um arquivos de tooselect de filtro de nome com padrão de nome especificado da saudação. Por exemplo, MySheet\*.xls\* inclui arquivos como MySheet001.xls e MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Especifica um filtro de intervalo de tempo. Os arquivos modificados após *TimeRangeFrom* e antes de *TimeRangeTo* são incluídos. |

> [!NOTE]
> Olá **AzureStorageConnection** credenciais necessário toobe correto e hello **BlobContainer** devem existir antes de tentar a transferência de saudação.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Baixar dados do armazenamento de blob do Azure
dados de toodownload do armazenamento de tooon local de armazenamento de BLOBs do Azure com o SSIS, use uma instância do hello [tarefa de carregamento de BLOBs do Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Cenários mais avançados de SSIS-Azure
feature pack do SSIS Olá permite mais complexa toobe fluxos tratada por tarefas de empacotamento juntos. Por exemplo, Olá blob foi de feed de dados diretamente em um cluster HDInsight, cuja saída foi possível baixar o blob tooa voltar e, em seguida, armazenamento tooon local. O SSIS pode executar trabalhos de Hive e Pig em um cluster HDInsight usando conectores adicionais do SSIS:

* toorun de cluster com o SSIS, use um script do Hive em um Azure HDInsight [tarefa Hive](https://msdn.microsoft.com/library/mt146771.aspx).
* toorun de cluster com o SSIS, use um script do Pig em um Azure HDInsight [tarefa de Pig de HDInsight do Azure](https://msdn.microsoft.com/library/mt146781.aspx).

