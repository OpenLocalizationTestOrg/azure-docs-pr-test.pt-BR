---
title: "aaaGetting iniciado com a sincronização de dados SQL do Azure (visualização) | Microsoft Docs"
description: "Esse tutorial ajudará você a começar a Sincronização de Dados SQL do Azure (Versão prévia)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Introdução à Sincronização de Dados SQL do Azure (visualização)
Neste tutorial, você aprenderá como tooset a sincronização de dados do SQL Azure, criando um grupo de sincronização híbrido que contém instâncias de banco de dados do SQL Azure e SQL Server. novo grupo de sincronização Hello está totalmente configurado e sincroniza no agendamento Olá definido.

Este tutorial presume que você tem pelo menos alguma experiência anterior com o Banco de Dados SQL e o SQL Server. 

Para obter uma visão geral da Sincronização de Dados SQL, confira [Sincronizar dados](sql-database-sync-data.md).

Para obter exemplos completos do PowerShell que mostram como tooconfigure sincronização de dados SQL, consulte Olá artigos a seguir:
-   [Use o PowerShell toosync entre vários bancos de dados do SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Use o PowerShell toosync entre um banco de dados do SQL Azure e um banco de dados do SQL Server local](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Olá completo conjunto de documentação técnica para sincronização de dados do SQL Azure, localizadas anteriormente no MSDN, está disponível como um. Documento PDF. Baixe [aqui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Etapa 1: Criar grupo de sincronização

### <a name="locate-hello-data-sync-settings"></a>Localize as configurações de sincronização de dados Olá

1.  No seu navegador, navegue toohello portal do Azure.

2.  No portal de hello, localize bancos de dados SQL do seu painel ou no ícone de bancos de dados SQL de saudação na barra de ferramentas de saudação.

    ![Lista de bancos de dados SQL do Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Em Olá **bancos de dados SQL** folha, selecione Olá SQL banco de dados existente que você deseja toouse como Olá banco de dados de hub para sincronização de dados. folha de banco de dados SQL de saudação abre.

4.  Na folha de banco de dados SQL Olá para o banco de dados selecionado hello, selecione **sincronizar bancos de dados tooother**. Abre a folha de sincronização de dados de saudação.

    ![Opção de sincronização de bancos de dados tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Criar um novo grupo de sincronização

1.  Na folha de sincronização de dados hello, selecione **novo grupo de sincronização**. Olá **novo grupo de sincronização** folha é aberta com a etapa 1, **criar grupo de sincronização**, realçado. Olá **criar grupo de sincronização de dados** também abre uma folha.

2.  Em Olá **criar grupo de sincronização de dados** folha, Olá coisas a seguir:

    1.  Em Olá **nome do grupo de sincronização** campo, digite um nome para o novo grupo de sincronização hello.

    2.  Em Olá **banco de dados de metadados de sincronização** , escolha se toocreate um novo banco de dados (recomendado) ou toouse um banco de dados existente.

        > [!NOTE]
        > A Microsoft recomenda que você crie um toouse de banco de dados novo e vazio como Olá banco de dados de metadados de sincronização. A Sincronização de Dados cria tabelas nesse banco de dados e executa uma carga de trabalho frequente. Este banco de dados é automaticamente compartilhado como Olá banco de dados de metadados de sincronização para todos os seus grupos de sincronização na região selecionada da saudação. Não é possível alterar o banco de dados de metadados de sincronização de saudação, seu nome ou seu nível de serviço sem removê-la.

        Se você escolheu **Novo banco de dados**, selecione **Criar novo banco de dados.** Olá **banco de dados SQL** folha é aberta. Em Olá **banco de dados SQL** folha, nome e configurar o novo banco de dados de saudação. Depois, selecione **OK**.

        Se você escolheu **banco de dados existente**, selecione banco de dados de saudação da lista de saudação.

    3.  Em Olá **sincronização automática** seção, primeiro selecione **na** ou **Off**.

        Se você escolheu **na**, em Olá **frequência de sincronização** seção, insira um número e selecione segundos, minutos, horas ou dias.

        ![Especificar frequência de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  Em Olá **resolução de conflitos** seção, selecione "Hub ganha" ou "Wins de membro".

        ![Especificar como os conflitos são resolvidos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Selecione **Okey** e aguarde Olá nova sincronização grupo toobe criados e implantados.

## <a name="step-2---add-sync-members"></a>Etapa 2: Adicionar membros de sincronização

Depois que o novo grupo de sincronização Olá é criado e implantado, a etapa 2, **adicionar membros de sincronização**, está realçado na Olá **novo grupo de sincronização** folha.

Em Olá **banco de dados Hub** seção, insira as credenciais existentes de saudação para o servidor de banco de dados SQL Olá quais Olá banco de dados de hub está localizado. Não insira *novas* credenciais nesta seção.

![Banco de dados hub foi adicionado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Adicionar um Banco de Dados SQL do Azure

Em Olá **banco de dados membro** seção, opcionalmente, adicione um grupo de sincronização do banco de dados do Azure SQL toohello selecionando **adicionar um banco de dados do Azure**. Olá **configurar banco de dados do Azure** folha é aberta.

Em Olá **configurar banco de dados do Azure** folha, Olá coisas a seguir:

1.  Em Olá **nome de membro de sincronização** campo, forneça um nome para o novo membro de sincronização hello. Esse nome é diferente do nome de saudação do hello próprio banco de dados.

2.  Em Olá **assinatura** Olá de campo, selecione associados a assinatura do Azure para fins de cobrança.

3.  Em Olá **Azure SQL Server** servidor de banco de dados SQL existente Olá campo, selecione.

4.  Em Olá **banco de dados do SQL Azure** Olá campo, selecione SQL banco de dados.

5.  Em Olá **direções de sincronização** , selecione a sincronização bidirecional, toohello Hub, ou de saudação Hub.

    ![Adicionar um novo membro de sincronização do Banco de Dados SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  Em Olá **Username** e **senha** campos, insira as credenciais existentes de saudação para o servidor de banco de dados SQL Olá quais Olá membro banco de dados está localizado. Não insira *novas* credenciais nesta seção.

7.  Selecione **Okey** e aguarde Olá nova sincronização membro toobe criados e implantados.

    ![Novo membro de sincronização do banco de dados SQL foi adicionado](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Adicionar um Banco de dados do SQL Server local

Em Olá **banco de dados membro** seção, opcionalmente, adicione um grupo de sincronização no local do SQL Server toohello selecionando **adicionar um banco de dados local**. Olá **configurar local** folha é aberta.

Em Olá **configurar local** folha, Olá coisas a seguir:

1.  Selecione **Olá escolher Gateway de agente de sincronização**. Olá **selecione o agente de sincronização** folha é aberta.

    ![Escolher gateway de agente de sincronização Olá](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Em Olá **Olá escolher Gateway de agente de sincronização** folha, escolha se toouse um agente existente ou criar um novo agente.

    Se você escolheu **existente agentes**, selecione Olá agente existente na lista de saudação.

    Se você escolheu **criar um novo agente**, Olá coisas a seguir:

    1.  Baixar o software de agente de sincronização de cliente Olá Olá link fornecido e instalá-lo no computador de saudação onde saudação do SQL Server está localizada.
 
        > [!IMPORTANT]
        > Você tem tooopen saída a porta TCP 1433 no agente de cliente de saudação do hello firewall toolet se comunicar com o servidor de saudação.


    2.  Insira um nome para o agente de saudação.

    3.  Selecione **Criar e Gerar Chave**.

    4.  Copiar Olá agente chave toohello área de transferência.
        
        ![Criando um novo agente de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Selecione **Okey** tooclose Olá **selecione o agente de sincronização** folha.

    6.  No computador do SQL Server hello, localize e execute o aplicativo do agente cliente de sincronização de saudação.

        ![aplicativo do agente cliente de sincronização de dados do Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  No aplicativo de agente de sincronização hello, selecione **Enviar chave do agente**. Olá **configuração de banco de dados de metadados de sincronização** caixa de diálogo é aberta.

    8.  Em Olá **configuração de banco de dados de metadados de sincronização** caixa de diálogo Colar na chave de agente Olá copiado da saudação portal do Azure. Também fornece credenciais de saudação existentes para o servidor de banco de dados do Azure SQL Olá quais Olá metadados de banco de dados está localizado. (Se você criou um novo banco de dados de metadados, esse banco de dados está em Olá mesmo servidor como banco de dados de hub hello.) Selecione **Okey** e aguarde Olá toofinish de configuração.

        ![Insira as credenciais de chave e o servidor de agente Olá](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Se você receber um erro de firewall neste ponto, você tem toocreate uma regra de firewall no tráfego de entrada do Azure tooallow do computador do SQL Server hello. Você pode criar a regra de saudação manualmente no portal de hello, mas talvez você ache mais fácil toocreate-lo no SQL Server Management Studio (SSMS). No SSMS, tente o banco de dados de hub toohello de tooconnect no Azure. Digite o nome como \<hub_database_name\>.database.windows.net. Siga as etapas de saudação na regra de firewall no Azure Olá do tooconfigure de caixa de diálogo hello. Em seguida, retorne toohello aplicativo de agente cliente de sincronização.

    9.  No aplicativo do agente cliente de sincronização de saudação, clique em **registrar** tooregister um banco de dados do SQL Server com o agente de saudação. Olá **configuração do SQL Server** caixa de diálogo é aberta.

        ![Adicionar e configurar um banco de dados do SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. Em Olá **configuração do SQL Server** caixa de diálogo caixa, escolha se tooconnect usando a autenticação do SQL Server ou autenticação do Windows. Se você escolher a autenticação do SQL Server, insira as credenciais existentes de saudação. Fornece saudação do SQL Server e nome de saudação do banco de dados de saudação que você deseja toosync. Selecione **Testar conexão** tootest suas configurações. Em seguida, selecione **Salvar**. banco de dados registrado Olá aparece na lista de saudação.

        ![O banco de dados do SQL Server agora está registrado](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Agora você pode fechar o aplicativo do agente cliente de sincronização de saudação.

    12. No portal Olá Olá **configurar local** folha, selecione **selecione Olá banco de dados.** Olá **Selecionar banco de dados** folha é aberta.

    13. Em Olá **Selecionar banco de dados** folha em Olá **nome de membro de sincronização** campo, forneça um nome para o novo membro de sincronização hello. Esse nome é diferente do nome de saudação do hello próprio banco de dados. Selecione o banco de dados de saudação da lista de saudação. Em Olá **direções de sincronização** , selecione a sincronização bidirecional, toohello Hub, ou de saudação Hub.

        ![Selecione Olá no banco de dados local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Selecione **Okey** tooclose Olá **Selecionar banco de dados** folha. Em seguida, selecione **Okey** tooclose Olá **configurar local** folha e aguardar Olá sincronizar novo membro toobe criados e implantados. Por fim, clique em **Okey** tooclose Olá **selecionar membros de sincronização** folha.

        ![No banco de dados local adicionado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL a sincronização de dados e o agente local do hello, adicionar a função de toohello de nome de usuário `DataSync_Executor`. Sincronização de dados cria essa função na instância do SQL Server hello.

## <a name="step-3---configure-sync-group"></a>Etapa 3: Configurar grupo de sincronização

Depois que os novos membros do grupo de sincronização Olá são criados e implantados, etapa 3, **Configurar grupo de sincronização**, está realçado na Olá **novo grupo de sincronização** folha.

1.  Em Olá **tabelas** folha, selecione um banco de dados de lista de saudação de sincronização de membros do grupo e, em seguida, selecione **atualizar esquema**.

2.  Na lista de saudação de tabelas disponíveis, selecione tabelas Olá que você deseja toosync.

    ![Selecione as tabelas toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Por padrão, todas as colunas na tabela de saudação são selecionadas. Se você não quiser toosync todas as colunas de hello, desabilite Olá a caixa de seleção para as colunas de saudação que você não deseja toosync. Certifique-se de coluna de chave primária de saudação tooleave selecionada.

    ![Selecionar campos toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Por fim, selecione **Salvar**.

## <a name="next-steps"></a>Próximas etapas
Parabéns. Você criou um grupo de sincronização que inclui uma instância do Banco de Dados SQL e um banco de dados do SQL Server.

Para obter mais informações sobre o Banco de Dados SQL e a Sincronização de Dados SQL, consulte:

-   [Baixar a documentação técnica do hello concluída a sincronização de dados SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Baixar a documentação da API de REST de sincronização de dados de SQL Olá](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Visão geral do Banco de Dados SQL](sql-database-technical-overview.md)
-   [Gerenciamento de ciclo de vida do banco de dados](https://msdn.microsoft.com/library/jj907294.aspx)
