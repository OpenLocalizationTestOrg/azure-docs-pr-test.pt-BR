---
title: aaaCopy um banco de dados SQL do Azure | Microsoft Docs
description: "Criar uma cópia de um Banco de Dados SQL do Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Copiar um Banco de Dados SQL do Azure

Banco de dados SQL do Azure fornece vários métodos para criar uma cópia transacionalmente consistente de um SQL Azure existentes do banco de dados em qualquer Olá mesmo servidor ou em um servidor diferente. Você pode copiar um banco de dados SQL usando o T-SQL, PowerShell ou Olá portal do Azure. 

## <a name="overview"></a>Visão geral

Uma cópia do banco de dados é um instantâneo do banco de dados de origem de hello a partir de tempo de saudação da solicitação de cópia de saudação. Você pode selecionar Olá mesmo servidor ou um servidor diferente, seu nível de desempenho e da camada de serviço ou um nível de desempenho diferentes dentro de saudação mesma camada de serviço (edição). Após a conclusão da cópia hello, ele se torna um banco de dados totalmente funcional e independente. Neste ponto, você pode atualizar ou fazer downgrade tooany edition. permissões, usuários e logons Olá podem ser gerenciadas independentemente.  

## <a name="logins-in-hello-database-copy"></a>Logons na cópia do banco de dados de saudação

Quando você copia um banco de dados toohello mesmo servidor lógico, Olá mesmos logons podem ser usados em ambos os bancos de dados. segurança de Olá principal de que usar o banco de dados do toocopy Olá se torna o proprietário do banco de dados de saudação no novo banco de dados de saudação. Todos os usuários de banco de dados, suas permissões e a segurança de SIDs (identificadores) são copiados toohello cópia de banco de dados.  

Quando você copia um servidor de lógico diferente do tooa banco de dados, segurança de Olá principal no novo servidor de saudação torna-se o proprietário do banco de dados de saudação no novo banco de dados de saudação. Se você usar [usuários de banco de dados independente](sql-database-manage-logins.md) para acesso a dados, verifique se ambos Olá primário e bancos de dados secundários sempre têm Olá mesmas credenciais de usuário, para que após a cópia de saudação concluir você podem acessar imediatamente com hello mesmo credenciais. 

Se você usar [Active Directory do Azure](../active-directory/active-directory-whatis.md), você pode eliminar completamente a necessidade de Olá para gerenciamento de credenciais na cópia de saudação. No entanto, quando você copiar o novo servidor de saudação banco de dados tooa, acesso baseado em logon de saudação pode não funcionar, porque não existem logons de Olá no novo servidor de saudação. toolearn sobre como gerenciar logons quando você copiar um banco de dados tooa servidor lógico diferente, consulte [como toomanage SQL Azure segurança banco de dados após a recuperação de desastres](sql-database-geo-replication-security-config.md). 

Após Olá cópia bem-sucedida e antes de outros usuários sejam remapeados, somente hello logon que iniciou a saudação copiando, proprietário do banco de dados de hello, pode fazer logon no novo banco de dados de toohello. logons tooresolve depois Olá operação de cópia for concluído, consulte [resolver logons](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Copiar um banco de dados usando Olá portal do Azure

toocopy um banco de dados usando Olá portal do Azure, página Olá aberta para o banco de dados e, em seguida, clique em **cópia**. 

   ![Cópia do banco de dados](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Cópia de banco de dados usando o PowerShell

toocopy um banco de dados usando o PowerShell, use Olá [AzureRmSqlDatabaseCopy novo](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Para um script de exemplo completo, consulte [copie um novo servidor de banco de dados tooa](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Cópia de banco de dados usando o Transact-SQL

Faça logon no mestre toohello banco de dados com logon principal no nível de servidor hello ou logon de Olá que criou o banco de dados de saudação desejado toocopy. Para copiar toosucceed de banco de dados, logons que não são de entidade de nível de servidor de saudação devem ser membros da função dbmanager de saudação. Para obter mais informações sobre logons e conectando o servidor toohello, consulte [gerenciar logons](sql-database-manage-logins.md).

Inicie a cópia do banco de dados de origem de saudação com hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instrução. Executar essa instrução inicia o processo de cópia de banco de dados do hello. Como copiar um banco de dados é um processo assíncrono, Olá instrução CREATE DATABASE retorna antes Olá cópia de banco de dados foi concluída.

### <a name="copy-a-sql-database-toohello-same-server"></a>Copiar um toohello de banco de dados do SQL server mesmo
Faça logon no mestre toohello banco de dados com logon principal no nível de servidor hello ou logon de Olá que criou o banco de dados de saudação desejado toocopy. Para copiar toosucceed de banco de dados, logons que não são de entidade de nível de servidor de saudação devem ser membros da função dbmanager de saudação.

Este comando copia Database1 tooa novo banco de dados denominado Database2 em Olá mesmo servidor. Dependendo do tamanho de saudação do banco de dados, Olá copiando operação pode levar algum tempo toocomplete.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Copiar um servidor diferente de tooa de banco de dados SQL

Faça logon no mestre toohello banco de dados do servidor de destino hello, servidor de banco de dados SQL Olá onde o novo banco de dados de saudação é toobe criado. Use um logon que tem Olá o mesmo nome e senha como proprietário do banco de dados de saudação do banco de dados de origem de saudação no servidor de banco de dados SQL de origem hello. logon Olá no servidor de destino Olá também deve ser um membro da função dbmanager de saudação ou ser logon principal no nível de servidor hello.

Este comando copia Database1 no servidor1 tooa novo banco de dados chamado Database2 no Servidor2. Dependendo do tamanho de saudação do banco de dados, Olá copiando operação pode levar algum tempo toocomplete.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Monitorar o progresso de saudação de saudação operação de cópia

Monitorar o processo de cópia de saudação consultando exibições de sys. Databases e sys.DM database_copies hello. Enquanto a cópia de saudação está em andamento, Olá **state_desc** coluna da exibição de sys. Databases Olá para o novo banco de dados de saudação está definida muito**copiar**.

* Se Olá cópia falhar, Olá **state_desc** coluna da exibição de sys. Databases Olá para o novo banco de dados de saudação está definida muito**SUSPEITAR**. Execute Olá instrução DROP no novo banco de dados de saudação e tente novamente mais tarde.
* Se Olá cópia for bem-sucedida, hello **state_desc** coluna da exibição de sys. Databases Olá para o novo banco de dados de saudação está definida muito**ONLINE**. Olá cópia foi concluída e Olá novo banco de dados for regulares que podem ser alteradas independente do banco de dados de origem de saudação.

> [!NOTE]
> Se você decidir toocancel Olá copiando enquanto ele está em andamento, execute Olá [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) declaração no novo banco de dados de saudação. Como alternativa, executar a instrução de DROP DATABASE de saudação no banco de dados de origem de saudação também cancela Olá processo de cópia.
> 

## <a name="resolve-logins"></a>Resolver logons

Depois que o novo banco de dados de saudação está online no servidor de destino Olá, use Olá [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) instrução tooremap Olá os usuários Olá novo banco de dados toologins no servidor de destino de saudação. os usuários tooresolve órfãos, consulte [solucionar problemas de usuários órfãos](https://msdn.microsoft.com/library/ms175475.aspx). Consulte também [como toomanage SQL Azure segurança banco de dados após a recuperação de desastres](sql-database-geo-replication-security-config.md).

Todos os usuários no novo banco de dados de saudação reter permissões de saudação que eles tinham no banco de dados de origem de saudação. usuário Olá que iniciou a cópia do banco de dados de saudação se torna o proprietário do banco de dados de saudação do novo banco de dados de saudação e é atribuído a um novo identificador de segurança (SID). Após Olá cópia bem-sucedida e antes de outros usuários sejam remapeados, somente hello logon que iniciou a saudação copiando, proprietário do banco de dados de hello, pode fazer logon no novo banco de dados de toohello.

toolearn sobre como gerenciar usuários e logons quando você copiar um banco de dados tooa servidor lógico diferente, consulte [como toomanage SQL Azure segurança banco de dados após a recuperação de desastres](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Próximas etapas

* Para obter informações sobre logons, consulte [gerenciar logons](sql-database-manage-logins.md) e [como toomanage SQL Azure segurança banco de dados após a recuperação de desastres](sql-database-geo-replication-security-config.md).
* tooexport um banco de dados, consulte [Exportar banco de dados de saudação tooa BACPAC](sql-database-export.md).
