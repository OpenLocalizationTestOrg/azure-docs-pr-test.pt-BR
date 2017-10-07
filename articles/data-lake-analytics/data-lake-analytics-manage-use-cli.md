---
title: "aaaManage análise Azure Data Lake usando a Interface de linha de comando do Azure | Microsoft Docs"
description: "Saiba como contas de análise Data Lake toomanage, fontes de dados, trabalhos e os usuários usando a CLI do Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Gerenciar a Análise Azure Data Lake usando a CLI (interface de linha de comando) do Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, os usuários e trabalhos usando Olá CLI do Azure. tópicos de gerenciamento toosee usando outras ferramentas, clique em ' hello, selecione acima.


**Pré-requisitos**

Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **CLI do Azure**. Consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).
  * Baixe e instale Olá **pré-lançamento** [ferramentas CLI do Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) em ordem toocomplete nesta demonstração.
* **Autenticação**usando Olá seguinte comando:
  
        azure login
    Para obter mais informações sobre autenticação usando uma conta corporativa ou escolar, consulte [conectar tooan assinatura do Azure do hello CLI do Azure](../xplat-cli-connect.md).
* **Modo do comutador toohello Azure Resource Manager**usando Olá seguinte comando:
  
        azure config mode arm

**toolist Olá repositório Data Lake e análise Data Lake comandos:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Gerenciar Contas
Antes de executar qualquer trabalho da Análise Data Lake, você deve ter uma conta da Análise Data Lake. Ao contrário do Azure HDInsight, você não paga por uma conta da Análise quando ela não estiver executando um trabalho.  Você só paga pelo tempo de saudação quando ele está executando um trabalho.  Para saber mais, consulte [Visão geral sobre a Análise Azure Data Lake](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Criar contas
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Atualizar contas
Olá, seguinte comando atualiza propriedades de saudação de uma conta existente do Data Lake análise

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Listar contas
Listar contas da Análise Data Lake 

    azure datalake analytics account list

Listar contas da Análise Data Lake em um grupo de recursos específico

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Obter detalhes de uma conta específica da Análise Data Lake

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Excluir contas da Análise Data Lake
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Gerenciar as fontes de dados da conta
Análise data Lake atualmente suporta Olá fontes de dados a seguir:

* [Repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md)
* [Armazenamento do Azure](../storage/common/storage-introduction.md)

Quando você cria uma conta de análise, você deve designar uma conta de armazenamento do armazenamento do Azure Data Lake conta toobe saudação padrão. Olá padrão publicitário conta de armazenamento é usada toostore metadados de trabalho e o trabalho de logs de auditoria. Depois de criar uma conta da Análise, é possíveis adicionar outras contas do Armazenamento do Data Lake e/ou uma conta do Armazenamento do Azure. 

### <a name="find-hello-default-adl-storage-account"></a>Localizar a conta de armazenamento de publicitário saudação padrão
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

valor de saudação é listado em propriedades: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Adicionar outras contas de armazenamento de Blob do Azure
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Há suporte apenas para nomes curtos do Armazenamento de Blobs.  Não use o FQDN, por exemplo "myblob.blob.core.windows.net".
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Adicionar outras contas do Repositório Data Lake
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] é uma opção facultativa tooindicate seja Olá Data Lake conta Olá Data Lake que está sendo adicionado. 

### <a name="update-existing-data-source"></a>Atualizar a fonte de dados existente
tooset um padrão de saudação do repositório Data Lake conta toobe existente:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate uma chave de conta de armazenamento de Blob existente:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Listar fontes de dados:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Excluir fontes de dados:
toodelete uma conta do repositório Data Lake:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete uma conta de armazenamento de Blob:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Gerenciar trabalhos
Você deve ter uma conta da Análise Data Lake antes de criar um trabalho.  Para saber mais, consulte [Gerenciar contas da Análise Data Lake](#manage-accounts).

### <a name="list-jobs"></a>Listar trabalhos
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Exibir detalhes do trabalho
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Enviar trabalhos
> [!NOTE]
> prioridade de padrão de saudação de um trabalho é 1000 e grau de padrão de saudação de paralelismo de um trabalho é 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Cancelar trabalhos
Use a id do trabalho Olá lista comando toofind hello e use Cancelar toocancel Olá trabalho.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Gerenciar o catálogo
Catálogo de saudação U-SQL é usada toostructure dados e código para que eles possam ser compartilhados por scripts U-SQL. Catálogo de saudação permite Olá maior desempenho possível com dados no Azure Data Lake. Para saber mais, consulte [Usar o Catálogo do U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Listar itens do catálogo
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

tipos de saudação incluem o banco de dados, esquema, assembly, fonte de dados externa, tabela, função com valor de tabela ou as estatísticas de tabela.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Usar grupos ARM
Aplicativos normalmente são compostos por vários componentes, como, por exemplo, um aplicativo Web, banco de dados, servidor de banco de dados, armazenamento e serviços de terceiros. Gerenciador de recursos do Azure (ARM) permite que você toowork com recursos de saudação em seu aplicativo como um grupo, chamado tooas um grupo de recursos do Azure. Você pode implantar, atualizar, monitorar ou excluir todos os recursos de saudação para seu aplicativo em uma única operação coordenado. Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção. Você pode esclarecer cobrança para sua organização exibindo custos acumulados de saudação para todo o grupo hello. Para saber mais, consulte [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md). 

Um serviço de análise Data Lake pode incluir Olá componentes a seguir:

* Conta da Análise Azure Data Lake
* Conta padrão do Armazenamento do Azure Data Lake obrigatória
* Adicionar outras contas do Armazenamento do Azure Data Lake
* Contas do Armazenamento do Azure adicionais

Você pode criar todos esses componentes em um toomake de grupo ARM-los toomanage mais fácil.

![Conta e armazenamento da Análise Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Uma conta da análise Data Lake e contas de armazenamento dependente de saudação devem ser colocadas em Olá mesmo data center do Azure.
No entanto o grupo ARM Olá pode estar localizado em um data center diferente.  

## <a name="see-also"></a>Consulte também
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Introdução à Análise do Data Lake usando o Portal do Azure](data-lake-analytics-get-started-portal.md)
* [Gerenciar a Análise do Azure Data Lake usando o Portal do Azure](data-lake-analytics-manage-use-portal.md)
* [Monitorar e solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

