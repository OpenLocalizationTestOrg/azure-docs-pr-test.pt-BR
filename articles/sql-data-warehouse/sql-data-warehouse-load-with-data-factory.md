---
title: "dados de aaaLoad no Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: "Este tutorial carrega dados no Azure SQL Data Warehouse com o uso do Azure Data Factory e usa um banco de dados do SQL Server como fonte de dados de saudação."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Carregar dados no SQL Data Warehouse com o Data Factory

Você pode usar dados do Azure Data Factory tooload no Azure SQL Data Warehouse de qualquer Olá [suporte para armazenamentos de dados de origem](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Por exemplo, é possível carregar dados de um Banco de Dados SQL do Azure ou um Banco de Dados Oracle em um SQL Data Warehouse usando o Data Factory. Tutorial neste artigo mostra como tooload dados do servidor SQL local banco de dados em um data warehouse do SQL.

**Tempo estimado**: neste tutorial leva cerca de toocomplete de 10 a 15 minutos depois de saudação pré-requisitos foram atendidos.

## <a name="prerequisites"></a>Pré-requisitos

- É necessário um **banco de dados do SQL Server** com tabelas que contêm dados saudação toobe copiou toohello do SQL data warehouse.  

- Você precisa de um **SQL Data Warehouse** online. Se você ainda não tiver um data warehouse, saiba como muito[criar um Data Warehouse do Azure SQL](sql-data-warehouse-get-started-provision.md).

- Você precisa de uma **Conta de Armazenamento do Azure**. Se você não tiver uma conta de armazenamento, saiba como muito[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md). Para melhor desempenho, localize a conta de armazenamento hello e saudação do data warehouse em hello mesma região do Azure.

## <a name="configure-a-data-factory"></a>Configurar uma fábrica de dados
1. Faça logon no toohello [portal do Azure][].
2. Localize o data warehouse e clique em tooopen-lo.
3. Na folha principal de saudação, clique em **carregar dados** > **do Azure Data Factory**.

    ![Iniciar o assistente para Carregar Dados](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Se você não tem uma fábrica de dados em sua assinatura do Azure, você verá um **nova fábrica de dados** caixa de diálogo em uma guia separada do navegador de saudação. Preencha Olá informações solicitadas e clique em **criar**. Após Olá fábrica de dados é criada, Olá **nova fábrica de dados** caixa de diálogo é fechada, e você vê Olá **selecionar Data Factory** caixa de diálogo.

    Se você tiver um ou mais fábricas de dados já está em Olá assinatura do Azure, você verá Olá **selecionar Data Factory** caixa de diálogo. Na caixa de diálogo, você pode selecionar uma fábrica de dados existente ou clique em **criar nova fábrica de dados** toocreate um novo.

    ![Configurar o Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. Em Olá **selecionar Data Factory** caixa de diálogo, Olá **carregar dados** opção é selecionada por padrão. Clique em **próximo** toostart criando um tarefa de carregamento de dados.

## <a name="configure-hello-data-factory-properties"></a>Configurar propriedades de fábrica de dados Olá
Agora que você criou uma fábrica de dados, Olá próxima etapa é agenda de carregamento de dados de saudação de tooconfigure.

1. Em **Nome da tarefa**, digite **DWLoadData-fromSQLServer**.
2. Usar saudação padrão **executar uma vez agora** opção, clique em **próximo**.

    ![Configurar o agendamento de carregamento](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Configurar armazenamento de dados de origem hello e gateway
Agora você informar a fábrica de dados sobre Olá local do SQL Server banco de dados do qual você deseja que os dados tooload.

1. Escolha **do SQL Server** dos dados de origem Olá suporte para armazenar o catálogo e clique em **próximo**.

    ![Escolher a fonte do SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. Um **banco de dados de SQL Server local especificar Olá** caixa de diálogo é exibida. Olá primeiro **nome de Conexão** campo é automaticamente preenchido. segundo campo de saudação solicita nome de saudação do hello **Gateway**. Se você estiver usando uma fábrica de dados existente que já tem um gateway, você pode reutilizar o gateway Olá selecionando-o na lista suspensa de saudação. Clique em Olá **criar Gateway** link toocreate um Gateway de gerenciamento de dados.  

    > [!NOTE]
    > Se o repositório de dados de origem de saudação é local ou em uma máquina virtual IaaS do Azure, é necessário um Gateway de gerenciamento de dados. Um gateway tem uma relação de 1-1 com uma fábrica de dados. Ele não pode ser usado em outro fábrica de dados, mas ele pode ser usado por vários dados carregando tarefas com hello mesma fábrica de dados. Um gateway pode ser usado tooconnect toomultiple os armazenamentos de dados ao executar tarefas de carregamento de dados.
    >
    > Para obter informações detalhadas sobre o gateway hello, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artigo.

3. Uma caixa de diálogo **Criar Gateway** será exibida. Em Nome, insira **GatewayForDWLoading** e clique em **Criar**.

4. Uma caixa de diálogo **Configurar Gateway** será exibida. Clique em **iniciar a instalação do express no computador** tooautomatically download, instalar e registrar o Gateway de gerenciamento de dados no computador atual. Olá progresso é mostrado em uma janela pop-up. Se a máquina de saudação não pode se conectar a toohello repositório de dados, você pode manualmente [baixar e instalar gateway Olá](https://www.microsoft.com/download/details.aspx?id=39717) em um computador que possa se conectar a dados toohello armazenar e usar tooregister chave hello.
    > [!NOTE]
    > a configuração expressa Olá nativamente funciona com o Microsoft Edge e Internet Explorer. Se você estiver usando o Google Chrome, primeiro instale extensão do ClickOnce de saudação do repositório do cromo da web.

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Aguarde Olá toocomplete de configuração de gateway. Depois que o gateway de saudação for registrado com êxito e está online, janela pop-up Olá fecha e novo gateway de saudação aparece no campo gateway de saudação. Em seguida, preencha o restante da saudação campos obrigatórios da seguinte maneira, em seguida, clique em **próximo**.
    - **Nome do servidor**: nome de saudação do SQL Server local.
    - **Nome do banco de dados**: banco de dados SQL Server.
    - **Criptografia de credencial**: usar o padrão de hello "pelo navegador da web".
    - **Tipo de autenticação**: escolha o tipo de saudação de autenticação você está usando.
    - **Nome de usuário** e **senha**: insira Olá nome de usuário e senha para um usuário que tem permissão toocopy Olá dados.

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Olá próxima etapa é toochoose tabelas de saudação de quais dados de saudação toocopy. Você pode filtrar tabelas hello usando palavras-chave. E você pode visualizar o esquema de dados e tabela de saudação no painel inferior de saudação. Depois de concluir a seleção, clique em **Avançar**.

    ![Selecionar tabelas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Configurar destino hello, o SQL Data Warehouse

Agora você informar a fábrica de dados sobre informações de destino hello.

1. As informações de conexão do SQL Data Warehouse são preenchidas automaticamente. Digite a senha de Olá Olá nome de usuário. e clique em **Avançar**.

    ![Configurar o destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Um mapeamento de tabela inteligente aparece que mapeia as tabelas de toodestination de origem com base em nomes de tabela. Se a tabela de saudação não existe no destino hello, por padrão ADF criará um com hello mesmo nome (isso se aplica tooSQL servidor ou banco de dados SQL Azure como origem). Você também pode escolher tabela existente de tooan toomap. Examine e clique em **Avançar**.

    ![Mapear tabelas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Examine o mapeamento de esquema Olá e procure por mensagens de erro ou aviso. O mapeamento inteligente é baseado no nome da coluna. Se há uma conversão de tipo de dados sem suporte entre a coluna de origem e destino hello, você verá uma mensagem de erro ao lado da tabela correspondente hello. Se você escolher automática de fábrica de dados toolet criar tabelas hello, conversão de tipo de dados adequado pode acontecer se necessário toofix incompatibilidade de saudação entre repositórios de origem e de destino.

    ![Mapear esquema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Clique em **Avançar**.

## <a name="configure-hello-performance-settings"></a>Definir configurações de desempenho de saudação
Olá configurações de desempenho, você configurar uma conta de armazenamento do Azure usada para teste antes de ele carrega no SQL Data Warehouse performantly usando Olá [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Após copiar hello, dados intermediários saudação no armazenamento serão limpas automaticamente.

Selecione uma conta de armazenamento do Azure existente e clique em **Avançar**.

![Configurar um blob de preparo](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Revisar informações de resumo e implantar o pipeline de saudação

Examine a configuração de saudação e clique em **concluir** pipeline de saudação do botão toodeploy.

![Implantar o data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Monitorar o progresso do carregamento de dados

Você pode ver o progresso da implantação hello e resulta em Olá **implantação** página.

1. Depois de implantação hello, clique o link de saudação que diz **clique aqui pipeline de cópia toomonitor** toomonitor dados progresso do carregamento.

    ![Monitorar o pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Olá recém-criado **DWLoadData fromSQLServer** pipeline de carregamento de dados é automaticamente selecionado do hello esquerdo **Gerenciador de recursos**.

    ![Exibir o pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Clique no pipeline de saudação no meio Olá Olá do painel toosee status detalhado para cada tabela que mapeia tooan atividade.

    ![Exibir a atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Ainda mais, clique em uma atividade e você vê dados Olá Carregando detalhes no painel direito hello, incluindo o tamanho dos dados, linhas, taxa de transferência, etc.

    ![Exibir os detalhes da atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch esse monitoramento exibição posterior, vá tooyour SQL Data Warehouse, clique **carregar dados > Azure Data Factory**, selecione sua fábrica e escolha **monitorar existentes ao carregar tarefas**.

## <a name="next-steps"></a>Próximas etapas

toomigrate tooSQL o banco de dados do Data Warehouse, consulte [visão geral da migração](sql-data-warehouse-overview-migrate.md).

toolearn mais sobre Azure Data Factory e seus recursos de movimentação de dados, consulte Olá artigos a seguir:

- [Introdução tooAzure fábrica de dados](../data-factory/data-factory-introduction.md)
- [Mover dados usando a Atividade de Cópia](../data-factory/data-factory-data-movement-activities.md)
- [Mover tooand de dados de uso do Azure Data Factory do Azure SQL Data Warehouse](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore seus dados no Data Warehouse do SQL, consulte Olá seguintes artigos:

- [Conecte-se tooSQL Data Warehouse com o Visual Studio e SSDT](sql-data-warehouse-query-visual-studio.md)
- [Dados visuais com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[portal do Azure]: https://portal.azure.com
