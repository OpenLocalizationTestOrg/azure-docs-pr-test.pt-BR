---
title: "Copiar dados de maneira incremental usando o Controle de Alterações e o Azure Data Factory | Microsoft Docs"
description: "Neste tutorial, você deve criar um pipeline do Azure Data Factory que copie incrementalmente os dados delta de várias tabelas em um banco de dados do SQL Server local para um banco de dados SQL do Azure. "
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/12/2018
ms.author: jingwang
ms.openlocfilehash: 93df74da6e9db1bd03885179cd3917205ab3b4ee
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a>Carregar incrementalmente os dados do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure usando informações de controle de alterações 
Neste tutorial, você cria um data factory do Azure com um pipeline que carrega dados delta com base em informações de  **controle de alterações** no Banco de Dados SQL do Azure de origem para um armazenamento de blobs do Azure.  

Neste tutorial, você executa as seguintes etapas:

> [!div class="checklist"]
> * Prepare o armazenamento de dados de origem
> * Criar uma fábrica de dados.
> * Criar serviços vinculados. 
> * Crie conjuntos de dados de origem, coletor e de controle de alterações.
> * Criar, executar e monitorar o pipeline de cópia completo
> * Adicionar ou atualizar dados nas tabelas de origem
> * Criar, executar e monitorar o pipeline de cópia incremental

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que já está disponível (GA), confira a [documentação do Data Factory versão 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Visão geral
Em uma solução de integração de dados, o carregamento incremental de dados depois de uma carga de dados inicial é um cenário amplamente usado. Em alguns casos, os dados alterados dentro de um período em seu armazenamento de dados de origem podem ser facilmente divididos (por exemplo, LastModifyTime, CreationTime). Em alguns casos, não há uma forma explícita de identificar os dados delta da última vez que você processou os dados. A tecnologia de Controle de Alterações com suporte dos repositórios de dados, como o Banco de Dados SQL do Azure e SQL Server, pode ser usada para identificar os dados delta.  Este tutorial descreve como usar o Azure Data Factory versão 2 para trabalhar com a tecnologia de Controle de Alterações do SQL a fim de carregar incrementalmente os dados delta do Banco de Dados SQL do Azure no Armazenamento de Blobs do Azure.  Para obter informações mais concretas sobre a tecnologia de Controle de Alterações do SQL, consulte [Controle de alterações no SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server). 

## <a name="end-to-end-workflow"></a>Fluxos de trabalho completos
Estas são as etapas normais de fluxo de trabalho de ponta a ponta para carregar incrementalmente os dados usando a tecnologia de Controle de Alterações.

> [!NOTE]
> O Banco de Dados SQL do Azure e o SQL Server oferecem suporte à tecnologia de Controle de Alterações. Este tutorial usa o Banco de Dados SQL do Azure como o armazenamento de dados de origem. Você também pode usar um SQL Server local. 

1. **Carregamento inicial de dados históricos** (execução única):
    1. Habilite a tecnologia de Controle de Alterações no Banco de Dados SQL do Azure de origem.
    2. Obtenha o valor inicial de SYS_CHANGE_VERSION no Banco de Dados SQL do Azure como a linha de base para capturar os dados alterados.
    3. Carregue todos os dados do Banco de Dados SQL do Azure na conta de Armazenamento de Blobs do Azure. 
2. **Carregamento incremental de dados delta em uma agenda** (executar periodicamente após o carregamento inicial de dados):
    1. Obtenha os valores de SYS_CHANGE_VERSION antigos e novos.
    3. Carregue os dados delta unindo as chaves primárias de linhas alteradas (entre dois valores SYS_CHANGE_VERSION) de **sys.change_tracking_tables** com os dados na **tabela de origem** e, em seguida, mova os dados delta para destino.
    4. Atualize o SYS_CHANGE_VERSION para o carregamento de delta na próxima vez.

## <a name="high-level-solution"></a>Solução de alto nível
Neste tutorial, você cria dois pipelines que executam as duas operações a seguir:  

1. **Carregamento inicial:** crie um pipeline com uma atividade de cópia que copia todos os dados de armazenamento de dados de origem (Banco de Dados SQL do Azure) para o armazenamento de dados de destino (Armazenamento de Blobs do Azure).

    ![Carregamento completo dos dados](media/tutorial-incremental-copy-change-tracking-feature-portal/full-load-flow-diagram.png)
1.  **Carga incremental:** crie um pipeline com as seguintes atividades e execute-o periodicamente. 
    1. Crie **duas atividades de pesquisa** para obter o SYS_CHANGE_VERSION novo e antigo do Banco de Dados SQL do Azure e passe-o para a atividade de cópia.
    2. Crie **uma atividade de cópia** para copiar os dados inseridos/atualizados/excluídos entre os dois valores SYS_CHANGE_VERSION do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure.
    3. Crie **uma atividade de procedimento armazenado** para atualizar o valor de SYS_CHANGE_VERSION para a próxima execução do pipeline.

    ![Incrementar o diagrama de fluxo de carga](media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-load-flow-diagram.png)


Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>pré-requisitos
* **Banco de dados SQL do Azure**. Você usa o banco de dados como um armazenamento de dados de **origem**. Se você não tiver um Banco de Dados SQL do Azure, veja o artigo [Criar um Banco de Dados SQL do Azure](../sql-database/sql-database-get-started-portal.md) para conhecer as etapas para criar um.
* **Conta de Armazenamento do Azure**. Você usa o Armazenamento de Blobs como um armazenamento de dados de **coletor**. Se você não tiver uma conta de Armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para conhecer as etapas para criar uma. Crie um contêiner denominado **adftutorial**. 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Criar uma tabela de fonte de dados no Banco de Dados SQL do Azure
1. Inicie o **SQL Server Management Studio** e conecte-se à réplica principal. 
2. No **Gerenciador de Servidores**, clique com o botão direito do mouse no **banco de dados** e escolha **Nova Consulta**.
3. Execute o comando SQL a seguir no Banco de Dados SQL do Azure para criar uma tabela chamada `data_source_table` como o repositório de fonte de dados.  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. Habilite o mecanismo de **Controle de Alterações** em seu banco de dados e na tabela de origem (data_source_table) executando a seguinte consulta SQL: 

    > [!NOTE]
    > - Substitua &lt;seu nome de banco de dados&gt; pelo nome do Banco de Dados SQL do Azure que tenha data_source_table. 
    > - Os dados alterados são mantidos por dois dias no exemplo atual. Se você carregar os dados alterados a cada três dias ou mais, alguns dados alterados não serão incluídos.  Você precisa de como alterar o valor de CHANGE_RETENTION para um número maior. Como alternativa, certifique-se de que seu período de carregamento dos dados alterados esteja dentro de dois dias. Para saber mais, consulte [Habilitar o controle de alterações de um banco de dados](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. Crie uma nova tabela e armazene o ChangeTracking_version com um valor padrão executando a consulta a seguir: 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > Se os dados não forem alterados após a habilitação do controle de alterações para o Banco de Dados SQL, o valor da versão do controle de alterações será 0.
6. Execute a consulta a seguir para criar um procedimento armazenado em seu Banco de Dados SQL do Azure. O pipeline chama esse procedimento armazenado para atualizar a versão do controle de alteração na tabela criada na etapa anterior. 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a>Azure PowerShell
Instale os módulos mais recentes do Azure PowerShell seguindo as instruções em [Como instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Criar uma data factory

1. Clique em **Novo** no menu à esquerda, clique em **Dados + Análise** e clique em **Data Factory**. 
   
   ![Novo -> DataFactory](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory-menu.png)
2. Na página **Novo data factory**, insira **ADFTutorialDataFactory** no campo **nome**. 
      
     ![Página de novo data factory](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory.png)
 
   O nome do Azure Data Factory deve ser **globalmente exclusivo**. Se você receber o seguinte erro, altere o nome de data factory (por exemplo, yournameADFTutorialDataFactory) e tente criar novamente. Confira o artigo [Data Factory - regras de nomenclatura](naming-rules.md) para ver as regras de nomenclatura para artefatos do Data Factory.
  
       `Data factory name “ADFTutorialDataFactory” is not available`
3. Selecione a **assinatura** do Azure na qual você deseja criar o data factory. 
4. Para o **Grupo de Recursos**, execute uma das seguintes etapas:
     
      - Selecione **Usar existente**e selecione um grupo de recursos existente na lista suspensa. 
      - Selecione **Criar novo**e insira o nome de um grupo de recursos.   
         
        Para saber mais sobre grupos de recursos, consulte [Usando grupos de recursos para gerenciar recursos do Azure](../azure-resource-manager/resource-group-overview.md).  
4. Selecione **V2 (Versão Prévia)** para a **versão**.
5. Selecione o **local** do data factory. Apenas os locais com suporte são exibidos na lista suspensa. Os armazenamentos de dados (Armazenamento do Azure, Banco de Dados SQL do Azure, etc.) e serviços de computação (HDInsight, etc.) usados pelo data factory podem estar em outras regiões.
6. Selecione **Fixar no painel**.     
7. Clique em **Criar**.      
8. No painel, você vê o seguinte bloco com status: **Implantando data factory**. 

    ![implantando bloco data factory](media/tutorial-incremental-copy-change-tracking-feature-portal/deploying-data-factory.png)
9. Após a criação, a página do **Data Factory** será exibida conforme mostrado na imagem.
   
   ![Página inicial da data factory](./media/tutorial-incremental-copy-change-tracking-feature-portal/data-factory-home-page.png)
10. Clique no bloco **Criar e Monitorar** para iniciar a interface do usuário do Azure Data Factory em uma guia separada.
11. Na página de **introdução**, alterne para a guia **Editar** no painel esquerdo, conforme mostrado na imagem a seguir: 

    ![Criar botão de pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/get-started-page.png)

## <a name="create-linked-services"></a>Criar serviços vinculados
Os serviços vinculados são criados em um data factory para vincular seus armazenamentos de dados e serviços de computação ao data factory. Nesta seção, você cria serviços vinculados para sua conta de Armazenamento do Azure e o Banco de Dados SQL do Azure. 

### <a name="create-azure-storage-linked-service"></a>Crie um serviço vinculado do Armazenamento do Azure.
Nesta etapa, você vincula a Conta de Armazenamento do Azure ao data factory.

1. Clique em **Conexões** e clique em **+ Novo**.

   ![Botão de nova conexão](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-connection-button-storage.png)
2. Na janela **Novo serviço vinculado**, selecione **Armazenamento de Blobs do Azure** e clique em **Continuar**. 

   ![Selecionar Armazenamento de Blobs do Azure](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-storage.png)
3. Na janela **Novo serviço vinculado** execute as seguintes etapas: 

    1. Insira **AzureStorageLinkedService** como o **Nome**. 
    2. Selecione sua conta de Armazenamento do Azure como o **Nome da conta de armazenamento**. 
    3. Clique em **Salvar**. 
    
   ![Configurações da Conta de Armazenamento do Azure](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-storage-linked-service-settings.png)


### <a name="create-azure-sql-database-linked-service"></a>Crie um serviço vinculado do Banco de Dados SQL do Azure.
Nesta etapa, você vincula o banco de dados SQL do Azure ao data factory.

1. Clique em **Conexões** e clique em **+ Novo**.
2. Na janela **Novo Serviço Vinculado**, selecione **Banco de Dados SQL do Azure** e clique em **Continuar**. 
3. Na janela **Novo Serviço Vinculado**, execute estas etapas: 

    1. Insira **AzureSqlDatabaseLinkedService** para o campo **Nome**. 
    2. Selecione o servidor SQL do Azure no campo **Nome do servidor**.
    4. Selecione o seu banco de dados SQL do Azure no campo **Nome do banco de dados**. 
    5. Insira o nome do usuário no campo **Nome de usuário**. 
    6. Insira a senha do usuário no campo **Senha**. 
    7. Clique em **Testar conectividade** para testar a conexão.
    8. Clique em **Salvar** para salvar o serviço vinculado. 
    
       ![Configurações do serviço vinculado para o Banco de Dados SQL do Azure](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-sql-database-linked-service-settings.png)

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados para representar a fonte de dados, o destino de dados. e o local para armazenar o SYS_CHANGE_VERSION.

### <a name="create-a-dataset-to-represent-source-data"></a>Criar um conjunto de dados para representar dados de origem 
Nesta etapa, você cria conjuntos de dados para representar os dados de origem. 

1. No modo de exibição de árvore, clique em **+ (adição)** e clique em **Conjunto de dados**. 

   ![Menu Novo conjunto de dados](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Selecione o **Banco de Dados SQL do Azure** e clique em **Concluir**. 

   ![Tipo de conjunto de dados de origem - Banco de Dados SQL do Azure](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-sql-database.png)
3. Você verá uma nova guia para configuração do conjunto de dados. Você também verá o conjunto de dados no modo de exibição de árvore. Na janela **Propriedades**, altere o nome do conjunto de dados para **SourceDataset**.

   ![Nome do conjunto de dados de origem](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-name.png)    
4. Alterne para a guia **Conexão** e siga estas etapas: 
    
    1. Selecione **AzureSqlDatabaseLinkedService** para **Serviço vinculado**. 
    2. Selecione **[dbo]. [ data_source_table]** para **Tabela**. 

   ![Conexão de Origem](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-connection.png)

### <a name="create-a-dataset-to-represent-data-copied-to-sink-data-store"></a>Criar um conjunto de dados para representar dados copiados para o armazenamento de dados do coletor. 
Nesta etapa, você cria um conjunto de dados para representar os dados copiados do armazenamento de dados de origem. Você cria o contêiner adftutorial em seu Armazenamento de Blobs do Azure como parte dos pré-requisitos. Crie o contêiner caso ele não exista ou defina-o para o nome de um contêiner existente. Neste tutorial, o nome do arquivo de saída é gerado dinamicamente pelo uso da expressão: `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.

1. No modo de exibição de árvore, clique em **+ (adição)** e clique em **Conjunto de dados**. 

   ![Menu Novo conjunto de dados](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Selecione **Armazenamento de Blobs do Azure** e clique em **Concluir**. 

   ![Tipo de conjunto de dados do coletor - Armazenamento de Blobs do Azure](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-type.png)
3. Você verá uma nova guia para configuração do conjunto de dados. Você também verá o conjunto de dados no modo de exibição de árvore. Na janela **Propriedades**, altere o nome do conjunto de dados para **SinkDataset**.

   ![Conjunto de dados do coletor - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-name.png)
4. Alterne para a guia **Conexão** na janela Propriedades e execute as seguintes etapas:

    1. Selecione **AzureStorageLinkedService** para **Serviço vinculado**.
    2. Digite **adftutorial/incchgtracking** para a parte da **pasta** no **Caminho do arquivo**.
    3. Digite **@CONCAT('Incremental-', pipeline().RunId, '.txt')** para a parte do **arquivo** no **Caminho do arquivo**.  

       ![Conjunto de dados do coletor - conexão](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-connection.png)

### <a name="create-a-dataset-to-represent-change-tracking-data"></a>Criar um conjunto de dados para representar dados de controle de alterações 
Nesta etapa, você cria um conjunto de dados para armazenar a versão do controle de alterações.  Você criou a tabela table_store_ChangeTracking_version como parte dos pré-requisitos.

1. No modo de exibição de árvore, clique em **+ (adição)** e clique em **Conjunto de dados**. 
2. Selecione o **Banco de Dados SQL do Azure** e clique em **Concluir**. 
3. Você verá uma nova guia para configuração do conjunto de dados. Você também verá o conjunto de dados no modo de exibição de árvore. Na janela **Propriedades**, altere o nome do conjunto de dados para **ChangeTrackingDataset**.
4. Alterne para a guia **Conexão** e siga estas etapas: 
    
    1. Selecione **AzureSqlDatabaseLinkedService** para **Serviço vinculado**. 
    2. Selecione **[dbo].[table_store_ChangeTracking_version]** para **Tabela**. 

## <a name="create-a-pipeline-for-the-full-copy"></a>Criar um pipeline para a cópia completa
Nesta etapa, crie um pipeline com uma atividade de cópia que copia todos os dados de armazenamento de dados de origem (Banco de Dados SQL do Azure) para o armazenamento de dados de destino (Armazenamento de Blobs do Azure).

1. Clique em **+ (adição)** no painel esquerdo e clique em **Pipeline**. 

    ![Menu do novo pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu.png)
2. Você verá uma nova guia para configuração do pipeline. Você também verá o pipeline no modo de exibição de árvore. Na janela **Propriedades**, altere o nome do pipeline para **FullCopyPipeline**.

    ![Menu do novo pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-name.png)
3. Na caixa de ferramentas **Atividades**, expanda o **Fluxo de dados** e arraste e solte a atividade **Copiar** para a superfície de designer do pipeline e defina o nome como **FullCopyActivity**. 

    ![Atividade de cópia completa - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-activity-name.png)
4. Alterne para a guia **Fonte** e selecione **SourceDataset** para o campo **Conjunto de dados de origem**. 

    ![Atividade de cópia - origem](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-source.png)
5. Alterne para a guia **Coletor** e selecione **SinkDataset** para o campo **Conjunto de dados do coletor**. 

    ![Atividade de cópia - Coletor](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-sink.png)
6. Para validar a definição do pipeline, clique em **Validar** na barra de ferramentas. Confirme se não houver nenhum erro de validação. Feche o **Relatório de validação do pipeline** clicando em **>>**. 

    ![Validar o pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-validate.png)
7. Para publicar as entidades (serviços vinculados, conjuntos de dados e pipelines), clique em **Publicar**. Aguarde até que a publicação seja bem-sucedida. 

    ![Botão Publicar](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button.png)
8. Aguarde até que você veja a mensagem **Publicado com êxito**. 

    ![Publicado com êxito](./media/tutorial-incremental-copy-change-tracking-feature-portal/publishing-succeeded.png)
9. Você também pode ver notificações clicando no botão à esquerda **Mostrar notificações**. Para fechar a janela de notificações, clique em **x**.

    ![Mostrar notificações](./media/tutorial-incremental-copy-change-tracking-feature-portal/show-notifications.png)


### <a name="run-the-full-copy-pipeline"></a>Executar o pipeline de cópia completa
Clique em **Gatilho** na barra de ferramentas para o pipeline e clique em **Disparar agora**. 

![Menu Disparar agora](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu.png)

### <a name="monitor-the-full-copy-pipeline"></a>Monitorar o pipeline de cópia completa

1. Clique na guia **Monitorar** à esquerda. Você verá a execução do pipeline na lista e o seu respectivo status. Para atualizar a lista, clique em **Atualizar**. Os links na coluna Ações permitem exibir execuções de atividade associadas com a execução do pipeline e executar novamente o pipeline. 

    ![Execuções de pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/monitor-full-copy-pipeline-run.png)
2. Para ver as execuções de atividade associadas com a execução do pipeline, clique no link **Exibir as execuções de Aatividade** na coluna **Ações**. Existe apenas uma atividade no pipeline, então você vê apenas uma entrada na lista. Para alternar novamente para a exibição de pipeline em execução, Clique em **Pipelines** na parte superior. 

    ![Execuções de atividade](./media/tutorial-incremental-copy-change-tracking-feature-portal/activity-runs-full-copy.png)

### <a name="review-the-results"></a>Revise os resultados
Você verá um arquivo chamado `incremental-<GUID>.txt` na pasta `incchgtracking` do contêiner `adftutorial`. 

![Arquivo de saída da cópia completa](media\tutorial-incremental-copy-change-tracking-feature-portal\full-copy-output-file.png)

O arquivo deve ter os dados do Banco de Dados SQL do Azure:

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a>Adicionar mais dados à tabela de origem

Execute a seguinte consulta no Banco de Dados SQL do Azure para adicionar uma linha e atualizar uma linha. 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a>Criar um pipeline para a cópia delta
Nesta etapa, você cria um pipeline com as seguintes atividades e execute-o periodicamente. As **atividades de pesquisa** obtêm o SYS_CHANGE_VERSION novo e antigo do Banco de Dados SQL do Azure e o passa para a atividade de cópia. A **atividade de cópia** copia os dados inseridos/atualizados/excluídos entre os dois valores SYS_CHANGE_VERSION do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure. A **atividade de procedimento armazenado** atualiza o valor de SYS_CHANGE_VERSION para a próxima execução do pipeline.

1. Na interface de usuário do Data Factory, alterne para a guia **Editar**. Clique em **+ (adição)** no painel esquerdo e clique em **Pipeline**. 

    ![Menu do novo pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu-2.png)
2. Você verá uma nova guia para configuração do pipeline. Você também verá o pipeline no modo de exibição de árvore. Na janela **Propriedades**, altere o nome do pipeline para **IncrementalCopyPipeline**.

    ![Nome do pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-pipeline-name.png)
3. Expanda **Banco de Dados SQL** na caixa de ferramentas **Atividades** e arraste e solte a atividade **Pesquisar** para a superfície do designer de pipeline. Defina o nome da atividade como **LookupLastChangeTrackingVersionActivity**. Essa atividade obtém a versão de controle de alterações usada na última operação de cópia armazenada na tabela **table_store_ChangeTracking_version**.

    ![Atividade de pesquisa - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-name.png)
4. Alterne para **Configurações** na janela **Propriedades** e selecione **ChangeTrackingDataset** para o campo **Conjunto de dados de origem**. 

    ![Atividade de pesquisa - configurações](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-settings.png)
5. Arraste e solte a atividade de **Pesquisa** da caixa de ferramentas **Atividades** para a superfície do designer de pipeline. Defina o nome da atividade como **LookupCurrentChangeTrackingVersionActivity**. Essa atividade obtém a versão atual de controle de alterações.

    ![Atividade de pesquisa - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-name.png)
6. Alterne para **Configurações** na janela **Propriedades** e execute as seguintes etapas:

    1. Selecione **SourceDataset** para o campo **Conjunto de dados de origem**.
    2. Selecione **Consulta** para **Usar consulta**. 
    3. Insira a seguinte consulta SQL para **Consulta**. 

        ```sql
        SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion
        ```

    ![Atividade de pesquisa - configurações](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-settings.png)
7. Na caixa de ferramentas **Atividades**, expanda **Fluxo de dados**e arraste e solte a atividade **Cópia** para a superfície do designer de pipeline. Defina o nome da atividade como **IncrementalCopyActivity**. Esta atividade copia os dados entre a última versão de controle de alterações e a versão atual de controle de alterações para o armazenamento de dados de destino. 

    ![Atividade de cópia - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-activity-name.png)
8. Alterne para a guia **Fonte** na janela **Propriedades** e execute as seguintes etapas:

    1. Selecione **SourceDataset** para o **Conjunto de dados de origem**. 
    2. Selecione **Consulta** para **Usar consulta**. 
    3. Insira a seguinte consulta SQL para **Consulta**. 

        ```sql
        select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}
        ```
    
    ![Atividade de cópia - configurações da fonte](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-source-settings.png)
9. Alterne para a guia **Coletor** e selecione **SinkDataset** para o campo **Conjunto de dados do coletor**. 

    ![Atividade de cópia - configurações do coletor](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-sink-settings.png)
10. **Conecte ambas as atividades de Pesquisa à atividade de Cópia** uma por uma. Arraste o botão **verde** anexado à atividade de **Pesquisa** para a atividade de **Cópia**. 

    ![Conecte as atividades de Pesquisa e Cópia](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-lookup-and-copy.png)
11. Arraste e solte a atividade de **Procedimento armazenado** da caixa de ferramentas **Atividades** para a superfície do designer de pipeline. Defina o nome da atividade como **StoredProceduretoUpdateChangeTrackingActivity**. Essa atividade atualiza a versão de controle de alterações na tabela **table_store_ChangeTracking_version**.

    ![Atividade de procedimento armazenado - nome](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-activity-name.png)
12. Alterne para a guia *Conta SQL** e selecione **AzureSqlDatabaseLinkedService** para o **Serviço vinculado**. 

    ![Atividade de procedimento armazenado - Conta SQL](./media/tutorial-incremental-copy-change-tracking-feature-portal/sql-account-tab.png)
13. Alterne para a guia **Procedimento armazenado** e execute as etapas a seguir: 

    1. Digite **Update_ChangeTracking_Version** para **Nome do procedimento armazenado**.  
    2. Na seção **parâmetros de procedimento armazenado**, use o botão **+ Novo** para adicionar os dois parâmetros a seguir:

        | NOME | type | Valor | 
        | ---- | ---- | ----- | 
        | CurrentTrackingVersion | INT64 | @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion} | 
        | TableName | Cadeia de caracteres | @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName} | 
    
        ![Atividade de procedimento armazenado - Parâmetros](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-parameters.png)
14. **Conecte a atividade de Cópia à atividade de Procedimento armazenado**. Arraste o botão **verde** anexado à atividade de Cópia para a atividade de Procedimento armazenado. 

    ![Conecte as atividades de Cópia e Procedimento armazenado](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-copy-stored-procedure.png)
15. Clique em **Validar** na barra de ferramentas. Confirme se não houver nenhum erro de validação. Feche a janela **Relatório de validação do pipeline** clicando em **>>**. 

    ![Botão Validar](./media/tutorial-incremental-copy-change-tracking-feature-portal/validate-button.png)
16.  Publique as entidades (serviços vinculados, conjuntos de dados e pipelines) para o serviço de Data Factory clicando no botão **Publicar**. Aguarde até que você veja a mensagem **Publicado com êxito**. 

        ![Botão Publicar](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button-2.png)    

### <a name="run-the-incremental-copy-pipeline"></a>Executar o pipeline de cópia incremental
Clique em **Gatilho** na barra de ferramentas para o pipeline e clique em **Disparar agora**. 

![Menu Disparar agora](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu-2.png)

### <a name="monitor-the-incremental-copy-pipeline"></a>Monitorar o pipeline de cópia incremental
1. Clique na guia **Monitorar** à esquerda. Você verá a execução do pipeline na lista e o seu respectivo status. Para atualizar a lista, clique em **Atualizar**. Os links na coluna **Ações** permitem exibir execuções de atividade associadas à execução do pipeline e executar novamente o pipeline. 

    ![Execuções de pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-pipeline-runs.png)
2. Para ver as execuções de atividade associadas com a execução do pipeline, clique no link **Exibir as execuções de Aatividade** na coluna **Ações**. Existe apenas uma atividade no pipeline, então você vê apenas uma entrada na lista. Para alternar novamente para a exibição de pipeline em execução, Clique em **Pipelines** na parte superior. 

    ![Execuções de atividade](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-activity-runs.png)


### <a name="review-the-results"></a>Revise os resultados
Você verá o segundo arquivo na pasta `incchgtracking` do contêiner `adftutorial`. 

![Arquivo de saída da cópia incremental](media\tutorial-incremental-copy-change-tracking-feature-portal\incremental-copy-output-file.png)

O arquivo deve ter apenas os dados delta do Banco de Dados SQL do Azure. O registro com `U` é a linha atualizada no banco de dados, e `I` é aquele adicionado à linha. 

```
1,update,10,2,U
6,new,50,1,I
```
As três primeiras colunas são dados alterados do data_source_table. As duas últimas colunas são os metadados da tabela do sistema de controle de alterações. A quarta coluna é SYS_CHANGE_VERSION de cada linha alterada. A quinta coluna é a operação: U = atualização, I = inserir.  Para obter detalhes sobre as informações de controle de alterações, consulte [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql). 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a>Próximas etapas
Avance para o tutorial a seguir para saber mais sobre como transformar dados usando um cluster Spark no Azure:

> [!div class="nextstepaction"]
>[Transformar dados usando o cluster Spark na nuvem](tutorial-transform-data-spark-portal.md)



