---
title: dados aaaMove - Data Management Gateway | Microsoft Docs
description: Configurar um gateway toomove de dados entre locais e hello nuvem. Use o Gateway de gerenciamento de dados no Azure Data Factory toomove seus dados.
keywords: "gateway de dados, integração de dados, mover dados, credenciais de gateway"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Mover dados entre fontes locais e na nuvem de saudação com Gateway de gerenciamento de dados
Este artigo fornece uma visão geral da integração de dados entre os armazenamentos de dados locais e os armazenamentos de dados na nuvem usando o Data Factory. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo e outros artigos de conceitos principais data factory: [conjuntos de dados](data-factory-create-datasets.md) e [pipelines](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Gateway de gerenciamento de dados
Você deve instalar o Gateway de gerenciamento de dados em seu tooenable de máquina local a movimentação de dados para/de um repositório de dados local. gateway de saudação pode ser instalado no mesmo computador como armazenamento de dados hello, ou em um computador diferente como gateway Olá pode se conectar o armazenamento de dados toohello de saudação.

> [!IMPORTANT]
> Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados. 

Olá seguir instruções passo a passo mostra como uma fábrica de dados com um pipeline que move dados de um local de toocreate **do SQL Server** tooan armazenamento de BLOBs do Azure do banco de dados. Como parte da saudação passo a passo, você instale e configure Olá Data Management Gateway em seu computador.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Passo a passo: copiar toocloud de dados local
Neste passo a passo, você Olá seguintes etapas: 

1. Criar uma fábrica de dados.
2. Criar um Gateway de Gerenciamento de Dados. 
3. Criar serviços vinculados para armazenamentos de dados de origem e de coletor.
4. Criar conjuntos de dados toorepresent entrada e saída de dados.
5. Crie um pipeline com um copiar atividade toomove Olá dados.

## <a name="prerequisites-for-hello-tutorial"></a>Pré-requisitos para o tutorial Olá
Antes de começar este passo a passo, você deve ter Olá pré-requisitos a seguir:

* **Assinatura do Azure**.  Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Consulte Olá [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) artigo para obter detalhes.
* **Conta de Armazenamento do Azure**. Use o armazenamento de blob hello como um **destino/coletor** repositório de dados neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.
* **SQL Server**. Neste tutorial, você utiliza um Banco de Dados do SQL Server local como um armazenamento de dados de **origem**. 

## <a name="create-data-factory"></a>Criar um data factory
Nesta etapa, você usa Olá toocreate portal do Azure que uma instância do Azure Data Factory chamado **ADFTutorialOnPremDF**.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+ NOVO**, clique em **Inteligência + análise** e clique em **Data Factory**.

   ![Novo -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. Em Olá **nova fábrica de dados** insira **ADFTutorialOnPremDF** para Olá nome.

    ![Adicionar tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: **"ADFTutorialOnPremDF" nome da fábrica de dados não está disponível**, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFTutorialOnPremDF) e tente criar novamente. Use esse nome em vez de ADFTutorialOnPremDF ao executar as etapas restantes neste tutorial.
   >
   > nome de Olá Olá da fábrica de dados pode ser registrado como um **DNS** nome no futuro hello e, portanto, se tornarão visíveis publicamente.
   >
   >
4. Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.
5. Selecione um **grupo de recursos** existente ou crie um grupo de recursos. Tutorial de hello, crie um grupo de recursos chamado: **ADFTutorialResourceGroup**.
6. Clique em **criar** em Olá **nova fábrica de dados** página.

   > [!IMPORTANT]
   > toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.
   >
   >
7. Após a conclusão da criação, você ver Olá **Data Factory** página conforme mostrado no Olá a imagem a seguir:

   ![Página inicial do Data Factory](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Criar gateway
1. Em Olá **Data Factory** , clique em **autor e implantar** bloco toolaunch Olá **Editor** Olá fábrica de dados.

    ![Bloco Criar e implantar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. No hello Editor da fábrica de dados, clique em **... Mais** Olá barra de ferramentas e, em seguida, clique em **novo gateway de dados**. Como alternativa, clique **Gateways de dados** no Olá a exibição de árvore e clique em **novo gateway de dados**.

   ![Novo gateway de dados na barra de ferramentas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. Em Olá **criar** insira **adftutorialgateway** para Olá **nome**e clique em **Okey**.     

    ![Página Criar Gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > Neste passo a passo, você pode criar gateway lógico Olá com apenas um nó (máquina do Windows local). Você pode expandir um gateway de gerenciamento de dados por meio da associação várias máquinas locais com o gateway de saudação. Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó. Esse recurso também está disponível para um gateway lógico com um único nó. Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.  
4. Em Olá **configurar** , clique em **instalar diretamente no computador**. Essa ação baixa o pacote de instalação de saudação para gateway hello, instala, configura e registra o gateway Olá no computador de saudação.  

   > [!NOTE]
   > Use o Internet Explorer ou um navegador da Web compatível com o Microsoft ClickOnce.
   >
   > Se você estiver usando o Chrome, vá toohello [repositório na web do Chrome](https://chrome.google.com/webstore/), pesquisar "ClickOnce" palavra-chave with, escolha uma das extensões de ClickOnce hello e instalá-lo.
   >
   > Olá mesmo para o Firefox (instalação do suplemento). Clique em **Abrir Menu** botão na barra de ferramentas da saudação (**três linhas horizontais** no canto superior direito de saudação), clique em **complementos**, pesquisar "ClickOnce" palavra-chave with, escolha uma saudação Extensões de ClickOnce e instalá-lo.    
   >
   >

    ![Página Gateway – Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    Dessa maneira é mais fácil toodownload de forma (um clique) hello, instalar, configurar e registrar o gateway de saudação em uma única etapa. Você pode ver Olá **Gerenciador de configuração do Gateway de gerenciamento de dados Microsoft** aplicativo está instalado no seu computador. Você também pode encontrar hello executável **ConfigManager.exe** na pasta Olá: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.

    Você também pode baixar e instalar o gateway manualmente usando os links de saudação nesta página e registrá-lo usando a chave Olá mostrado no hello **nova chave** caixa de texto.

    Consulte [Data Management Gateway](data-factory-data-management-gateway.md) para todos Olá detalhes sobre o gateway de saudação do artigo.

   > [!NOTE]
   > Você deve ser um administrador no hello tooinstall de computador local e configurar Olá Data Management Gateway com êxito. Você pode adicionar usuários adicionais toohello **usuários do Gateway de gerenciamento de dados** grupo local do Windows. membros desse grupo Olá podem usar o gateway de saudação do hello Gerenciador de configuração de Gateway de gerenciamento de dados ferramenta tooconfigure.
   >
   >
5. Aguarde alguns minutos ou aguarde até que você veja Olá mensagem de notificação a seguir:

    ![Instalação do gateway bem-sucedida](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Inicie o aplicativo **Gerenciador de Configuração de Gateway de gerenciamento de dados** no computador. Em Olá **pesquisa** , digite **Data Management Gateway** tooaccess este utilitário. Você também pode encontrar hello executável **ConfigManager.exe** na pasta Olá: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

    ![Gerenciador de configuração de gateway](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Confirme que você vê a mensagem `adftutorialgateway is connected toohello cloud service`. Olá Olá inferior exibe da barra de status **conectado serviço de nuvem toohello** juntamente com um **marca de seleção verde**.

    Em Olá **início** guia, você também pode fazer Olá seguintes operações:

   * **Registrar** um gateway com uma chave de saudação portal do Azure usando o botão de registrar hello.
   * **Parar** Olá dados serviço Gateway de gerenciamento Host em execução no seu computador do gateway.
   * **Agendar atualizações** toobe instalado em uma hora específica do dia de saudação.
   * Exibir quando o gateway Olá foi **atualizado pela última vez**.
   * Especifique a hora em que um gateway de toohello de atualização pode ser instalado.
8. Alternar toohello **configurações** certificado de saudação do guia especificado no hello **certificado** seção é usada tooencrypt/descriptografar credenciais para armazenamento de dados do hello local que você especificar no portal de saudação. (opcional) Clique em **alteração** toouse seu próprio certificado em vez disso. Por padrão, o gateway Olá usa Olá certificado é gerado automaticamente pelo Olá serviço da fábrica de dados.

    ![Configuração do certificado do gateway](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    Você também pode fazer Olá seguintes ações no hello **configurações** guia:

   * Exibir ou exportar certificado hello está sendo usado pelo gateway de saudação.
   * Alterar o ponto de extremidade HTTPS de saudação usado pelo gateway hello.    
   * Defina um toobe de proxy HTTP usado pelo gateway hello.     
9. (opcional) Alternar toohello **diagnóstico** guia, verifique Olá **Habilitar log detalhado** opção se você quiser tooenable detalhado de log que você pode usar tootroubleshoot quaisquer problemas com o gateway de saudação. Olá informações de log podem ser encontradas em **Visualizador de eventos** em **Applications and Services Logs** -> **Data Management Gateway** nó.

    ![Guia Diagnósticos](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Você também pode executar Olá seguintes ações no hello **diagnóstico** guia:

   * Use **Conexão de teste** fonte de dados seção tooan local usando Olá gateway.
   * Clique em **Exibir Logs** toosee Olá Gateway de gerenciamento de dados de log em uma janela do Visualizador de eventos.
   * Clique em **enviar Logs de** tooupload um arquivo zip com logs dos últimos sete dias tooMicrosoft toofacilitate de solução de problemas de seus problemas.
10. Em Olá **diagnóstico** guia Olá **Conexão de teste** seção, selecione **SqlServer** para o tipo de saudação de dados Olá armazenar, insira o nome de saudação do servidor de banco de dados Olá, nome do Olá banco de dados, especifique o tipo de autenticação, digite o nome de usuário e senha e clique em **teste** tootest se gateway Olá pode se conectar a banco de dados toohello.
11. Navegador do toohello de comutador e em Olá **portal do Azure**, clique em **Okey** em Olá **configurar** página e, em seguida, em Olá **novo gateway de dados** página.
12. Você deve ver **adftutorialgateway** em **Gateways de dados** na exibição de árvore Olá Olá esquerda.  Se você clicar nele, você verá Olá associados JSON.

## <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você cria dois serviços vinculados: **AzureStorageLinkedService** e **SqlServerLinkedService**. Olá **SqlServerLinkedService** vincula um banco de dados do SQL Server local e hello **AzureStorageLinkedService** serviço vinculado vincula uma fábrica de dados de toohello de armazenamento de BLOBs do Azure. Você pode criar um pipeline posteriormente neste passo a passo que copia dados de armazenamento de BLOBs do Azure de toohello Olá local do SQL Server banco de dados.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Adicionar um banco de dados do serviço vinculado tooan local do SQL Server
1. Em Olá **Editor da fábrica de dados**, clique em **novo repositório de dados** na barra de ferramentas hello e selecione **do SQL Server**.

   ![Serviço vinculado do SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. Em Olá **editor de JSON** em Olá direita, Olá seguintes etapas:

   1. Para Olá **gatewayName**, especifique **adftutorialgateway**.    
   2. Em Olá **connectionString**, Olá seguintes etapas:    

      1. Para **servername**, digite nome de saudação do servidor de saudação que hospeda o banco de dados do SQL Server hello.
      2. Para **databasename**, insira o nome de saudação do banco de dados de saudação.
      3. Clique em **Encrypt** botão na barra de ferramentas de saudação. Consulte o aplicativo do Gerenciador de credenciais hello.

         ![Aplicativo do Gerenciador de credenciais](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. Em Olá **definindo credenciais** caixa de diálogo, especifique o tipo de autenticação, nome de usuário e senha e clique em **Okey**. Se a conexão de saudação for bem-sucedida, credenciais Olá criptografado são armazenadas em Olá JSON e Olá caixa de diálogo é fechada.
      5. Fechar Guia do navegador vazia Olá que iniciou a caixa de diálogo Olá se não for fechada automaticamente e voltar à guia toohello com hello portal do Azure.

         No computador do gateway hello, essas credenciais são **criptografado** usando um certificado que Olá fábrica de dados de serviço possui. Se você quiser toouse Olá certificado associado com hello Gateway de gerenciamento de dados em vez disso, consulte [definir credenciais com segurança](#set-credentials-and-security).    
   3. Clique em **implantar** no comando Olá barra toodeploy Olá serviço vinculado do SQL Server. Você deve ver o serviço Olá vinculado na exibição de árvore de saudação.

      ![Serviço vinculado do SQL Server no modo de exibição de árvore de saudação](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Adicionar um serviço vinculado para uma conta de armazenamento do Azure
1. Em Olá **Editor da fábrica de dados**, clique em **novo repositório de dados** Olá barra de comandos e clique em **armazenamento do Azure**.
2. Inserir nome de saudação da sua conta de armazenamento do Azure para Olá **nome da conta**.
3. Insira a chave de saudação para sua conta de armazenamento do Azure para Olá **chave de conta**.
4. Clique em **implantar** toodeploy Olá **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você pode criar entrada e saída de conjuntos de dados que representam dados de entrada e saídos para a operação de cópia de saudação (banco de dados do SQL Server no local = > armazenamento de BLOBs do Azure). Antes de criar conjuntos de dados, Olá etapas (etapas detalhadas segue lista Olá):

* Criar uma tabela chamada **emp** em Olá banco de dados do servidor SQL é adicionado como uma fábrica de dados do serviço vinculado toohello e inserir alguns exemplos de entradas na tabela de saudação.
* Criar um contêiner de blob denominado **adftutorial** em hello Azure adicionada como uma fábrica de dados do serviço vinculado toohello de conta de armazenamento de blob.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Preparar SQL Server no local para o tutorial Olá
1. No banco de dados de saudação especificada para saudação do SQL Server local de serviço vinculado (**SqlServerLinkedService**), use Olá Olá de toocreate de script SQL a seguir **emp** tabela no banco de dados de saudação.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Insira algum exemplo na tabela de saudação:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada

1. Em Olá **Editor da fábrica de dados**, clique em **... Mais**, clique em **novo conjunto de dados** Olá barra de comandos e clique em **tabela do SQL Server**.
2. Substitua Olá JSON no painel direito Olá Olá texto a seguir:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Observe Olá pontos a seguir:

   * **tipo** está definido muito**SqlServerTable**.
   * **tableName** está definido muito**emp**.
   * **linkedServiceName** está definido muito**SqlServerLinkedService** (você tinha criou esse serviço vinculado anteriormente neste passo a passo.).
   * Para um conjunto de dados entrado que não é gerado por outro pipeline na fábrica de dados do Azure, você deve definir **externo** muito**true**. Ele indica que os dados de entrada hello estão toohello externo produzido serviço do Azure Data Factory. Você pode opcionalmente especificar quaisquer políticas de dados externa usando Olá **externalData** elemento Olá **política** seção.    

   Confira [Mover dados para/de SQL Server](data-factory-sqlserver-connector.md) para obter detalhes sobre as propriedades JSON.
3. Clique em **implantar** no comando Olá barra toodeploy Olá dataset.  

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída

1. Em Olá **Editor da fábrica de dados**, clique em **novo conjunto de dados** Olá barra de comandos e clique em **armazenamento de BLOBs do Azure**.
2. Substitua Olá JSON no painel direito Olá Olá texto a seguir:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Observe Olá pontos a seguir:

   * **tipo** está definido muito**AzureBlob**.
   * **linkedServiceName** está definido muito**AzureStorageLinkedService** (você tivesse criado esse serviço vinculado na etapa 2).
   * **folderPath** está definido muito**adftutorial/outfromonpremdf** onde outfromonpremdf é pasta Olá no contêiner de adftutorial hello. Criar hello **adftutorial** contêiner se ele ainda não existir.
   * Olá **disponibilidade** está definido muito**por hora** (**frequência** definido muito**hora** e **intervalo** definido muito **1**).  Olá serviço da fábrica de dados gera uma fatia de dados de saída a cada hora Olá **emp** tabela hello Azure SQL Database.

   Se você não especificar um **fileName** para um **tabela de saída**, arquivos Olá Olá gerado **folderPath** são nomeados em Olá formato a seguir: dados.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** e **fileName** dinamicamente com base nas Olá **SliceStart** de tempo, use a propriedade de partitionedBy hello. No hello exemplo a seguir, folderPath usa o ano, mês e dia de saudação SliceStart (hora de início da fatia Olá processada) e fileName usa a hora de SliceStart de saudação. Por exemplo, se uma fatia está sendo produzida para 2014-10-20T08:00:00, Olá folderName é definido toowikidatagateway/wikisampledataout/2014/10/20 e nome de arquivo hello é definido too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Confira [Mover dados para/de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md) para obter detalhes sobre as propriedades JSON.
3. Clique em **implantar** no comando Olá barra toodeploy Olá dataset. Confirme se os dois conjuntos de dados Olá na exibição de árvore de saudação.  

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você criará um **pipeline** com uma **Atividade de Cópia** que usa **EmpOnPremSQLTable** como entrada e **OutputBlobTable** como saída.

1. No Editor de Data Factory, clique em **... Mais** e clique em **Novo pipeline**.
2. Substitua Olá JSON no painel direito Olá Olá texto a seguir:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte.
   >
   >

   Observe Olá pontos a seguir:

   * Na seção de atividades hello, há apenas atividades cujo **tipo** está definido muito**cópia**.
   * **Entrada** para atividade de saudação é definida muito**EmpOnPremSQLTable** e **saída** para atividade de saudação é definida muito**OutputBlobTable**.
   * Em Olá **typeProperties** seção, **SqlSource** é especificado como Olá **tipo de fonte** e * * BlobSink * * é especificado como Olá **dotipodecoletor**.
   * Consulta SQL `select * from emp` é especificado para Olá **sqlReaderQuery** propriedade **SqlSource**.

   Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41Z. Olá **final** tempo é opcional, mas usamos neste tutorial.

   Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**". pipeline de saudação toorun indefinidamente, especifique **9/9/9999** como valor Olá Olá **final** propriedade.

   Você está definindo tempo de duração na qual Olá fatias de dados são processadas com base em Olá Olá **disponibilidade** propriedades que foram definidas para cada conjunto de dados do Azure Data Factory.

   No exemplo hello, há 24 fatias de dados como cada fatia de dados é produzida por hora.        
3. Clique em **implantar** no comando Olá barra toodeploy Olá dataset (tabela é um conjunto de dados retangular). Confirmar esse pipeline Olá aparece na exibição de árvore de saudação em **Pipelines** nó.  
4. Agora, clique em **X** duas vezes tooclose Olá página tooget back toohello **Data Factory** página Olá **ADFTutorialOnPremDF**.

**Parabéns!** Você criou com êxito uma fábrica de dados do Azure, serviços vinculados, conjuntos de dados e um pipeline e pipeline de saudação agendado.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Fábrica de dados de saudação de exibição em uma exibição de diagrama
1. Em Olá **portal do Azure**, clique em **diagrama** lado a lado na página inicial Olá Olá **ADFTutorialOnPremDF** fábrica de dados. :

    ![Link do diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Você deve ver toohello semelhante do diagrama Olá imagem a seguir:

    ![Exibição de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Você pode ampliar, zoom, zoom too100%, toofit de zoom, automaticamente pipelines de posição e conjuntos de dados e mostrar informações de linhagem (realça os itens de upstream e downstream dos itens selecionados).  Clique duas vezes em Propriedades de toosee um objeto (ou pipeline de conjunto de dados de entrada/saída) para ele.

## <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você deve usar Olá toomonitor de portal do Azure que está acontecendo em uma fábrica de dados do Azure. Você também pode usar pipelines e conjuntos de dados de toomonitor de cmdlets do PowerShell. Para obter detalhes sobre monitoramento, consulte [Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md).

1. No diagrama de saudação, clique duas vezes em **EmpOnPremSQLTable**.  

    ![Fatias de EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Observe que todos os dados de saudação fatias de backup estão em **pronto** estado porque duração de pipeline hello (hora de tooend de tempo de início) está em Olá anterior. Também é porque você inseriu dados saudação no banco de dados do SQL Server hello e haja todo o tempo de saudação. Confirme que nenhuma fatia aparecerão em Olá **fatias problema** seção na parte inferior da saudação. tooview todas as fatias hello, clique **consulte mais** final Olá Olá lista das fatias.
3. Agora, em Olá **conjuntos de dados** , clique em **OutputBlobTable**.

    ![Fatias de OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Clique em qualquer fatia de dados da lista de saudação e você deverá ver Olá **fatia de dados** página. Você verá a atividade for executada por fatia hello. Você normalmente vê apenas uma atividade sendo executada.  

    ![Folha Fatia de dados](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Se fatia Olá não está em Olá **pronto** estado, você pode ver fatias de upstream Olá que não estão prontos e estão bloqueando a fatia atual Olá executadas em Olá **fatias de Upstream que não estão prontas** lista.
5. Clique em Olá **execução da atividade** de lista Olá Olá inferior toosee **detalhes da execução de atividade**.

   ![Página Detalhes da Execução da Atividade](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Você verá informações como taxa de transferência, a duração e o gateway Olá usados dados de saudação tootransfer.
6. Clique em **X** tooclose todos Olá páginas até que você
7. Voltar home page do toohello Olá **ADFTutorialOnPremDF**.
8. (opcional) Clique em **Pipelines**, clique em **ADFTutorialOnPremDF** e execute uma consulta drill-through nas tabelas de entrada (**Consumed**) ou nos conjuntos de dados de saída (**Produced**).
9. Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) tooverify que um blob/arquivo é criado para cada hora.

   ![Gerenciador de Armazenamento do Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Próximas etapas
* Consulte [Data Management Gateway](data-factory-data-management-gateway.md) artigo para todos os Olá detalhes sobre Olá Gateway de gerenciamento de dados.
* Consulte [copiar dados de Blob do Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn sobre como repositório de dados do coletor tooa do repositório de dados de toomove de atividade de cópia toouse de uma fonte de dados.
