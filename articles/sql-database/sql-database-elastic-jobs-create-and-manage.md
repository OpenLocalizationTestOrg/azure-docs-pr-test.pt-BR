---
title: grupos de aaaManage de bancos de dados SQL do Azure | Microsoft Docs
description: "Explore a criação e o gerenciamento de um trabalho elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Criar e gerenciar Bancos de Dados SQL do Azure com escala horizontal usando trabalhos elásticos (preview)


**Trabalhos de Banco de Dados Elástico** simplificam o gerenciamento de grupos de bancos de dados executando operações administrativas como alterações de esquema, gerenciamento de credenciais, atualizações de dados de referência, coleta dados de desempenho ou de telemetria do locatário (cliente). Trabalhos do banco de dados Elásticos está disponível por meio de saudação portal do Azure e cmdlets do PowerShell. No entanto, a saudação funcionalidade reduzida superfícies de portal do Azure limitado tooexecution em todos os bancos de dados em um [(visualização) do pool Elástico](sql-database-elastic-pool.md). recursos adicionais de tooaccess e execução de scripts em um grupo de bancos de dados incluindo uma coleção personalizadas ou um fragmento definem (criada usando [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-scale-introduction.md)), consulte [criando e gerenciando trabalhos usando o PowerShell](sql-database-elastic-jobs-powershell.md). Para saber mais, confira [Visão geral de trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um pool elástico. Consulte [Sobre pools elásticos](sql-database-elastic-pool.md).
* Instalação dos componentes de serviço do trabalho de banco de dados elástico. Consulte [instalar o serviço de trabalho de banco de dados Elástico Olá](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Criando trabalhos
1. Usando Olá [portal do Azure](https://portal.azure.com), de um pool de trabalho do banco de dados Elástico existente, clique em **criar trabalho**.
2. Digite hello nome de usuário e senha do administrador de banco de dados de saudação (criado na instalação de trabalhos) para o banco de dados do controle de trabalhos hello (armazenamento de metadados para trabalhos).
   
    ![Nome do trabalho hello, digite ou cole no código e clique em executar][1]
3. Em Olá **criar trabalho** folha, digite um nome para o trabalho de saudação.
4. Digite hello usuário nome e senha tooconnect toohello destino bancos de dados com permissões suficientes para toosucceed de execução do script.
5. Cole ou digite no script hello T-SQL.
6. Clique em **Salvar** e em **Executar**.
   
    ![Criar trabalhos e executar][5]

## <a name="run-idempotent-jobs"></a>Executar trabalhos idempotentes
Quando você executa um script em um conjunto de bancos de dados, você deve ter certeza de script hello é idempotente. Ou seja, Olá script deve ser capaz de toorun várias vezes, mesmo se ele tiver falhado antes em um estado incompleto. Por exemplo, quando um script falha, o trabalho de saudação será automaticamente repetido até obter êxito (dentro dos limites, como repetir Olá lógica eventualmente deixarão Olá tentando novamente). Olá maneira toodo é toouse Olá uma cláusula "IF EXISTS" e excluir qualquer instância encontrada antes de criar um novo objeto. Veja um exemplo aqui:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Como alternativa, use uma cláusula "IF NOT EXISTS" antes de criar uma nova instância:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Esse script, em seguida, atualiza a tabela de saudação criada anteriormente.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Verificando o status do trabalho
Após o início de um trabalho, você pode verificar seu andamento.

1. Na página de pool Elástico hello, clique **gerenciar trabalhos**.
   
    ![Clique em “Gerenciar trabalhos”][2]
2. Clique em Olá nome (a) de um trabalho. Olá **STATUS** pode ser "Concluído" ou "Failed". detalhes do trabalho Olá aparecem (b) com sua data e hora de criação e execução. lista de saudação (c) abaixo Olá que mostra o progresso de saudação do script hello cada banco de dados no pool de hello, dando a seus detalhes de data e hora.
   
    ![Verificando um trabalho concluído][3]

## <a name="checking-failed-jobs"></a>Verificação de trabalhos com falha
Se um trabalho falhar, será possível encontrar um log de sua execução. Clique o nome de saudação do hello falha no trabalho toosee seus detalhes.

![Verificar um trabalho com falha][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


