---
title: aaaLoad terabytes de dados no SQL Data Warehouse | Microsoft Docs
description: Demonstra como 1 TB de dados podem ser carregado no Azure SQL Data Warehouse em 15 minutos com o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Data Factory
O [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais.  Criado em arquitetura MPP (processamento paralelo maciço), o SQL Data Warehouse é otimizado para cargas de trabalho do data warehouse corporativas.  Ele oferece elasticidade com armazenamento de tooscale flexibilidade Olá de nuvem e computação independentemente.

A introdução ao Azure SQL Data Warehouse agora é mais fácil do que nunca, usando o **Azure Data Factory**.  A fábrica de dados do Azure é um serviço de integração de dados totalmente gerenciado baseado em nuvem, que pode ser usado toopopulate um SQL Data Warehouse com dados de saudação do seu sistema existente e salvando tempo valioso durante a avaliação SQL Data Warehouse e criação de sua análise soluções. Aqui estão os principais benefícios de saudação do carregamento de dados no Azure SQL Data Warehouse usando o Azure Data Factory:

* **Fácil tooset backup**: etapa 5 intuitivas de assistente sem scripts necessários.
* **Suporte de armazenamento de dados avançados**: suporte interno para um conjunto avançado de armazenamentos de dados locais e baseados em nuvem.
* **Seguras e compatíveis**: dados são transferidos por HTTPS, ou rota expressa e a presença do serviço global garante que os dados nunca saem limites geográficos Olá
* **Desempenho incomparável usando PolyBase** – usando o Polybase é toomove dados de maneira mais eficientes de saudação no Azure SQL Data Warehouse. Usando Olá recurso de blob de preparo, você pode obter velocidades de alta carga de todos os tipos de armazenamentos de dados além do armazenamento de BLOBs do Azure, que Olá suporta Polybase por padrão.

Este artigo mostra como toouse dados do Assistente para cópia de fábrica de dados tooload 1 TB de armazenamento de BLOBs do Azure no Azure SQL Data Warehouse em menos de 15 minutos, com taxa de transferência mais 1,2 GBps.

Este artigo fornece instruções passo a passo para a movimentação de dados no Azure SQL Data Warehouse usando o Assistente para cópia de saudação.

> [!NOTE]
>  Para obter informações gerais sobre os recursos da fábrica de dados na movimentação de dados para/do Azure SQL Data Warehouse, consulte [mover tooand de dados de uso do Azure Data Factory do Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) artigo.
>
> Você também pode criar pipelines usando o Portal do Azure, Visual Studio, PowerShell, etc. Consulte [Tutorial: copiar dados de Blob do Azure tooAzure banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para uma rápida explicação passo a passo com instruções passo a passo para usar o hello atividade de cópia na fábrica de dados do Azure.  
>
>

## <a name="prerequisites"></a>Pré-requisitos
* Armazenamento de Blobs do Azure: esse teste usa o Armazenamento de Blobs do Azure (GRS) para armazenar o conjunto de dados de teste do TPC-H.  Se você não tiver uma conta de armazenamento do Azure, saiba [como uma conta de armazenamento do toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) dados: vamos toouse TPC-H como Olá teste de conjunto de dados.  toodo, é necessária toouse `dbgen` do Kit de ferramentas TPC-H, que ajuda a gerar o conjunto de dados de saudação.  Você pode baixar código-fonte para `dbgen` de [ferramentas TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilá-lo por conta própria ou download Olá compilado binário de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Execução dbgen.exe com os seguintes Olá comandos de arquivo simples de 1 TB de toogenerate para `lineitem` visualização de tabela em 10 arquivos:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Saudação de cópia geradas agora arquivos tooAzure Blob.  Consulte também[mover tooand de dados de um sistema de arquivos local usando o Azure Data Factory](data-factory-onprem-file-system-connector.md) como toodo que usando a cópia do ADF.    
* Azure SQL Data Warehouse: este experimento carrega dados no Azure SQL Data Warehouse criado com 6.000 DWUs

    Consulte também[criar um Data Warehouse do Azure SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obter instruções detalhadas sobre como toocreate um SQL Data Warehouse banco de dados.  tooget Olá melhor possíveis de carga desempenho no SQL Data Warehouse usando Polybase, escolhemos o número máximo de unidades de depósito de dados (DWUs) permitido na configuração de desempenho de saudação, que é de 6.000 DWUs.

  > [!NOTE]
  > Durante o carregamento de BLOBs do Azure, o desempenho do carregamento de dados de saudação são número de toohello diretamente proporcional de DWUs que você configurar no hello SQL Data Warehouse:
  >
  > Carregar 1 TB em um SQL Data Warehouse com 1.000 DWUs leva 87 minutos (vazão de dados de cerca de 200 MBps) Carregar 1 TB em um SQL Data Warehouse com 2.000 DWUs leva 46 minutos (vazão de dados de cerca de 380 MBps) Carregar 1 TB em um SQL Data Warehouse com 6.000 DWUs leva 14 minutos (vazão de dados de cerca de 1,2 GBps)
  >
  >

    toocreate um SQL Data Warehouse com 6.000 DWUs, mova Olá desempenho seletor de todos os toohello de maneira Olá à direita:

    ![Controle deslizante de Desempenho](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Um banco de dados existente que não está configurado com 6.000 DWUs poderá ser escalado verticalmente por você usando o Portal do Azure.  Navegue toohello banco de dados no portal do Azure e não há um **escala** botão Olá **visão geral** painel mostrada a saudação a imagem a seguir:

    ![Botão Dimensionar](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Clique em Olá **escala** seguinte de saudação do botão tooopen do painel, mover o valor máximo do toohello Olá controle deslizante e clique em **salvar** botão.

    ![Caixa de diálogo Dimensionar](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Este experimento carrega dados no Azure SQL Data Warehouse usando a classe de recurso `xlargerc`.

    necessidades de cópia de tooachieve melhor transferência possíveis, toobe executada por meio de um usuário do SQL Data Warehouse pertencentes muito`xlargerc` classe de recurso.  Saiba como toodo que seguindo [alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Crie o esquema da tabela de destino no banco de dados do Azure SQL Data Warehouse, executando Olá instrução DDL a seguir:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Com etapas de pré-requisito Olá concluídas, estamos agora pronto tooconfigure atividade de cópia de saudação usando o Assistente para cópia de saudação.

## <a name="launch-copy-wizard"></a>Iniciar o Assistente de cópia
1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+ novo** no canto superior esquerdo de saudação, clique em **Intelligence + análise**e clique em **Data Factory**.
3. Em Olá **nova fábrica de dados** folha:

   1. Digite **LoadIntoSQLDWDataFactory** para Olá **nome**.
       nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: **"LoadIntoSQLDWDataFactory" nome da fábrica de dados não está disponível**, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameLoadIntoSQLDWDataFactory) e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.  
   2. Selecione sua **assinatura**do Azure.
   3. Para o grupo de recursos, siga um destes Olá etapas a seguir:
      1. Selecione **usar existente** tooselect um grupo de recursos existente.
      2. Selecione **criar novo** tooenter um nome para um grupo de recursos.
   4. Selecione um **local** Olá fábrica de dados.
   5. Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.  
   6. Clique em **Criar**.
4. Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir:

   ![Página inicial da data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Na home page do hello fábrica de dados, clique em Olá **copiar dados** bloco toolaunch **Assistente para cópia de**.

   > [!NOTE]
   > Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** configuração (ou) manter habilitado e criar uma exceção para **login.microsoftonline.com**e tente iniciar o Assistente de saudação novamente.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Etapa 1: configurar o cronograma de carregamento de dados
Olá primeira etapa é a agenda de carregamento de dados de saudação de tooconfigure.  

Em Olá **propriedades** página:

1. Insira **CopyFromBlobToAzureSqlDataWarehouse** para o **Nome da tarefa**
2. Selecione opção **Executar uma vez agora**.   
3. Clique em **Avançar**.  

    ![Assistente de Cópia – página Propriedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Etapa 2: Configurar a origem
Este mostra seção Olá origem de saudação tooconfigure etapas: Blob do Azure que contém Olá 1 TB TPC-arquivos de item de linha de H.

1. Selecione Olá **armazenamento de BLOBs do Azure** como dados saudação armazenar e clique em **próximo**.

    ![Assistente de Cópia – selecionar página de origem](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Preencher informações de conexão de saudação para Olá conta de armazenamento de BLOBs do Azure e, em seguida, clique em **próximo**.

    ![Assistente de Cópia – informações de conexão de origem](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Escolha Olá **pasta** que contém a linha hello TPC-H arquivos de item e clique em **próximo**.

    ![Assistente de Cópia – selecionar pasta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Após clicar em **próximo**, configurações de formato de arquivo hello são detectadas automaticamente.  Verificar toomake-se de que delimitador de coluna é ' | 'em vez da saudação padrão por vírgulas','.  Clique em **próximo** depois de ter visualizado dados saudação.

    ![Assistente de Cópia – configurações de formato de arquivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Etapa 3: Configurar o destino
Esta seção mostra como tooconfigure Olá destino: `lineitem` tabela no banco de dados do hello Azure SQL Data Warehouse.

1. Escolha **Azure SQL Data Warehouse** como destino Olá armazenar e clique em **próximo**.

    ![Assistente de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Forneça informações de conexão Olá para o Azure SQL Data Warehouse.  Certifique-se de especificar usuário Olá que é um membro da função de saudação `xlargerc` (consulte Olá **pré-requisitos** seção para obter instruções detalhadas) e clique em **próximo**.

    ![Assistente de Cópia – informações de conexão de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Escolher tabela de destino hello e clique em **próximo**.

    ![Assistente de Cópia – página de mapeamento de tabela](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. Na página de mapeamento de esquema, deixe a opção "Aplicar o mapeamento de coluna" desmarcada e clique em **Avançar**.

## <a name="step-4-performance-settings"></a>Etapa 4: Configurações de desempenho

A opção **Permitir polybase** é marcada por padrão.  Clique em **Avançar**.

![Assistente de Cópia – página de mapeamento de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Etapa 5: Implantar e monitorar os resultados de carga
1. Clique em **concluir** toodeploy do botão.

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Após a conclusão da implantação de saudação, clique em `Click here toomonitor copy pipeline` toomonitor cópia de saudação andamento da execução. Pipeline de cópia Olá selecione criado no hello **atividade Windows** lista.

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Você pode exibir a cópia Olá detalhes da execução em Olá **Pesquisador de objetos de janela de atividade** o painel direito hello, incluindo Olá volume de dados lidos na origem e gravado no destino, a duração e a taxa de transferência média para Olá executar hello.

    Como você pode ver da saudação captura de tela a seguir, copiando 1 TB de armazenamento de BLOBs do Azure no SQL Data Warehouse levou 14 minutos, efetivamente para alcançar a taxa de transferência GBps 1,22!

    ![Assistente de Cópia – caixa de diálogo de êxito](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Práticas recomendadas
Aqui estão algumas práticas recomendadas para a execução de seu banco de dados do Azure SQL Data Warehouse:

* Use uma classe de recurso maior durante o carregamento em um ÍNDICE COLUMNSTORE CLUSTERIZADO.
* Para junções mais eficientes, considere usar a distribuição de hash por uma coluna selecionada em vez da distribuição round robin padrão.
* Para velocidades de carga, considere usar o heap para dados transitórios.
* Crie estatísticas depois de terminar de carregar o Azure SQL Data Warehouse.

Veja [Práticas Recomendadas para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) para obter detalhes.

## <a name="next-steps"></a>Próximas etapas
* [Assistente para cópia de fábrica de dados](data-factory-copy-wizard.md) -este artigo fornece detalhes sobre o Assistente para cópia de saudação.
* [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md) -este artigo contém medidas de desempenho de referência hello e guia de ajuste.
