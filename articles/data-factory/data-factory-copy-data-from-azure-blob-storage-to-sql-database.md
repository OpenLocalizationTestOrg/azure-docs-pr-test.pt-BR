---
title: dados de aaaCopy do armazenamento de Blob tooSQL banco de dados - Azure | Microsoft Docs
description: "Este tutorial mostra como toouse atividade de cópia em uma fábrica de dados do Azure pipeline toocopy dados do banco de dados de tooSQL de armazenamento de Blob."
keywords: "sql para blob, armazenamento de blobs, cópia de dados"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Tutorial: Copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Neste tutorial, você pode criar uma fábrica de dados com um pipeline toocopy do banco de dados Blob armazenamento tooSQL.

Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure. Ela é habilitada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.  

> [!NOTE]
> Para obter uma visão geral detalhada da saudação serviço da fábrica de dados, consulte Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Pré-requisitos para o tutorial Olá
Antes de começar este tutorial, você deve ter Olá pré-requisitos a seguir:

* **Assinatura do Azure**.  Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Consulte Olá [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) artigo para obter detalhes.
* **Conta de Armazenamento do Azure**. Use o armazenamento de blob hello como um **fonte** repositório de dados neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.
* **Banco de dados SQL do Azure**. Você usa um banco de dados SQL do Azure como um armazenamento de dados de **destino** neste tutorial. Se você não tiver um banco de dados SQL do Azure que você pode usar o tutorial hello, consulte [como toocreate e configurar um banco de dados do SQL Azure](../sql-database/sql-database-get-started.md) toocreate um.
* **SQL Server 2012/2014 ou Visual Studio 2013**. Use o SQL Server Management Studio ou Visual Studio toocreate um banco de dados de exemplo e os dados de resultado de saudação tooview no banco de dados de saudação.  

## <a name="collect-blob-storage-account-name-and-key"></a>Coletar o nome e a chave da conta de armazenamento de blobs
Você precisa conta Olá chave de nome e a conta do armazenamento do Azure conta toodo neste tutorial. Anote o **nome da conta** e a **chave de conta** da sua conta de armazenamento do Azure.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **mais serviços** em Olá deixado menu e selecione **contas de armazenamento**.

    ![Procurar - Contas de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. Em Olá **contas de armazenamento** folha, selecione Olá **conta de armazenamento do Azure** que você deseja toouse neste tutorial.
4. Selecione o link **Chaves de acesso** em **CONFIGURAÇÕES**.
5. Clique em **cópia** (imagem) botão Avançar muito**nome da conta de armazenamento** texto caixa e salvar/colá-lo em algum lugar (por exemplo: em um arquivo de texto).
6. Repetir Olá toocopy de etapa anterior ou anote Olá **key1**.

    ![Chave de acesso de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Feche todas as folhas de saudação clicando **X**.

## <a name="collect-sql-server-database-user-names"></a>Coletar o servidor SQL, o banco de dados, os nomes de usuário
Neste tutorial você precisa de nomes de saudação do servidor, banco de dados e toodo de usuário do SQL Azure. Anote os nomes do **servidor**, **banco de dados** e **usuário** para seu banco de dados SQL do Azure.

1. Em Olá **portal do Azure**, clique em **mais serviços** em Olá esquerdo e selecione **bancos de dados SQL**.
2. Em Olá **folha de bancos de dados SQL**, selecione Olá **banco de dados** que você deseja toouse neste tutorial. Anote Olá **nome do banco de dados**.  
3. Em Olá **banco de dados SQL** folha, clique em **propriedades** em **configurações**.
4. Anote os valores hello para **nome do servidor** e **logon de administrador de servidor**.
5. Feche todas as folhas de saudação clicando **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Permitir que os serviços do Azure tooaccess SQL server
Certifique-se de que **permitir acesso a serviços tooAzure** configuração desativado **ON** para o servidor do SQL Azure para esse serviço da fábrica de dados Olá possa acessar seu servidor do SQL Azure. tooverify e ativar essa configuração, Olá seguintes etapas:

1. Clique em **mais serviços** hub no hello esquerda e clique em **servidores SQL**.
2. Selecione seu servidor e clique em **Firewall** em **CONFIGURAÇÕES**.
3. Em Olá **configurações de Firewall** folha, clique em **ON** para **permitir acesso a serviços tooAzure**.
4. Feche todas as folhas de saudação clicando **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Preparar o Armazenamento de Blobs e o banco de dados SQL
Agora, prepare o armazenamento de BLOBs do Azure e o banco de dados SQL do Azure para tutorial Olá executando Olá etapas a seguir:  

1. Inicie o Bloco de notas. Copie Olá texto a seguir e salve-o como **emp.txt** muito**C:\ADFGetStarted** pasta no disco rígido.

    ```
    John, Doe
    Jane, Doe
    ```
2. Use ferramentas como [Azure Storage Explorer](http://storageexplorer.com/) toocreate Olá **adftutorial** Olá contêiner e tooupload **emp.txt** arquivo toohello recipiente.

    ![Gerenciador de Armazenamento do Azure. Copiar dados do banco de dados do Blob storage tooSQL](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Olá Use Olá de toocreate de script SQL a seguir **emp** tabela no banco de dados SQL do Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Se você tiver instalado no computador do SQL Server 2012/2014:** siga as instruções de [gerenciamento de banco de dados SQL usando o SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour script SQL de saudação de servidor e execução de SQL Azure. Este artigo usa Olá [portal clássico do Azure](http://manage.windowsazure.com), Olá não [novo portal do Azure](https://portal.azure.com), tooconfigure firewall para um servidor do SQL Azure.

    Se o cliente não é permitido tooaccess hello Azure do SQL server, será necessário tooconfigure firewall para o acesso ao SQL Azure server tooallow em seu computador (endereço IP). Consulte [neste artigo](../sql-database/sql-database-configure-firewall-settings.md) firewall de saudação tooconfigure etapas para o servidor do SQL Azure.

## <a name="create-a-data-factory"></a>Criar uma data factory
Você concluiu os pré-requisitos de saudação. Você pode criar uma fábrica de dados usando uma das maneiras a seguir de saudação. Clique em uma das opções de saudação na lista suspensa de saudação na superior de saudação ou Olá seguir links tooperform Olá tutorial.     

* [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
* [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
* [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Ela não transforma dados de saída de tooproduce de dados de entrada. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie sua primeira pipeline tootransform de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).
> 
> É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas. 
