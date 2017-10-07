---
title: o banco de dados do SQL Server de aaaMigrate tooAzure banco de dados SQL | Microsoft Docs
description: Saiba toomigrate sua tooAzure de banco de dados do SQL Server banco de dados SQL.
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Migrar seu banco de dados de SQL Server tooAzure banco de dados SQL

Movendo o SQL Server tooAzure de banco de dados SQL de banco de dados é um processo de três partes - primeiro preparar, em seguida, exportar e, em seguida, importar o banco de dados de saudação. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Preparar um banco de dados em um SQL Server para migração tooAzure banco de dados SQL usando Olá [Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Exportar arquivo BACPAC de tooa Olá banco de dados
> * Importar arquivo BACPAC de saudação para um banco de dados do SQL Azure

Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

- A versão mais recente instalada saudação do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). Instalar o SSMS também instala a versão mais recente de saudação do SQLPackage, um utilitário de linha de comando que pode ser usado tooautomate uma variedade de tarefas de desenvolvimento de banco de dados. 
- Olá instalado [Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Você identificou e tem acesso tooa banco de dados toomigrate. Este tutorial usa Olá [do SQL Server 2008R2 banco de dados AdventureWorks OLTP](https://msftdbprodsamples.codeplex.com/releases/view/59211) em uma instância do SQL Server 2008R2 ou mais recente, mas você pode usar qualquer banco de dados de sua escolha. problemas de compatibilidade de toofix, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Preparar para a migração

Você está pronto tooprepare para migração. Siga essas Olá de toouse etapas  **[Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess Olá preparação do banco de dados para migração tooAzure banco de dados SQL.

1. Olá abrir **Assistente de migração de dados**. Você pode executar DMA em qualquer computador com conectividade toohello instância contendo Olá dados do SQL Server que você planeja toomigrate, não será necessário tooinstall-lo no computador que hospeda Olá Olá a instância do SQL Server.

     ![abra o assistente de migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. No menu à esquerda do hello, clique em **+ novo** toocreate um **avaliação** projeto. Preencha o formulário de saudação com um **nome do projeto** (todos os outros valores devem ser deixados em seus valores padrão) e clique em **criar**. Olá **opções** página será aberta.

     ![novo projeto do assistente de migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Em Olá **opções** , clique em **próximo**. Olá **selecione fontes** página será aberta.

     ![novas opções de migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Em Olá **selecione fontes** insira Olá nome da instância do SQL Server que contém o servidor Olá planejar toomigrate. Alteração Olá outros valores dessa página, se necessário. Clique em **Conectar**.

     ![nova seleção de fontes da migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. Em Olá **adicionar fontes** parte da saudação **selecione fontes** , marque as caixas de seleção Olá Olá bancos de dados toobe testada quanto à compatibilidade. Clique em **Adicionar**.

     ![nova seleção de fontes da migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Clique em **Iniciar avaliação**.

     ![nova avaliação de início da migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Ao concluir a avaliação hello, primeiro olhar toosee se banco de dados de saudação toomigrate suficientemente compatível. Procure Olá a marca de seleção em um círculo verde.

     ![novos resultados da avaliação de migração de dados compatíveis](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Examine os resultados de saudação. Olá **paridade de recursos do SQL Server** resultados mostrados são saudação padrão resultados tooreview. Especificamente Revise informações Olá sobre recursos parcialmente suportados e sem suporte e informações de saudação fornecida sobre as ações recomendadas. 

     ![nova paridade da avaliação de migração de dados](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Saudação de revisão **problemas de compatibilidade** clicando-se essa opção na parte superior esquerda do hello. Especificamente revisão Olá informações sobre bloqueadores de migração, as alterações de comportamento e recursos para cada nível de compatibilidade preteridos. Banco de dados AdventureWorks2008R2 de hello, revise as alterações de hello a pesquisa de texto tooFull desde o SQL Server 2008 e hello altera tooSERVERPROPERTY('LCID') desde o SQL Server 2000. Para obter detalhes sobre essas alterações, são fornecidos links para obter mais informações. Muitas opções de pesquisa e as configurações de pesquisa de texto completo foram alteradas 

   > [!IMPORTANT] 
   > Depois de migrar seu banco de dados SQL do tooAzure de banco de dados, você pode escolher toooperate Olá banco de dados em seu nível de compatibilidade atual (nível 100 para o banco de dados do hello AdventureWorks2008R2) ou em um nível superior. Para obter mais informações sobre implicações de saudação e opções para a operação de um banco de dados em um nível de compatibilidade específicos, consulte [nível de compatibilidade do banco de dados ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Consulte também [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre configurações de nível de banco de dados adicionais relacionados toocompatibility níveis.
   >

10. Opcionalmente, clique em **Exportar relatório** toosave relatório de saudação como um arquivo JSON.
11. Saudação de fechar o Assistente de migração de dados.

## <a name="export-toobacpac-file"></a>Exportar arquivo tooBACPAC 

Um arquivo BACPAC é um arquivo ZIP com uma extensão de BACPAC que contém os metadados de saudação e dados de um banco de dados do SQL Server. Um arquivo BACPAC pode ser armazenado no armazenamento de BLOBs do Azure ou no armazenamento local para arquivamento ou para a migração - como do SQL Server tooAzure banco de dados SQL. Para toobe uma exportação transacionalmente consistente, você não deve garantir que nenhuma gravação atividade estiver ocorrendo durante a exportação de saudação.

Siga estas etapas toouse Olá SQLPackage utilitário de linha de comando tooexport Olá AdventureWorks2008R2 banco de dados toolocal armazenamento.

1. Abra um prompt de comando do Windows e altere sua pasta de tooa do diretório no qual você tenha Olá **130** versão de SQLPackage, como **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Executar Olá SQLPackage comando no prompt de comando de Olá tooexport Olá a seguir **AdventureWorks2008R2** do banco de dados **localhost** muito**AdventureWorks2008R2.bacpac**. Altere esses valores como ambiente tooyour apropriado.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![exportação de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Após a conclusão da execução de saudação arquivo BACPAC de saudação gerado é armazenado no diretório de Olá onde Olá sqlpackage executável está localizado. Neste exemplo, C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Faça logon no toohello [portal do Azure](https://portal.azure.com/). Registro em log no computador de saudação do qual você estiver executando o utilitário de linha de comando do hello SQLPackage facilita a criação de Olá Olá de regra de firewall na etapa 5.

## <a name="create-a-sql-server-logical-server"></a>Criar um servidor lógico do SQL Server

Um [servidor lógico do SQL Server](sql-database-features.md) atua como um ponto administrativo central para vários bancos de dados. Siga estas etapas toocreate uma saudação do SQL server servidor lógico toocontain migrados banco de dados do Adventure Works OLTP SQL Server. 

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Tipo **do sql server** na janela de pesquisa Olá Olá **novo** página e selecione **banco de dados SQL (servidor lógico)** de saudação lista filtrada.

    ![selecionar servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Em Olá **tudo** , clique em **do SQL server (servidor lógico)** e, em seguida, clique em **criar** em Olá **do SQL Server (servidor lógico)** página .

    ![criar um servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Preencha Olá SQL server (servidor lógico) formulário com hello seguintes informações, conforme mostrado na saudação anterior imagem:     

   | Configuração       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | Digite qualquer nome exclusivo globalmente | Para ver os nomes do servidor válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Logon de administrador do servidor** | Digite qualquer nome válido | Para ver os nomes de logon válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Senha** | Digite qualquer senha válida | Sua senha deve ter pelo menos 8 caracteres e deve conter caracteres de três das Olá categorias a seguir: caracteres em letras maiusculas, letras minúsculas, números e caracteres não alfanuméricos. |
   | **Assinatura** | Selecionar uma assinatura | Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions). |
   | **Grupo de recursos** | Escolha um grupo de recursos existente ou crie um novo grupo, como **myResourceGroup** |  Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Localidade** | Insira qualquer local válido para o novo servidor de saudação | Para obter mais informações sobre as regiões, consulte [Regiões do Azure](https://azure.microsoft.com/regions/). |

   ![criar formulário de servidor lógico concluído](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Clique em **criar** servidor lógico do tooprovision hello. O provisionamento demora alguns minutos. 

> [!IMPORTANT]
> Lembre o nome do servidor, o nome do logon do administrador do servidor e a senha. Você precisa dos seguintes valores mais tarde neste tutorial.
>

## <a name="create-a-server-level-firewall-rule"></a>Criar uma regra de firewall no nível de servidor

Olá serviço de banco de dados SQL cria um [firewall no nível de servidor de saudação](sql-database-firewall-configure.md) que impede que aplicativos externos e ferramentas conectem toohello server ou bancos de dados no servidor de saudação a menos que uma regra de firewall será criada tooopen Olá firewall para endereços IP específicos. Siga essas etapas toocreate uma regra de firewall de nível de servidor de banco de dados SQL para o endereço IP de saudação do computador de saudação do qual você estiver executando o utilitário de linha de comando do hello SQLPackage. Isso permite que o SQLPackage tooconnect toohello SQL serverDatabase servidor lógico através do firewall do banco de dados do Azure SQL hello. 

1. Clique em **todos os recursos** no menu esquerdo hello e clique em seu novo servidor na Olá **todos os recursos** página. página de visão geral de saudação do servidor é aberta e oferece opções de configuração adicional.

     ![visão geral do servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Clique em **Firewall** no menu à esquerda da saudação em **configurações** na página de visão geral de saudação. Olá **configurações de Firewall** página para o servidor de banco de dados SQL Olá é aberta. 

3. Clique em **Adicionar IP do cliente** no endereço IP de Olá Olá barra de ferramentas tooadd do computador Olá você está usando no momento e, em seguida, clique em **salvar**. Uma regra de firewall no nível do servidor é criada para o endereço IP atual.

     ![definir regra de firewall do servidor](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Clique em **OK**.

Agora você pode conectar tooall bancos de dados neste servidor usando o SQL Server Management Studio ou outra ferramenta de sua escolha usando esse endereço IP usando a conta de administrador de servidor de saudação criada anteriormente.

> [!NOTE]
> O Banco de Dados SQL se comunica pela porta 1433. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede. Nesse caso, você não pode conectar o servidor de banco de dados do Azure SQL tooyour, a menos que o departamento de TI abre a porta 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Importar um arquivo BACPAC tooAzure banco de dados SQL 

versões mais recentes de saudação do hello SQLPackage utilitário de linha de comando oferecem suporte à criação de um banco de dados do SQL Azure em determinado [nível de desempenho e da camada de serviço](sql-database-service-tiers.md). Para melhor desempenho durante a importação, selecione um nível de desempenho e da camada de serviço de alta e reduzir, em seguida, após a importação se o nível de desempenho e da camada de serviço Olá é maior do que você precisa imediatamente.

Siga estas etapas use Olá SQLPackage utilitário de linha de comando tooimport Olá AdventureWorks2008R2 banco de dados tooAzure banco de dados SQL. Embora você possa usar o SQL Server Management Studio para essa tarefa, SQLPackage é o método hello preferido para a maioria dos ambientes de produção para obter a máxima flexibilidade e melhor desempenho. Consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Executar Olá SQLPackage comando no prompt de comando de Olá tooimport Olá a seguir **AdventureWorks2008R2** banco de dados do servidor lógico de armazenamento local toohello SQL server que você tooa criado anteriormente novo banco de dados, um serviço camada de **Premium**e um objetivo de serviço de **P6**. Substituir valores hello colchetes angulares com valores apropriados para seu servidor lógico do SQL server e especifique um nome para Olá novo banco de dados (também substituir Olá colchetes). Também é possível toochange valores de saudação para edição de banco de dados e o serviço objectgive como ambiente tooyour apropriado. Para propósito Olá deste tutorial, é chamado de banco de dados migrado Olá **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage import](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Um servidor lógico do SQL Server ouve na porta 1433. Se você estiver tentando tooconnect tooa lógico servidor do SQL server de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo Olá para toosuccessfully você se conectar.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Conectar-se usando o SQL Server Management Studio (SSMS)

Use o SQL Server Management Studio tooestablish um servidor de banco de dados SQL do tooyour de conexão e banco de dados migrado recentemente, chamado **myMigratedDatabase** neste tutorial. Se você estiver executando o SQL Server Management Studio em um computador diferente da qual você executou o SQLPackage, crie uma regra de firewall para este computador usando as etapas de saudação no procedimento anterior hello.

1. Abra o SQL Server Management Studio.

2. Em Olá **conectar tooServer** caixa de diálogo, digite Olá informações a seguir:
   - **Tipo de servidor**: especifique mecanismo de banco de dados
   - **Nome do servidor**: insira seu nome do servidor totalmente qualificado, como **mynewserver20170403.database.windows.net**
   - **Autenticação**: especifique a Autenticação do SQL Server
   - **Logon**: insira a conta do administrador do servidor
   - **Senha**: insira a senha de saudação para sua conta de administrador do servidor
 
    ![conectar com SSMS](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Clique em **Conectar**. Olá Pesquisador janela será aberta. 

4. No Pesquisador de objetos, expanda **bancos de dados** e, em seguida, expanda **myMigratedDatabase** tooview objetos de saudação no banco de dados de exemplo hello.

## <a name="change-database-properties"></a>Alterar as propriedades de banco de dados

Você pode alterar a camada de serviço hello, o nível de desempenho e o nível de compatibilidade usando o SQL Server Management Studio. Durante a fase de importação hello, recomendamos que você importe tooa maior desempenho da camada banco de dados para melhor desempenho, mas se você reduzir após Olá importação money toosave até que você esteja pronto tooactively use Olá banco de dados importado. Alterar o nível de compatibilidade Olá pode resultar em melhor desempenho e recursos mais recentes de acesso toohello de saudação serviço do Azure SQL Database. Ao migrar um banco de dados mais antigo, seu nível de compatibilidade do banco de dados é mantida no nível de hello mais baixo com suporte que é compatível com o banco de dados de hello está sendo importado. Para obter mais informações, consulte [Desempenho de consultas aprimorado com nível de compatibilidade 130 no banco de dados SQL do Azure](sql-database-compatibility-level-query-performance-130.md).

1. No Pesquisador de Objetos, clique com o botão direito do mouse em **myMigratedDatabase** e clique em **Nova Consulta**. Banco de dados conectado tooyour é aberta uma janela de consulta.

2. Executar Olá seguindo a camada de serviço do comando tooset Olá muito**padrão** e Olá o nível de desempenho muito**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![alterar camada de serviço](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Executar Olá seguindo o nível de compatibilidade do banco de dados do comando toochange Olá muito**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![alterar nível de compatibilidade](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Próximas etapas 
Neste tutorial, você preparou, exportou e importou seu banco de dados. Você aprendeu a:

> [!div class="checklist"]
> * Preparar um banco de dados em um SQL Server para migração tooAzure banco de dados SQL
> * Exportar arquivo BACPAC de tooa Olá banco de dados
> * Importar arquivo BACPAC de saudação para um banco de dados do SQL Azure

Avançar toolearn tutorial do próximo toohello como toosecure seu banco de dados.

> [!div class="nextstepaction"]
> [Proteja o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).


